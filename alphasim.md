>  Time ~30min

>  Prerequisities - Agave CLI, general knowledge of executing using Agave, Access to the Discovery Environment within CyVerse, and Stampede allocation (if you want)

>  Helpful Documentation
>> Alphasim http://www.alphagenes.roslin.ed.ac.uk/wp-content/uploads/AlphaSimManual/AlphaSim.html

>>  Alphasim parameter file https://github.com/CyVerse-Validate/Stampede-Files/blob/master/AlphaSim-1.04/AlphaSimInputInformation.txt 

##Locating and Opening the parameter file
-   The parameter files is located here (place holder url) in the GitHub
        The parameter file allows you to pass commands into the AlphaSim software
-   Once you have access the parameter file upload it to your Discovery Environment 
        Currently the parameter file has specifications for running multiple generations for corn genetics
-   Save the following as a JSON file (This can be save locally as long as you have the Agave CLI installed) 
       with usename replaced with your CyVerse username
       And the path to the file to the parameter file within your Discovery Environment.
```json
{
"jobName": "testAlphaSim",
"softwareName": "AlphaSim-1.04",
"requestedTime": "05:00:00",
"archive": true,
    "inputs":{
        "specificationFile": "agave://data.iplantcollaborative.org/USERNAME/ALPHASIM_SPEC_PATH
    }
}
```
- With the following command you can run AlphaSim (publicly available  on Agave)
        This is assuming that you don't want to change any of the parameters
```
jobs-submit -F (your path the JSON file you just saved) 
```
