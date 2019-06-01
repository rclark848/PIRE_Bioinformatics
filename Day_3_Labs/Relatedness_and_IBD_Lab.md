Relatedness and Isolation-by-Distance
================

In our last lab, we used *F*<sub>*ST*</sub> as a measure of genetic differentiation among *populations*. Here, we'll use relatedness as a measure of genetic differentiation among *individuals*. Using individual-based measures are especially useful if your samples don't naturally group into populations and are spread more evenly across the landscape.

***Calculate relatedness***
---------------------------

vcftools will calculate relatedness for us (specifically, the probability of choosing identical alleles when randomly sampling one allele from two individuals at a given locus). We'll again exclude the loci that we think may be under selection.

Log on to Turing. From your workspace:

``` bash
salloc -c 12
bash -l

enable_lmod
module load vcftools/0.1
```

Type (all on one line):

``` bash
vcftools --vcf /cm/shared/courses/Bioinfo_Workshop/clownfish_data/output.hicov2.snps.only.vcf --exclude-positions /cm/shared/courses/Bioinfo_Workshop/clownfish_data/outlier_candnames.txt --relatedness2 --out clownfish
```

Arguments we used:

-   **--vcf** ---------------- read in data from a VCF file
-   **--exclude-positions** -- specify name of text file with loci to exclude
-   **--relatedness2** ------- calculate relatedness
-   **--out** ---------------- specify name of output file

Let's look at the output:

``` bash
less clownfish.relatedness
```

The first two columns of the output file give us the individuals being compared (`INDV1` and `INDV2`). The final column (`RELATEDNESS_PHI`) estimates relatedness by giving us the probability of choosing identical alleles when randomly sampling one allele from two individuals at a loci that is heterozygous in at least one of the individuals. Here, anything greater than 0.25 indicates a first-degree relationship (siblings or parent-offspring relationship).

*How related is individual J11 to J13?*
\
\
\
\
*Is individual J11 more or less related to J13 than to P1?*
\
\
\
\
*Why do you think individuals are related with a value of 0.5 to themselves (e.g. INDV1 = J11 and INDV2 = J11 has a relatedness\_phi of 0.5)?* *Hint: Think about what this relatedness score is really indicating.*
\
\
\
\
\
\
Exit out of the `clownfish.relatedness` file when done.

***Plot relatedness vs. geographic distance***
----------------------------------------------

Type

``` bash
module load R/3.4 vegan/2.5
```

Open R by typing

``` bash
R
```

We will read in a matrix of geographic distances (in km) between each sample that I calculated earlier. Type:

``` r
dists <- read.csv("/cm/shared/courses/Bioinfo_Workshop/clownfish_data/dists.csv")
```

To see the last few lines of what you read in, type:

``` r
tail(dists)
```

*How far apart are individuals N6 and N7? (The `geo` column is in kilometers (km).)*
\
\
\
\
Then read in the relatedness values you calculated. Type (all on one line):

``` r
rels <- read.table("/cm/shared/courses/Bioinfo_Workshop/Workspace/yourworkspace/clownfish.relatedness", header=TRUE)
```

And look at it:

``` r
head(rels)
```

Then we can merge the two datasets together:

``` r
dat <- merge(dists, rels, by=c("INDV1", "INDV2"))
```

This allows us to make a plot of relatedness vs. geographic distance:

``` r
pdf(width=5, height=5, file="relatedness.pdf")
plot(dat$geo, dat$RELATEDNESS_PHI, xlab="Distance (km)", ylab="Relatedness")
dev.off()
```

Download the `relatedness.pdf` file from Turing and open it.

*How does relatedness vary with geographic distance?*
\
\
\
\
*Does this fit an isolation-by-distance pattern? Why or why not?*
\
\
\
\
\
\
Log back on to Turing when done.

***Plot *F*<sub>*ST*</sub> vs. geographic distance***
-------------------------------------------------------

Let's switch back to R on Turing and look at isolation-by-distance from a population perspective using *F*<sub>*ST*</sub> instead of relatedness values. First, we will create a dataframe to hold the *F*<sub>*ST*</sub> values we calculated earlier. Type (all on one line):

``` r
fsts <- data.frame(POP1=c("J", "J", "P"), POP2=c("P", "N", "N"), fsts=NA, geo=NA)
```

Then read in the Japan-Philippines *F*<sub>*ST*</sub> values that were output by vcftools in our previous lab and save it to our new dataframe. Type:

