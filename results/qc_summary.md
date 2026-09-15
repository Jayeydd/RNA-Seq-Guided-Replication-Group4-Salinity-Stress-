### Overall QC Interpretation

| Output | Result |
|---|---|
| General sequence quality | The samples contained approximately 27.9–31.6 million reads per file, with a consistent read length of 101 bp. Read counts were relatively similar across samples, indicating no major imbalance in sequencing depth. GC content was also relatively consistent, ranging from 43–46%. |
| Adapter contamination | FastQC/MultiQC Adapter Content analysis showed all 8 samples passed, with less than 0.1% adapter contamination detected across all samples. No adapter trimming was necessary. |
| Overrepresented sequences | The presence and identity of overrepresented sequences should be evaluated using the FastQC Overrepresented Sequences module. In RNA-seq data, some overrepresented sequences may result from highly abundant transcripts, but their identity should be checked before determining whether they represent contamination. |
| Any obvious quality problem | The main observation is high sequence duplication (73.8–79.3%), typical of RNA-seq due to highly expressed transcripts. GC content and read length were consistent across samples. Adapter content was examined via MultiQC and confirmed clean (<0.1% contamination, 8/8 samples passed), supporting the decision not to trim. |
