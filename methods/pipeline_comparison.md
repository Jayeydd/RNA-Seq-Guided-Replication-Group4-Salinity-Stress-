# RNA-Seq Analysis Pipeline

## Original Authors' Pipeline

The original study used the following RNA-seq analysis pipeline:

Raw RNA-seq reads
→ Trimmomatic
→ Trinity (de novo transcriptome assembly)
→ CD-HIT-EST
→ TransDecoder
→ Bowtie2 + RSEM
→ RSEM-FPKM (transcript-level quantification)
→ edgeR (TMM normalization)
→ Differentially expressed genes
→ BLAST annotation

The original authors used Trimmomatic for read processing and Trinity for de novo transcriptome assembly. CD-HIT-EST was used to reduce redundancy, followed by TransDecoder. Bowtie2 and RSEM were used for transcriptome alignment and expression quantification. RSEM produced transcript-level FPKM values, and edgeR with TMM normalization was used for differential expression analysis. The resulting sequences were annotated using BLAST and functional databases.

## Our Galaxy Re-analysis Pipeline

Our group used the following Galaxy workflow:

NCBI SRA
→ Raw paired-end RNA-seq reads
→ FastQC + MultiQC
→ Quality assessment
→ No trimming
→ Vicia villosa reference genome
→ HISAT2
→ BAM files
→ featureCounts
→ Gene-level count matrix
→ DESeq2
→ Differentially expressed genes
→ PCA, MA plot, dispersion plot, and p-value histogram

Four RNA-seq samples were analyzed: two control samples and two 24-hour salinity-stress samples.

FastQC and MultiQC showed less than 0.1% adapter contamination and no poor-quality reads. Therefore, trimming was not performed.

The group used the Vicia villosa Roth HV-30 reference genome, assembly Vvil1.0, accession GCF_029867415.1. Reads were aligned using HISAT2. The resulting BAM files were processed using featureCounts to obtain gene-level counts. Differential expression analysis was performed using DESeq2.

## Pipeline Comparison

| Analysis Step | Original Authors | Our Galaxy Re-analysis |
|---|---|---|
| Quality control | Phred Q20/Q30 | FastQC + MultiQC |
| Trimming | Trimmomatic | None |
| Reference strategy | De novo transcriptome | Reference genome |
| Assembly | Trinity | Not performed |
| Redundancy reduction | CD-HIT-EST | Not performed |
| Coding prediction | TransDecoder | Not performed |
| Alignment/quantification | Bowtie2 + RSEM | HISAT2 |
| Expression measurement | RSEM — FPKM, transcript-level | featureCounts — gene-level counts |
| Differential expression | edgeR with TMM normalization | DESeq2 |
| Annotation | BLAST and functional databases | NCBI GFF/GTF predicted LOC IDs |
| Significance criteria | |FC| ≥ 2 and raw p < 0.05 | padj < 0.05 and log2FC ≥ 1 |

## Overall Comparison

The original study used a de novo transcriptome approach, while our group used a reference genome from Vicia villosa.

The original authors used Bowtie2 + RSEM for transcript-level quantification and edgeR for differential expression. Our group used HISAT2 for genome alignment, featureCounts for gene-level counting, and DESeq2 for differential expression.

The original study also included more salinity-stress time points and biological replicates, while our re-analysis used only four samples: two controls and two 24-hour stress samples.

Because the reference, software, statistical methods, and sample selection differed, our analysis is a guided re-analysis rather than an exact replication of the original study.
