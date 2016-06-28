# Quick(er) Guide

The goal of this guide is to get new users through the validate software pipeline so that they can begin running the workflow more quickly. 

  1. Install agave on your local computer
  2. Example Workflow

        A. FastLMM

        B. Winnow


# Installing Agave

  - Setup an CyVerse (iPlant) account. https://user.cyverse.org/
  - From terminal type 
  
  -     git clone https://github.com/iPlantCollaborativeOpenSource/cyverse-sdk.git
  
  -     cd cyverse-sdk
  
  -     tar xf cyverse-cli.tgz

  -     mv cyverse-cli $HOME
 
  -     echo "PATH=\$PATH:\$HOME/cyverse-cli/bin" >> ~/.bashrc
 
  -     source ~/.bashrc
  
  -     tenants-init -t iplantc.org
  
  -     clients-create -S -v -N my_client -D "Client used for app development"
  
  -     auth-tokens-create -S  
  
  - Last two need CyVerse username and password
  

# Example workflow
##FastLMM
- From a working directory download the FastLMM job skeleton with the following command

-       wget https://www.dropbox.com/s/ij43c5qwsk6hakf/fastlmm-job.json

- jobName doesnt really matter, but software name has to be a valid agave app. 

- You can list all valide agave apps with the command apps-list. 

- RequestedTime is self explanatory, archive will save the output to your discovery environment (DE) folder.

- Inputs reference input files that Agave will download before running. Parameters are app parameters

- FastLMM needs either PED/MAP or BED/BIM/FAM and a phenotype file.

- In the example, these are part of the public syngenta_sim dataset

- To use your own files, which are on the DE, you would replace everything after .org/ with the file path on your system

- i.e. agave://data.iplantcollaborative.org/swb5015/data/dongwang.fam where is swb8106  your username and the rest is the path of your files

- To use PED/MAP files you would delete the inputFAM, inputBED, and inputBIM and add inputPED and inputMAP

- There are other parameters but for our example we will only be defining the output name

- To submit the job, from your working directory where the JSON file is located, enter `jobs-submit -F fastlmm-job.json`
 
- If all goes well you will get a response along the lines of Job [job_id] successfully submitted

- You can check the status of this job by copying the job id and entering jobs-status followed by the job id

- Once the job is completed you can get the output files by entering `jobs-output` followed by the job id

- There should be a file with the output parameter as its prefix

- You can download this file by entering `jobs-output —download —path [file name] [job id]

- `jobs-output --download --path [file name] [job id]` (edited) 




