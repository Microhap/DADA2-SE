# DADA2-SE
This R script performs ASVs inference and haplotype identification steps in the analysis of Illumina MiSeq sequencing data for microhaplotypes using DADA2.
<br> 
<br> 
![figure](https://github.com/user-attachments/assets/e8381d63-39fb-4836-82fc-f63a7eeb89e9)
<br>

## Requirements
- R version >= 4.0
- Required packages: `dada2`, `ShortRead`, `stringr`

<br>

## Inputs

### FASTQ File Preparation
- This pipeline recommends using **only the forward reads** as input.
  **Merged paired-end reads into a single FASTQ file are not recommended** due to potential quality issues in reverse reads.
- At least **two FASTQ files** are required, corresponding to at least two independent samples.
- The FASTQ files should be generated from the **same batch of sequencing** to ensure consistent error modeling and quality control.
- Make sure to modify the path in the script to reflect the actual path of your FASTQ files.
  <br> (e.g., "E:/DADA2/MH-MiSeq") 

<br>

### Configuration File Preparation
- Make sure to modify the path in the script to reflect the actual path of your config file.
  <br> (e.g., "E:/DADA2/MH24_241224.config")

<br>

## Example Data in `example/`
The `example/` directory now includes:
1. **Two FASTQ files for 2800M reference DNA**: `2800M#1_S1_L001_R1_001.fastq` and `2800M#2_S2_L001_R1_001.fastq`<br> <br>
2. A **configuration file** for STRait Razor format conversion: `MH24_241224.config`

<br>

## Usage
1. Place your Configuration and FASTQ files in the appropriate directories.
2. Modify the Configuration and FASTQ file paths in the script to reflect the actual paths.
3. Run the script.
