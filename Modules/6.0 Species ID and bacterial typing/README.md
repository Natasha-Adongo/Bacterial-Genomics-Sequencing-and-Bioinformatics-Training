# Computational Practical 6
# Species ID and Bacterial Typing
## Module Developer : Collins Kigen
## Introduction
# Part A: Species ID
# **Principle of Mash**

Mash is a fast tool for estimating genome similarity using the **MinHash algorithm**. Instead of full alignment, it summarizes sequences into small sets called **sketches**.

---

## **How It Works**
1. **Split into k-mers**  
   Break sequences into small pieces of length *k* (default 21).

2. **Hash and Sketch**  
   Convert k-mers into numeric hashes and keep only a small subset (default 1000).  
   This subset is the **sketch**.

3. **Compare Sketches**  
   Similarity is estimated using the **Jaccard index** (shared hashes / total hashes).

4. **Compute Distance**  
   Convert similarity to a distance score:  
   - **Smaller score = more similar genomes**.

---

## **Why Mash?**
- Very fast and memory-efficient  
- Works on assemblies or raw reads  
- Ideal for species ID, clustering, and contamination checks  

---




## Step A1. Navigate to working directory
```
cd ~/Documents/Training
```

## Step A2. Create `spedies_id` directory and navigate into it
```
mkdir species_id
cd species_id
```
## Step A3. Copy short-read assembly and rename to actual sample ID
```
cp ../short-read-assembly/assembly/contigs.fasta
mv contigs.fasta ERR12511689.fasta
```

## Step A4. Activate mash environment
```
conda activate mash
```

## Step A5. Perform mash screen
```
mash screen ../refseq.genomes.k21s1000.msh ERR1251168.fasta > mash_screen.txt
```
## Step A6. Sort mash results and visualize
```
sort -gr mash_screen.txt > mash_screen_sorted.txt
less mash_screen_sorted.txt
```
# Part B: Strain Typing
## Step B1. Navigate to working directory
```
cd ~/Documents/Training
```

## Step B2. Create `typing` and navigate into it
```
mkdir typing
cd typing
```

## Step B3. Copy assembly files
```
cp ../species_id/ERR12511689.fasta .
```

## Step B4. Activate mlst
```
conda activate mlst
```

## Step B5. Perform MLST typing

```
mlst ERR12511689.fasta
```
# Part C: Sccmec typing
## Step C1. Activate sccmec
```
conda activate sccmec
```
## Step C2. Perform sccmec typing
```
sccmec ERR12511689.fasta
```
# Part D: Spa typing
## Step D1. Activate spatyper environment
```
conda activate spatyper
```
## Step D2. Perform spatyping
```
spatyper ERR12511689.fasta
```
