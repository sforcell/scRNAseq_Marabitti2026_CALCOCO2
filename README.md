# Single-Cell RNA-seq Preprocessing and Data Integration

This repository contains two Jupyter notebooks for the preprocessing, quality control, normalization, and downstream analysis of single-cell RNA-seq (scRNA-seq) data from medulloblastoma samples.

The workflow is designed for **droplet-based single-cell RNA-seq data** and is implemented in Python using `Scanpy`, `AnnData`, and additional bioinformatics and statistical packages.

The analysis is based on scRNA-seq data from medulloblastoma, encompassing the four molecular subgroups: **WNT, SHH, Group 3 (GP3), and Group 4 (GP4)**.

The dataset used for the preprocessing workflow was obtained from the following study:

Riemondy KA, Venkataraman S, Willard N, Nellan A, Sanford B, Griesinger AM, Amani V, Mitra S, Hankinson TC, Handler MH, Sill M, Ocasio J, Weir SJ, Malawsky DS, Gershon TR, Garancher A, Wechsler-Reya RJ, Hesselberth JR, Foreman NK, Donson AM, Vibhakar R. *Neoplastic and immune single-cell transcriptomics define subgroup-specific intra-tumoral heterogeneity of childhood medulloblastoma.* Neuro Oncol. 2022 Feb 1;24(2):273–286. doi:10.1093/neuonc/noab135. PMID: 34077540; PMCID: PMC8804892.


---

## Workflow overview

The analysis is divided into two main steps:

### 1. Preprocessing and Quality Control

`01_preprocessing.ipynb` prepares the raw count matrix for downstream single-cell analysis.

The main steps are:

1. Read the raw count matrix
2. Create an `AnnData` object
3. Add sample and molecular subgroup metadata
4. Split the dataset by sample
5. Annotate genes using Ensembl/BioMart
6. Identify mitochondrial genes
7. Perform quality-control analysis
8. Detect and remove outlier cells
9. Remove genes/cells with no counts
10. Detect and remove doublets using Scrublet
11. Normalize the expression data
12. Merge the processed samples
13. Save the processed dataset as an H5AD file

The notebook uses the `AnnData` structure to keep raw counts and normalized expression values in separate layers.

---

### 2. Data Integration and Downstream Analysis

`02_data_integration.ipynb` starts from the preprocessed H5AD object and performs exploratory analysis and downstream processing.

The main steps include:

* normalization and log-transformation;
* identification of highly variable genes (HVGs);
* PCA;
* neighborhood graph construction;
* UMAP visualization;
* Leiden clustering;
* identification and removal of selected normal-cell clusters;
* exclusion of the `GP3/4` subgroup;
* pseudobulk generation;
* pseudobulk quality assessment and PCA;
* metadata association analysis;
* gene filtering for downstream differential expression analysis;
* differential expression analysis between GP3 and SHH;
* visualization of differential expression using volcano plots;
* focused analysis of **CALCOCO2** and **OTX2**;
* correlation analysis between CALCOCO2 and OTX2;
* preliminary CNV visualization/inference around CALCOCO2 on chromosome 17.

The notebook explicitly compares **GP3**, described in the analysis as the more aggressive subgroup, with **SHH**, described as the less aggressive subgroup.
