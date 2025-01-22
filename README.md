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

### 1. FASTQ Files 
- This pipeline recommends using **only the forward reads** as input.
  **Merged paired-end reads into a single FASTQ file are not recommended** due to potential quality issues in reverse reads.
- At least **two FASTQ files** are required, corresponding to at least two independent samples.
- The FASTQ files should be generated from the **same batch of sequencing** to ensure consistent error modeling and quality control.
- Make sure to modify the path in the script to reflect the actual path of your FASTQ files.
  <br> (e.g., "E:/DADA2/MH-MiSeq") 

<br>

### 2. Configuration File 
- Make sure to modify the path in the script to reflect the actual path of your config file.
  <br> (e.g., "E:/DADA2/MH24_241224.config")
  
- Below is an example of a properly formatted configuration file:

    | Marker      | Type | 5' Flank       | 3' Flank       | Motif | Period | Offset |
    |-------------|------|----------------|----------------|-------|--------|--------|
    | mh09KK-153  | MH   | GGCAGTCTTCAT   | GGCTGTATGATA   | A     | 1      | 155    |
    | mh02KK-134  | MH   | CCCTTGGCAGGA   | TACGAGCCTCAA   | A     | 1      | 118    |
    | mh13KK-213  | MH   | CAGCAAGGAGAA   | TTGAGTTGATCA   | A     | 1      | 194    |

  - **Marker**: The identifier for the microhaplotype marker (e.g., mh09KK-153).
  - **Type**: The type of marker. In this analysis, the value is always "MH" for microhaplotypes.
  - **5'Flank**: The sequence of the 5' flanking region of the marker.
  - **3'Flank**: The sequence of the 3' flanking region of the marker.
  - **Motif**: The repeating motif in the marker region (e.g., "A").
  - **Period**: The number of bases in the repeating unit of the motif.
  - **Offset**: The offset or position information for the marker in the sequence.

<br>

## Example data in `example/` directory
The `example/` directory now includes:
1. **Two FASTQ files for 2800M reference DNA**: `2800M#1_S1_L001_R1_001.fastq` and `2800M#2_S2_L001_R1_001.fastq`<br> <br>
2. A **configuration file** for STRait Razor format conversion: `MH24_241224.config`

## Outputs






