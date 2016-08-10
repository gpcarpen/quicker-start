The genetic structure is based on 280 wheat accessions in the Nebraska Wheat Breeding program that are harvested in 2010.  The marker data include genotype for 442 markers.  
The original data have more than 1000 markers but the file here only includes markers of high quality, higher minor allele frequency and with some highly correlated markers removed.  The simulated marker effects are:

Marker	   effect_size
"wPt.2150" 	9.51 
"wPt.0596" 	8.07 
"wPt.1171" 	11.11
"wPt.1903" 	14.02
"wPt.6116" 	5.99 
"tPt.5675" 	7.11 
"wPt.4064" 	11.46
"wPt.6064" 	9.86 

All the other markers are assumed to have no effects.  For the phenotype values, besides marker effects, I added the random effects that are associated with the relationship matrix, then added environmental residues from 9 locations.  
Specifically, for line k, I take the (real) phenotype values from 9 Nebraska locations measured in 2010 for line k and subtract the mean value across locations for this line to obtain the 9 environmental residues, which should include environmental effect and residual random error.  I added these 9 numbers to the simulated marker effects and genetic random effect to obtain the simulated phenotype for line k at 9 environments.  

The attached files are for marker genotypes (missing entries were imputed with minor allele frequency) and simulated phenotype.  Hopefully they are self-explanatory.
