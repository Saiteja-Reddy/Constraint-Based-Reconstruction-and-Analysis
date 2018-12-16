## Using the RAVEN Toolbox

### Input and Output of Reconstructions and Models

The RAVEN Toolbox supports the use of models in multiple formats, including:
1. Systems Biology Markup Language (SBML) format
2. Excel format
3. MAT-file format
4. COBRA formats

*The most commonly used model format is a *SBML-file format* where when imported has a simple MATLAB struct contains one or more of the fields defined **[here](raven_format.md)**

*To import a model* in SBML (RAVEN) format,
```
model = importModel(fileName);
```

*To import a model* in SBML (COBRA) format,
```
model = importModel(fileName, isSBML2COBRA=true);
```

*To import a model* in Excel format,
```
model = importExcelModel(fileName);
```

*To export a model* to an SBML file,
```
exportModel(model,fileName);
```

*To export a model* to Microsoft Excel model format,
```
exportToExcelFormat(model,fileName);
```

**To convert between RAVEN and COBRA model structures** in RAVEN Toolbox we use the following,
```
newModel=ravenCobraWrapper(model)
```

This function is a bidirectional tool to convert between RAVEN and COBRA structures. It recognises COBRA structure by checking field 'rules' existense, which is only found in COBRA Toolbox structure.

### Reporter Metabolite Analysis

**To do Reporter Metabolite Analysis**, use
```
repMets = reporterMetabolites(model, genes, Pgenevalues, printResults, outputFile);
```
where,
- *genes* is a cell array of gene names (should match with model.genes)
- *genePValues* are the P-values for differential expression of the genes
- *printResults* - true if the top 20 Reporter Metabolites should be printed to the screen (optional, default is false)
- *outputFile* - the results are printed to this file (optional)

The output repMets is an array of structures with the following fields.
1. *test* - a string the describes the genes that were used to calculate the Reporter Metabolites ('all', 'only up', or 'only down').
2. *mets* - a cell array of metabolite IDs for the metabolites for which a score could be calculated
3. *metZScores* - Z-scores for differential expression around each metabolite in "mets"
4. *metPValues* - P-values for differential expression around each metabolite in "mets"
5. *metNGenes* - number of neighbouring genes for each metabolite in "mets"
6. *meanZ* - average Z-scores for the genes around each metabolite in "mets"
7. *stdZ* - standard deviations of the Z-scores around each metabolite in "mets"

**Sample Run** -
```
>> load('Recon3D_301.mat');
>> model = Recon3D;
>> num = readtable("degs/region_L3_BP-DEGs-DC.csv");
>> genes = num.entrez;
>> genes = strcat(genes, '.1');
>> pvalues = num.P_Value;
>> repMets = reporterMetabolites(model, genes, pvalues, true, 'reps_L3_BP_recon3.txt');

TOP 20 REPORTER METABOLITES
TEST TYPE: all
ID	NAME	P-VALUE
e4hglu[m]	Erythro-4-Hydroxy-L-Glutamate	0.00040622
12HPET[n]	12-Hydroperoxyeicosa-5,8,10,14-tetraenoate	0.001114
C04849[n]	(5Z,9E,14Z)-(8Xi,11R,12S)-11,12-Epoxy-8-Hydroxyicosa-5,9,14-Trienoate	0.001114
M03067[c]	TRNA(Cys)	0.0017919
M02351[c]	L-Cysteinyl-tRNA(Cys)	0.0017919
phe_L[m]	L-Phenylalanine	0.0020786
tyr_L[m]	L-Tyrosine	0.0020786
M00222[c]	1-(1-Alkenyl)-Sn-Glycero-3-Phosphate	0.0021643
adp[r]	Adenosine Diphosphate	0.0021985
5hoxindact[m]	(5-Hydroxyindol-3-Yl)Acetaldehyde	0.0025706
crtsl[r]	Cortisol	0.0029422
pi[m]	Orthophosphate	0.0035126
vitd3[e]	Calciol	0.0036855
ala_B[m]	Beta-Alanine	0.0037673
5hoxindoa[m]	5-Hydroxyindoleacetate	0.0038388
id3acald[m]	Indol-3-Ylacetaldehyde	0.0038388
ind3ac[m]	Indole-3-Acetate	0.0038388
bamppald[m]	Beta-Aminopropion Aldehyde	0.0038388
glac[m]	D-Glucurono-6,3-Lactone	0.0038388
glcr[m]	D-Glucarate	0.0038388

```

The above used files are provided [here](resources/).


**References:**
1. [Uncovering transcriptional regulation of metabolism by using metabolic network topology](https://www.pnas.org/content/102/8/2685)
2. [Reporter pathway analysis from transcriptome data: Metabolite-centric versus Reaction-centric approach](https://www.nature.com/articles/srep14563)
3. [RAVEN Official Tutorials](https://github.com/SysBioChalmers/RAVEN/tree/master/tutorial)

[Back to Contents](../README.md)
