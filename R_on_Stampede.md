>  Time ~min
>  Prerequisities - Agave CLI, Access to the Data Store within CyVerse, General knowledge of R, and Stampede allocation

>  Purpose of this tutorial - This is a list of how to complete frequent user tasks compiled from use cases with the relevant commands 

>  Useful resources
>   - Discovery Environment https://de.iplantcollaborative.org/de/

## Loading and installing the version of R is the base version of R
- Login to your stampede allocation username@stampede.tacc.utexas.edu
- Enter the following commands which will load, save, and then allow you to run R
```
module load R
module save
R
```

## Downloading and installing a more current version of R

- Enter the following commands to download and 

```
cdw
wget http://cran.utstat.utoronto.ca/src/base/R-3/R-3.2.2.tar.gz (this will change depending on which version you want)
tar xzvf R-3.2.2.tar.gz (this will change depending on which version you want)
cd R-3.2.2
./configure
make
make check
echo "PATH=\$PATH:\$WORK/R-3.2.2/bin" >> ~/.bashrc
source ~/.bashrc
cdh
module unload R
module save
R
```

## Installing a package

```
install.packages('package_name', dependencies=TRUE, repos='http://cran.rstudio.com/')
```

    (This might give you a warning that says, "package 'x' is not available (for R version 3.2.2))
    (This warning can be ignored)

## Removing a module

```
rm -r R-3.2.5*
```

## Removing a file

```
rm filename 
```
