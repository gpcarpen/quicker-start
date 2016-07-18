> Prerequisites

> Stampede Files:

>            a. Validate
       
>            b. BED, BIM, FAM, and	Phenotype files	
       
>            c. Known	Truth	File

# Job Launcher,	FastLMM,	and	Winnow

### Notes
- I	will	be	using	8	of	the	Syngenta	data	sets	
(i.e.	PheHasStruct_001_Trait_H_06_GenotypeData_NoMissing	…
…	PheHasStruct_008_Trait_H_06_GenotypeData_Nomissing)
- My	Syngenta	data	is	organized	– for	example	my	first	data	set	– as:
$HOME/syn/one/

- The	output	from	FastLMM will	be	stored	in:
$HOME/syn/output


- The	location	of	the	Fast	LMM	executable	on	my	system is:
$HOME/Validate-Master-master/CurrentReleaseStable/GWAS_09/fastlmmc


- The	location	of	the	main	Winnow	file	on	my	system	is:
$HOME/Validate-Master-master/CurrentReleaseStable/Winnow_09/winnow.py


### Setting	Up	the	Parametric	Launcher	Job	File
- The	parametric	launcher	uses	a	paramlist	file	(text	file	with	no	extension)	to	execute	
jobs.	Each	line	in	this	file	represents	a	task.
- Create	a	paramlist	file,	the	command	“vim	paramlist”	creates	the	file	and	opens	the	VIM	
editor.	(Enter	“i”	to	enter	insert	mode,	“ESC”	to	exit	insert	mode,	and	“:wq” to	save	and	
exit	VIM)
- On	each	line,	enter	the	fastlmm	command	pertaining	to	one	of	the	datasets.	

My	first	line	is:

>>$HOME/Validate-Master-master/CurrentReleaseStable/GWAS_09/fastlmmc -bfile
$HOME/syn/one/PheHasStruct_001_Trait_H_06_GenotypeData_NoMissing	-bfilesim
$HOME/syn/one/PheHasStruct_001_Trait_H_06_GenotypeData_NoMissing	-pheno
$HOME/syn/one/PheHasStruct_001_Trait_H_06_GenotypeData_NoMissing.fampheno.txt	-out
$HOME/syn/output/oneOut.txt”


My	last	line	is:
>>“$HOME/Validate-Master-master/CurrentReleaseStable/GWAS_09/fastlmmc -bfile
$HOME/syn/eight/PheHasStruct_008_Trait_H_06_GenotypeData_NoMissing	-bfilesim
$HOME/syn/eight/PheHasStruct_008_Trait_H_06_GenotypeData_NoMissing	-pheno
$HOME/syn/eight/PheHasStruct_008_Trait_H_06_GenotypeData_NoMissing.fampheno.txt	-out	
$HOME/syn/output/eightOut.txt”

- Click the	escape key followed by “:wq” to save and exit VIM.	


### Setting	Up	the	Winnow	Job	File
- Create	a	.sh	file	for	running	Winnow.	Enter	“vim	winnow_job.sh”.	This	is	a	normal	job	
file	for	SLURM.	

- Enter	the	following:

-      #!/bin/bash

-      #SBATCH –t 04:00:00

-      #SBATCH –n 1

-      #SBTACH –p normal

-      python $HOME/Validate-Master-master/CurrentReleaseStable/Winnow_09/winnow.py	--Folder

-      $HOME/syn/output --Class $HOME/syn/SynTruth06.txt --Snp SNP --Score Pvalue --filename 

-      $HOME/syn/winnow_output --kttype OTE --seper tab

- --python	…	…	winnow.py	is	the	command	to	run	winnow
- --Folder	___	is	the	folder	containing	the	FastLMM	output	as	noted	above.	
-      -Notice	this	is	the	output	folder	designated	in	the	FastLMM	commands from	the	paramlist	file.

- --Class	is	the	known	truth	file	corresponding	to	the	Syngenta	data	sets

- --Snp is	the	header	of	the	SNP	column.	For	FastLMM	this	is	SNP.    

- --Score	is	the	header	of	the	p-value	column.	For	FastLMM	this	is	Pvalue.

- --filename	is	the	output	file.

- --kttype	is	the	known-truth	type.	OTE	in	this	case.


### Running
- Enter “module load launcher”

- Make sure the statsmodels package is installed, enter “pip install --user statsmodels”

- Make sure that you are in the same directory as the paramlist file.

- Enter “sbatch –N 2 –n 4 $TACC_LAUNCHER_DIR/launcher.slurm”

       o This	creates a job with two nodes with two tasks per node.

- You will receive a message along the lines of “Submitted batch job 665014.” Take note of that number, it is the job id.	

- We don’t want to execute the winnow job until the FastLMM job is completed, so we will use the --dependency flag.

- Enter “sbatch --dependency=afterok:6685014 winnow_job.sh”

       o This	will submit the winnow_job.sh job but it will not begin until the job with id 6685014 has completed.	

- When	you check your queue you should see something like this: As you can see, the winnow job (ID 6685021) is pending because of a Dependency
