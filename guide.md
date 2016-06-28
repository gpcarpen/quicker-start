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
- From a working directory download this FastLMM job skeleton
- i.e. wget https://www.dropbox.com/s/ij43c5qwsk6hakf/fastlmm-job.json