``` r
infile <- readLines("/cm/shared/courses/Bioinfo_Workshop/Workspace/yourworkspace/FST_J-P.log")

fsts&fsts[1] <- as.numeric(gsub("Weir and Cockerham weighted Fst estimate: ", '', grep("weighted", infile, value=TRUE)))
```

Look at your dataframe to see that it worked. You should see the `fsts` column begin to fill:

``` r
fsts
```

Now repeat for Japan-Indonesia:

``` r
infile <- readLines ("/cm/shared/courses/Bioinfo_Workshop/Workspace/yourworkspace/FST_J-N.log")

fsts$fsts[2] <- as.numeric(gsub("Weir and Cockerham weighted Fst estimate: ", '', grep("weighted", infile, value=TRUE)))
```

And for Philippines-Indonesia:

``` r
infile <- readLines("/cm/shared/courses/Bioinfo_Workshop/Workspace/yourworkspace/FST_P-N.log")

fsts$fst[3] <- as.numeric(gsub("Weir and Cockerham weighted Fst estimate: ", '', grep("weighted", infile, value=TRUE)))
```

Look at your dataframe to see that it worked. The `fsts` column should be filled with values now:

``` r
fsts
```

*What is the *F*<sub>*ST*</sub> between Philippines and Indonesia?*
\
\
\
\
We'll calculate geographic distances as the average among all pairwise distances between individuals, first for Japan and Philippines, then J-N and P-N:

``` r
fsts$geo[1] <- mean(dists$geo[grepl("J", dists$INDV1) & grepl("P", dists$INDV2)])
fsts$geo[2] <- mean(dists$geo[grepl("J", dists$INDV1) & grepl("N", dists$INDV2)])
fsts$geo[3] <- mean(dists$geo[grepl("P", dists$INDV1) & grepl("N", dists$INDV2)])
```

Look at your dataframe to see that it worked. The geo column should be filled with values now:

``` r
fsts
```

*What is the average geographic distance between individuals in the Philippines and Indonesia?*
\
\
\
\
Isolation-by-distance theory predicts that *F*<sub>*ST*</sub>/(1 − *F*<sub>*ST*</sub>) should have a linear relationship with distance (in 1D space) or ln(distance) (in 2D space). Either way, we should transform *F*<sub>*ST*</sub>:

``` r
fsts$linfst <- fsts$fst/(1-fsts$fst)
```

Now we can plot linearized *F*<sub>*ST*</sub>s vs. distance, with a best fit line added for good measure:

``` r
pdf(width=5, height=5, file="fsts.pdf")
plot(fsts$geo, fsts$linfst, xlab="Distance (km)", ylab="Linearized FST")
abline(lm(linfst ~ geo, data=fsts))
dev.off()
```

Download this plot (`fsts.pdf`) and look at it.

*What evidence do you see for or against isolation-by-distance patterns at the population level?*
\
\
\
\
\
\
Finally, we'll run a statistical test for a relationship between *F*<sub>*ST*</sub> and geographic distance. Because our pairwise distance measures aren't independent, we can't use a linear regression. Instead, we use a Mantel test, which tests for correlations among matrices.
Back in R on Turing, we'll load a package with a Mantel test and then use it:

``` r
require(vegan)
```

First, turn our *F*<sub>*ST*</sub> dataframe into a distance matrix:

``` r
un1 <- unique(unlist(fsts[,1:2]))
fstmat <- matrix(0, nrow=length(un1), ncol=length(un1), dimnames=list(un1, un1))
fstmat[cbind(match(fsts$POP1, rownames(fstmat)), match(fsts$POP2, colnames(fstmat)))] <- fsts$linfst
fstmat <- fstmat + t(fstmat)
```

Look at it:

``` r
fstmat
```

Now, let's do the same for our geographic distances:

``` r
geomat <- matrix(0, nrow=length(un1), ncol=length(un1), dimnames=list(un1, un1))
geomat[cbind(match(fsts$POP1, rownames(geomat)), match(fsts$POP2, colnames(geomat)))] <- fsts$geo
geomat <- geomat + t(geomat)
```

Look at it:

``` r
geomat
```

With our data formatted, we're finally ready to run a Mantel test:

``` r
mantel(fstmat, geomat)
```

The results are reported to the screen. The Mantel statistic *r* is a measure of correlation from 0 (low) to 1 (high). The p-value is reported as `Significance`.

*How correlated are *F*<sub>*ST*</sub> and geographic distance? Is this value low or high?*
\
\
\
\
*Is the correlation statistically significant?*
\
\
\
\
*Please explain how you might change the study design to better test for isolation-by-distance patterns.*