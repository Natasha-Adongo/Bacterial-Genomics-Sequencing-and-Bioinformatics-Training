# Computational Practical 6
# Species ID and Bacterial Typing
## Module Developer : Collins Kigen
## Introduction
# Part A: Species ID


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
mash screen ../mash/refseq.genomes.k21s1000.msh ERR1251168.fasta > mash_screen.txt
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
