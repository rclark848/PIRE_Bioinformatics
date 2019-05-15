Hardy-Weinberg Proportions (HWP)
================

We are going to build off the previous lab, which looked at different ways to calculate heterozygosity, to assess whether our clownfish populations are in Hardy-Weinberg Proportions (HWP) or not. Remember that departure from HWP can indicate non-random mating, strong selection acting on a locus, or other evolutionary forces at play.
\
\
Look back to the first secion of the heterozygosity lab, where we calculated the frequencies for allele 1 and allele 2, *H*<sub>*e*</sub> and *H*<sub>*o*</sub> by hand. Write these values down below
\
\
*Frequency of allele 1*: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_
\
\
*Frequency of allele 2*: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_
\
\
_*H*<sub>*e*</sub>_: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_
\
\
_*H*<sub>*o*</sub>_: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_
\
\
*Do the observed and expected heterozygosities match? Using your judgment, does the population seem to be in Hardy-Weinberg equilibrium?*
\
*(Hint: *H*<sub>*e*</sub> is expected heterozygosity assuming population is at HWE.)*
\
\
\
\
Open up the Excel file from the previous lab if you closed it out earlier.

***HWP by hand***
-----------------

Let's go further than judgment and see if we can construct a test for this one locus. Let's divide the samples into three genotypes: the *homozygotes* for allele 1 (the 1,1 individuals), the homozygotes for allele 2 (the 2,2, individuals) and the *heterozygotes* (the 1,2 individuals). Note that our locus has 2 alleles.
\
\
If we have Hardy-Weinberg proportions, we expect the number of homozygotes from allele 1 and allele 2 to be
\
\
*E*[*Homozygotes*<sub>1</sub>]=*Np*<sub>1</sub><sup>2</sup> = 8*p*<sub>1</sub><sup>2</sup> = *E*<sub>1</sub>
\
\
*E*[*Homozygotes*<sub>2</sub>]=*Np*<sub>2</sub><sup>2</sup> = 8*p*<sub>2</sub><sup>2</sup> = *E*<sub>2</sub>
\
\
where *N* is the number of individuals and the *p*<sub>*k*</sub>s are the allele frequencies of each allele. Similarly, we expect the number of heterozygotes to be everything else, which we can calculate as
$$E[Heterozygotes] = N(1-sum[p_k^2]) = 8(1 - p_1^2 - p_2^2) = E_{3}$$
Calculate the *E*[*Hom*<sub>1</sub>\], *E*[*Hom*<sub>2</sub>\] and *E[Het]* calculations using the allele frquencies you recorded above
\
\
*E*[*Hom*<sub>1</sub>\]=*E*<sub>1</sub>= \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_
\
\
*E*[*Hom*<sub>2</sub>\]=*E*<sub>2</sub>= \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_
\
\
*E*[*Het*\]=*E*<sub>3</sub>= \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_
\
\
The observed numbers of homozygotes and heterozygotes can be found by counting them up in your file. What are they?
\
\
*O*[*Hom*<sub>1</sub>\]=*O*<sub>1</sub>= \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_
\
\
*O*[*Hom*<sub>2</sub>\]=*O*<sub>2</sub>= \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_
\
\
*O*[*Het*\]=*O*<sub>3</sub>= \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_
\
\
To test whether the observed values (*O*<sub>1</sub>, *O*<sub>2</sub>, and *O*<sub>3</sub>) match the values expected under HWP (*E*<sub>1</sub>, *E*<sub>2</sub>, and *E*<sub>3</sub>), we used a chi-squared (*X*<sup>2</sup>) test. The traditional *X*<sup>2</sup> test takes the form
$$X^2 = sum_{j=1}^{3}(O_{j}-E_{j})^2/E_{j} = (O_{1}-E_{1})^2/E_{1} + (O_{2}-E_{2})^2/E_{2} + (O_{3}-E_{3})^2/E_{3}$$
Let's calculate that value from the data.
\
\
*What is your *X*<sup>2</sup> value? Show your work.*
\
\
\
\
We can compare this answer against a *X*<sup>2</sup>-table to determine statistical significance. With three classes (two homozygote classes and one heterozygote class), we have one degree of freedom (DF). For a *X*<sup>2</sup> with one DF, we have a critical value of 3.84. This critical value means that a value in excess of 3.84 has only a five percent (5%) chance of occurring under the null hypothesis of HWP. We typically say that we reject the null hypothesis of HWP if *X*<sup>2</sup> &gt; 3.84.
\
\
*How large is your answer, compared with the critical value of 3.84? Can we reject the null hypothesis of HWP?*
\
\
\
\
When you are done, don't exit out of Excel yet. You will use it later in the lab.

