# Peatland-SIP-16S-Pipeline
A reproducible bioinformatics pipeline for analyzing 16S rRNA gene sequencing data from peatland stable isotope probing (SIP) experiments. The workflow processes paired-end reads from primer trimming through denoising, taxonomy, phylogeny, differential abundance, and quantitative SIP analysis.


This repository contains a reproducible bioinformatics pipeline for analyzing 16S rRNA gene sequencing data from peatland Stable Isotope Probing (SIP) experiments. The workflow is designed to handle paired-end reads from MiSeq or MiniSeq runs, from primer trimming to taxonomic analysis, differential abundance testing, and quantitative SIP analysis. The pipeline is modular, built with Bash shell scripts and R-based Quarto markdown files, allowing stepwise execution and transparent documentation.

---

## Workflow steps

1. **Primer removal (cutadapt)**  
   Removes the 515F and 806r primers from raw reads. Generates a log file (`00_cutadapt.log`) with trimming statistics.

2. **DADA2 pipeline**  
   Processes 16S reads: quality filtering, denoising, merging paired-end reads, and creating a feature table. Taxonomic assignment is done against SILVA and GTDB databases.

3. **Decontamination**  
   Identifies and removes potential contaminant ASVs using the `decontam` R package.

4. **Taxa filtering**  
   Filters rare taxa to improve downstream analysis.

5. **Phylogenetic tree calculation**  
   Aligns sequences using **SINA** and builds a maximum-likelihood tree with **IQ-TREE** for phylogenetically informed analysis.

6. **Differential abundance analysis**  
   Multiple methods are applied to detect taxa actively incorporating ¹³C:  
   - **ANCOM-BC2**: compares "heavy" fractions between ¹³CH₄ (labeled) and ¹²CH₄ (unlabeled) treatments.  
   - **DESeq2**: identifies differentially abundant taxa and tests effects of ammonium addition.  

7. **Quantitative SIP (qSIP2)**  
   Estimates atom fraction ¹³C incorporation per taxon, providing quantitative measures of metabolic activity.

8. **Comparison of results**  
   Compares outcomes across ANCOM-BC2 and DESeq2 to identify consistent vs. method-specific findings.

---

## Dependencies

The workflow requires a Linux server environment with Bash, R, and Quarto installed.

### Software
- `cutadapt`  
- `SINA`  
- `FastTree`  
- `mothur`  
- `IQ-TREE`

### Languages
- **R** (≥ 4.0)  
- **Bash**

### R packages
- `tidyverse`  
- `phyloseq`  
- `Biostrings`  
- `decontam`  
- `ANCOMBC`  
- `DESeq2`  
- `qSIP2`

Quarto files are configured to automatically check for and install missing dependencies.

---

## Usage

The Bash scripts (`.sh`) serve as the primary entry points. Each script calls the relevant R and Quarto files in sequence, ensuring a reproducible, step-by-step analysis pipeline. Users can run individual steps or the entire workflow, depending on their needs.

---

## Citation

If you use this pipeline, please cite:  
*Justus Nweze. Peatland-SIP-16S-Pipeline (2023).*
