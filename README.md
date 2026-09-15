# RNA-Seq Guided Replication Using Galaxy and GitHub
Assignment: RNA-Seq Guided Replication Using Galaxy and GitHub — Group 4 (Salinity Stress)

**Group Number:** Group 4

**Assigned Topic:** Salinity Stress

## Group Members and Assigned Roles
| Member | Role |
|---|---|
| Batigulao, Jehiah Bless | Literature Lead |
| Obiñeta, Inah Marie A. | Galaxy Lead |
| Oficiar, Francis Kyle | Interpretation Lead |
| Pasculado, Mark Ryan | Data Lead |
| Suan, Jade Angela | Documentation Lead |

## Citation of the Selected Paper
> Afzal, M., Alghamdi, S. S., Khan, M. A., Al-Faifi, S. A., & Rahman, M. H. (2023). *Transcriptomic analysis reveals candidate genes associated with salinity stress tolerance during the early vegetative stage in faba bean genotype, Hassawi-2.* **Scientific Reports, 13**, 21223.
>
> **Article Link:** https://pmc.ncbi.nlm.nih.gov/articles/PMC10692206/

## Research Question of the Original Study
The original study aimed to identify genes and biological pathways associated with salinity stress tolerance in faba bean (*Vicia faba* L.) genotype Hassawi-2, by analyzing transcriptome changes across different time points after salt exposure.

## Organism and Tissue Used
- **Organism:** Faba bean (*Vicia faba* L.), genotype Hassawi-2
- **Tissue:** Leaf tissue, early vegetative (3-leaf) stage

  ## Control and Treatment Conditions
- **Control:** Plants grown without salt treatment
- **Treatment:** 200 mM NaCl salinity stress; samples collected at 6, 12, 24, 48, and 72 hours

## RNA-Seq Accession Numbers
- **BioProject:** PRJNA943415
- **SRA Link:** https://www.ncbi.nlm.nih.gov/sra/?term=PRJNA943415
- **Samples Used:**
  - Control Replicate 1 — SRR23869388
  - Control Replicate 2 — SRR23869382
  - Stress 24h Replicate 1 — SRR23869383
  - Stress 24h Replicate 2 — SRR23869381

## Reference Genome and Annotation Versions
- **Species used in our analysis:** Hairy vetch (*Vicia villosa* Roth), genotype HV-30
- **Assembly:** Vvil1.0 — Accession: GCF_029867415.1
- **Source:** NCBI Genome — https://www.ncbi.nlm.nih.gov/datasets/genome/GCF_029867415.1/
- **Genome file:** GCF_029867415.1_Vvil1.0_genomic.fna.gz
- **Annotation file:** GCF_029867415.1_Vvil1.0_genomic.gtf.gz
> **Note:** Original authors used de novo transcriptome assembly from Vicia faba. We substituted with Vicia villosa because the Vicia faba genome (~11.9 Gb) repeatedly caused memory errors in Galaxy and could not be indexed. Vicia villosa is a related but different species, which explains the low mapping percentages shown above.

# Original Authors' Analysis Pipeline
Quality control (Q20/Q30 filter) → Trimmomatic (trimming) → Trinity (de novo assembly)
→ CD-HIT-EST → TransDecoder → Bowtie2 + RSEM (alignment & quantification)
→ edgeR (differential expression, TMM normalization)
→ BLAST annotation (NR, Swiss-Prot, GO, KEGG, COG/KOG, Pfam)
→ Threshold: |FC| ≥ 2, raw p < 0.05

## Galaxy Pipeline Used by the Group
Download FASTQ reads from SRA → FastQC + MultiQC (quality control)
→ No trimming needed (passed all QC) → HISAT2 (genome alignment)
→ featureCounts (gene-level counting) → DESeq2 (differential expression)
→ Threshold: adjusted p-value < 0.05, log2FC ≥ 1

