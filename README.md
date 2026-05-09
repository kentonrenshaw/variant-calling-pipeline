# variant-calling-pipeline

## Project Overview
This project implements an end‑to‑end DNA variant calling pipeline. It takes raw sequencing reads in FASTQ format, performs quality control and alignment, and produces a VCF file containing the genetic variants identified in the sample. The goal is to demonstrate practical experience with real bioinformatics workflows and industry‑standard tools used in genomics research and clinical sequencing.

---

## Pipeline Overview
- **Quality Control** – Assess read quality using FastQC  
- **(Optional) Trimming** – Remove low‑quality bases or adapter sequences  
- **Alignment** – Map reads to a reference genome using BWA  
- **Post‑processing** – Convert, sort, and index alignments with Samtools  
- **Variant Calling** – Identify SNPs and indels using FreeBayes  
- **Variant Filtering** – Use bcftools to refine and inspect variant calls  
- **Results Summary** – Produce interpretable outputs and QC reports  

This pipeline can be implemented using **Snakemake** or **Nextflow** for reproducibility and scalability.

---

## Tools Used
- **FastQC** – Quality assessment of raw FASTQ reads  
- **Cutadapt / Trimmomatic** – Adapter and quality trimming (optional)  
- **BWA** – Alignment of reads to the reference genome  
- **Samtools** – BAM conversion, sorting, and indexing  
- **FreeBayes** – Variant calling  
- **bcftools** – Variant filtering and inspection  
- **Snakemake / Nextflow** – Workflow management  

---

## Input Data

### FASTQ Files — Raw DNA Sequencing Reads
- Contains nucleotide sequences and per‑base quality scores  
- Represents the “raw camera footage” of the genome  

### FASTA File — Reference Genome
- Curated, high‑quality sequence used as the alignment template  
- Represents the “official map” of the genome  

Example datasets may come from the **1000 Genomes Project**, **ENA**, or **NCBI SRA**.

---

## How to Run

1. **Place FASTQ files** in `data/raw/`  
   - The workflow automatically detects all FASTQ files in this directory  
   - Sample names are inferred from filenames (e.g., `sample1_R1.fastq.gz`)  

2. **Place the reference genome** (FASTA + index files) in `data/reference/`  
   - The workflow checks for required index files and generates them if missing  

3. **Activate the project environment** (conda or mamba)

4. **Run the workflow** using Snakemake or Nextflow  
   - The workflow automatically determines which steps need to run  
   - Existing outputs are reused unless inputs have changed  
   - No manual cleanup is required  

5. **Outputs will be written to:**  
   - `results/qc/` – FastQC reports  
   - `results/bam/` – Sorted BAM files  
   - `results/vcf/` – Final VCF files  

---

## Output Description

The pipeline produces:

### QC Reports (HTML)
- Read quality summaries from FastQC  

### Aligned BAM Files
- Reads mapped to the reference genome  
- Sorted and indexed  

### Index Files (.bai)
- Required for variant calling  

### VCF File
- List of SNPs and indels detected in the sample  
- Includes:  
  - Chromosome and position  
  - Reference and alternate alleles  
  - Quality metrics  
  - Genotype information  

This is the **primary deliverable** of the workflow.

---

## Biological Context
Variant calling is a foundational task in genomics. By comparing a sample’s DNA to a reference genome, we can identify genetic differences such as SNPs and small insertions/deletions. These variants can be used for:

- Population genetics  
- Disease association studies  
- Clinical diagnostics  
- Pharmacogenomics  
- Research into inherited traits  

This project demonstrates the computational steps required to transform raw sequencing data into biologically meaningful variant information.

---

## Future Improvements
Potential enhancements include:

- Adding **GATK HaplotypeCaller** as an alternative variant caller  
- Implementing containerization with **Docker** or **Singularity**  
- Deploying the workflow on **AWS Batch** or **Google Cloud Life Sciences**  
- Adding automated QC thresholds and filtering rules  
- Creating a small **visualization notebook** for variant summaries  
- Supporting **multiple samples** and joint genotyping  

---

## What This Project Demonstrates
- Ability to work with core genomics file formats (**FASTQ**, **BAM**, **VCF**)  
- Familiarity with essential bioinformatics tools (FastQC, BWA, Samtools, FreeBayes, bcftools)  
- Understanding of an end‑to‑end variant calling workflow used in real genomics pipelines  
- Ability to design reproducible, automated pipelines using a workflow engine (Snakemake or Nextflow)  
- Practical experience transforming raw sequencing data into interpretable variant information  
- Clear documentation, structured project organization, and engineering‑oriented workflow design  
