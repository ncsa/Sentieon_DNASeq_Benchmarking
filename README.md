# Sentieon_DNASeq_Benchmarking

This repository contains an example script used for benchmarking. Full paths and other system-specific information have been removed. 

This code derives from the sample DNASeq script Sentieon provides. Alterations include the addition of a separate timelog that measured the start and end of each tool. For some runs, we also included calls to our in-house memory profiler.

The code remained consistent for each run except for changes to 1) the number of threads ($nt); 2) the data being processed; and 3) whether or not the Realigner tool was used.

# Command used to generate synthetic reads and Golden VCF:

python genreads.py -r hg38_chr20_21_22.fa -R 100 --pe 300 30 -M 0.001 -E 0.001 --bam --vcf

# Command used to run accuracy comparisons:

python vcf-compare.py -r hg38.fa -g golden_truth.vcf -w workflow.vcf --vcf-out -o output_directory \
                      -t ConfidentRegions.bed -T 0 --incl-homs --incl-fail --no-plot




