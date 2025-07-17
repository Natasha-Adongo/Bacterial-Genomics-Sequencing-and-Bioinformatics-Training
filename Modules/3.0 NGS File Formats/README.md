# Computational Practical 3
# NGS File Formats
## Module Developer: Collins Kigen
## 1.0 Introduction
## 📚 Introduction to NGS File Formats

Next-Generation Sequencing (NGS) technologies produce large volumes of data that must be stored, processed, and shared using standardized file formats. These formats ensure interoperability between tools, facilitate downstream analysis, and maintain data integrity.

---

### ✅ Why File Formats Matter
- Enable **compatibility** between bioinformatics tools.
- Represent different stages: **raw data**, **alignments**, **variants**, and **annotations**.
- Support **data sharing** and **reproducibility**.

---

### 🔍 Common NGS File Formats

| **Format** | **Purpose** | **Description** |
|------------|-------------|------------------|
| **FASTA**  | Reference sequences | Stores nucleotide or protein sequences without quality scores. |
| **FASTQ**  | Raw reads + quality | Contains sequencing reads with Phred quality scores. |
| **SAM/BAM**| Alignments | SAM = text format, BAM = binary compressed version of SAM. |
| **VCF**    | Variants | Lists SNPs, indels, and other variants with annotations. |
| **GFF/GTF**| Annotations | Genome feature annotations such as genes and exons. |
| **BED**    | Regions | Genomic intervals (used for regions of interest). |

---

### ✅ File Extensions
- `*.fasta`, `*.fa` → FASTA
- `*.fastq`, `*.fq` → FASTQ
- `*.sam`, `*.bam` → Alignments
- `*.vcf`, `*.vcf.gz` → Variants
- `*.gff`, `*.gtf` → Annotations
- `*.bed` → Genomic intervals

---

### 📂 Typical Workflow
1. **Sequencing output** → FASTQ
2. **Alignment to reference** → SAM/BAM
3. **Variant calling** → VCF
4. **Annotation and feature mapping** → GFF/GTF, BED

---

#### 🔗 Useful Tools
- `samtools` – View, sort, and index BAM/SAM files.
- `bcftools` – Process VCF files.
- `bedtools` – Genomic interval operations.
- `seqtk` – FASTA/FASTQ manipulation.

---

<img width="768" height="464" alt="image" src="https://github.com/user-attachments/assets/da1c7731-228f-48e4-b81c-342a98a548d8" />



### Fastq file
FASTQ files are text files containing sequence data with a quality (Phred) score for each base, represented as an ASCII character. 
<img width="553" height="311" alt="image" src="https://github.com/user-attachments/assets/8ebc939d-6a86-4266-82cd-7435086d955f" />
## Phred Quality Scores Explained

Phred quality scores (`Q`) are logarithmically related to base-calling error probabilities (`P`) and are defined as:

Q = -10 * log10(P)


This relation can also be expressed as:

P = 10^(-Q/10)


For example:
- If `Q = 30`, the probability that this base is called incorrectly is **1 in 1,000**.

---

### ✅ Quick Reference Table

| **Phred Quality Score (Q)** | **Probability of Incorrect Base Call (P)** | **Base Call Accuracy** |
|------------------------------|--------------------------------------------|--------------------------|
| 10                           | 1 in 10                                    | 90%                     |
| 20                           | 1 in 100                                   | 99%                     |
| 30                           | 1 in 1,000                                 | 99.9%                   |
| 40                           | 1 in 10,000                                | 99.99%                  |
| 50                           | 1 in 100,000                               | 99.999%                 |
| 60                           | 1 in 1,000,000                             | 99.9999%                |

---

## 📄 FASTA Files

The **FASTA** format is widely used for representing nucleotide or protein sequences. Each entry in a FASTA file consists of:

- A **header line** starting with `>` followed by a sequence identifier and optional description.
- One or more lines of the **sequence** (DNA, RNA, or protein).

### ✅ Example FASTA Entry (DNA)
<pre>
>sequence_1 description
ATGCGTATCGACTAGCTAGCTAGCGTAGCTAGCTA
ATGCTAGCTAGCTAGCTAGCTAGCGATCGATGCT
</pre>

<pre>
>protein_1 description
MTEYKLVVVGAGGVGKSALTIQLIQNHFVDEYDPT
IEKQYKSTIGAAK
</pre>
---

### 🔍 Notes:
- Sequences should **only contain valid IUPAC characters** (A, T, G, C for DNA).
- No blank lines are allowed between header and sequence.
- FASTA files are commonly used as input for tools like BLAST, genome assembly, and alignment software.

---

### 📂 Typical Use Cases
- **Reference genomes** for mapping.
- **Protein databases** for homology searches.
- **Input for bioinformatics pipelines**.

---

## Practical
### Step 1: Navigate to training directory
```
cd ~/Documents/Training
```
### Step 2: Create a directory called `NGS-formats` and move into it
```
mkdir NGS-formats
cd NGS-formats
```
### Step 3: Copy ERR from ~/Documents/Training into the current directory
```
cp ../ERR12511689_1.fastq.gz .
```
### Step 4: Uncompress the fastq.gz
```
gunzip ERR12511689_1.fastq.gz
```
 
### Step 5: Download SA19KEN.fasta
```
wget https://raw.githubusercontent.com/AMR-Bioinformatics/Bacterial-Genomics-Sequencing-and-Bioinformatics-Training/refs/heads/main/Datasets/SA19KEN.fasta
```
## Exercise
1. Open the first 10 lines of ERR12511689_1.fastq
2. Write a code to count the number of reads in ERR12511689_1.fastq
3. Open the first 5 lines of SA19KEN.fasta
4. List all the header lines of SA19KEN.fasta
5. Count the number of sequences in SA19KEN.fasta
