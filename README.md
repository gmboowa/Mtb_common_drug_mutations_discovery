# Mtb Common Drug Mutations Discovery

## Overview
This repository focuses on UG sub-lineage mutations and drug resistance mutation discovery for *Mycobacterium tuberculosis* (MTB). It leverages tools like **FastQC**, **MultiQC**, and **Snippy** for rapid bacterial SNP genotype and drug resistance calling (Version 1.0.0).

---

## Author
Gerald Mboowa

---

## Synopsis
**Snippy** identifies SNPs between a haploid reference genome and HTS datasets. It detects both substitutions (SNPs) and insertions/deletions (indels). Snippy is designed for speed and efficiency, supporting multi-threading on a single machine. It produces consistent output files in a single folder. (Tested with Snippy 4.3.2 - [Torsten Seemann's Snippy](https://github.com/tseemann/snippy)).

### Key Tools:
1. **FastQC**  
   Provides quality control checks on raw sequence data from high-throughput sequencing pipelines.

2. **MultiQC**  
   Aggregates analysis logs into a single HTML report, summarizing outputs from multiple tools like FastQC.

3. **Snippy**  
   Processes samples for SNP discovery and annotation.

4. **MTB Genotypes and Drug Resistance Annotations**  
   Identifies MTB sub-lineages and drug resistance mutations, including MDR and XDR strains.

5. **Redundant File Cleanup**  
   Deletes unnecessary files generated during the pipeline execution.

---

## Output Files
The pipeline generates the following output files:
- Text files detailing **MTB genotypes**
- Text files summarizing **drug resistance mutations** for both MDR and XDR strains

---

## Issues
For suggestions or to report bugs, please use the [Issue Tracker](https://github.com/gmboowa/Mtb_common_drug_mutations_discovery/issues).

---

## Requirements

### Software
- **FastQC**
- **MultiQC**
- **Perl** (>= 5.12)  
  - Modules: `Time::Piece` (core with modern Perl), `Bioperl` (>= 1.6)
- **BWA MEM** (>= 0.7.12)
- **Minimap2** (>= 2.0)
- **Samtools** (>= 1.7)
- **Bedtools** (>= 2.0)
- **BCFtools** (>= 1.7)
- **GNU Parallel** (>= 2013xxxx)
- **FreeBayes** (>= 1.1)  
  - Includes: `freebayes`, `freebayes-parallel`, `fasta_generate_regions.py`
- **VCFtools (vcflib)** (>= 1.0)  
  - Includes: `vcfstreamsort`, `vcfuniq`, `vcffirstheader`
- **VT** (>= 0.5)
- **ReadSeq** (>= 2.0)
- **SnpEff** (>= 4.3)
- **Samclip** (>= 0.2)
- **Seqtk** (>= 1.2)
- **Snp-Sites** (>= 2.0)
- **Wgsim** (>= 1.8) (for testing only)

### Bundled Binaries
This pipeline has been tested on **macOS Mojave** using precompiled binaries.

---

## Disclaimer
Ensure the listed dependencies are properly installed and configured before running the pipeline. Refer to the respective tool documentation for detailed installation and usage guidelines.

---

## Contact
For further inquiries or collaborations, please contact the author.
