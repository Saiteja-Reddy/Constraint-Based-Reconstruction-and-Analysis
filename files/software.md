## Using the COBRA Toolbox

### Input and Output of Reconstructions and Models

The COBRA Toolbox supports the use of models in multiple formats, including:
- MAT-file format
- Systems Biology Markup Language (SBML) format
- SimPheny format
- Excel format

The most commonly used model format is a *MAT-file (.mat ) format* where by a simple MATLAB struct contains one or more of the fields defined [here](fields.md)

**To read a model into Cobra Toolbox:**

```
>>> initCobraToolbox();
>>> fileName = 'my_model.mat';
>>> model = readCbModel(fileName);
```

The **readCbModel** function has a second optional input that specifies the file type being loaded. In the above example the file type does not need to be specified since the input default is a 'Matlab' file type. To load file types other than a MAT-file, specificy the file type for input as: ‘SBML’, ‘SimPheny’, ‘SimPhenyPlus’, ‘SimPhenyText’, or 'Excel’.

Once the model is loaded it can be used directly with The COBRA Toolbox functions. On printing the loaded model contents, usually looks like below.

<img src="pics/8.1.png" width="400" height="300">

In general, the following fields should always be present:

- rxns, the identifiers of the reactions
- mets, the identifiers of the metabolites
- genes, the list of genes in your model (can be empty)
- rules, the Gene-protein-reaction rules in a computer readable format present in your model.
- S, the stoichiometric matrix
- lb, the lower bounds of the reactions
- ub, the upper bounds of the reactions
- osense, the objective sense (by convention, -1 indicates maximisation, 1 minimisation)
- b, Accumulation (positive) or depletion (negative) of the corresponding metabolites. 0 Indicates no concentration change.
- csense, indicator whether the b vector is a lower bound ('G'), upper bound ('L'), or hard constraint 'E' for the metabolite.

**To write a model from Cobra Toolbox:**

We use the **writeCbModel** function which has an optional input that specifies the file type in which the model should be written and saved. If the file type is not specified, the default file type to be saved is as a MAT-file. To use the function to write a file types other than a MAT-file, specificy the file type for input as: ‘text’,’xls’, or ‘sbml’.

*Sample Usage:*

```
writeCbModel(model, 'fileName','test_file.sbml','format','sbml')
```

### Flux Balance Analysis (FBA)

Through the use of genome-scale metabolic network reconstructions, Flux Balance Analysis (FBA) can be used to calculate the flow of metabolites through a metabolic network. This capability makes it possible to predict the growth rate of an organism and/or the rate of production of a given metabolite.

FBA has limitations! It does not use kinetic parameters, thus it cannot predict metabolite concentrations. It is also only capable of determining fluxes at steady state. Typically, FBA does not account for regulatory effects such as activation of enzymes by protein kinases or regulation of gene expression. Therefore, its predictions may not always be accurate.

<img src="pics/8.2.png" width="450" height="550">

Above is the flow chart for FBA Analysis.

Sample FBA Analysis:

```
initCobraToolbox
changeCobraSolver ('gurobi', 'all');
global CBTDIR

modelFileName = 'Recon2.0model.mat';

modelDirectory = getDistributedModelFolder(modelFileName); %Look up the folder for the distributed Models.

modelFileName= [modelDirectory filesep modelFileName]; % Get the full path. Necessary to be sure, that the right model is loaded

model = readCbModel(modelFileName);

modelaerobic = model;
printRxnFormula(model, 'DM_atp_c_');
modelaerobic = changeObjective (modelaerobic, 'DM_atp_c_');

modelaerobic = changeRxnBounds (modelaerobic, 'EX_glc(e)', -20, 'l');
modelaerobic = changeRxnBounds (modelaerobic, 'EX_o2(e)', -1000, 'l');

FBAaerobic = optimizeCbModel (modelaerobic, 'max')
```

When oxygen and all carbon sources (internal and external) are provided the flux through ATP demand reaction can reach its maximum rate of 1000 mol/min/gDW.

Refer: [Flux Balance Analysis Cobra](https://opencobra.github.io/cobratoolbox/stable/tutorials/tutorialFBA.html)


### Flux Variability analysis (FVA)

The flux distributions calculated by FBA are often not unique. In many cases, it is necessary for a biological system to achieve the same objective value by using alternate equivalent optimal pathways, creating phenotypically different alternate optimal solutions (silent phenotypes). For large models there can be a very large number of alternate equivalent optimal solutions.

Flux variability analysis (FVA) is a widely used computational tool for evaluating the minimum and maximum range of each reaction flux that can still satisfy the constraints using a double LP problem (i.e. a maximization and a subsequent minimization) for each reaction of interest.

Sample Run Example:

```
initCobraToolbox
changeCobraSolver ('gurobi', 'all');

global CBTDIR
modelFileName = 'Recon2.0model.mat';
modelDirectory = getDistributedModelFolder(modelFileName); %Look up the folder for the distributed Models.
modelFileName= [modelDirectory filesep modelFileName]; % Get the full path. Necessary to be sure, that the right model is loaded
model = readCbModel(modelFileName);

[selExc, selUpt] = findExcRxns(model);
uptakes = model.rxns(selUpt);
subuptakeModel = extractSubNetwork(model, uptakes);
hiCarbonRxns = findCarbonRxns(subuptakeModel,1);
modelalter = changeRxnBounds(model, hiCarbonRxns, 0, 'b');

energySources = {'EX_adp'; 'EX_amp(e)'; 'EX_atp(e)'; 'EX_co2(e)';...
'EX_coa(e)'; 'EX_fad(e)'; 'EX_fe2(e)'; 'EX_fe3(e)'; 'EX_gdp(e)';...
'EX_gmp(e)'; 'EX_gtp(e)'; 'EX_h(e)'; 'EX_h2o(e)'; 'EX_h2o2(e)';...
'EX_nad(e)'; 'EX_nadp(e)'; 'EX_no(e)'; 'EX_no2(e)'; 'EX_o2s(e)'};
modelalter = changeRxnBounds (modelalter, energySources, 0, 'l');

% modelfva1 represents aerobic condition
modelfva1 = modelalter;
modelfva1 = changeRxnBounds(modelfva1, 'EX_glc(e)', -20, 'l');
modelfva1 = changeRxnBounds(modelfva1, 'EX_o2(e)', -1000, 'l');

% modelfva2 represents anaerobic condition
modelfva2 = modelalter;
modelfva2 = changeRxnBounds(modelfva2, 'EX_glc(e)', -20, 'l');
modelfva2 = changeRxnBounds(modelfva2, 'EX_o2(e)', 0, 'l');


% Selecting several reactions of the model that we want to analyse with FVA
rxnsList = {'DM_atp_c_'; 'ACOAHi'; 'ALCD21_D'; 'LALDO'; 'ME2m';...
'AKGDm'; 'PGI'; 'PGM'; 'r0062'};

% Run FVA analysis for the model with the constraints that simulates aerobic conditions:
[minFlux1, maxFlux1, Vmin1, Vmax1] = fluxVariability(modelfva1, 100, 'max', rxnsList)

% Run FVA analysis for the model with the constraints that simulates anaerobic conditions:
[minFlux2, maxFlux2, Vmin2, Vmax2] = fluxVariability(modelfva2, [], [], rxnsList)
```

Refer: [Flux Variability analysis Cobra](https://opencobra.github.io/cobratoolbox/stable/tutorials/tutorialFVA.html)


[Back to Contents](../README.md)
