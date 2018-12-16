## RAVEN Model Fields List

The following fields are defined in the RAVEN toolbox. If the field is present in a model, it should have the properties defined here and should be of the mentioned types.

| Field name          	| Subfield name 	| Data type                              	| Description                                                         	| Mandatory                                                   	|
|---------------------	|---------------	|----------------------------------------	|---------------------------------------------------------------------	|-------------------------------------------------------------	|
| id                  	|               	| String                                 	| Model ID                                                            	| Mandatory field                                             	|
| description         	|               	| String                                 	| Model name                                                          	| Mandatory field                                             	|
| annotation          	|               	| Struct                                 	| Additional information about the model                              	| Non-mandatory field                                         	|
|                     	| taxonomy      	| String                                 	| The taxonomy for the target species                                 	| Non-mandatory field                                         	|
|                     	| defaultLB     	| Double                                 	| Default lower bound values for reactions                            	| Non-mandatory field                                         	|
|                     	| defaultUB     	| Double                                 	| Default upper bound values for reactions                            	| Non-mandatory field                                         	|
|                     	| givenName     	| String                                 	| The name of the main model author                                   	| Non-mandatory field                                         	|
|                     	| familyName    	| String                                 	| The surname of the main model author                                	| Non-mandatory field                                         	|
|                     	| email         	| String                                 	| An e-mail address of the main model author                          	| Non-mandatory field                                         	|
|                     	| organization  	| String                                 	| The organization of the main model author                           	| Non-mandatory field                                         	|
|                     	| note          	| String                                 	| Additional comments about the model                                 	| Non-mandatory field                                         	|
| rxns                	|               	| Column Cell Array of Strings           	| Reaction IDs                                                        	| Mandatory field                                             	|
| mets                	|               	| Column Cell Array of Strings           	| Metabolite IDs                                                      	| Mandatory field                                             	|
| S                   	|               	| Sparse or Full Matrix of Double        	| Stoichiometric (S) matrix                                           	| Mandatory field                                             	|
| lb                  	|               	| Column Vector of Doubles               	| Reaction lower bounds                                               	| Mandatory field                                             	|
| ub                  	|               	| Column Vector of Doubles               	| Reaction upper bounds                                               	| Mandatory field                                             	|
| rev                 	|               	| Column Vector of Doubles               	| Reaction reversibility vector (1-reversible, 0-irreversible)        	| Mandatory field                                             	|
| c                   	|               	| Column Vector of Doubles               	| Coefficients for objective function                                 	| Mandatory field                                             	|
| b                   	|               	| Column Vector of Doubles               	| Equality constraints for metabolite equations                       	| Mandatory field                                             	|
| comps               	|               	| Column Cell Array of Strings           	| Compartment IDs                                                     	| Mandatory field                                             	|
| compNames           	|               	| Column Cell Array of Strings           	| Compartment names                                                   	| Non-mandatory field                                         	|
| compOutside         	|               	| Column Cell Array of Strings           	| Compartment ID for compartment surrounding each of the compartments 	| Non-mandatory field                                         	|
| compMiriams         	|               	| Struct                                 	| Structure with MIRIAM information about the compartments            	| Non-mandatory field                                         	|
|                     	| name          	| Column Cell Array of Strings           	| The name of MIRIAM prefix                                           	| Non-mandatory field                                         	|
|                     	| value         	| Column Cell Array of Strings           	| The ID for particular MIRIAM entry                                  	| Non-mandatory field                                         	|
| rxnNames            	|               	| Column Cell Array of Strings           	| Reaction description                                                	| Non-mandatory field                                         	|
| rxnComps            	|               	| Column Vector of Doubles               	| Reaction compartments                                               	| Non-mandatory field                                         	|
| grRules             	|               	| Column Cell Array of Strings           	| The name of MIRIAM prefix                                           	| Non-mandatory field                                         	|
| rxnGeneMat          	|               	| Sparse or Full Matrix of Double        	| Reaction-to-gene mapping in sparse matrix form                      	| Non-mandatory field                                         	|
| subSystems          	|               	| Column Struct of Cell Array of Strings 	| Subsystem names for each reaction                                   	| Non-mandatory field                                         	|
| eccodes             	|               	| Column Cell Array of Strings           	| EC-codes for the reactions                                          	| Non-mandatory field                                         	|
| rxnMiriams          	|               	| Struct                                 	| Structure with MIRIAM information about the reactions               	| Non-mandatory field                                         	|
|                     	| name          	| Column Cell Array of Strings           	| The name of MIRIAM prefix                                           	| Non-mandatory field                                         	|
|                     	| value         	| Column Cell Array of Strings           	| The ID for particular MIRIAM entry                                  	| Non-mandatory field                                         	|
| rxnNotes            	|               	| Column Cell Array of Strings           	| Notes for each reaction                                             	| Non-mandatory field                                         	|
| rxnReferences       	|               	| Column Cell Array of Strings           	| Non-PubMed references for each reaction                             	| Non-mandatory field                                         	|
| rxnConfidenceScores 	|               	| Column Vector of Doubles               	| Confidence scores for each reaction (5 - best, 1 - worst)           	| Non-mandatory field                                         	|
| genes               	|               	| Column Cell Array of Strings           	| List of all genes                                                   	| Non-mandatory field                                         	|
| geneComps           	|               	| Column Cell Array of Strings           	| Compartments for genes                                              	| Non-mandatory field                                         	|
| geneMiriams         	|               	| Struct                                 	| Structure with MIRIAM information about the genes                   	| Non-mandatory field                                         	|
|                     	| name          	| Column Cell Array of Strings           	| The name of MIRIAM prefix                                           	| Non-mandatory field                                         	|
|                     	| value         	| Column Cell Array of Strings           	| The ID for particular MIRIAM entry                                  	| Non-mandatory field                                         	|
| geneShortNames      	|               	| Column Cell Array of Strings           	| Gene alternative names (e.g. ERG10)                                 	| Non-mandatory field                                         	|
| metNames            	|               	| Column Cell Array of Strings           	| Metabolite names                                                    	| Non-mandatory field                                         	|
| metComps            	|               	| Column Vector of Doubles               	| Compartments for metabolites                                        	| Mandatory field                                             	|
| inchis              	|               	| Column Cell Array of Strings           	| InChI-codes for metabolites                                         	| Non-mandatory field                                         	|
| metFormulas         	|               	| Column Cell Array of Strings           	| Chemical formulas for metabolites                                   	| Non-mandatory field                                         	|
| metMiriams          	|               	| Struct                                 	| Structure with MIRIAM information about the metabolites             	| Non-mandatory field                                         	|
|                     	| name          	| Column Cell Array of Strings           	| The name of MIRIAM prefix                                           	| Non-mandatory field                                         	|
|                     	| value         	| Column Cell Array of Strings           	| The ID for particular MIRIAM entry                                  	| Non-mandatory field                                         	|
| metCharges          	|               	| Column Vector of Doubles               	| Charge information for metabolites                                  	| Non-mandatory field                                         	|
| unconstrained       	|               	| Column Vector of Doubles               	| Binary vector, positive for exchange (boundary) metabolites         	| Non-mandatory field                                         	|
| rxnFrom             	|               	| Column Cell Array of Strings           	| The name of template model from which particular reaction was taken 	| Non-mandatory field for internal use, not exported anywhere 	|


[Back to "Using the RAVEN Toolbox"](raven_usage.md)
