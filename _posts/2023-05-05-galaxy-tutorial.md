---
title: 'Reference Based RNA Sequencing Analysis - Galaxy Tutorial'
date: 2023-05-05
permalink: /posts/2023/05/galaxy-tutorial
layout: single
excerpt: "This tutorial goes over the full RNA sequencing pipeline in Galaxy, an open source web-based platform for data intensive biomedical research. Galaxy is great for conducting RNA-seq analysis when you don't have access to the appropriate computing resources."
categories: resource
toc: true
tags:
  - RNA Sequencing
---

_This tutorial is loosely based on the training material offered by Galaxy that can be found [here](https://training.galaxyproject.org/training-material/topics/transcriptomics/tutorials/ref-based/tutorial.html). This tutorial starts from the beginning, assuming little to no experience with Galaxy._

**In this tutorial, you will go from raw sequencing reads (FASTQ files) to gene counts in Galaxy**

# Introduction

In my research, we often use reference based RNA sequencing (RNA-Seq) to determine diverse gene expression changes following exposure to environmental contaminants. Additionally, we go on to determine molecular pathways that are differentially expressed between exposed and control as well. This can give information about the mechanisms of toxicity following exposures. Achieving these end results takes of course the experimentation and the analysis. This walkthrough takes care of the analysis. 

**Why Galaxy?**

RNA-Seq requires __a lot__ of data and memory. Most analysis cannot be completed on a personal machine. I would say the minimum RAM memory would have to be upwards of 32 GB. Storage space also has to be ample. Galaxy is a platform that gives free storage and access to high performance computing clusters and even gives a Graphical User Interface (GUI) for typical bioinformatics softwares. This makes running and RNA-seq analysis a lot more attainable and approachable for non computational scientists. If you are interested and have access to a computing cluster or computer with ample storage and RAM, you should check out my tutorial on performing the same RNA-Seq Analysis on the cluster (coming soon ...).

# Getting Started on Galaxy

First thing is first, make an account on [Galaxy](usegalaxy.org)! On the right hand side, you'll see `History`. This is where you will eventually organize the project and see all the data we generate. On the left hand side, you'll see `Tools` and a search bar. This is where we will be searching for any tool we will use. 

**Create a History**

On the top left hand corner, click the `+` sign to create a new history. You can think of a History as a project. Right now you will see Unnamed History on the top right. Go ahead and click the <i class="fas fa-fw fa-solid fa-pen" aria-hidden="true"></i> icon and rename the history to the project name. Here I will use TCPMOH since I will be using TCPMOH data. We should be good to go. Let's upload the data!

**Tips and Tricks**

- If an item is grey, it has yet to be sent to the queue to run. You'll also see the <i class="fa-solid fa-clock"></i> icon on the top left of the history item. 
- If an item in the history is pinkish and has a <i class="fa-solid fa-spinner"></i> icon, the item is running. 
- If an item in the history is green, if is fully uploaded/generated with no issues. 
- If an item in the history is red, there was an error generating that file. 

# Data

The starting point for all RNA-Seq analysis is to assess and organize the data you have. Typically, you will receive the raw sequencing reads from the sequencing center in FASTQ format. These files should have a suffix of `.fastq`, `.fastq.gz`, `.fq`, or `.fq.gz`. Naming conventions are also super important. I am including typical illumina naming conventions here for more information ([see here for more](https://support.illumina.com/help/BaseSpace_OLH_009008/Content/Source/Informatics/BS/NamingConvention_FASTQ-files-swBS.htm)):

>FASTQ files are named with the sample name and the sample number, which is a numeric assignment based on the order that the sample is listed in the > sample sheet. For example: `SampleName_S1_L001_R1_001.fastq.gz`
>    - `SampleName`—The sample name provided in the sample sheet. If a sample name is not provided, the file name includes the sample ID, which is a required field in the sample sheet and must be unique.
>    - `S1`—The sample number based on the order that samples are listed in the sample sheet starting with 1. In this example, S1 indicates that this sample is the first sample listed in the sample sheet.
>    - `L001`—The lane number.
>    - `R1`—The read. In this example, R1 means Read 1. For a paired-end run, there is at least one file with R2 in the file name for Read 2. When generated, index reads are I1 or I2.
>    - `001`—The last segment is always `001`.

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

For this tutorial, we will analyze the impact of TCPMOH on the developing zebrafish. Data is available publicly on the Gene Expression Omnibus, [GSE165920](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE165920). I will be using a subset of this data and performing the analysis as if the full data was present. The full file names are:

```
1_DMSO_S64_L003_R1_001.fastq.gz
1_DMSO_S64_L003_R2_001.fastq.gz
2_DMSO_S65_L003_R1_001.fastq.gz
2_DMSO_S65_L003_R2_001.fastq.gz
11_TCPMOH_S74_L003_R1_001.fastq.gz
11_TCPMOH_S74_L003_R2_001.fastq.gz
12_TCPMOH_S75_L003_R1_001.fastq.gz
12_TCPMOH_S75_L003_R2_001.fastq.gz
```

I renamed each file to:
```
DMSO_1_R1.fastq.gz
DMSO_1_R2.fastq.gz
DMSO_2_R1.fastq.gz
DMSO_2_R2.fastq.gz
TCPMOH_1_R1.fastq.gz
TCPMOH_1_R2.fastq.gz
TCPMOH_2_R1.fastq.gz
TCPMOH_2_R2.fastq.gz
```

**Upload the Data**

On the left hand side, you will see a button that looks like **<i class="fas fa-fw fa-solid fa-upload"></i> Upload Data**. Click **<i class="fas fa-fw fa-solid fa-desktop"></i> Choose Local Files** and upload the files that are located on your computer. Make sure you press the **Start** Button. FYI: this takes a while.

Once completed, you should see all the files in the history and they should all be the color green. If you click on the file name, in my case `TCPMOH_1_R1.fastq.gz` you should see the following stats and items:
- 1.3 GB (or however many GB yours is)
- format fastqsanger.gz
  - If you see the datatype is `fastq` and not `fastqsanger`, follow these steps:
    - Click on the <i class="fas fa-pencil" aria-hidden="true"></i> pencil icon for the dataset to edit its attributes
    - In the central panel, click on the **<i class="fas fa-gear"></i> Convert** tab on the top
    - In the lower part **<i class="fas fa-database"></i> Datatypes**, select `fastqsanger`
      - tip: you can start typing the datatype into the field to filter the dropdown menu
    - Click the **Save** button
- a short snippet of the file:
  ```
  @A00953:253:HYYGVDSXY:3:1101:2627:1000 1:N:0:CCTGCGGAAC+AGCCTATGAT
  ACCCTCCTCTATAGACAGCACCTCATGCATTTTCTTTAGGCAATCATTGCCAACTTTCAATCCTTCAATAACTTTCATCTCTATTTGTGCAAATTCAATAT
  +
  ```
  Note:
  Remember for FASTQ files the first line is the sequence id, the second line is the sequence of neucleotides, and the third line is the transition line, which should be a `+` on its own. 

**Organizing the Data**

Many Galaxy tutorials recommend using collections. Collections are a way to combine all the samples into a 'folder' of sorts. You can then run tools on the entire collection. There are a few issues with this strategy:
1. The collections put the original files in the hidden portion of the history and renames the collection that ends up non descriptive for quality control analysis. 
2. If you run a tool on the entire collection and one file in the collection fails, it is nearly impossible to recover the original file to run it on that one sample again (see point above). The only option would be to re-run the tool on the entire collection. 

Instead of using collections, I like to use Tags. Tags will essentially give a tag to each sample that will automatically Tag any file generated from the original file with the same Tag. **You must** put a `#` in the tag for the tag to cascade. 

>To add a tag:
>- click on the sample file name
>- click **Add Tags <i class="fas fa-database"></i>**
>- type `#sample_name`, for example `#DMSO_1`.

The R1 and R2 files from the same sample should have the same tag. From here, if you click the actual tag, you will see each of the files with that tag. 

# Quality Control

Now that we have all the data populated and organized, we can assess the quality of the reads. We will do this using FastQC. From the [FastQC documentation](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/), _FastQC aims to provide a simple way to do some quality control checks on raw sequence data coming from high throughput sequencing pipelines. It provides a modular set of analyses which you can use to give a quick impression of whether your data has any problems of which you should be aware before doing any further analysis._ Check out the [FastQC Galaxy Tutorial](https://training.galaxyproject.org/training-material/topics/sequence-analysis/tutorials/quality-control/tutorial.html) for an in depth overview of how to inspect FastQC reports. Here, we will discuss some of these as well. 

## FastQC

On the left hand side tool search bar, search for FastQC. Click on `FastQC Read Quality Reports` and you should see the tool options populate the middle column on the webpage. 

> **FastQC <i class="fas fa-wrench"></i><i class="fas fa-gear"></i>** with the following parameters:
> - Raw read data from your current history
>   - click multiple files (middle button)
>   - highlight each of the fastq files you have (R1 and R1 for each sample)
> - **<i class="fas fa-play"></i> Run Tool**

This will generate two files for each sample in your history and each file should have the sample name tag on it to help you identify the sample. The files will have names something like:
- FastQC on data 1: Webpage
- FastQC on data 1: Raw
The webpage will be a html report where we can visualize the statistics for each sample. The tag does help us identify the samples, but the changing the sample names is also important. Otherwise, the sample name in the report will show up as  `FastQC on data 1` and not the actual sample name `DMSO_1`. 

Check out [here](/files/posts/galaxy-tutorial/DMSO_1_R1_FastQC.html) for the full FastQC report for the `DMSO_1_R1` sample. Notice the read length is 101. This will come in handy later!

> **Rename each file**
> - click the <i class="fas fa-pen"></i> icon to the left of the item name.
> - Edit Dataset Attributes will pop up in the middle
> - Edit the Name accordingly
> - click <i class="fas fa-save"></i> Save

**Inspect the FastQC Results**

We can now inspect each individual quality control report using the webpage output by clicking on the <i class="fas fa-eye"></i> to the right of the file name. 

### MiltiQC

MultiQC is a tool that will aggregate each FastQC report from every sample and run into one file for comparison. Type MultiQC in the tool search bar and click `MultiQC aggregate results form bioinformatics analyses into a single report`.

> **MultiQC <i class="fas fa-wrench"></i><i class="fas fa-gear"></i>** with the following parameters:
> - In the Results box
>   - Which tool was used to generate logs?
>     - select FastQC from the dropdown
>   - FastQC Ouput
>     - select each of the FastQC raw outputs
> - **<i class="fas fa-play"></i> Run Tool**

Check out [here](/files/posts/galaxy-tutorial/MultiQC_RawData_TCPMOH.html) for the full MultiQC report for each of the samples used in this study. 

# Trimming

 Based on the quality control report, you can decide whether or not trimming is necessary. One interesting thing to not is that aligners like STAR will auto trim a bit so trimming is sometimes not advised unless there is a major issue (lots of poor quality bases, high adapter content, etc). It also depends on the library prep and their recommendations. In any case, we can trim using the cutadapt tool.

 Check out [illumina's documentation](https://knowledge.illumina.com/library-preparation/general/library-preparation-general-reference_material-list/000001314) to see which adapter sequences to trim. Additionally, illumina recommends to [trim the t-overhang](https://www.illumina.com/content/dam/illumina/gcs/assembled-assets/marketing-literature/illumina-stranded-rna-t-overhang-tech-note-470-2020-010/illumina-stranded-rna-t-overhang-tech-note-470-2020-010.pdf).

 In the tool search bar, type cutadapt and click on `Cutadapt: Remove adapter sequences from FASTQ/FASTA`

> **<i class="fas fa-wrench"></i> Cutadapt** with the following parameters:
> - Single-end or Paired-end reads?
>   - Paired-end (since we have two reads R1/R2 per sample)
> - FASTQ/A file #1:
>   - click the middle icon for multiple datsets
>   - select all R1 fastqc files
> - FASTQ/A file #2:
>   - click the middle icon for multiple datsets
>   - select all R2 fastqc files
> - In "Read 1 Options"
>   - 3' (End) Adapters, this is where you would input the adapter sequence for read 1
>     - <i class="fas fa-plus"></i> Insert 3' (End) Adapters
>       - In "Source"
>         - Select `enter custom sequence` from drop down
>         - "Enter custom 3' adapter name": name it whatever you'd like
>         - "Enter custom 3' adapter sequence": AGATCGGAAGAGCACACGTCTGAACTCCAGTCA
>   - cut bases from from reads before adapter trimming: 1
> - In "Read 2 Options"
>   - 3' (End) Adapters, this is where you would input the adapter sequence for read 1
>     - <i class="fas fa-plus"></i> Insert 3' (End) Adapters
>       - In "Source"
>         - Select `enter custom sequence` from drop down
>         - "Enter custom 3' adapter name": name it whatever you'd like
>         - "Enter custom 3' adapter sequence": AGATCGGAAGAGCGTCGTGTAGGGAAAGAGTGT
>   - cut bases from the second read in each pair: 1
> - In "Filter Options"
>   - Minimum length (R1): 20
> - In "Read Modification Options
>   - Quality cutoff: 20
> - In "Outputs selector"
>   - <i class="fa-solid fa-square-check"></i>  Report: Cutadapt's per-adapter statistics. You can use this file with MultiQC.
> - **<i class="fas fa-play"></i> Run Tool**

**Important!** There is a trick here. Since we are running multiple datasets and galaxy doesn't allow you to choose which R1 matches wihich R2, it defaults to the chosen order. If they are not in order, there will be a major issue. If they are not in order, run the tool on each pair by choosing one file at a time in FASTQ/A file #1 and FASTQ/A file #2 options. The downside to this is you have to repeat the process each time. This shouldn't be a problem but it is something to look out for!

It is always a good idea to rename the files!

> **Rename each file**
> - click the <i class="fas fa-pen"></i> icon to the left of the item name.
> - Edit Dataset Attributes will pop up in the middle
> - Edit the Name accordingly: DMSO_1_R1_tr
> - click <i class="fas fa-save"></i> Save

**Ensure the Trimmed Reads Improve Quality**

Now that we trimmed the reads, we can re-run FastQC and MultiQC to make sure the read quality improved. This gives us a little more confidence in the trimming process. 

1. Run FastQC as shown above for the trimmed reads
2. Run MultiQC to aggregate the FastQC reports from the trimmed reads as shown above

Check out [here](/files/posts/galaxy-tutorial/DMSO_1_R1_tr_FastQC.html) for the full FastQC report for the `DMSO_1_R1_trimmed` sample. 

Check out [here](/files/posts/galaxy-tutorial/MultiQC_TrimmedFastq_TCPMOH.html) for the full MultiQC report for each of the trimmed samples generated from cutadapt.

It is useful to compare the FastQC reports from the trimmed samples to the original. The biggest difference you should see is that in the trimmed report there is no adapter content visible!

# Aligning and Mapping the Reads

To make sense of the reads, we need to first figure out where the sequences originated from in the genome, so we can then determine to which genes they belong. When a reference genome for the organism is available, this process is known as aligning or “mapping” the reads to the reference. For the zebrafish, we have a couple of options. Lets use the latest genome assembly danRer11. These files can be found [here](https://hgdownload.soe.ucsc.edu/goldenPath/danRer11/bigZips/). 

In Galaxy, we can fetch the necessary data from the web using the `Upload Data` tool. 

> **<i class="fas fa-upload"></i> Upload Data**
> - Paste/Fetch Data
>   - In "Download data from the web by entering URLs (one per line) or directly paste content." copy and paste the following two lines. 
>     ```
>     https://hgdownload.soe.ucsc.edu/goldenPath/danRer11/bigZips/danRer11.fa.gz
>     https://hgdownload.soe.ucsc.edu/goldenPath/danRer11/bigZips/genes/danRer11.ncbiRefSeq.gtf.gz
>     ```
> **Start**

You should now then see the following two files in the History:

```
danRer11.fa.gz
danRer11.ncbiRefSeq.gtf.gz
```

`danRer11.fa.gz` is the full genome file and the `danRer11.ncbiRefSeq.gtf.gz` is the gene annotation file. 


## STAR

Search the tools for STAR and click `RNA STAR Gapped-read mapper for RNA-seq data`.

> **<i class="fas fa-wrench"></i> RNA STAR** with the following parameters:
> - In "Single-end or paired-end reads"
>   - Paired-end (as individual datasets)
>   - RNA-Seq FASTQ/FASTA file, forward reads
>     - multiple datasets -> select all R1 files
>   - RNA-Seq FASTQ/FASTA file, reverse reads
>     - multiple datasets -> select all R2 files
> - In "Custom or built-in reference genome"
>   - In the first drop down, select "select reference genome from history and create temporary index"
>   - Select a reference genome
>     - choose the .fa file you fetched: danRer11.fa.gz
>   - In "Build index with or without known splice junctions annotation":
>     - In the first drop down select build index with gene-model
>   - Gene model (gff3,gtf) file for splice junctions: 
>     - select .gtf file that was fetched: danRer11.ncbiRefSeq.gtf.gz
>   - Length of the genomic sequence around annotated junctions
>     - This is `read length - 1` and if you remember from FastQC we saq our read length was 101, so we would type 100 here. 
> - **<i class="fas fa-play"></i> Run Tool**

You should see three files per sample. This step will take the longest! In fact, STAR requires lots of memory. I have found at times when Galaxy is backed up, STAR can fail due to memory usage. This doesn't mean your samples are messed up, this just means there was an issue with the job. If your're trouble shooting, I recommend clicking the <i class="fas fa-info"></i> icon on the failed file and reading through the job statistics. You can also easily re-reun the job with the same parameters by pressing the <i class="fas fa-replay"></i> icon on the failed file. Just make sure the variables are as you expect them! Upon proper completion, the three file names for each sample should look something like:

```
RNA STAR ... : log
RNA STAR ... : mapped.bam
RNA STAR ... : splice junctions.bed
```

The .bam files are the files we will use to count the number of genes per annotation. The log file gives you statistics on the STAR run. This is particularly useful to look at the success of the run and time. 

It is always a good idea to rename the files!

> **Rename each file**
> - click the <i class="fas fa-pen"></i> icon to the left of the item name.
> - Edit Dataset Attributes will pop up in the middle
> - Edit the Name accordingly: e.g. `DMSO_1 RNA STAR: mapped.bam`
> - click <i class="fas fa-save"></i> Save

**Check STAR Results**

We can use the `MultiQC` tool to double check the stats from the alignment step!

> **MultiQC <i class="fas fa-wrench"></i><i class="fas fa-gear"></i>** with the following parameters:
> - In the Results box
>   - Which tool was used to generate logs?
>     - STAR
>   - STAR Ouput: Log
>     - select each log files that were outputted from STAR
> - **<i class="fas fa-play"></i> Run Tool**

Check out [here](/files/posts/galaxy-tutorial/MultiQC_STAR.html) for the full MultiQC report for each of the samples used in this study. Pay close attention to the % aligned. We would like this to be > 70%, which it is for each sample.  

# Counting the Reads per Annotated Gene

**Identifying the Strandedness**

To actually count the number of reads per annotated gene, we have to confirm the strandedness of our samples. To do this we will use Infer Experiment, which is a tool in the quality control RSeQC toolbox. 

In the tool search bar, search "convert GTF" and select `Convert GTF to BED 12`

> **<i class="fas fa-wrench"></i> Convert GTF to BED12** with the following parameters:
> - GTF File to convert: danRer11.ncbiRefSeq.gtf.gz
> - **<i class="fas fa-play"></i> Run Tool**

In the tool search bar, search "infer experiment" and select " Infer Experiment
speculates how RNA-seq were configured"

> **<i class="fas fa-wrench"></i> Infer Experiment** with the following parameters:
> - Input BAM file: select multiple datasets (middle icon)
>   - select every file that ends in mapped.bam (output from STAR)
> - Reference gene model: select the converted GTF file with name such as "Convert GTF to BED12 on data43: BED 12
> - **<i class="fas fa-play"></i> Run Tool**

For a reference on how to analyze the output, the Infer Experiment documentation has some useful information:

```
Example1

=========================================================
This is PairEnd Data ::

Fraction of reads explained by "1++,1--,2+-,2-+": 0.4992
Fraction of reads explained by "1+-,1-+,2++,2--": 0.5008
Fraction of reads explained by other combinations: 0.0000
=========================================================
Conclusion: We can infer that this is NOT a strand specific because 50% of reads can be explained by "1++,1--,2+-,2-+", while the other 50% can be explained by "1+-,1-+,2++,2--".

Example2

============================================================
This is PairEnd Data

Fraction of reads explained by "1++,1--,2+-,2-+": 0.9644 ::
Fraction of reads explained by "1+-,1-+,2++,2--": 0.0356
Fraction of reads explained by other combinations: 0.0000
============================================================
Conclusion: We can infer that this is a reverse strand-specific RNA-seq data. strandness of read1 is consistent with that of gene model, while strandness of read2 is opposite to the strand of reference gene model.
```

You can see that really what we want to know is if we have data that is forward stranded, reverse stranded, or unstranded. Investigating the output from **InferExperiment** on one sample on Galaxy we have:

```
This is PairEnd Data
Fraction of reads failed to determine: 0.0056
Fraction of reads explained by "1++,1--,2+-,2-+": 0.0071
Fraction of reads explained by "1+-,1-+,2++,2--": 0.9873
```

We can conclude our data is reverse stranded. We can also run **MultiQC** on the **InferExperiment** results to aggregate all the samples. This is especially useful when you have many samples. 

> **MultiQC <i class="fas fa-wrench"></i><i class="fas fa-gear"></i>** with the following parameters:
> - In the Results box
>   - Which tool was used to generate logs?
>     - RSeQC
>   - + Insert RSeQC Output
>     - Type of RSeQC output? Infer Experiment
>       - select each file outputted from Infer Experiment
> - **<i class="fas fa-play"></i> Run Tool**

Check out [here](/files/posts/galaxy-tutorial/MultiQC_InferExperiment.html) for the full `MultiQC` report for each of the samples used in this study. Pay close attention to the % aligned. Notice they all have >90% antisense, which means they are all reverse stranded as expected. 

## featureCounts

Now that we have confirmed the strandedness, we can actually count all the genes! For this, we will use the `featureCounts` tool. In the tool search bar, search for `featureCounts` and select `featureCounts
Measure gene expression in RNA-Seq experiments from SAM or BAM files`.

> **<i class="fas fa-wrench"></i> featureCounts** with the following parameters:
> - Alignment file: select multiple datasets (middle icon)
>   - select each of the mapped.bam files (output from STAR) for each sample
> - Specify strand information: Stranded (Reverse)
> - In "Gene annotation file":
>   - select "A GFF/GTF file in your history"
>   - Gene annotation file: danRer11.ncbiRefSeq.gtf.gz
> - In "Does the input have read pairs?"
>   - select "Yes, paired-end and count them as 1 single fragment" from the drop bar

**Check featureCounts Results**

To analyze the results of `featureCounts`, we will use `MultiQC`. 

> **MultiQC <i class="fas fa-wrench"></i><i class="fas fa-gear"></i>** with the following parameters:
> - In the Results box
>   - Which tool was used to generate logs?
>     - `featureCounts`
>   - + Insert `featureCounts` output
>     - select each of the summary report outputs from `featureCounts`
> - **<i class="fas fa-play"></i> Run Tool**

At this point, you have two options. You can run DESeq2 on Galaxy or on R. I like to run DESeq on R since I can generate plots and other items directly. To do this, download the `featureCounts` results and follow the [next tutorial](/posts/2023/05/deseq2-tutorial)!

# References 

1. Bérénice Batut, Mallory Freeberg, Mo Heydarian, Anika Erxleben, Pavankumar Videm, Clemens Blank, Maria Doyle, Nicola Soranzo, Peter van Heusden, Lucille Delisle, Reference-based RNA-Seq data analysis (Galaxy Training Materials). https://training.galaxyproject.org/training-material/topics/transcriptomics/tutorials/ref-based/tutorial.html Online; accessed TODAY
1. Batut et al., 2018 Community-Driven Data Analysis Training for Biology Cell Systems 10.1016/j.cels.2018.05.012