BayPass (Part I)
================

Scanning for *F*<sub>*ST*</sub> outliers is just one of several methods for identifying signs of local adaptation. Another, more recently developed way to detect these patterns is by looking for correlations between allele frequencies and environmental variables (environmental association analyses). One way to check for these correlations is by testing a null model that accounts for population structure against an alternative model that includes a linear relationship between allele frequencies and a given environmental variable. If our empirical evidence (observed allele frequencies) better supports the alternative model than the null model, then selection may be taking place. We will use the program BayPass to analyze associations between allele frequencies and several environmental variables.

***Create input for BayPass***
------------------------------

We'll use PGDSpider to convert our .vcf file to the format that BayPass expects.
\
\
Open up PuTTY and log on to your Turing account.
\
\
Type

``` bash
salloc -c 12
```

To use PGDSpider, we will need our vcf file to be converted, as well as a .spid file that specifies the parameters PGDSpider will use during the conversion. This .spid file has already been created for you.
\
\
Copy the .spid file to your sandbox by typing (all on one line)

``` bash
cp /cm/shared/courses/Bioinfo_Workshop/clownfish_data/VCF_BayPass.spid /cm/shared/courses/Bioinfo_Workshop/sandboxes/yoursandbox/
```

From your sandbox, open up the file in less to examine the settings:

``` bash
less VCF_BayPass.spid
```

*Parser file format:* \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_
\
\
\
*Writer file format:* \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_
\
\
\
*Ploidy of the data:* \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_
\
\
\
*Do we want to include non-polymorphic SNPs?* \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_
\
\
Exit out of the .spid file. Move to your sandbox if you're not there already.
\
\
We will need to make a text file that specifies what population each individual belongs to in order to convert our .vcf file to the proper format. Go ahead and do that now by typing

``` bash
nano Pop_assignments.txt
```

Enter the information below (exactly as is). Make sure that each individual is on a separate line and separated from its population assignment by a tab.

``` bash
J11   Pop_1
J13   Pop_1
J15   Pop_1
J17   Pop_1
J19   Pop_1
J3    Pop_1
J5    Pop_1
J9    Pop_1
N1    Pop_2
N2    Pop_2
N3    Pop_2
N4    Pop_2
N5    Pop_2
N6    Pop_2
N7    Pop_2
P1    Pop_3
P10   Pop_3
P14   Pop_3
P16   Pop_3
P18   Pop_3
P20   Pop_3
P22   Pop_3
P24   Pop_3
P3    Pop_3
P6    Pop_3
```

When you are finished, exit out of nano.
\
\
To create our correctly formatted BayPass input file using PGDSpider, we will use a batch script. First, you need to copy this script to your sandbox. Type the following (all on one line)

``` bash
cp /cm/shared/courses/Bioinfo_Workshop/clownfish_data/PGDSpider_Script.sbatch /cm/shared/courses/Bioinfo_Workshop/sandboxes/yoursandbox
```

Once you've done that, open up the script to take a look at what we will be calling

``` bash
less PGDSpider_Script.sbatch
```

You can see the command for PGDSpider is very long, so we wrote a script to simplify the process.
\
\
When you are done looking at the script, close out of it. Run PGDSpider by typing

``` bash
sbatch PGDSpider_Script.sbatch
```

The program should only take ~1 minute to run. Type `ls -ltrh` to check and see that it's running properly. If it worked, you should see an output file titled `output_BayPass.snps` appear.
\
\
Arguments we used:

-   **-inputfile** -------- read in data from a VCF file
-   **-inputformat** ------ format of the input file
-   **-outputfile** ------- specify the name of the output file
-   **-outputformat** ----- format of the output file
-   **-spid** ------------- specify the name of the .spid file with the necessary parameters

Open the `output_BayPass.snps` file. Each line in the file corresponds to an allele. For example, the first two lines display the allele counts for allele 1 and allele 2 at the first locus in all three populations.
\
\
*What is the allele count of the first allele at the first locus in all three populations?*
\
\
\
\
*What is the allele count of the second allele at the first locus in all three populations?*
\
\
\
\
Unfortunately, this file is still not formatted correctly for BayPass. If you hadn't noticed when we converted the file with PGDSpider, it actually created a file for input into a program called BayEnv. BayEnv is a similar program to BayPass. It also detects patterns of differential selection by looking for correlations between allele frequencies and environmental variables, it just uses a slightly different model to do so.
\
\
We've already created an input file for BayPass for you to use when running the program. To do so, we used the BayEnv output file that PGDSpider created and re-formatted it slightly with R. Go ahead and open that file now by typing (all on one line)

``` bash
less /cm/shared/courses/Bioinfo_Workshop/clownfish_data/clownfish_allele_counts.geno
```

*What are some differences in how this file is formatted compared to the file you created using PGDSpider? (Opening up the two files in different windows/on different computers may be useful.)*
\
\
\
\
\
\
Go ahead and close the `clownfish_allele_counts.geno` file when done.

***Run BayPass***
-----------------

To run BayPass, we also need environmental data. Open up the file with environmental data by typing (all on one line)

``` bash
less /cm/shared/courses/Bioinfo_Workshop/clownfish_data/clownfish_env.env
```

Each column in the file corresponds to a population (Japan, Philippines, Indonesia). Each line in the file represents a different environmental variable in the following order:

-   Sea Surface Salinity (Mean) (psu)
-   Sea Surface Temperature (Mean) (C)
-   Sea Surface Temperature (Minimum) (C)
-   Sea Surface Temperature (Maximum) (C)
-   Latitude (degrees)

*Which population has the highest SST Mean? What is the value?*
\
\
\
\
*Which population has the lowest SSS Mean? What is the value?*
\
\
\
\
Just like BayeScan, BayPass also uses Markov Chain Monte Carlo (MCMC) methods. To see the arguments that you can specify for the program, type

``` bash
module load baypass/2
baypass -help
```

*Read the help file. What is the default number of post-burnin iterations and thinning size?*
\
\
\
\
BayPass gives you the ability to run several different models. We are going to run the auxiliary model. This model requires a covariance matrix of allele frequencies. It also requires that the environmental variables have been standardized. Both of these files have been created for you. To run BayPass type (all on one line)

``` bash
baypass -npop 3 -efile /cm/shared/courses/Bioinfo_Workshop/clownfish_data/clownfish_data_scaled.env -gfile /cm/shared/courses/Bioinfo_Workshop/clownfish_data/clownfish_allele_counts.geno -auxmodel -omegafile /cm/shared/courses/Bioinfo_Workshop/clownfish_data/clownfish_mat.cov -burnin 50000 -outprefix BayPass_aux_output
```

Arguments we used:

-   **-npop** ---------- number of populations in analysis
-   **-efile** --------- specify name of the file with the (standardized) environmental variables
-   **-gfile** --------- specify name of the file with the allele counts per population/loci
-   **-auxmodel** ------ specify the desired model
-   **-omegafile** ----- specify name of the file with the covariance matrix
-   **-burnins** ------- number of burn-in iterations for the MCMC
-   **-outprefix** ----- specify prefix for the output files

As the program runs, you will see its progress being printed to the screen. BayPass will take ~30 minutes to run. We will come back to this after the break to check our results.
