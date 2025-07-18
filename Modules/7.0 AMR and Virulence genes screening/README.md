
# AMR & Virulence genes screening
 <img width="375" height="430" alt="image" src="https://github.com/user-attachments/assets/5abacc4a-7389-4416-83e0-173825761d26" />

 ## Genome characterization 

- The genome is all the nucleotide sequences of DNA (or RNA in viruses) in organisms which is highly associated with biological processes, cell function and contains the information of evolution as well.
- *Genome characterization* is the process of identifying genes, regulatory elements, and other functional components in a genome.

### Key concepts in genome characterization
1. <ins>Sequencing</ins>: Determining the order of nucleotide in a genome. Typically done using high-throughput tecnologies like NGS platforms (Illumina Nextseq1000/ONT) [Click here for more information](https://github.com/AMR-Bioinformatics/Bacterial-Genomics-Sequencing-and-Bioinformatics-Training/blob/main/Lectures/History%20of%20Sequencing%2C%20Overview%20and%20Comparison%20of%20NGS%20Technologies.pdf)
2. <ins>Annotation</ins>: This is the process of finding and designating locations of individual genes and other biological features on nucleotide sequences. Some pipelines for annotation include;
    - [PGAP](https://github.com/ncbi/pgap) (Prokaryotic Genome annotation pipeline) & [Prokka](https://github.com/tseemann/prokka) : Annoation of prokaryotic genomes
    - [EGAP](https://github.com/ncbi/egapx) (Eukaryotic Genome annotation Pipeline): Eukaryotic genomes excluding fungi and protozoan
    - [Pharokka](https://github.com/gbouras13/pharokka) : Rapid annotation tool for bacteriophage genomes 
3. <ins>Functional genomics</ins>: It is the processes of characterizing genomes with a gol of elucidating how the genes perform their function. [Read more here](https://www.sciencedirect.com/topics/biochemistry-genetics-and-molecular-biology/functional-genomics)

Antibiotic resistance poses a significant health challenge because drugs that were once highly effective are no longer able to cure bacterial infections. In AMR surveillance genome characterzation has become a instrumental in the detection of resistance markers and pahogenic markers that have lead to bacterial infections becoming a  significant public health concern. In this practical, we will analyze Whole Genome Sequences to identify antimicrobial resistance genes. 

<img width="624" height="345" alt="image" src="https://github.com/user-attachments/assets/9ab743bb-773b-450a-a24c-308e7cdea3e5" />


#### STEP 1: Navigate to working directory 

```
cd ~/Documents/Training/
```

#### STEP 2 : Create `AMR_genes` directory and navigate into it

```
mkdir AMR_genes
cd AMR_genes
```
## WGS-based prediction of AMR using ABRicate
### Introduction to ABRicate

ABRicate is a tool for mass screening of contigs for antimicrobial resistance or virulence genes. The name ABRicate was chosen as the first 3 letters are a common acronym for “Anti-Biotic Resistance”
- It only supports contigs, not FASTQ reads
- It only detects acquired resistance genes, NOT point mutations
- It uses a DNA sequence database, not protein
- It comes bundled with multiple databases:

| **Abbrv** | **Full name** |
|-----------|-------------- |
| **NCBI**   | National Center for Biotechnology Information |
| **CARD**   | Comprehensive Antibiotic Resistance Database |
| **ARG-ANNOT**   | Antibiotic Resistance Gene-ANNOTation |
| **Resfinder**   | Resfinder |
| **MEGARES**   | Microbal Ecology Group Resistance  |
| **EcOH**   | EcOH |
| **PlasmidFinder**   | PlasmidFinder |
| **Ecoli_VF**   | Escherichia coli virulence factors |
| **VFDB**   | Virulence Factor Database|

----

#### Step 3:  Check the help/manual
```
abricate --help
```
<pre>
SYNOPSIS
  Find and collate amplicons in assembled contigs
AUTHOR
  Torsten Seemann (@torstenseemann)
USAGE
  % abricate --list
  % abricate [options]  > out.tab
  % abricate [options] --fofn fileOfFilenames.txt > out.tab
  % abricate --summary    ... > summary.tab
GENERAL
  --help                This help.
  --debug               Verbose debug output.
  --quiet               Quiet mode, no stderr output.
  --version             Print version and exit.
  --check               Check dependencies are installed.
  --threads             [N] Use this many BLAST+ threads [1].
  --fofn [X]            Run on files listed in this file [].
DATABASES
  --setupdb             Format all the BLAST databases.
  --list                List included databases.
  --datadir [X]         Databases folder [/opt/homebrew/Cellar/abricate/1.0.1_2/libexec/db].
  --db [X]              Database to use [ncbi].
OUTPUT
  --noheader            Suppress column header row.
  --csv                 Output CSV instead of TSV.
  --nopath              Strip filename paths from FILE column.
FILTERING
  --minid [n.n]         Minimum DNA %identity [80].
  --mincov [n.n]        Minimum DNA %coverage [80].
MODE
  --summary             Summarize multiple reports into a table.
DOCUMENTATION
  https://github.com/tseemann/abricate
</pre>

#### Step 4: Check the databases installed

```
abricate --list
```
<pre>
  DATABASE        SEQUENCES   DBTYPE  	DATE
card            2631        nucl    	2023-Nov-4
ecoli_vf        2701        nucl    	2023-Nov-4
plasmidfinder 	460         nucl    	2023-Sep-9
ecoh            597         nucl    	2023-Sep-9
ncbi          	5386        nucl    	2023-Sep-9
resfinder      	3077        nucl    	2023-Sep-9
</pre>


#### Step 5: Update databases

```
abricate-get_db --db ncbi
abricate-get_db --db card
abricate-get_db --db resfinder
```
```
abricate --list
```

##### Step 6: Run ABRicate

```
abricate -db resfinder ../species_id/ERR12511689.fasta > ./ERR12511689.tab
```

<pre>
abricate           : run the tool
-db                : flag used to specify the database to use
resfinder          : database. Alternatively, we can use NCBI or CARD here
ERR12511689.fasta  : path to contig file
">"                : redirection symbol used to save the output to a file
ERR12511689.tab    : path to output file
</pre>

##### Open the file with the AMR results

List to check output file
```
ls
```
Open the result file

```
less -S ERR12511689.tab
```

<pre>
less                : bash command to open files one page at a time
-S                  : flag to prevent text wrapping
ERR12511689.tab     : path to output file
  
</pre>

Virulence genes detection
----
Virulence genes are genes in a pathogen ie bacteria that encode proteins or other molecules that contribute to the pathogen's ability to cause disease. 
These genes enable the pathogen to infect a host, evade the host's ummune system and cause damage to host tissues.

<img width="850" height="440" alt="image" src="https://github.com/user-attachments/assets/e912cf31-a19f-4af4-ab81-e95896d8e4eb" />

#### Step 1 : Navigate to the working dircetory 
```
cd ~/Documents/Training/
```

#### STEP 2 : Create `AMR_genes` directory and navigate into it

```
mkdir Vir_genes
cd Vir_genes
```

##### Step 3: Run ABRicate

```
abricate -db VFDB ../species_id/ERR12511689.fasta > ./ERR12511689.tab
```

<pre>
abricate           : run the tool
-db                : flag used to specify the database to use
VFDB          : database. 
ERR12511689.fasta  : path to contig file
">"                : redirection symbol used to save the output to a file
ERR12511689.tab    : path to output file
</pre>

##### Open the file with the Virulence results

List to check output file
```
ls
```
Open the result file

```
less -S ERR12511689.tab
```

<pre>
less                : bash command to open files one page at a time
-S                  : flag to prevent text wrapping
ERR12511689.tab     : path to output file
  
</pre>

Exercises
----
1.  Screen for AMR genes using the NCBI database on the same sequence
2.  Screen for plasmid replicons using the plasmidfinder db on the same sequence

