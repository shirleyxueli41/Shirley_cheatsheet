# Essential NGS Tools

## 1. Quality Control

- **FastQC** — read-level QC  
- **MultiQC** — aggregate QC reports  
- **fastp** — trimming + filtering  
- **Trimmomatic** — read trimming  
- **Cutadapt** — adapter trimming  

## 2. Read Alignment / Mapping

### DNA / Whole Genome / Exome

- **BWA / BWA-MEM**  
- **Bowtie2**  
- **minimap2**

### RNA-seq

- **STAR**  
- **HISAT2**  
- **TopHat2** *(legacy)*

### Long-read (ONT / PacBio)

- **minimap2**  
- **NGMLR**  
- **GraphMap**

## 3. File Handling, Sorting, Indexing, Dedup

- **samtools** — view/sort/index  
- **picard** — MarkDuplicates  
- **htslib**  
- **GATK** (utilities)

## 4. Variant Calling (SNPs & Indels)

- **GATK HaplotypeCaller**  
- **GATK Mutect2**  
- **bcftools mpileup/call**  
- **FreeBayes**  
- **DeepVariant**  
- **Strelka2**

## 5. Variant Filtering / Joint Calling / Genotyping

- **GATK GenotypeGVCFs**  
- **GATK VQSR**  
- **bcftools filter / merge**  
- **PLINK / PLINK2**

## 6. Variant Annotation

- **VEP (Variant Effect Predictor)**  
- **ANNOVAR**  
- **SnpEff**  
- **SnpSift**

## 7. RNA-seq Quantification

- **Salmon**  
- **Kallisto**  
- **RSEM**  
- **featureCounts**  
- **HTSeq-count**

## 8. Differential Expression & Downstream RNA-seq

- **DESeq2**  
- **edgeR**  
- **limma-voom**  
- **Sleuth**

## 9. Gene Set / Pathway / Enrichment Tools

- **GSEA**  
- **fgsea**  
- **clusterProfiler**  
- **DAVID**  
- **Enrichr**

## 10. Single-Cell RNA-seq / Multiome

- **CellRanger**  
- **Seurat**  
- **Scanpy**  
- **STARsolo**  
- **Alevin-fry**  
- **Velocyto**  
- **scVelo**

## 11. ATAC-seq / ChIP-seq / Epigenomics

- **MACS2**  
- **BEDTools**  
- **HOMER**  
- **deepTools**  
- **chromVAR**

## 12. Structural Variants & Copy Number

- **CNVkit**  
- **GATK gCNV**  
- **Manta**  
- **Delly**  
- **LUMPY**  
- **BreakDancer**

## 13. Metagenomics

- **Kraken2**  
- **Bracken**  
- **MetaPhlAn**  
- **QIIME2**  
- **HUMAnN**  
- **Centrifuge**

## 14. Long-read Assembly & Polishing

- **Flye**  
- **Canu**  
- **Shasta**  
- **Pilon**  
- **Medaka**

## 15. General Genomics Toolkits

- **BEDTools**  
- **bcftools**  
- **PLINK / PLINK2**  
- **UCSC tools**  
- **seqtk**

## 16. Workflow Management / Pipelines

- **Nextflow**  
- **Snakemake**  
- **Cromwell / WDL**  
- **nf-core pipelines**  
- **Docker / Singularity**

