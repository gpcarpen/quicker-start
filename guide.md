> Estimated time to complete this tutorial is ~2 hours

> Prior knowledge needed - Basic bash command familiarity, terminal use familiarity

> Tools needed - Computer, internet access


# Quick(er) Guide

The goal of this guide is to get new users through the validate software pipeline so that they can begin running the workflow more quickly. 

  1. Install agave on your local computer
  2. Example Workflow

        A. FastLMM

        B. Winnow


# Installing Agave 

  - Setup an CyVerse (iPlant) account. https://user.cyverse.org/
  - We will now install the Agave API into the home directory,
  - From your terminal type: 
  
  -     git clone https://github.com/iPlantCollaborativeOpenSource/cyverse-sdk.git
  
  -     cd cyverse-sdk
  
  -     tar xf cyverse-cli.tgz

  -     mv cyverse-cli $HOME
 
  -     echo "PATH=\$PATH:\$HOME/cyverse-cli/bin" >> ~/.bashrc
 
  -     source ~/.bashrc
  -     (note) this is the default profile for linux if you are one a mac it is .bash_profile
  
  -     tenants-init -t iplantc.org

  - These Last two commands will require a CyVerse username and password
  
  -     clients-create -S -v -N my_client -D "Client used for app development"
  
  -     auth-tokens-create -S  
  -     (note) if asked for an authentication token, use the command "auth-tokens-refresh -S"

  - At this point you can check to make sure that the agave API has been installed by running the commmand `apps-list`. If all worked correctly then this command should list all publicly available apps.
  - If everything is installed correctly you can move forward from this point in the future without having to run the above setup.
  - You can now either run an app from this list, or you can continue with the next section to see what an example workflow may look like. 
  
###Note: If you are getting errors when attempting to create tokens for agave
  -   go to https://agave.iplantc.org/store/?requestedPage=/store/site/pages/subscriptions.jag
 
  -   click on "my applicaitons" then scroll down to the bottom, you will see a line for active tokens, click the delete button
  -   go back into your terminal and enter the following commands
 
  -       clients-create -S -v -N my_client -D "Client used for app development"
  
  -       auth-tokens-create -S
  
  -   This should recreate the agave token and allow you to continue with the workflow

# Example workflow
##FastLMM
- From a working directory download the FastLMM job skeleton with the following command

-       wget https://www.dropbox.com/s/ij43c5qwsk6hakf/fastlmm-job.json
-       (note) this is not installed by default on macs, this can be downloaded by visiting this url

- Open the fastlmm-job.json file with the command 

-       VIM fastlmm-job.json

- Within the json file follow the next directions to edit for your own purposes.

- jobName doesnt really matter, but software name has to be a valid agave app. 

- You can list all valide agave apps with the command `apps-list`. 

- RequestedTime is self explanatory, archive will save the output to your discovery environment (DE) folder.

- Inputs reference input files that Agave will download before running. Parameters are app parameters

- FastLMM needs either PED/MAP or BED/BIM/FAM and a phenotype file.

- In the example, these are part of the public syngenta_sim dataset

- To use your own files, which are on the DE, you would replace everything after .org/ with the file path on your system

- i.e. agave://data.iplantcollaborative.org/swb5015/data/dongwang.fam where is swb8106  your username and the rest is the path of your files

- To use PED/MAP files you would delete the inputFAM, inputBED, and inputBIM and add inputPED and inputMAP

- There are other parameters but for our example we will only be defining the output name

- To submit the job, from your working directory where the JSON file is located, enter `jobs-submit -F fastlmm-job.json`
 
- If all goes well you will get a response along the lines of `Job [job_id] successfully submitted`

- You can check the status of this job by copying the job id and entering `jobs-status jobidnumber`

- Once the job is completed you can get the output files by entering `jobs-output jobidnumber`

- There should be a file with the output parameter as its prefix

- You can download this file by entering `jobs-output --download --path [file name] [job id]` 
  -   The path refers to where it is within the Discovery Environment and not where it is within the current directory. The Download        with automatically save it to the current directory.  

##Winnow
- The required files for winnow are the Known Truth file and the output from a GWAS tool (FastLMM in our case)

- Once you download the fastlmm output, upload it to a new location in your DE 
-     files-upload -S data.iplantcollaborative.org -F [fastlmm output which should now be local] swb5075/data

- use wget to grab the winnow example skeleteon
`wget https://www.dropbox.com/s/pnhebgvx18mh6f5/winnow-job.json`
