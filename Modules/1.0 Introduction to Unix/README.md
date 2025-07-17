 
 # UNIX/Linux CommandLine
 ![UNIX CMD](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQgHiozN_t_BRDczEOFqq_LpbUl3LvdlnEYTseJCdyL8cLxQAMUCHM4PXxJHkdQyCv1TSU&usqp=CAU)

 # UNIX vs Windows
 | UNIX | Windows |
 | ---- | ----- |
 | Open-source - highly flexible, portable, and well-suited for network management | A proprietary system designed with a graphical user interface (GUI) for user-friendly interaction |
 | Predominantly text-based (CLI) | Uses icons and clicks (GUI) |
 | Employs Unix File System | File Allocation Tables (FAT32) / New Technology File System (NTFS) |
 | Prioritizes security | More susceptible to malware |

 # UNIX CLI
 | Advantages | Disadvantages |
 | --- | --- |
 | Gives user more control of the system | Steep Learning curve |
 | Most UNIX OS are freely available online | |
 | Built using powerful commands | |
 | Excellent for automation | |
 | Demands fewer system resources | |
 | Preferred for remote connections (SSH) | |
 | Allows for modularization of complex tasks | | 

# Manipulating Files

| command | function |
| ----- | ---- |
| ls | list your files |
| ls -l | lists your files in 'long format' |
| ls -a | lists all files including hidden files |
| touch | creates an empty file |
| more filename | shows the first part of a file on a new screen window, use spacebar or q to quit the screen |
| less filename | Displays the contents of a file one page at a time |
| head filename | Displays the first ten lines of a file |
| tail filename | Displays the last ten lines of a file |
| grep filename | Search for a pattern within the file |
| find <location> -name <pattern> | Finds files matching an expression |
| cp filename1 filename2 | copies a file |
| mv filename1 filename2 | moves a file i.e. gives it a different name, or moves it into a different directory |
| rm filename | removes a file. It is wise to use the option rm -i, which will ask you for confirmation before actually deleting anything.  |
| diff filename1 filename2 | compares files, and shows where they differ |
| wc filename | tells you how many lines, words, and characters there are in a file |
| chmod options filename | lets you change the read, write, and execute permissions on your files. |
| gzip filename | compresses files, so that they take up much less space. Gzip produces files with the ending '.gz' appended to the original filename. |
| gunzip filename | uncompresses files compressed by gzip. |
| cat filename1 filename2 | Concatenates files |


# Manipulating directories / Navigating your file system
| command | function |
| ----- | ---- |
| mkdir dirname | make a new directory |
| cd dirname | change directory. You basically 'go' to another directory |
| pwd | tells you where you currently are |
| rmdir | deletes an empty directory |

# Tutorial
## Creating directories/files
``` 
mkdir linux_tutorial 
cd linux_tutorial 
touch file1.txt 
echo "Hello, world!" > file1.txt
```

## Copying and moving files 
```
cp file1.txt file2.txt 
mkdir -p ~/new_dir 
mv ~/linux_tutorial/file1.txt ~/new_dir 
```

## Manipulating fastq files
``` 
wget https://zenodo.org/records/3736457/files/1_control_ITS2_2019_minq7.fastq?download=1 -O ~/new_dir
cd ~/new_dir
ls -lhrt ~/new_dir
head -n 10 1_control_ITS2_2019_minq7.fastq

# How many files does the file have?
wc -l 1_control_ITS2_2019_minq7.fastq

#How many reads are there in the file
echo "<output of previous command>/4" | bc

#What is the fragment size of the 1st read?
head -n 4 1_control_ITS2_2019_minq7.fastq | head -n 2 | tail -n 1 >> read1_sequence.txt
cat read1_sequence.txt | wc -c

#Is that the correct answer?
The correct answer is the answer above -1
#why? 
The commands above introduce a newline character that is read as an extra character
```

## Assignment
1. write the last four lines of the fastq file used in the previous section into a file named 'last_read.txt'
2. Determine the fragment length of the 50th read in the fastq file used in the previous section
3. Compress the file above to its .gz format

