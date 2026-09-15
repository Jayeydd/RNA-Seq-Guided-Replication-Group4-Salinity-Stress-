# Galaxy Workflow History

* History Name:   GROUP4_Salinity_Stress_RNASeq_Assignment3
* Author:         inah.obineta2
* Link:           https://usegalaxy.org/u/inah.obineta2/h/group4-salinity-stress-rnaseq-assignment3-2

# Complete Pipeline Steps

* Step 1:  Import FASTQ reads from SRA database
    * Samples: Control_rep1, Control_rep2, Stress24h_rep1, Stress24h_rep2
* Step 2:  FastQC — Quality check on all 4 samples
    * Output: Raw data reports + HTML webpage reports
* Step 3:  MultiQC — Combine all FastQC results
    * Output: AllSamples_Combined statistics + summary webpage
* Step 4:  Upload reference genome & annotation
    * Genome: GCF_029867415.1_Vvil1.0_genomic.fna.gz
    * Annotation: GCF_029867415.1_Vvil1.0_genomic.gtf.gz
* Step 5:  HISAT2 — Genome alignment
    * Control_rep1 → BAM file
    * Control_rep2 → BAM file
    * Stress24h_rep1 → BAM file
    * Stress24h_rep2 → BAM file
* Step 6:  featureCounts — Gene-level read quantification
    * Output: Counts table + Summary table per sample
* Step 7:  Merge counts → RNAseq_gene_counts.csv
* Step 8:  DESeq2 — Differential expression analysis
    * Results: Control vs Stress24h
    * Output: Results table sorted by log2FC, PCA plot, MA plot, dispersion plot
