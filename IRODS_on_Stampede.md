>  Time ~min
>  Prerequisities - Agave CLI installed, A Data Store allocation within CyVerse, and a Stampede allocation

>  Purpose of this tutorial - This is a list of how to setup and install IRODS so that you can access your data store using iCommands 

>  Useful resources
>   - Discovery Environment https://de.iplantcollaborative.org/de/
>   - IRODS and CyVerse explained (includes iCommands cheatsheet) https://pods.iplantcollaborative.org/wiki/display/DS/Using+iCommands
>   - IRODS and TACC explained    https://portal.tacc.utexas.edu/software/irods

## iCommands Are...
- iCommands are basic commands that are used for the IRODS system which allows you to access your data store from the terminal. A point worth making is that the discovery environment is the GUI for the data store. The data store itself is server space which you are given for storing and sharing data with other CyVerse users and the public. Being able to access your data store is handy for file inputs/outputs in data analysis amongst other things. 

## Loading and installing IRODS on Stampede
- Login to your stampede allocation username@stampede.tacc.utexas.edu
- Enter the following commands which will load, save, and then allow you to use iCommands
```
module load irods
iinit
Host: data.iplantcollaborative.org
Port: 1247
User: YourUserNameForCyVerse
Zone: iplant
Password: YourUserPasswordForCyVerse
Default Resouce: leave blank
```
- To check to see if the above worked type
```
ils /iplant/home/YourUserNameForCyVerse
```
- The above should then list whatever is in your home directory in your data store alloaction

- Note: If you are recieving errors about improper configuration start from the top just after module load irods. 
- If you are recieving errors about file paths ensure that you are being careful with capitlization, spelling, and the like
