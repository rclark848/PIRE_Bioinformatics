Calculating Heterozygosity and Inbreeding Statistics
================

Today we will explore how to calculate heterozygosity and other measures of genetic diversity. We will start by doing some calculations by hand, and then move to the computer cluster to see how we can use different programs to compute the calculations for us. If this material is review for you, please bear with us. We're starting simple so that everyone is on the same page.
Remember there are two kinds of heterozygosity:

-   **Observed heterozygosity (*H*<sub>*o*</sub>)** is the proportion of individuals that are heterozygous (have two different alleles) at a given locus
-   **Expected heterozygosity (*H*<sub>*e*</sub>)** is the probability of picking two different alleles from a population if you sampled randomly

*H*<sub>*e*</sub> = *H*<sub>*o*</sub> if a population meets Hardy-Weinberg Proportions (HWP).
\
\
In this lab, we are going to calculate the allele frquencies, *H*<sub>*o*</sub> and *H*<sub>*e*</sub> at a particular locus in a sample population. As a quick reminder, the equation for these terms are as follows:
\
\
***Allele frequencies*** can be calculated as: *(copies of given alleles)/(total number alleles in population)*
\
\
*__Observed heterozygosity (*H*<sub>*o*</sub>)__* can be calculated as: *N(Het)/N* where *N*(*Het*) is the number of individuals that are heterozygous at a given locus and *N* is the total number of individuals in the population.
\
\
*__Expected heterozygosity (*H*<sub>*e*</sub>)__* can be calculated as: 2*pq* where *p* is the allele frequency of allele 1 and *q* is the allele frequency of allele 2 (at a biallelic locus).

***Heterozygosity by hand***
----------------------------

\
Navigate to <https://github.com/rclark848/PIRE_Bioinformatics>. This is a repository that contains .md (markdown) and .Rmd (R markdown) copies of all the labs we will be doing over the next three days. It is also home to any data, scripts, or input files you will need for the upcoming analyses. Open up the directory titled `Day_1_Labs` and then download the Excel file titled `Genotypes.xlsx`. (Click on `Genotypes.xlsx` and then click `Download`.)
\
\
The first line of the data file shows you four things, each in a cell: 1) the number of loci, 2) the number of individuals, 3) the number of populations, and 4) the number of individuals in the first population. Enter this below:
\
\
\
*Number of loci:*\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_
\
\
\
*Number of individuals:*\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_
\
\
\
*Number of populations:*\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_
\
\
\
*Number of individuals in population \#1:*\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_
\
\
The third line of the file begins the genotype data. Column 1 has the individual ID, column 2 has the population name, and columns 3 and 4 have the two alleles for each individual (these individuals are diploid) at a particular locus. The alleles are coded as 1 or 2 (e.g., these might represent A and T at a single nucleotide polymorphism).
\
\
*What is the genotype of individual J19?*
\
\
\
\
*What is the allele frequency of allele \#1?*
\
(Hint: Refer to the first page of the lab if you forget how to calculate allele frequencies. In Excel, simply click on a blank cell and type `=`. Then count the number of times allele 1 appears and type that after the `=`. Divide that by the total number of alleles in the population. Hit `Enter`.)
\
\
\
\
*What is the allele frequency of allele \#2?*
\
\
\
\
*What is your expected heterozygosity (*H*<sub>*e*</sub>)?*
\
(Hint: Refer to the first section of the lab if you forget how to calculate *H*<sub>*e*</sub>. In Excel, simply click on a blank cell and type `=2`. Then multiply that two by the two allele frequencies you just calculated. Hit `Enter`.)
\
\
\
\
*What is your observed heterozygosity (*H*<sub>*o*</sub>)?*
\
(Hint: Refer to the first section of the lab if you forget how to calculate *H*<sub>*o*</sub>. In Excel, simply click on a blank cell and type `=`. Then count the number of heterozygotes in the population and type that after the `=`. Divide that by the total number of individuals in the population. Hit `Enter`.)
\
\
\
\
*How does the expected heterozygosity compare to the maximum possible heterozygosity for a biallelic locus?*
\
\
\
\
*What are the implications of a very low heterozygosity for an individual locus? Why?*
\
\
\
\
\
\
Exit out of Excel when you are done.

***Heterozygosity with vcftools***
----------------------------------

Heterozygosity can be calculated in two different ways:

1.  ***Heterozygosity per locus:*** Expected (or observed) proportion of heterozygous individuals at a locus in a population
2.  ***Heterozygosity per individual:*** Expected (or observed) proportion of heterozygous loci in an individual

When we did our heterozygosity calculations by hand, we measured heterozygosity on a per locus basis. Let's try calculating heterozygosity per individual using **vcftools**.
\
\
Open up PuTTY and log on to your Turing account. Type

``` bash
salloc -c 12
bash -l
```

For the labs today (and the rest of the week) we will be working with a VCF file that contains genotype information for clownfish from three different populations (Japan, Philippines, and Indonesia). Open up the VCF file by typing (all on one line)

``` bash
less -S /cm/shared/courses/Bioinfo_Workshop/clownfish_data/output.hicov2.snps.only.vcf
```

To skip the header and get to the data part of the file, search for the word `CHROM` by typing

