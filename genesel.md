>  Time ~30min

>  Prerequisities - Agave CLI, general knowledge of executing using Agave, Access to the Discovery Environment within CyVerse, and Stampede allocation (if you want)

>  Helpful Documentation
>> Genesel (User Manual) http://www.biomedcentral.com/content/supplementary/1471-2105-12-186-s1.pdf 

>> Gensel (Cyverse page) https://pods.iplantcollaborative.org/wiki/display/DEapps/GenSel

##Locating the parameter/input files and running Gensel
-   To run the software you need one parameter file (.inp) and three input files (.gs, .newbin, .192)

>  -All of these files can be found in the Discovery Envrionment following the path
>  iplant/home/shared/iplantcollaborative/example_data/gensel/

>  -For more information on these inputs read the documentaiton listed above

-   Save the following as a JSON file (This can be save locally as long as you have the Agave CLI installed) 

```json
{
"jobName": "testGenSel",
"softwareName": "GenSel-2.14",
"nodeCount": 1,
"batchQueue": "serial",
"requestedTime": "02:00:00",
"processorsPerNode": 16,
"archive": false,
"archivePath": "",
   "inputs":{
       "phenotypeFileName":"agave://data.iplantcollaborative.org/shared/iplantcollaborative/example_data/gensel/DMI.gs",
       "markerFileName":"agave://data.iplantcollaborative.org/shared/iplantcollaborative/example_data/gensel/gpegeno.newbin",
       "includeFileName":"agave://data.iplantcollaborative.org/shared/iplantcollaborative/example_data/gensel/DMIg.192"
   },
   "parameters":{
       "Parameter_File":"agave://data.iplantcollaborative.org/shared/iplantcollaborative/example_data/gensel/run.inp"
   }
}
```

- With the following command you can run Gensel (publicly available on Agave)
        This is assuming that you don't want to change any of the parameters/inputs
```
jobs-submit -F (your path the JSON file you just saved) 
```
