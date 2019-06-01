Hardy-Weinberg Proportions (WHP) & Linkage Disequilibrium (LD)
================

First, we are going to pick up where we left off this morning thinking about expected heterozygosity, observed heterozygosity, and Hardy-Weinberg proportions (HWP). Remember that departure from HWP can indicate non-random mating, strong selection acting on a locus, or other evolutionary forces at play.
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
Open up the Excel file from the previous lab if you closed it out earlier.

***HWP by hand***
-----------------

Let's go further than judgment and see if we can construct a test for this one locus. Let's divide the samples into three genotypes: the *homozygotes* for allele 1 (the 1,1 individuals), the homozygotes for allele 2 (the 2,2 individuals) and the *heterozygotes* (the 1,2 individuals). Note that our locus has 2 alleles.
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
\
\
*E*[*Heterozygotes*]=*N*(1-*sum*[*p*<sub>*k*</sub><sup>2</sup>]) = 8(1 - *p*<sub>1</sub><sup>2</sup> - *p*<sub>2</sub><sup>2</sup>) = *E*<sub>3</sub>
\
\
Calculate the *E*[*Hom*<sub>1</sub>\], *E*[*Hom*<sub>2</sub>\] and *E[Het]* calculations using the allele frequencies you recorded above
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
\
\
*X*<sup>2</sup> = *sum*[(*O*<sub>*j*</sub> - *E*<sub>*j*</sub>)<sup>2</sup>/*E*<sub>*j*</sub>] = (*O*<sub>1</sub> - *E*<sub>1</sub>)<sup>2</sup>/*E*<sub>1</sub> + (*O*<sub>2</sub> - *E*<sub>2</sub>)<sup>2</sup>/*E*<sub>2</sub> + (*O*<sub>3</sub> - *E*<sub>3</sub>)<sup>2</sup>/*E*<sub>3</sub>
\
\
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
When you are done, go ahead and exit out of Excel.

***HWP with vcftools***
-----------------------

We are now going to check for HWP in our clownfish populations using vcftools. This calculation will give us a test for whether each locus in each population is in HWP.
\
\
Open up PuTTY and log on to your Turing account. Type

``` bash
salloc -c 12
bash -l
```

We only want to calculate HWP within each population. Today, we are going to continue to focus on the Japanese population.
\
\
To get ready, navigate to your workspace if you're not already there

``` bash
cd /cm/shared/courses/Bioinfo_Workshop/Workspace/yourworkspace/
```
To calculate HWP using vcftools, type the following

``` bash
module load vcftools/0.1

vcftools --vcf /cm/shared/courses/Bioinfo_Workshop/clownfish_data/output.hicov2.snps.only.vcf --hardy --keep J_individuals.txt --out hardy_J
```

Arguments we used:

-   **--vcf** -------- read in data from a VCF file
-   **--hardy** ------ calculate a p-value for each locus from HWP test
-   **--keep** ------- name of the text file with individuals to include in analysis
-   **--out** -------- name of the output file

Open the `hardy_J.hwe` output file. Each line in the file corresponds to a locus. This file has columns in the following order:

-   Chromosome ID
-   SNP bp position
-   Number of observed homozygotes and heterozygotes at the given locus
-   Number of expected homozygotes and heterozygotes at the given locus
-   *X*<sup>2</sup>-value
-   p-value for HWP test (null hypothesis is that the population is in HWP at given locus)
-   p-value for heterozygosity deficit
-   p-value for heterozygosity excess

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
*What process could cause one locus to be out of HWP in several populations?*
\
\
\
\
\
\
Exit out of `hardy_J.hwe` when you are done.

## *__Calculating LD__*

\
Linkage disequilibrium (also called gametic disequilibrium) is the non-random association of alleles at two different loci. For example, imagine two loci. One has alleles A and T and the other has C and G. These two loci would be in strong linkage disequilibrium if A always appears with C, and T always appears with G. We generally find stronger linkage between loci that are physically close to each other on a chromosome or in regions of a chromsome with less recombination, and between loci on which selection is acting jointly.

vcftools conveniently calculates *r*<sup>2</sup> (a measure of LD) between pairs of loci for us. To do this type (all on one line)

``` bash
vcftools --vcf /cm/shared/courses/Bioinfo_Workshop/clownfish_data/output.hicov2.snps.only.vcf --geno-r2 --ld-window-bp 5000 --keep J_individuals.txt --out ld_J
```

Arguments we used:

-   **--vcf** ----------- read in data from a VCF file
-   **--geno-r2** ------- calculate LD as squared correlation coefficient between genotypes
-   **--ld-window-bp** -- defines maximum number of bases between SNPs being tested
-   **--keep** ---------- specify name of the text file with individuals to include in analysis
-   **--out** ----------- specify name of output file

Now open the output file in less

``` bash
less ld_J.geno.ld
```

This file is organized in columns:

-   **CHR:** The name of the chromosome (or in our case, the contig from the transcriptome)
-   **POS1:** The position of the first locus
-   **POS2:** The position of the second locus
-   **N\_INDIV:** The number of individuals for which genotypes were available at these loci
-   **R^2:** The squared correlation coefficient between genotypes (`-nan` means a calculation was not possible)

Remember that you can search within less by typing `/` and the search string. Since a period (.) usually means any character, you can put a `\` before a period to force less to look for an actual period, as in

``` bash
/0\.5
```

to look for "0.5" in the file. You can move to the next instance of the search string by typing

``` bash
n
```

*Please find five (5) pairs of loci with *r*<sup>2</sup> &gt; 0.8 and list them here. (Please list both contig name and position of the SNPs.)*
\
\
\
\
*What does high LD imply about the statistical independence between the loci in each pair?*
\
\
\
\
Quit from less when you are done

``` bash
q
```

***Make a plot of LD vs. distance between SNPs***
-------------------------------------------------

We are going to make a plot from these data to show how linkage changes on average as the distance between pairs of loci increases. To do so, we will use a statistical program called R. R is very flexible and useful for a wide range of tasks, but we'll learn more about it next week. Type:

``` bash
module load R/3.4 data.table/1.11
R
```

R can be customized by loading specialized functions that come in packages. We'll load one package that is useful for reading and working with large data files:

``` r
require(data.table)
```

Now we'll read in the file with our LD data:

``` r
dat <- fread("ld_J.geno.ld")
```

It will be easier if we remove a strange character (^) from one of the column names:

``` r
setnames(dat, 5, "r2")
```

We can then calculate the *log*<sub>10</sub> distance between each pair of sites:

``` r
dat[,logdist:=log10(abs(POS2-POS1))]
```

We want to calculate average LD for all pairs of loci with a similar distance apart. Here, we'll round distance down to the nearest multiple of 0.25 *log*<sub>10</sub> basepairs apart:

``` r
dat[,distclass:=floor(logdist/0.25)*0.25+0.25/2]
```

We can then easily calculate average *r*<sup>2</sup> within each distance class:

``` r
bins <- dat[!is.na(r2),.(r2ave=mean(r2)), by=distclass]
```

Now sort by distance class:

``` r
setkey(bins, distclass)
```

And make a plot of average *r*<sup>2</sup> vs. *log*<sub>10</sub> distance! We will write the plot straight to a PDF file on Turing. The `pdf()` command starts the plot, and the `dev.off()` command ends writing to the plot.

``` r
pdf(width=4, height=4, file="ld_decay.pdf")
bins[,plot(distclass, r2ave, type="1", xlab="Distance (log10 bp)", ylab="Average correlation (r2)", main="LD decay", xlim=c(0,3))]
dev.off()
```

Quit from R by typing:

``` bash
q()
```

And then typing

``` bash
n
```

To choose not to save your workspace (it's not necessary).
\
\
Now use WinSCP to download the pdf that you just made to your local computer. The absolute path to the pdf is

``` bash
/cm/shared/courses/Bioinfo_Workshop/Workspace/yourworkspace/ld_decay.pdf
```

*Please describe how linkage between loci varies as a function of physical distance between them.*
\
\
\
\
*At what distance (in bp) does average LD flatten out to a low value?*
\
Hint: The x-axis on your graph is in *log*<sub>10</sub> bp so you will have to convert back to bp.
\
\
\
\
*We ran this analysis on data from RNAseq. How does this affect the analysis, compared to a similar analysis that might be run on RADseq or whole genome sequencing data?*
