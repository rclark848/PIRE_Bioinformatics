*F*<sub>*ST*</sub> From Transcriptomic Data
================

In this lab, we are going to investigate *F*<sub>*ST*</sub> values. *F*<sub>*ST*</sub> values (or fixation indices) are a measure of population differentiation due to population structure. They compare the amount of variation among subpopulations to the amount of variation in the entire population.
\
\
*F*<sub>*ST*</sub> values range from 0 to 1. A value of 0 indicates that there is no differentiation among subpopulations (all subpopulations have the same allele frequencies). A value of 1 indicates complete differentiation among subpopulations (all subpopulations are fixed for different alleles).
\
\
We have looked at *F*<sub>*ST*</sub> values before when we ran BayeScan and identified *F*<sub>*ST*</sub> outliers, or loci that diverge more than "expected" due to selection. Selection is not the only evolutionary process that can affect *F*<sub>*ST*</sub> values, however. Gene flow can also impact *F*<sub>*ST*</sub> values, as it tends to decrease the amount of differentiation among subpopulations.
\
\
*Would gene flow increase or decrease *F*<sub>*ST*</sub> values? Why?*
\
\
\
\
\
\
*Can you think of any other evolutionary processes that may impact *F*<sub>*ST*</sub>*s*, besides selection and gene flow? Explain your answer.*
\
\
\
\
\
\
Go ahead and log in to Turing.

**F*<sub>*ST*</sub>*s* with vcftools*
---------------------------------------

We are going to calculate *F*<sub>*ST*</sub> values for our clownfish dataset using vcftools. This will give us an estimate of how much variation there is among our clownfish subpopulations (Japan, Indonesia, and the Philippines).
\
\
On Turing, navigate to your sandbox, and get a node to work on:

``` bash
salloc -c 12
```

Open up the text file with the candidate loci that we identified yesterday by typing (all on one line)

``` bash
less /cm/shared/courses/Bioinfo_Workshop/clownfish_data/outlier_candnames.txt
```

Do these loci look familiar? They should. This text file is a list of all the candidate loci for selection that we identified yesterday with BayeScan and BayPass. We are going to exclude these from our analysis today, as we already know they are *F*<sub>*ST*</sub> outliers (and thus will not accurately represent any population differentiation due to population structure).
\
\
To calculate *F*<sub>*ST*</sub>*s* between Japan and the Philippines using vcftools, type the following

``` bash
enable_lmod
module load vcftools/0.1
```

Type (all on one line)

``` bash
vcftools --vcf /cm/shared/courses/Bioinfo_Workshop/clownfish_data/output.hicov2.snps.only.vcf --exclude-positions /cm/shared/courses/Bioinfo_Workshop/clownfish_data/outlier_candnames.txt --weir-fst-pop J_individuals.txt --weir-fst-pop P_individuals.txt --out FST_J-P
```

Arguments we used:

-   **--vcf** ------------------- read in data from a VCF file
-   **--exclude-positions** ----- specify name of text file with loci to exclude from analysis
-   **--weir-fst-pop** ---------- specify name of the text file with populations for analysis
-   **--out** ------------------- specify name of the output file

Once vcftools has finished running, you will see some information printed to the screen.
\
\
*What is the Weir and Cockerham mean *F*<sub>*ST*</sub> estimate for Japan-Philippines?*
\
\
\
\
Open up the `FST_J-P.weir.fst` output file. Each line in the file corresponds to a SNP. This file has columns in the following order:

-   Chromosome ID
-   SNP bp position
-   Weir and Cockerham *F*<sub>*ST*</sub> estimate (a commonly used estimator for *F*<sub>*ST*</sub>)

Search for chromosome TRINITY\_DN39030\_c1\_g1\_i1, SNP position 686.
\
\
*What is the *F*<sub>*ST*</sub> estimate for this SNP?*
\
\
\
\
*Is this SNP highly differentiated between the two populations, or not? How can you tell? (Hint: *F*<sub>*ST*</sub>*s* &gt; 0.15 are generally considered to be highly differentiated.)*
\
\
\
\
\
\
*Is there a lot of genetic differentiation between these two populations? (Hint: look at the mean *F*<sub>*ST*</sub> estimate you recorded earlier.)*
\
\
\
\
Now repeat the *F*<sub>*ST*</sub> calculation for Japan-Indonesia (use `--out FST_J-N`) and Philippines-Indonesia (use `--out FST_P-N`). Make sure you are including the correct population files!
\
\
*What are the Weir and Cockerham mean *F*<sub>*ST*</sub> values for each pair of populations (there should be three pairs)?*
\
\
\
\
*Which population pair has the highest Weir and Cockerham mean *F*<sub>*ST*</sub>?*
\
\
\
\
*Which population pair has the lowest Weir and Cockerham mean *F*<sub>*ST*</sub>?*
\
\
\
\
*Do the *F*<sub>*ST*</sub> values appear to better fit an island model (all *F*<sub>*ST*</sub>*s* about equal) or an isolation-by-distance model (*F*<sub>*ST*</sub>*s* are lower for populations that are geographically closer)?*
\
\
\
\
Close out of any file you may have open.

****F*<sub>*ST*</sub> and gene flow***
----------------------------------------

We know that gene flow impacts *F*<sub>*ST*</sub> values. Thus, one might be tempted to use *F*<sub>*ST*</sub>*s* to estimate migration rates among populations. One way to do so uses the island model formula:

*F*<sub>*ST*</sub> = 1/(4*Nm* + 1)

In this formula, *N* represents the population size and *m* represents the migration rate among populations (as a proportion). The island model assumes that all populations are of equal size and migration rates are the same for all populations as well. Often, these terms are combined together, as we are generally interested in the number of migrant individuals among populations (*Nm*).
\
\
Go ahead and use the island model formula to calculate the number of migrant individuals (*Nm*) for Japan-Philippines. Use the Weir and Cockerham mean *F*<sub>*ST*</sub>*s* estimate you wrote down earlier.
\
\
*How many migrants per generation (Nm) does this calculation suggest these populations receive? Does this seem reasonable?*
\
\
\
\
\
\
*If we assume a population size of 100 clownfish, what would our migration rate be? (Hint: Solve for m in the equation with N = 10 and *F*<sub>*ST*</sub> = your Weir and Cockerham mean *F*<sub>*ST*</sub> estimate.)*
\
\
\
\
\
\
The island model makes many assumptions about our dataset and the demographic patterns at work. These assumptions are as follows:

1.  Infinite number of populations
2.  All populations are the same size
3.  Each population exchanges migrants at the same rate
4.  Populations are at HWE

*Think back to what you know about our clownfish dataset. To what extent do our data meet these assumptions?*
\
\
\
\
\
\
*Do you think the island model formula is a useful tool for estimating migration rates? Why or why not?*
