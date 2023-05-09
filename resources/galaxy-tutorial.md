---
title: 'Galaxy Tutorial'
date: 2023-05-05
permalink: /resources/galaxy-tutorial/
layout: single
toc: true
tags:
  - rnaseq
  - tutorial
---

_This tutorial follows the training material offered by Galaxy that can be found [here](https://training.galaxyproject.org/training-material/topics/transcriptomics/tutorials/ref-based/tutorial.html). This tutorial starts from the beginning, assuming little to no experience with Galaxy._

# Introduction

In my research, we often use reference based RNA sequencing (RNA-Seq) to determine diverse gene expression changes following exposure to environmental contaminants. Additionally, we go on to determine molecular pathways that are differentially expressed between exposed and control as well. This can give information about the mechanisms of toxicity following exposures. Achieving these end results takes of course the experimentation and the analysis. This walkthrough takes care of the analysis. 

## Why Galaxy?

RNA-Seq requires __a lot__ of data and memory. Most analysis cannot be completed on a personal machine. I would say the minimum RAM memory would have to be upwards of 32 GB. Storage space also has to be ample. Galaxy is a platform that gives free storage and access to high performance computing clusters and even gives a Graphical User Interface (GUI) for typical bioinformatics softwares. This makes running and RNA-seq analysis a lot more attainable and approachable for non computational scientists. If you are interested and have access to a computing cluster or computer with ample storage and RAM, you should check out my tutorial on performing the same RNA-Seq Analysis on the cluster (coming soon ...).

# Data

The starting point for all RNA-Seq analysis is to assess and organize the data you have. Typically, you will receive the raw sequencing reads from the sequencing center in FASTQ format. These files should have a suffix of `.fastq`, `.fastq.gz`, `.fq`, or `.fq.gz`. Naming conventions are also super important. I am including typical illumina naming conventions here for more information ([see here for more](https://support.illumina.com/help/BaseSpace_OLH_009008/Content/Source/Informatics/BS/NamingConvention_FASTQ-files-swBS.htm)):

>FASTQ files are named with the sample name and the sample number, which is a numeric assignment based on the order that the sample is listed in the > sample sheet. For example: SampleName_S1_L001_R1_001.fastq.gz
>    - SampleName—The sample name provided in the sample sheet. If a sample name is not provided, the file name includes the sample ID, which is a required field in the sample sheet and must be unique.
>    - S1—The sample number based on the order that samples are listed in the sample sheet starting with 1. In this example, S1 indicates that this sample is the first sample listed in the sample sheet.
>    - L001—The lane number.
>    - R1—The read. In this example, R1 means Read 1. For a paired-end run, there is at least one file with R2 in the file name for Read 2. When generated, index reads are I1 or I2.
>    - 001—The last segment is always 001.

The important things are to recognize your sample names and remind yourself if you have a single or paired-end read. If you have a paired end read, you should have two files per sample, one with R1 in the file name and another with R2. Sometimes you might end up with four files per sample. This usually means you have two R1 files and two R2 files. Sometimes the sequencing center will send the FASTQ files that way to reduce the storage per file. If this is the case, each R1 file just needs to be concatenated, and same with the R2 files. It can be done on Galaxy or on your command line! If you want to concatenate on the command line, you would do this before you upload the files to Galaxy. 

Option 1: Concatenate files on the command line
Here is an example of a time I ran into this. I saved all my FASTQ files in a folder and saw that there were 4 files per sample. To concatenate them on the command line I executed the following commands in my terminal:

1. Move to the folder where your files are located
``` bash
# move to the folder where your files are located
cd /Users/ashleyschwartz/Documents/Research/05_boscalite_boscalid/raw_data
```
2. Remind yourself of the file names by listing all files in the folder. If you do this you should see all your files listed and it should look something like this"
``` bash
ls
```
with output (just showing first few lines):
``` 
A1_DMSO_1_S119_L004_R1_001.fastq.gz
A1_DMSO_1_S119_L004_R2_001.fastq.gz
A1_DMSO_1_S92_L001_R1_001.fastq.gz
A1_DMSO_1_S92_L001_R2_001.fastq.gz
```
3. Concatenate them! We can see that we have two R1 files for DMSO 1 and two R2 files. We can concatenate them by typing:

```
cat A1_DMSO_1_S119_L004_R1_001.fastq.gz A1_DMSO_1_S92_L001_R1_001.fastq.gz > DMSO_1_R1.fastq.gz
cat A1_DMSO_1_S119_L004_R2_001.fastq.gz A1_DMSO_1_S92_L001_R2_001.fastq.gz > DMSO_1_R1.fastq.gz
```

4. (optional) You could write a script to do this automatically for all files in the folder. Some tricks to get going on this would be a few of these commands (I might come back to this and finish out the script):
``` bash
# get the DMSO R1 file names
find . -type f -name '*DMSO_1*R1*'
```

## 

> <hands-on-title>Quality control</hands-on-title>
>
> 1. **Flatten Collection** <i class="fas fa-fw fa-wrench" aria-hidden="true"></i> with the following parameters convert the list of pairs into a simple list:
>     - *"Input Collection"*: `2 PE fastqs`
{: .hands_on}

<i class="fas fa-fw fa-wrench" aria-hidden="true"></i>