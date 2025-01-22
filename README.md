# DADA2-SE
This R script performs ASVs inference and haplotype identification steps in the analysis of Illumina MiSeq sequencing data for microhaplotypes using DADA2. The subsequent genotype calling step is performed by Visual Microhap (http://forensic.yonsei.ac.kr/VisualMH/index.html).
<br> 
<br> 
![figure](https://github.com/user-attachments/assets/e8381d63-39fb-4836-82fc-f63a7eeb89e9)
<br>

## Requirements
- R version >= 4.0
- Required packages: `dada2`, `ShortRead`, `stringr`

If these packages are not installed, please install them before running the script. 

```r
# CRAN
install.packages(c("dada2", "ShortRead", "stringr"))
```
<br>

## Inputs

### 1. FASTQ files 
- This pipeline recommends using **only the forward reads** as input.
  **Merged paired-end reads into a single FASTQ file are not recommended** due to potential quality issues in reverse reads.
- At least **two FASTQ files** are required, corresponding to at least two independent samples.
- The FASTQ files should be generated from the **same batch of sequencing** to ensure consistent error modeling and quality control.
- Make sure to modify the path in the script to reflect the **absolute path** of your FASTQ files.
  <br> (e.g., "E:/DADA2/MH-MiSeq") 

<br>

### 2. Configuration file 
- Make sure to modify the path in the script to reflect the **absolute path** of your configuration file.
  <br> (e.g., "E:/DADA2/MH24_241224.config")
  
- Below is an example of a configuration file:

    | Marker      | Type | 5'Flank       | 3'Flank       | Motif | Period | Offset |
    |-------------|------|----------------|----------------|-------|--------|--------|
    | mh09KK_153  | MH   | GGCAGTCTTCAT   | GGCTGTATGATA   | A     | 1      | 155    |
    | mh02KK_134  | MH   | CCCTTGGCAGGA   | TACGAGCCTCAA   | A     | 1      | 118    |
    | mh13KK_213  | MH   | CAGCAAGGAGAA   | TTGAGTTGATCA   | A     | 1      | 194    |

  - **Marker**: The identifier for the microhaplotype marker (e.g., mh09KK-153).
  - **Type**: The type of marker ("MH" for microhaplotypes).
  - **5'Flank**: Part of the 5'-end sequence of each marker.
  - **3'Flank**: Part of the 3'-end sequence of each marker.
  - **Motif**: The repeat motif of the marker, set to "A" in this microhaplotype analysis.
  - **Period**: The number of bases in the repeat unit of the motif, set to "1" in this microhaplotype analysis.
  - **Offset**: The length of the sequence inside the 5'Flank and 3'Flank regions.

<br>

## Example data 
The `example/` directory now includes:
- **Two FASTQ files for 2800M reference DNA**: Amplicon sequencing data for 24 microhaplotype markers. `2800M#1_S1_L001_R1_001.fastq` and `2800M#2_S2_L001_R1_001.fastq`<br> 
- A **configuration file** for haplotype identification: `MH24_241224.config`

<br>

## Outputs



- Below is an example of the output file for 2800M#1:

    | Marker      | Size(bp) | Sequence                                                                                                                                                                                                                                      | Coverage#1 | Coverage#2 |
    |-------------|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------|
    | mh09KK_153  | 155            | GCTCTGAACAATTGGGTATTCTTTTTTCTTAGAGCCCAGATGCATTTTTTTGAAAGTCGTTCCAGGGGCCTGAGATGAAGTGGGGGTGTGAGAAGTAAGTTGGCTAGGGCAGATAGAACCTAAGTGTCTTCTCCTTAAGTCAGCTCCCCTTATGA                                     | 1677          | 0    |
    | mh09KK_153  | 155            | GCTCTGAACAATTGGGTATTCTTTTTTCTTAGAGCCCAGATGCATTTTTTTGAAAGTCGTTCCAGGGGCCTGAGATGAAGTGGGGGTGTGAGAAGTAAGTTGGCTAGGGCAGATAGCACCTAAGTGTCTTCTCCTTAAGTCAGCTCCCCTTATGA                                     | 1186          | 0    |
    | mh02KK_134  | 118            | ACCCTCACTACCTAAGGATGGGCAATGGCTCATGAGTGAGAAACATGGAGCCGTGGGAACTCAGAATGACATGCTACCTGGAGATTGTGGTAACGCCCTGTTTTTTTGTGGGCATATC                                                                                   | 1651          | 0    |
    | mh02KK_134  | 118            | ACCCTCTCTACCTAAGGATGGGCAATGGCTTATGAGTGAGAAACATGGAGCCGTGGGAACTCAGAATGACATGCTACCTGGAGATTGTGGTAACGCCCTGTTTTTTTGTGGGCATATC                                                                                   | 1429          | 0    |
    | mh13KK_213  | 195            | CTTCAGTTGTCAAGGTATTGGGTACAGGGGTCAGAAAGAAACATGACTCCATGGACCACTGCTTGGCCCAAGACCAGATGTCAAAACCACAGAGCCCTGCTGTAGAGCATTACAAATGTATTCCACCAAATGTTGGGATGCATCCTAGACCTGTGCTGACCAGCAGTCCCCAGCTGTGAGGAGAAGCCCGCCATT | 2133          | 0    |

- This output file can be directly used as input for **Visual Microhap** (http://forensic.yonsei.ac.kr/VisualMH/index.html), enabling genotype calling of microhaplotype.

<br>

## Citation
