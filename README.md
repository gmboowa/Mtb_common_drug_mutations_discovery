# Mtb_common_drug_mutations_discovery
UG sub_lineage mutations drug resistant mutations discovery
FastQC MultiQC Snippy Rapid Bacterial SNP Genotype and Drug Resistance Calling Version 1.0.0


Author
Gerald Mboowa

Synopsis
Snippy finds SNPs between a haploid reference genome and your HTS dataset. It will find both substitutions (snps) and insertions/deletions (indels). It will use as many CPUs as you can give it on a single computer. It is designed with speed in mind, and produces a consistent set of output files in a single folder  (this has been tested with Snippy 4.3.2 (https://github.com/tseemann/snippy - Torsten Seemann) . 

i.	FastQC
Aims to provide a simple way to do some quality control checks on raw sequence data coming from high throughput sequencing pipelines.

I.	MultiQC
Searches a given directory for analysis logs and compiles a HTML report. It's a general use tool, perfect for summarising the output from numerous FastQC reports

ii.	Running Snippy for the Samples

iii.	Running MTB Genotypes and Drug Resistance Annotations for the Samples

iv.	Deleting all Redundant files generated


Output Files

Text files for 
¬	MTB genotypes 
¬	Drug resistance mutations both MDR and XDR


Issues
Please submit suggestions and bug reports to the Issue Tracker

Requirements
FastQC
MultiQC
Perl >= 5.12
Perl Modules: Time::Piece (core with modern Perl), Bioperl >= 1.6
bwa mem >= 0.7.12
minimap2 >= 2.0
samtools >= 1.7
bedtools >= 2.0
bcftools >= 1.7
GNU parallel >= 2013xxxx
freebayes >= 1.1 (freebayes, freebayes-parallel, fasta_generate_regions.py)
vcflib >= 1.0 (vcfstreamsort, vcfuniq, vcffirstheader)
vt >= 0.5
readseq >= 2.0
snpEff >= 4.3
samclip >= 0.2
seqtk >= 1.2
snp-sites >= 2.0
wgsim >= 1.8 (for testing only - wgsim command)
Bundled binaries
Tested on macOS (compiled on macOS Mojave) 

