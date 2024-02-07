## modkit_methcompare.py

This is the python script to make the split violin plot graphs comparing modkit methylation frequencies over specified intervals for R9, R10, and bisulfite sequencing data files for the HG002 cell line. These graphs were featured in ____________ paper. 

In general, this script can be used to compare interval-specific methylation frequences from three different modkit files with one of the files being used for binning. 

## Input data

Three different modkit files. The modkit package and output format is described here: https://github.com/nanoporetech/modkit. 
Commands used to generate the modkit files used in the paper: 

'''
#!/bin/bash

SAMPLE_NAME=$1
BAM_FILE=$2
OUT_PATH=$3

ml modkit 

modkit pileup --cpg --ref /data/CARDPB/resources/hg38/GCA_000001405.15_GRCh38_no_alt_analysis_set.fa --only-tabs --threads 24 --ignore h --combine-strands ${BAM_FILE} ${OUT_PATH}${SAMPLE_NAME}.hg38.modkit.comb.bed

#sbatch --mem=10G --cpus-per-task=25 --time=24:00:00 modkit_hg38_comb.sh SAMPLE_NAME BAM_FILE OUT_PATH


'''


