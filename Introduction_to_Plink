# Plink

## What is Plink

Used to perform different analysis on genotype data. For example:
- Quality control which involves cleaning data to remove errors and problematic samples
-	Associations studies which find connections between genetic variants and diseases or traits
-	Analyissng generic differences between populations

Plink can be used to prepare data for polygenic risk score analysis. -	PLINK helps filter variants based on statistical significance and applies weights (effect sizes) to each variant in the score calculation.

1. When using PLINK the first thing you must do is call the software, which we saved in an app in the OneDrive earlier. 
2. 	The next thing you do is import the data file which can come in three formats.
o	- - bfile prefix loads binary files (.bed, .bim, .fam)
o	- - ped file.ped  and –map file.map loads text based PED/MAP files 
o	- - vcf file.vcf loads files in a VCE format.
3.	Next you apply flags to the data which are operations or filters you want to perform on the data. For example;
o	 --chr 1 keeps only chromosome 1 
o	 --maf 0.05 removes SNPs with minor allele frequency below 5% 
o	 --recode converts the format 
o	 --hardy calculates Hardy-Weinberg equilibrium
4.	Then to set the output file name. This - - out flag specifies where and what to name the results. 
o	--out results/mydata creates output files like mydata.bed, mydata.log, etc.
