# Computational Practical 4
# Sequence Data Quality Control
## Module Developer : Collins Kigen
## Introduction
A typical whole genome sequencing process involves genomic DNA isolation, library preparation and sequencing. Errors can be introduced during the library preparation and sequencing steps which may cause inaccurate representations of the original DNA sequences. 

Potential problems or quality related issues with raw next generation sequencing (NGS) data include:

1. Low base quality \- sequencing technologies can produce reads with varying quality
2. Contamination with adapter sequences
3. Base composition biases  
4. GC content distribution
5. Sequence duplication 

***Several tools are available for performing quality control and preprocessing of fastq data*** 

Some popular standalone tools tools include:

1. FASTQC \- quality control tool for visualizing key quality profiling metrics  
2. Cutadapt \- adapter removal and read filtering  
3. Trimmomatic \- adapter removal, read pruning and filtering e.g. using sliding window cutting  
4. TrimGalore \- a wrapper tool around cutadapt and FASTQC

In recent years tools that integrate both quality control and read filtering have been developed, such as TrimGalore, AfterQC, fastp, etc. In this practical we will introduce and use fastp for raw data quality control, filtering, adapter removal and base correction for fastq data. Fastp is an ultra-fast multithreaded tool that incorporates most features of fastqc, cutadapt, trimmomatic and AfterQC, and is best suited for short reads, but with basic support for long read data QC.

> For visualization of quality metrics we will use MultiQC

The preprocessing of FASTQ data, which means removing adapter contamination, filtering low-quality reads, and correcting wrongly represented bases, is an indispensable but resource intensive part of sequencing data analysis.

**2.1 Fastq format**   
In NGS, fastq data format is broadly adopted as the standard for the raw output data regardless of the sequencing platform and the sequencing throughput. 


**2.2. (Phred) Quality Scores Interpretation**


FASTQ data need to go through quality control and a series of preprocessing steps before they can enter the downstream analysis to ensure that clean and accurate reads are processed downstream.

## 2.3 Common QC metrics for raw data

## Removal of adapter contamination

* Sequence-matching based adapter trimming  
- Tools: Cutadapt, Trimmomatic etc.  
* Adapter trimming based on finding overlaps of read-pairs  
- Tools: Fastp, AfterQC  
- Automatic adapter detection

### Base correction

* Mainly applied to paired-end data  
* Only base pairs with an imbalance quality score are corrected

### Improving read quality

* Sliding window quality pruning method  
  * Drops low quality bases in each reads 5\` or 3\` region  
* Filtering reads using a low-quality base percentage, N base number and read length

### Trimming of polyG and polyX tails

Some Illumina sequencing platforms such as the NextSeq series can produce reads with polyG tails due to their fluorescence chemistry resulting in some T and C bases being interpreted as Gs in read tails when signal strength of each cluster becomes weaker in subsequent cycles. The polyG tail issue can result in a serious base content separation problem, meaning that A and T or C and G have substantially different base content ratios. 

### Overrepresented sequence analysis

# PART 1: Quality Control



**Objective:**  
Perform quality control on raw sequencing data using **FastQC**, interpret results, and open the generated reports.

---

## ✅ Prerequisites
- **Conda** installed
- **FastQC** installed in a Conda environment
- Sequencing data in **FASTQ** format (`*.fastq` or `*.fastq.gz`)

---


## Step 1. Activate the Conda environment where FastQC is installed
```
conda activate fastqc
```

## Step 2. Navigate to the working directory containing your FASTQ files
```
cd ~/Documents/Training
```
## Step 3. Create QC dir and move into it
```
mkdir QC
cd QC
```
## Step 4. Copy ERR12511689_1.fastq from NGS-formats
```
cp ../NGS-Formats/ERR12511689_1.fastq .
```
## Step 5. Run FastQC on a single FASTQ file
```
fastqc ERR12511689_1.fastq
```

# Step 6. Check generated output: FastQC creates two files per sample
    - ERR12511689_1.html (interactive report)
    - ERR12511689_1.zip  (raw analysis data)

## Step 7. Open the HTML report in a browser
navigate to the folder and double-click the HTML file


# PART 2: TRIMMING



**Objective:**  
Learn how to remove low-quality bases and adapter contamination from raw sequencing reads using **Trimmomatic**.

---

## ✅ Prerequisites
- **Conda** installed
- **Trimmomatic** installed in a Conda environment
- Raw sequencing data in FASTQ format (`*.fastq` or `*.fastq.gz`)
- Adapter sequence file (commonly provided with Trimmomatic, e.g., `TruSeq3-PE.fa`)

---



## Step 1. Activate the Conda environment where Trimmomatic is installed
```
conda activate trimmomatic
```

## Step 2. Navigate to the working directory with your FASTQ files
```
cd ~/Documents/Training
```

## Step 3. Run Trimmomatic on paired-end reads
### Syntax:
`trimmomatic PE -threads <N> <input_forward> <input_reverse> <output_forward_paired> <output_forward_unpaired> <output_reverse_paired> <output_reverse_unpaired> <options>`

```
trimmomatic PE -threads 4 \
ERR12511689_1.fastq ERR12511689_2.fastq \
ERR12511689_1_paired.fastq ERR12511689_1_unpaired.fastq \
ERR12511689_2_paired.fastq ERR12511689_2_unpaired.fastq \
LEADING:3 TRAILING:3 SLIDINGWINDOW:4:15 MINLEN:36
```
Explanation of Parameters
PE → Paired-end mode.

-threads 4 → Uses 4 CPU threads for speed.

ILLUMINACLIP:TruSeq3-PE.fa:2:30:10 → Removes adapter sequences.

2 → Maximum mismatches.

30 → Palindrome clip threshold.

10 → Simple clip threshold.

LEADING:3 → Removes low-quality bases from start (Q<3).

TRAILING:3 → Removes low-quality bases from end.

SLIDINGWINDOW:4:15 → Scans with a 4-base window, trimming when average Q < 15.

MINLEN:36 → Drops reads shorter than 36 bases after trimming.
## Step 4. Check the output files:
 - Paired-end mode creates 4 files: forward_paired, forward_unpaired, reverse_paired, reverse_unpaired


## Step 5. Post-trimming QC
fastqc ERR12511689_1_paired.fq.gz ERR12511689_2_paired.fq.gz



Some sequences, or even entire reads, can be overrepresented in FASTQ data. Analysis of these overrepresented sequences provides an overview of certain sequencing artifacts such as PCR over-duplication, polyG tails and adapter contamination.

### Hands-on exercise 1: (20 min)
Perform QC check on ERR12511690, Trimming and post-trim QC
