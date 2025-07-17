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

## 🛠 Complete Workflow: Genome Assembly in 6 Steps


# 1. Activate the Conda environment with SPAdes 
conda activate spades

# 2. Navigate to your working directory
cd /path/to/your/data

# 3. Run SPAdes for genome assembly
# Syntax:
# spades.py -1 <forward_reads> -2 <reverse_reads> -o <output_directory> [options]

spades.py \
  -1 sample_R1_paired.fq.gz \
  -2 sample_R2_paired.fq.gz \
  -o spades_output \
  --careful \
  -t 4 \
  -m 8

# Options:
# --careful : reduces mismatches and indels
# -t : number of threads
# -m : maximum memory in GB

# 4. Check assembly results in the output folder
# Key files:
# - spades_output/contigs.fasta
# - spades_output/scaffolds.fasta
# - spades_output/spades.log

# 5. Assess assembly quality using QUAST
# Syntax:
# quast.py <assembly_fasta> -o <output_directory>

quast.py spades_output/contigs.fasta -o quast_report

# 6. View QUAST report
# HTML report location:
# quast_report/report.html
