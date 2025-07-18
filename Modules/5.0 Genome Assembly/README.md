# Computational Practical 5
# Genome Assembly
## Module Developer : Collins Kigen
## Introduction
# 🧩 Genome Assembly Module

**Objective:**  
1. Learn how to assemble genomes from raw sequencing reads using **SPAdes** (for Illumina short reads) **Flye** (for ONT long reads)
2. Visualize assembly graphs using **Bandage**
3. Interpret assembly statistics with **QUAST**.

---

## ✅ Prerequisites
- **Conda** installed
- Installed tools:
  - **SPAdes** for short read assembly
  - **Flye** for long read assembly
  - **Bandage** for graph visualization
  - **QUAST** for assembly quality assessment
- Paired-end sequencing reads (e.g., `sample_R1_paired.fq.gz`, `sample_R2_paired.fq.gz`)

---

# PART A: SHORT READ ASSEMBLY
## Step A1. Activate the Conda environment with SPAdes 
```
conda activate spades
```

## Step A2. Navigate to your working directory
```
cd ~/Documents/Training
```
## Step A3. Create `short-read-assembly` directory and navigate to it
```
mkdir short-read-assembly
cd short-read-assembly
```
## Step A4. Copy raw reads 
```
cp ../QC/ERR12511689_1_paired.fastq .
cp ../QC/ERR12511689_2_paired.fastq .
```

## Step A5. Run SPAdes for genome assembly

>spades.py -1 <forward_reads> -2 <reverse_reads> -o <output_directory> [options]
```
spades.py -1 ERR12511689_1_paired.fastq -2 ERR12511689_2_paired.fastq -o spades_output -t 4
```

## Step A6. Check assembly results in the output folder
# Key files:
>- assembly/contigs.fasta
>- assembly/scaffolds.fasta
>- assembly/spades.log
>- assembly/assembly.fastg
```
ls assembly
```

### Exerecise

#### Count the number of sequences in `contigs.fasta`

## Step A7. Activate Bandage
```
conda activate bandage
```
## Step A8. Load the graph file
```
Bandage load assembly/assembly.fastq
```
## Step A9. Activate quast
```
conda activate quast
```
## Step A10. Assess assembly quality using QUAST
>quast.py <assembly_fasta> -o <output_directory>

```
quast.py assembly/contigs.fasta -o quast_report
```
## Step 11. View QUAST report
```
cd quast_report
cat report.tsv
```
# PART B: LONG READ ASSEMBLY
## Step B1. Activate the Conda environment with flye 
```
conda activate flye
```

## Step B2. Navigate to your working directory
```
cd ~/Documents/Training
```
## Step B3. Create `long-read-assembly` directory and navigate to it
```
mkdir long-read-assembly
cd long-read-assembly
```
## Step B4. Copy raw reads 
```
cp ../QC/sampleX.fastq.gz .
```

## Step B5. Run flye for genome assembly

flye 
```
flye --nano-raw sampleX.fastq -o assembly -t 8 -i 
```

## Step B6. Check assembly results in the output folder
# Key files:
>- assembly/assembly.fasta
>- assembly/assembly_graph.gfa
>- assembly/assembly_info.txt

```
ls assembly
```

### Exerecise

#### Count the number of sequences in `assembly.fasta`

## Step B7. Activate Bandage
```
conda activate bandage
```
## Step B8. Load the graph file
```
Bandage load assembly/assembly_graph.gfa
```
## Step B9. Activate quast
```
conda activate quast
```
## Step B10. Assess assembly quality using QUAST
>quast.py <assembly_fasta> -o <output_directory>

```
quast.py assembly/assembly.fasta -o quast_report
```
## Step B11. View QUAST report
```
cd quast_report
cat report.tsv
```
