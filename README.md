# Overview

As reliable, efficient genome sequencing becomes ubiquitous, the need for similarly reliable and efficient variant calling becomes increasingly important. The Genome Analysis Toolkit (GATK), maintained by the Broad Institute, is currently the widely accepted standard for variant calling software. However, alternative solutions may provide faster variant calling without sacrificing accuracy. One such alternative is Sentieon DNASeq, a toolkit analogous to GATK but built on a highly optimized backend. We conducted an independent evaluation of the DNASeq single-sample variant calling pipeline in comparison to that of GATK. Our results support the near-identical accuracy of the two software packages, showcase optimal scalability and great speed from Sentieon, and describe computational performance considerations for the deployment of DNASeq.

Please see our full pre-print manuscript for further details: [Computational performance and accuracy of Sentieon DNASeq variant calling workflow](https://www.biorxiv.org/content/10.1101/396325v1)

# Sentieon DNASeq Benchmarking

This repository contains an example script used for benchmarking. Full paths and other system-specific information have been removed. 

This code derives from the sample DNASeq script Sentieon provides. Alterations include the addition of a separate timelog that measured the start and end of each tool. For some runs, we also included calls to our in-house memory profiler.

The code remained consistent for each run except for changes to 1) the number of threads ($nt); 2) the data being processed; and 3) whether or not the Realigner tool was used.

# Generating synthetic reads and Golden VCF

We used the [NEAT package](https://github.com/zstephens/neat-genreads) (see manuscript references) to generate synthetic data and an accompanying Golden VCF with the following command.

*python genreads.py -r hg38_chr20_21_22.fa -R 100 --pe 300 30 -M 0.001 -E 0.001 --bam --vcf*

# Accuracy comparisons

We used the vcf-compare packages associated with [NEAT](https://github.com/zstephens/neat-genreads) to compare GATK and Sentieon with each other and various truth sets using the following command.

*python vcf-compare.py -r hg38.fa -g golden_truth.vcf -w workflow.vcf --vcf-out -o output_directory \
                      -t ConfidentRegions.bed -T 0 --incl-homs --incl-fail --no-plot*