``` bash
/CHROM
```

and hitting `enter`. `CHROM` is useful because it's a word in the header of the data section.
\
\
The header line starts with `#CHROM` and has the following columns:

-   **CHROM** ------------ the name of the "chromosome" or contig in our case
-   **POS** -------------- the basepair position of the SNP on the contig
-   **ID** --------------- a name for this variant (left as ".")
-   **REF** -------------- the reference allele at this position
-   **ALT** -------------- the alternate allele at this position
-   **QUAL** ------------- phred-scaled quality score for if this position is a SNP
-   **FILTER** ----------- indicates if a SNP passed filters
-   **INFO** ------------- lots of information about the SNP
-   **FORMAT** ----------- defines the order of dat in the genotype columns. GT:AD:DP:GQ:PL means genotype (0 for reference, 1 for alternate), depths of reads for each allele, total depth of reads, Phred score, Phred-scaled genotype likelihoods
-   **Name of samples** -- each of these columns is for the individual given in the header

The sample names are coded so that J represents Japan, P represents Philippines, and N represents individuals from Indonesia.
\
\
To quit from the less program, type

``` bash
q
```

Now navigate to your workspace if you're not there already

``` bash
cd /cm/shared/courses/Bioinfo_Workshop/Workspace/yourworkspace/
```

At first, we only want to calculate the heterozygosity of individuals from the Japanese population. To do so, we need to create a text file that specifies which individuals to keep and which to exclude. Create a new text file by typing

``` bash
nano J_individuals.txt
```

The text file is super simple: it just needs to have the names of all the individuals that we want to group together in a population. The names need to match what is in the .vcf file. Therefore, enter the following information (make sure to put each individual ID on a separate line):

``` bash
J3
J5
J9
J11
J13
J15
J17
J19
```

To exit nano, look at the bottom of the screen. You will see that it says `^X` for Exit. This means `Control X`. Type that, then follow the instructions to save the file as `J_individuals.txt`.
\
\
To calculate heterozygosity using vcftools, we need to load the program first. Type the following (all on one line):

``` bash
module load vcftools/0.1
```

Now we can run vcftools. Type (all on one line)

``` bash
vcftools --vcf /cm/shared/courses/Bioinfo_Workshop/clownfish_data/output.hicov2.snps.only.vcf --het --keep J_individuals.txt --out het_J
```

Arguments we used:

-   **--vcf** --- read in data from a VCF file
-   **--het** --- calculate heterozygosity (really homozygosity) per individual
-   **--keep** -- specify name of text file with individuals to include
-   **--out** --- specify name of output file

Open the `het_J.het` ouput file by typing

``` bash
less het_J.het
```

Each line in the file corresponds to an individual. This file has columns in the following order:

-   Individual ID
-   Number of homozygous loci (observed)
-   Number of homozygous loci (expected)
-   Number of loci that were included in the analysis
-   Fixation index (inbreeding coefficient -- defined in the section below)

As you can tell, vcftools calculates homozygosity instead of heterozygosity.
\
\
*Calculate the expected (*H*<sub>*e*</sub>) and observed (*H*<sub>*o*</sub>) \# of heterozygous loci for individual J19.*
\
(Hint: To calculate *H*<sub>*o*</sub>, simply subtract O(Hom) from the total number of loci included in th analysis. To calculate *H*<sub>*e*</sub>, subtract E(Hom) from the total number of loci.)
\
\
\
\
*How do *H*<sub>*o*</sub> and *H*<sub>*e*</sub> in J19 compare to the values in other individuals in the population?*
\
\
\
\
Exit out of the `het_J.het` file when finished.

***Understanding the inbreeding coefficient***
----------------------------------------------

\
vcftools also calculates a metric denoted as *F*<sub>*IS*</sub>, otherwise known as the inbreeding coefficient. This can be thought of as the probability that two alleles at a given locus are identical by descent (inherited from same ancestor). It also represents the mean *reduction* in the *heterozygosity* of an individual due to inbreeding, or non-random mating within a subpopulation. Its value can range from -1 to 1, with 1 indicating a complete reduction in heterozygosity (all individuals are homozygous at a given locus).
\
\
We can estimate the inbreeding coefficient (*F*<sub>*IS*</sub>) for an individual by hand using the following formula:
*F*=1−(*H*<sub>*o*</sub>)/(*H*<sub>*e*</sub>)
\
\
*What do you think an *F*<sub>*IS*</sub> of 0 indicates?*
\
\
\
\
*Using your previously calculated values of *H*<sub>*e*</sub> and *H*<sub>*o*</sub>, what is the inbreeding coefficient for individual J19? (Show your work.)*
\
\
\
\
*Now look at the `het_J.het` file. Does your value match the results from vcftools? Why or why not?*
\
\
\
\
\
\
*How does *F*<sub>*IS*</sub> for individual J19 compare to the *F*<sub>*IS*</sub> of other individuals in Japan?* *Is *F*<sub>*I*</sub> in Japan generally low or high? (Remember, *F*<sub>*IS*</sub> is capped between -1 and 1.)*
\
\
\
\
\
\
*How does inbreeding affect long-term population fitness? Why?*