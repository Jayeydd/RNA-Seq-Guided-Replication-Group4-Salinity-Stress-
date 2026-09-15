# Galaxy Workflow History

**History Name:**   GROUP4_Salinity_Stress_RNASeq_Assignment3
**Author:**         inah.obineta2
**Link:**           https://usegalaxy.org/u/inah.obineta2/h/group4-salinity-stress-rnaseq-assignment3-2

# Complete Pipeline Steps

Step 1: Import FASTQ reads from SRA (4 samples)
         - Control_R1_rep1, Control_R2_rep1
         - Control_R1_rep2, Control_R2_rep2
         - Stress24hrs_R1_rep1, Stress24hrs_R2_rep1
         - Stress24hrs_R1_rep2, Stress24hrs_R2_rep2

Step 2: FastQC — Quality check on all 4 samples
         - Raw data reports + HTML webpage reports

Step 3:  MultiQC — Combine all FastQC results into one summary report
         - AllSamples_Combined: Stats + Webpage

Step 4:  Reference genome upload
         - GCF_029867415.1_Vvil1.0_genomic.fna.gz
         - GCF_029867415.1_Vvil1.0_genomic.gtf.gz

Step 5:  HISAT2 — Read alignment to Vicia villosa genome
         - Control_rep1 → BAM file
         - Control_rep2 → BAM file
         - Stress24h_rep1 → BAM file
         - Stress24h_rep2 → BAM file

Step 6:  featureCounts — Count reads per gene
         - Counts table + Summary table for each sample

Step 7:  Combine counts → RNAseq_gene_counts.csv

Step 8:  DESeq2 — Differential Expression Analysis
         - Results: Control vs Stress24h
         - Results sorted by log2FC
         - Plots: PCA, MA, Dispersion, etc.
