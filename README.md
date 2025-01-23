# DADA2-SE
DADA2-SE is an R script that performs denoising of single-end Illumina MiSeq sequencing data for microhaplotypes using DADA2. 

The denoising pipeline for microhaplotype consisted of three main steps: ASVs inference, haplotype identification, and genotype calling. This script performs ASVs inference and haplotype identification steps. The subsequent genotype calling step is performed by Visual Microhap (http://forensic.yonsei.ac.kr/VisualMH/index.html).
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

### 1.  FASTQ files 
This pipeline recommends using only the forward reads as input. Merged paired-end reads into a single FASTQ file are not recommended due to potential quality issues in reverse reads. At least two FASTQ files are required, corresponding to at least two independent samples. The FASTQ files should be generated from the same batch of sequencing to ensure consistent error modeling and quality control.

Make sure to modify the path in the script to reflect the absolute path of your FASTQ files.
  
```
path <- "E:/DADA2/MH-MiSeq"   # CHANGE ME to the directory containing the fastq files after unzipping
```


### 2.  Configuration file 
Haplotype identification was performed by referencing a configuration file containing marker-specific sequences. The configuration file uses the same format as that of STRait Razor 3.0.

Below is an example of a configuration file:

| Marker      | Type | 5'Flank        | 3'Flank        | Motif | Period | Offset |
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
 
Make sure to modify the path in the script to reflect the absolute path of your configuration file.
  
```
configInfo <- read.table("E:/DADA2/MH24_241224.config", sep="\t")   # CHANGE ME to the directory containing Configuration file 
```

<br>

## Trimming options
You may need to adjust several parameters, such as trimming lengths or maximum expected errors, to optimize the quality of your sequencing data.

```
out <- filterAndTrim(fnFs, filtFs,  
                     maxN = 0, maxEE = 2, truncQ = 2, minLen = 120, 
                     rm.phix = TRUE, compress = TRUE, 
                     multithread = FALSE) # on windows, set multithread = FALSE
```
For more information on DADA2, refer to the official documentation: 


<br>

## Example dataset 
You can download the example dataset in the `example/` directory. 

The `example/` directory now includes:

- Two FASTQ files for 2800M reference DNA with amplicon sequencing data for 24 microhaplotypes:
```
./example/2800M#1_S1_L001_R1_001.fastq
```
```
./example/2800M#2_S2_L001_R1_001.fastq
```

- A configuration file for 24 microhaplotypes:
```
./example/MH24_241224.config
```


<br>

## Outputs
Output file contains denoised haplotype data for each marker.

Below is an example of the output file for 2800M#1:

| Marker      | Size(bp) | Sequence                                                                                                                                                                                                                                      | Coverage#1 | Coverage#2 |
|-------------|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------|
| mh09KK_153  | 155            | GCTCTGAACAATTGGGTATTCTTTTTTCTTAGAGCCCAGATGCATTTTTTTGAAAGTCGTTCCAGGGGCCTGAGATGAAGTGGGGGTGTGAGAAGTAAGTTGGCTAGGGCAGATAGAACCTAAGTGTCTTCTCCTTAAGTCAGCTCCCCTTATGA                                     | 1677          | 0    |
| mh09KK_153  | 155            | GCTCTGAACAATTGGGTATTCTTTTTTCTTAGAGCCCAGATGCATTTTTTTGAAAGTCGTTCCAGGGGCCTGAGATGAAGTGGGGGTGTGAGAAGTAAGTTGGCTAGGGCAGATAGCACCTAAGTGTCTTCTCCTTAAGTCAGCTCCCCTTATGA                                     | 1186          | 0    |
| mh02KK_134  | 118            | ACCCTCACTACCTAAGGATGGGCAATGGCTCATGAGTGAGAAACATGGAGCCGTGGGAACTCAGAATGACATGCTACCTGGAGATTGTGGTAACGCCCTGTTTTTTTGTGGGCATATC                                                                                   | 1651          | 0    |
| mh02KK_134  | 118            | ACCCTCTCTACCTAAGGATGGGCAATGGCTTATGAGTGAGAAACATGGAGCCGTGGGAACTCAGAATGACATGCTACCTGGAGATTGTGGTAACGCCCTGTTTTTTTGTGGGCATATC                                                                                   | 1429          | 0    |
| mh13KK_213  | 195            | CTTCAGTTGTCAAGGTATTGGGTACAGGGGTCAGAAAGAAACATGACTCCATGGACCACTGCTTGGCCCAAGACCAGATGTCAAAACCACAGAGCCCTGCTGTAGAGCATTACAAATGTATTCCACCAAATGTTGGGATGCATCCTAGACCTGTGCTGACCAGCAGTCCCCAGCTGTGAGGAGAAGCCCGCCATT | 2133          | 0    |


It can be directly used as input for **Visual Microhap** (http://forensic.yonsei.ac.kr/VisualMH/index.html), enabling genotype calling of microhaplotype.


<br>

## Citation
If you use this script in your research, please cite the following paper: 


