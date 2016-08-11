>  Time ~30min

>  Prerequisities - Agave CLI, general knowledge of executing using Agave, Access to the Discovery Environment within CyVerse, and Stampede allocation (if you want)

>  Helpful Documentation
>> Qxpal http://bmcbioinformatics.biomedcentral.com/articles/10.1186/1471-2105-12-202

>>  Qxpak parameter file http://mirrors.iplantcollaborative.org/browse/iplant/home/shared/iplantcollaborative/example_data/qxpak


## To Begin, Command Line Usage
-   Normally in QxPak you would alter the parameter file so that you call specific input files for each data analysis fun. This tutorial is written around a wrapper script that was written to make the process of data analysis more easy to do with many different inputs. Instead of having to alter the parameter file each time, you can simply changes the inputs within the command line. 
-   1. Install the qxpakwrapper.py and copy it to your instance.
-   2. Download and copy the input files from the Discovery environment which can be found here.  
-   3. Then run the following line of code making sure that all the input files you are calling are within your current working directory.
(this example utilizes all the options, all the example inputs, and uses an output results file with a .CSV extension so that it is easier to read)
(note, this will output directly in your current working directory and has many files as output so )
