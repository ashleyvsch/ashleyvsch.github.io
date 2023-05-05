---
title: 'Markdown Tricks'
date: 2023-05-05
permalink: /resources/markdown-tricks/
toc: true
tags:
  - references
  - bash
---

These are things

## here is a header

``` bash
#!/bin/bash

#PBS -k o
#PBS -q batch
#PBS -V 
#PBS -l nodes=1:ppn=16 # note here I am allocating 16 cores in the node
#PBS -N align
#PBS -j oe

# important dirs
IDX_DIR="/home/avschwartz/rnaseq/genomes/danRerIndex"
PROJ_DIR="/home/avschwartz/rnaseq/projects/tcpmoh"
DATA_DIR=${PROJ_DIR}"/data"
RES_DIR=${PROJ_DIR}"/results/STAR"

# I need to make sure my bioinfo environment is activated to grab STAR
source /home/avschwartz/anaconda3/bin/activate
conda activate bioinfo

echo -e "\nAligning..."
start=`date +%s`

STAR --genomeDir ${IDX_DIR} \
--runThreadN 16 \
--readFilesCommand zcat \
--readFilesIn $1_1.fastq.gz $1_2.fastq.gz \
--outFileNamePrefix ${RES_DIR}/$1 \
--outSAMtype BAM SortedByCoordinate \
--outSAMunmapped Within \
--outSAMattributes Standard \

echo -e "STAR Alignment Complete!\n"

end=`date +%s`
runtime=$((end-start))
echo -e "Execution time was ${runtime} seconds.\n"
```