**Galaxy Workflow:** https://usegalaxy.org/u/inah.obineta2/h/group4-salinity-stress-rnaseq-assignment3-2
## Differences Between the Authors' Pipeline and the Group's Pipeline.
| Step | Original Authors | Our Galaxy Re-analysis |
|---|---|---|
| Reference | De novo transcriptome assembly | *Vicia villosa* genome (GCF_029867415.1) |
| Trimming | Trimmomatic | None — QC was clean |
| Aligner | Bowtie2 (transcriptome) | HISAT2 (genome) |
| Quantification | RSEM — FPKM (transcript-level) | featureCounts — gene-level counts |
| DE Tool | edgeR | DESeq2 |
| Significance | |FC| ≥ 2, raw p < 0.05 | adjusted p < 0.05, log2FC ≥ 1 |
| Samples | 5 time points × 3 replicates | 2 conditions × 2 replicates |
## Main Quality-Control Results
- **Read count:** ~27.9–31.6 million reads per sample
- **Read length:** 101 bp, paired-end
- **GC content:** 43–46% across samples
- **Adapter contamination:** < 0.1% — all samples passed
- **Quality scores:** All samples passed Q20/Q30 thresholds
- **Duplication:** 73.8–79.3% (typical for RNA-seq)
- **Conclusion:** Data was clean — **no trimming performed**
## Mapping Results (HISAT2)
| Sample | Total Reads | % Mapped | % Uniquely Mapped |
|---|---|---|---|
| Control Rep 1 | 28,209,473 | 47.89% | 21.45% |
| Control Rep 2 | 27,949,472 | 43.71% | 20.33% |
| Stress 24h Rep 1 | 31,558,920 | 49.08% | 19.64% |
| Stress 24h Rep 2 | 31,491,668 | 42.25% | 17.81% |

> **Note:** Mapping rates are low because we used a different species genome (*Vicia villosa*) instead of the actual faba bean transcriptome.
## Differential Expression Results
- **Total genes tested:** 21,159
- **Significantly DE genes (padj < 0.05):** 304
- **Upregulated genes:** 139
- **Downregulated genes:** 165
- **PCA plot:** PC1 = 69%, PC2 = 21%; samples grouped clearly by condition
- **Replicates:** Clustered together — showing good reproducibility
## Three To Five Genes Selected For Interpretation.
| Gene ID | log2FC | Adjusted p-value | Regulation | Predicted Function | Role in Salinity Response |
|---|---|---|---|---|---|
| LOC131616617 | +9.39 | 4.69E-05 | UP | Ion transporter / Na+ efflux pump | Removes excess salt; maintains ion balance |
| LOC131603188 | +9.14 | 6.59E-13 | UP | Osmoprotectant synthase | Produces protective molecules; prevents water loss |
| LOC131643483 | +8.66 | 0.250 | UP | Antioxidant / ROS-scavenging enzyme | Reduces oxidative damage from salt stress |
| LOC131661771 | -23.55 | 4.19E-15 | DOWN | Growth / cell division-related | Growth slowed; energy redirected to defense |
| LOC131620268 | -8.56 | 7.28E-14 | DOWN | Basic metabolic enzyme | Core metabolism reprogrammed for stress response |
## Comparison with Published Results
- **Biological response:** We recovered the same general pattern — salt stress induces ion transport, osmoprotection, and antioxidant pathways, while growth and metabolism genes decrease.
- **Gene overlap:** Exact gene IDs could not be matched because the authors used de novo transcripts and we used a different species genome — but functional pathways match.
- **Similarities:** Stress vs control separation; upregulation of protective functions; downregulation of growth-related genes.
- **Differences:** Lower mapping rates; fewer samples; different tools and statistical thresholds; different reference genome.
- **Conclusion:** Biological patterns were reproducible even with different tools and reference.
## Limitations
- **Reference genome mismatch:** Using *Vicia villosa* instead of *Vicia faba* reduced mapping accuracy and prevented direct gene ID comparison.
- **Small sample size:** Only 2 replicates per condition instead of 3.
- **Different tools:** HISAT2/featureCounts/DESeq2 differs from Bowtie2/RSEM/edgeR → results differ quantitatively.
- **No trimming:** Authors used Trimmomatic; we did not — may affect read counts.
- **Annotation quality:** Only predicted LOC IDs available; limited functional information.
## Group Conclusion
We successfully reproduced the **biological findings** of the original study — salinity stress induces genes for salt exclusion, osmoprotection, and damage repair while suppressing growth — even though our technical pipeline and reference genome were different. This shows that **RNA-seq results are biologically reproducible**, but exact numbers and gene lists depend on the tools, reference genome, and thresholds chosen. This exercise taught us that choosing the right reference genome and analysis parameters is critical for accuracy, and that biological patterns are more robust than exact quantitative results.
