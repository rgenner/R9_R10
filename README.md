## modkit_methcompare.py

This is the python script to make the split violin plot graphs comparing modkit methylation frequencies over specified intervals for R9, R10, and bisulfite sequencing data files for the HG002 cell line. These graphs were featured in ____________ paper. 

In general, this script can be used to compare interval-specific methylation frequences from three different modkit files with one of the files being used for binning. 

## Input data

The script requires three different bed or bed-like files with columns for genomic position (chromosome and start/end position), probability of the target base being modified, and coverage level of the base called.  

The violin plot in the paper was made from bedMethyl files generated by the modkit, a package for analysing ONT modified bases.  

More info about the modkit package and bedMethyl output file can be found at https://github.com/nanoporetech/modkit.  

The command used to generate the modkit files used in the paper are shown below:  

```
#!/bin/bash

SAMPLE_NAME=$1
REF=$2
BAM_FILE=$2
OUT_PATH=$3

ml modkit 

modkit pileup --cpg --ref ${REF} --only-tabs --threads 24 --ignore h --combine-strands ${BAM_FILE} ${OUT_PATH}${SAMPLE_NAME}.hg38.modkit.comb.bed

#sbatch --mem=10G --cpus-per-task=25 --time=24:00:00 modkit_hg38_comb.sh SAMPLE_NAME REF BAM_FILE OUT_PATH
```

## Parameters

```
--sample_name : sample name (string value)

--r9_modkit : path to R9 bedfile

--r10_modkit : path to R10 bedfile 

--bis_modkit : path to bisulfite bedfile 

--cov_min : minimum coverage threshold, default = 20 (int value)

--cov_max : maximum coverage threshold, default = 200 (int value)

--interval : number of evenly spaced intervals for binning data, default = 10 (ex. 0, 10, 20, 30, ... 100) (int value)

--custom_interval : a list of custom unevenly spaced interval values for binning data (ex. [0, 5, 10, 50, 90, 95, 100])

--binning : dataset to bin the graph by , either 'r9', 'r10', or 'Bisulfite' (string value)

--bw : number from 0.0 - 1.0 (float value) that scales the violin plot bandwidth for more or less smoothing, default = 0.1 (float value)

--scale : method to normalizes each density to determine the violin's width: 'width' = default; all violins have the same, 'area' = all violins have the same area,  = violin widths are proportional to number of observations (string value)

--out__dir : output directory path

```

## Sample command 

```
python modkit_methcompare.py \
--cov_min 20 \
--cov_max 200 \
--r9_modkit /Users/gennerrm/Desktop/modkit_files/HG002_R9.hg38.modkit.comb.bed \
--r10_modkit /Users/gennerrm/Desktop/modkit_files/HG002_R10.hg38.modkit.comb.bed \
--bis_modkit /Users/gennerrm/Desktop/modkit_files/CpG.gz.bismark.zero.merged.cov \
--interval 10 \
--sample_name HG002_bis \
--binning Bisulfite  \
--out_dir /Users/gennerrm/Desktop/figs/py_figs/test

```

![HG002_bis_VP](https://github.com/rgenner/R9_R10/assets/87498696/e1453298-0103-4c9e-b09c-4184705bdf2c)

![HG002_bis_VP_cov](https://github.com/rgenner/R9_R10/assets/87498696/97614943-bbaa-4010-9e57-ac72244dfd64)

![HG002_bis_lines](https://github.com/rgenner/R9_R10/assets/87498696/f64c016c-6ab9-4a33-9735-bcaea68a842d)