***HWP with vcftools***
-----------------------

We are now going to check for HWP in our clownfish populations using vcftools. This calculation will give us a test for whether each locus in each population is in HWP.
\
\
Open up PuTTY and log on to your Turing account. Type

``` bash
salloc -c 12
```

We only want to calculate HWP within each population. To do so, we need to create a text file that specifies which individuals to keep and which to exclude for each population, just like in the previous lab. We alraedy have a file for Japan (J), but for now we need files for Indonesia (N) and Philippines (P).
\
\
To get ready, navigate to your andbox if you're not already there

``` bash
cd /cm/shared/courses/Bioinfo_Workshop/sandboxes/yoursandbox/
```

We can then create these files using nano. Create a new text file by typing

``` bash
nano N_individuals.txt
```

Enter the following information (make sure to put each individual ID on a separate line, just like you did when creating the J\_individuals.txt file from the last lab).

``` bash
N1
N2
N3
N4
N5
N6
N7
```

Exit nano and save your work. Create a new text file by typing

``` bash
nano P_individuals.txt
```

Enter the following information, in the same format as before

``` bash
P1
P10
P14
P16
P18
P20
P22
P24
P3
P6
```

Exit nano and save your file.
\
\
To calculate HWP using vcftools, type the following

``` bash
module load vcftools/0.1

vcftools --vcf /cm/shared/coureses/Bioinfo_Workshop/clownfish_data/output.hicov2.snps.only.vcf --hardy --keep J_individuals.txt --out hardy_J
```

Arguments we used:

-   **--vcf** -------- read in data from a VCF file
-   **--hardy** ------ calculate a p-value for each locus from HWP test
-   **--keep** ------- name of the text file with individuals to include in analysis
-   **--out** -------- name of the output file

We will need to calculate HWP for the other two populatiosn as well, so we will run vcftools two more times. Type (each on one line)

``` bash
vcftools --vcf /cm/shared/courses/Bioinfo_Workshop/clownfish_data/output.hicov2.snps.only.vcf --hardy --keep P_individuals.txt --out hardy_P

vcftools --vcf /cm/shared/courses/Bioinfo_Workshop/clownfish_data/output.hicov2.snps.only.vcf --hardy --keep N_individuals.txt --out hardy_N
```

Open the hardy\_J.hwe output file. Each line in the file corresponds to a locus. This file has columns in the following order:

-   Chromosome ID
-   SNP bp position
-   number of observed homozygotes and heterozygotes at the given locus
-   number of expected homozygotes and heterozygotes at the given locus
-   *X*<sup>2</sup>-value
-   p-value for HWP test (null hypothesis is that the population is in HWP at given locus)
-   p-value for heterozygosity deficit
-   p-value for heterozygosity excess

Search for chromosome TRINITY\_DN14497\_c0\_g1\_i1, SNP position 109 by typing

``` bash
/DN14997_c0_g2_i2
```

It turns out the example you did by hand has the same allele frequencies as this locus (in the Japanese population).
\
\
*Do your E(Het), O(Het), and *X*<sup>2</sup>-values match these results? If not, why not?*
\
\
\
\
*Scroll up and down the file. Which loci do you see that might be out of HWP in the Japanese population?*
\
\
\
\
*A locus can be out of HWP due to either a heterozygote excess or a deficit. What processes could cause either a heterozygosity excess or deficit to occur in a population?*
\
\
\
\
Type (all on one line)

``` bash
less /cm/shared/courses/Bioinfo_Workshop/clownfish_data/HWE_all.txt
```

This is a text file constructed from the HWP p-values for all 3 populations at every locus. Search for chromosome TRINITY\_DN36934\_c0\_g2\_i2, SNP position 221.
\
\
*What are the p-values for chromosome TRINITY\_DN36934\_c0\_g1\_i1 SNP position 221 for each population? Are any of the populations out of HWP at this locus?*
\
\
\
\
Go ahead and close out of the HWE\_all.txt file when you are done.

***Data analysis***
-------------------

Use WinSCP on your Desktop to download the HWE\_all.txt file to your local computer (saving it to the desktop or under my documents is fine). Open Excel and then import the file by going to Data -&gt; From Text/CSV and then selecting the file for import.
\
\
Explore these data to see what you can learn. Try sorting these data in different ways, and create scatter plots (or other figures) if you feel they might be of use.
\
\
*Are there any loci that appear to be out of HWP in every population? (If so, list the loci.) What processes could be operating to cause one locus to be out of HWP in every population?*
\
\
\
\
*Do any populations appear to have more loci out of HWP than the other two? If so, which one? What processes could be operating to cause one population to have more loci out of HWP than the other populations?*
