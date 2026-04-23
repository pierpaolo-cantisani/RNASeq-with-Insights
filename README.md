# RNA-Seq analysis case study
## Overview
The repository contains a case study of a full RNA-Seq pipeline, from raw reads to biological interpretation.  

This project is meant as a case study to showcase both my organizational skills and my approach to interpreting results and obtaining biological insights. The project is structured as a “presentation” of the workflow, with the main analyses and comments provided in the Jupyter notebook "RNA_seq_case_study.ipynb".

## Dataset
This is a bulk RNA-sequencing dataset of in-vitro Th2 cells, subjected to L-phenylalanine treatment to assess its effect on gene expression. Cells were obtained from 5 donors, and incubated for 24h with either Phenylalanine or Vehicle (Ctrl) with simultaneous activation with anti-CD2, anti-CD3 and anti-CD28 antibody beads.  
The experimental design therefore consists of:
- 10 samples (S1-S10).
- From 5 different donors (D1-D5).
- On 2 conditions: L-Phenylalanine treatment and Veh treatment (Ctrl).
- Paired setup (Phe vs Ctrl on the same donor): design = ~ donor + condition.  

Original dataset from GEO: GSE291310.  
Sequencing platform: Illumina NovaSeq X Plus.

## Pipeline diagram
The RNA-Seq pipeline was performed as follows:
```mermaid
flowchart TD
    subgraph A["Module A - Mapping (Bash)"]
        A1[Conda environment set-up] --> A2[Raw FASTQ files download]
        A2 --> A3[Quality Control<br/>FastQC + MultiQC]
        A3 --> A4[Trimming<br/>Fastp]
        A4 --> A5[Quality Control 2<br/>FastQC + MultiQC]
        A5 --> A6[Pseudo-mapping<br/>Kallisto]
    end

    subgraph B["Module B - DE (R)"]
        B1[Import counts<br/>Tximport] --> B2[Exploratory analysis<br/>PCA-t-SNE-heatmap]
        B2 --> B3[Differential Expression<br/>DESeq2]
        B3 --> B4[Data visualization and discussion<br/>Volcano plot-DE heatmap]
      
    end

    subgraph C["Module C - FE (R)"]
        C1[Literature and database research]
        C2[ORA<br/>ClusterProfiler]
        C3[GSEA<br/>ClusterProfiler]
        C4[Comparison and biological insight]
    end

    subgraph D["Conclusions"]
        D1[Final overview]
        D2[Open issues and possible solutions]
    end

    A --> B
    B --> C
    C --> D
    C1 --> C4
    C2 --> C4
    C3 --> C4
```

## Conclusions and findings
L-phenylalanine was found to have a moderate influence on key biological processes of Th2 cells, such as differentiation, cell cycle regulation and renal metabolism. To a lesser extent, also cell motility, tissue morphogenesis, and hormone biosynthesis and signalling appear to be affected.

## Jupyter Notebook
The project is formatted in a single Jupyter notebook for organization and clarity. As previously stated, the notebook contains two sections using different languages: bash (for bioinformatics tools) and R (for statistical analysis).  
To reproduce the analysis:
- Bash cells: run with the Python kernel using the %%bash magic command at the top of each cell. The conda environment "bioinf" must be activated beforehand.
- R cells: run by switching to the IRkernel. All required R packages are listed in the R Package Versions section below.

## Tools & Versions
| Tool | Version | Environment |
|------|---------|-------------|
| sra-tools | 3.2.1 | Bash |
| fastqc | 0.12.1 | Bash |
| multiqc | 1.33 | Bash |
| fastp | 1.1.0 | Bash |
| Kallisto | 0.51.1 | Bash |
| rtracklayer | 1.68.0 | R |
| dplyr | 1.2.0 | R |
| tximport | 1.36.1 | R |
| factoextra | 1.0.7 | R |
| Rtsne | 0.17 | R |
| pheatmap | 1.0.13 | R |
| DESeq2 | 1.48.2 | R |
| ggplot2 | 4.0.2 | R |
| org.Hs.eg.db | 3.21.0 | R |
| clusterProfiler | 4.16.0 | R |
| enrichplot | 1.28.4 | R |
| AnnotationDbi | 1.70.0 | R |
| ggridges | 0.5.7 | R |
