# Computational Practical 6
# Species ID and Bacterial Typing
## Module Developer : Collins Kigen
## Introduction
# Species ID

## Step 1. Activate mash environment


## Step Navigate to working directory
```
cd ~/Documents/Training
```

## Step Create mash directory and navigate into it
```
mkdir mash
cd mash
```
## Copy short-read assembly and rename to actual sample ID
```
cp ../short-read-assembly/assembly/contigs.fasta
mv contigs.fasta ERR12511689.fasta
```

## Step 1a.
```
conda activate mash
```

## Step 1b. Perform mash screen
```
mash screen refseq.genomes.k21s1000.msh ERR1251168.fasta > mash_screen.txt
```
## Step Sort mash results and visualize
```
sort -gr mash_screen.txt > mash_screen_sorted.txt
less mash_screen_sorted.txt
```
# Strain Typing
## Step 1. Navigate to working directory
```
cd ~/Documents/Training
```

## Step 2 Create typing and navigate into it
```
mkdir typing
cd typing
```

## Step  Copy assembly
```
cp ../mash/ERR12511689.fasta .
```


## Step 1. Activate mlst
```
conda activate mlst
```

## Step 1. Perform MLST typing

```
mlst ERR12511689.fasta
```

## Step 1. Activate sccmec
```
conda activate sccmec
```
## Step Perform sccmec typing
```
sccmec ERR12511689.fasta
```
## Step Perform spatyping
```
spatyper ERR12511689.fasta
```
