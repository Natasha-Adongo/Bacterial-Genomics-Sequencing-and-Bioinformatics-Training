# Computational Practical 5
# Genome Assembly
## Module Developer : Collins Kigen
## Introduction
# 🧩 Genome Assembly Module

**Objective:**  
Learn how to assemble genomes from raw sequencing reads using **SPAdes** (for Illumina short reads) and interpret assembly statistics with **QUAST**.

---

## ✅ Prerequisites
- **Conda** installed
- Installed tools:
  - **SPAdes** for genome assembly
  - **QUAST** for assembly quality assessment
- Paired-end sequencing reads (e.g., `sample_R1_paired.fq.gz`, `sample_R2_paired.fq.gz`)
- Sufficient system memory (≥ 8 GB for small bacterial genomes)

---


## Step 1. Activate the Conda environment with SPAdes 
```
conda activate spades
```

## Step 2. Navigate to your working directory
```
cd ~/Documents/Training
```
## Step 3. Create `Assembly` directory and navigate to it
```
mkdir Assembly
cd Assembly
```
## Step 4. Copy raw reads 
```
cp ../ERR*.fastq.gz .
```

## Step 5. Run SPAdes for genome assembly

`spades.py -1 <forward_reads> -2 <reverse_reads> -o <output_directory> [options]`
```
spades.py -1 sample_R1_paired.fq.gz -2 sample_R2_paired.fq.gz -o spades_output -t 4
```


## Step 6. Check assembly results in the output folder
# Key files:
` - spades_output/contigs.fasta`
` - spades_output/scaffolds.fasta`
` - spades_output/spades.log`

## Step 7. Assess assembly quality using QUAST
`quast.py <assembly_fasta> -o <output_directory>`

```
quast.py spades_output/contigs.fasta -o quast_report
```
# Step 8. View QUAST report
```
cd quast_report
cat report.tsv
```
