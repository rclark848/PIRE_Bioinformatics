Linkage Disequilibrium (LD)
================

Linkage disequilibrium (also called gametic disequilibrium) is the non-random association of alleles at two different loci. For example, imagine two loci. One has alleles A and T and the other has C and G. These two loci would be in strong linkage disequilibrium if A always appears with C, and T always appears with G. We generally find stronger linkage between loci that are physically close to each other on a chromosome or in regions of a chromsome with less recombination, and between loci on which selection is acting jointly.

***Calculating LD***
--------------------

First, log in to Turing, navigate to your workspace, and get a node to work on:

``` bash
salloc -c 12
bash -l
```

vcftools conveniently calculates *r*<sup>2</sup> (a measure of LD) between pairs of loci for us. To do this type

``` bash
module load vcftools/0.1
```

Then type (all on one line)

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
You can put together another reasonably complex search to look for a tab (\t) followed by a one (1), followed by an end of line character ($). This works because *r*<sup>2</sup> is at the right-hand side of each line:

``` bash
/\t1$
```

*Can you find any pairs of loci with *r*<sup>2</sup> = 1 that are more than 1000 bp apart? If so, list the pairs here. (Please list both contig name and position of the SNPs.)*
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
/cm/shared/courses/Bioinfo_Workshop/sandboxes/yoursandbox/ld_decay.pdf
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
