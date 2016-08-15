>  Time ~30min

>  Prerequisities - Agave CLI, general knowledge of executing using Agave, Access to the Discovery Environment within CyVerse, and Stampede allocation (if you want)

>  Helpful Resources
>> Qxpak documentation http://bmcbioinformatics.biomedcentral.com/articles/10.1186/1471-2105-12-202

>>  Qxpak example input http://mirrors.iplantcollaborative.org/browse/iplant/home/shared/iplantcollaborative/example_data/qxpak/input

>>  Qxpak example output http://mirrors.iplantcollaborative.org/browse/iplant/home/shared/iplantcollaborative/example_data/qxpak/output

>> Qxpak dependecies https://github.com/UNCW-iPlant/Stampede-Files/tree/master/GWASTools/qxpak-5.05


## To Begin, Command Line Usage
-   Normally in QxPak you would alter the parameter file so that you call specific input files for each data analysis fun. This tutorial is written around a wrapper script that was written to make the process of data analysis more easy to do with many different inputs. Instead of having to alter the parameter file each time, you can simply changes the inputs within the command line. 
-   1. Install the qxpakwrapper.py and copy it to your instance.
-   2. Download and copy the input files from the Discovery environment which can be found here.  
-   3. Then run the following line of code making sure that all the input files you are calling are within your current working directory.

```qxpakwrapper.py -p parameterFile.par -d dataFile.dat -g pedigreeFile.ped -m markerFile.mkr -i userInverse.inverse -t UserDirect.direct -h haplotypes.haplo -o results.csv```


```(this example utilizes all the options, all the example inputs, and uses an output results file with a .CSV extension so that it is easier to read)```

```(note, this will output directly in your current working directory and has many files as output so )```

-   4.After you copy this line into your terminal and press enter a large amount of data will scroll through the terminal and when the QxPak analysis has finished the terminal prompt will return.

##  Explaination of flags
|          |                                                                                                                          |
|--------------|--------------------------------------------------------------------------------------------------------------------------|
| -p, --par    | Name of the parameter file using the $ markers above.                                                                    |
| -d, --data   | Name of the data file; the replacement for $data.                                                                        |
| -g, --ped    | Name of the pedigree file; the replacement for $pedigree.                                                                |
| -m, --mkr    | Name of the marker file; the replacement for $marker.                                                                    |
| -i, --uInv   | Name of the user-defined inverse file; replacement for $userInverse.                                                     |
| -t, --uDir   | Name of the user-defined direct file; replacement for $userDirect.                                                       |
| -h, --haplo  | Name of the haplotype file; replacement for $haplotype.                                                                  |
| -o, --output | Name of the output file; defaults to result.txt. Several other files may be generated depending upon the parameter file. |

##  Explaination of input files
### Parameter File
-   A parameter file should be prepared and uploaded to the Data Store along with the other input files. Some special markers, though, are replaced by the wrapper program so that filenames do not need to be (and should not be) hardcoded into the parameter file. Specifically, the following markers should be used, and they will be replaced with the command line arguments.

|              |                                                    |
|--------------|----------------------------------------------------|
| $data        | Data file                                          |
| $pedigree    | Pedigree file                                      |
| $marker      | Marker file                                        |
| $userInverse | User inverse - user-defined covariance matrix file |
| $userDirect  | User direct - user-defined covariance matrix file  |
| $haplotype   | Haplotype file                                     |
| $output      | Output file                                        |

### Data File
- The data file is a .dat file, a free-format file without a header that always contains the individual in the first column, whether it be numeric or alphanumeric. Record order is not important. Subsequent columns include traits and effects and may include more than are used in the model.

```
(Missing values must be coded as 0. If the actual value is 0, recode it as 0.000001.)
```

### Pedigree File
- A pedigree file is required for quantitative trait locus (QTL) analysis. This file includes the individual, father, mother, sex, and breed. The last two are optional if analyzing non-sex chromosomes or within breed populations. Individuals do not have to be coded; missing parents should be indicated with a 0. Breed is irrelevant unless at least one parent is unknown.

### Marker File
- Two formats are available: “usual” and “transposed”. In the usual format, the first record contains the chromosome name and successive records contain: individual, allele1_mkr1, allele2_mkr1, etc. Missing alleles are specified by 0.

- The transposed format is appropriate when there are many more markers than individuals. In this format, the first row is a list of individual codes, and successive rows contain: SNP_name, chr_number, ind1_allele1, ind1_allele2, ind2_allele1, ind2_allele2, etc. Unknown markers should be coded as 0, and chromosomes must have numbers rather than names; markers should be arranged by chromosome 1, 2, etc.

## Optional inputs
### User-Defined Covariance Matrix Files

- One or two files can be included to allow for the including of random effects distributed as N(0,V), where V can be any positive definite matrix which is stored in the file. The matrix is then invertyed to obtain random effects predictions, and the inverse can also be included to save computation. The parameter file must be modified appropriately to apply the effects to specific columns.

- The format of these files is: row, column, value in space-delimited form like the other files.

### Haplotype File

- Contains known haplotypes if any. The first record contains the name of the chromosome. Successive records include individual, order of markers where phases known. If several chromosomes are analyzed, the format should be repeated for each.
 
## Explanation of Output Files

### q.0

- Contains running output that might be useful for, among other things, checking convergence.

### Primary Output File

- A variety of different results are reported in the same file.

### Haplotype Output File

- If the applicable section in the parameter file is specified, the haplotypes sampled at each MCMC iteration are written. The format is: chromosome, MCMC_iteration, individual, phase, alleles.

### Z Files

- Z files contain the IDB probabilities or SNP configurations.

### Other Output Files

- There are numerous other undocumented output files.
