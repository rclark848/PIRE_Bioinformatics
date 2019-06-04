Calculating Heterozygosity and Inbreeding Statistics
================

Today we will explore how to calculate heterozygosity and other measures of genetic diversity. We will start by doing some calculations by hand to get everyone familiar with the theory behind most of the analyses we will run in the future. If this material is review for you, please bear with us. We're starting simple so that everyone is on the same page.
\
\
Remember there are two kinds of heterozygosity:

-   **Observed heterozygosity (*H*<sub>*o*</sub>)** is the proportion of individuals that are heterozygous (have two different alleles) at a given locus
-   **Expected heterozygosity (*H*<sub>*e*</sub>)** is the probability of picking two different alleles from a population if you sampled randomly

*H*<sub>*e*</sub> = *H*<sub>*o*</sub> if a population meets Hardy-Weinberg Proportions (HWP).
\
\
In this lab, we are going to calculate the allele frequencies, *H*<sub>*o*</sub> and *H*<sub>*e*</sub> at a particular locus in a sample population. As a quick reminder, the equation for these terms are as follows:
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
*Do the observed and expected heterozygosities match? Using your judgment, does the population seem to be in Hardy-Weinberg equilibrium at this locus?*
\
*(Hint: *H*<sub>*e*</sub> is expected heterozygosity assuming population is at HWE.)*
\
\
\
\
\
\
Exit out of Excel when you are done.

***Understanding the inbreeding coefficient***
----------------------------------------------

\
We can also calculate a metric denoted as *F*<sub>*IS*</sub>, otherwise known as the inbreeding coefficient. This can be thought of as the probability that two alleles at a given locus are identical by descent (inherited from same ancestor). It also represents the mean *reduction* in the *heterozygosity* of an individual due to inbreeding, or non-random mating within a subpopulation. Its value can range from -1 to 1, with 1 indicating a complete reduction in heterozygosity (all individuals are homozygous at a given locus).
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
*How does inbreeding affect long-term population fitness? Why?*