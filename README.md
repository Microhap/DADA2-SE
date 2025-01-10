# DADA2-SE
This R script performs ASVs inference and haplotype identification steps in the analysis of MiSeq sequencing data for microhaplotypes using DADA2.
<br> 
<br> 
![figure](https://github.com/user-attachments/assets/e8381d63-39fb-4836-82fc-f63a7eeb89e9)
<br>

## Requirements
- R version >= 4.0
- Required packages: `dada2`, `ShortRead`, `stringr`

<br>

## Configuration File Preparation
- Make sure to modify the path in the script to reflect the actual path of your config file.
  <br> (e.g., "E:/DADA2/MH24_241224.config")

<br>

## FASTQ File Preparation
- This pipeline is designed to use **forward reads** generated from MiSeq, which provides high sequencing quality.
  **Paired-end reads merged into a single FASTQ file are not recommended** due to potential quality issues in reverse reads.
- At least **two FASTQ files** are required to run this pipeline.
- The FASTQ files should be generated from the **same batch of sequencing** to ensure consistent error modeling and quality control.
- Make sure to modify the path in the script to reflect the actual path of your FASTQ files
  (e.g., "E:/DADA2/MH-MiSeq"). 

<br>

## Example Data in `example/`
The `example/` directory now includes:
1. A **configuration file** for STRait Razor format conversion: `MH24_241224.config`
2. **Two FASTQ files for 2800M reference DNA**:`2800M#1_S1_L001_R1_001.fastq` and `2800M#2_S2_L001_R1_001.fastq`

<br>

## Usage
1. Place your Configuration and FASTQ files in the appropriate directories.
2. Modify the Configuration and FASTQ file paths in the script to reflect the correct paths.
3. Run the script.
