# Single-Cell Gene Expression Analysis - Project

<p align="center">9 December 2025</p>

## Overview
The **lab exam project** for the course *"Artificial Intelligence – Module 1"* in the **[LM] Data Science, Data Analytics and Artificial Intelligence in Health Sciences** master's degree program, held by **Professor Francesca Buffa**, **Professor Federico Borra**, and **Professor Carlo Lucibello**.

The main objective of the project is to develop a **machine/deep learning pipeline capable of classifying cell types** based on single-cell gene expression profiles from **Single-Cell RNA Sequencing (scRNA-seq)** data, where observations represent individual cells and variables represent quantified, normalized (log1p transformed) gene expression levels.

---

## Objectives
- Develop a classification pipeline for cell-type prediction from scRNA-seq data
- Explore and analyze a high-dimensional gene expression dataset (1,499 cells × 4,290 genes)
- Investigate potential confounders (sequencing depth, mitochondrial content, cell cycle phase)
- Apply unsupervised and supervised learning techniques
- Engineer biologically meaningful features (Signature Scores) to address scRNA-seq sparsity
- Predict **cell types** along the hematopoietic differentiation hierarchy

---

## Dataset
The dataset is in `.h5ad` format (AnnData) and originates from **Mus musculus (Mouse)** hematopoietic cells.

| Property | Value |
|---|---|
| **Cells** | 1,499 (1,074 training) |
| **Genes** | 4,290 |
| **Normalization** | log1p transformed |
| **Target labels** | 10 cell types + 1 "other" |

---

## Methodology

### Data Exploration & Preprocessing
- Imported and merged the `.h5ad` expression matrix with training labels
- Verified data integrity (no null values) and explored metadata
- Analyzed possible confounders and confirmed cell cycle as a biological signal

### Unsupervised Learning
- PCA / SVD
- UMAP
- Leiden Clustering
- Self-Organizing Maps (SOM)

### Supervised Learning
- Random Forest
- SVM
- XGBoost
- MLP

### Feature Engineering & Optimization
- Wilcoxon-based marker gene selection
- Biological Signature Scores
- Cellular Filtering
- Soft-Voting Ensemble

---

## Results

| Configuration | Test Score |
|---|---:|
| Base Ensemble | 0.5385 |
| + Biological Signature Scoring | 0.5467 |
| + Cellular Filtering | **0.549** |

---

## Conclusion
The final model — a **Weighted Voting Ensemble augmented by Cellular Filtering and Biological Signature Scoring** — achieved a **test accuracy of 0.549**. Signature scores effectively addressed scRNA-seq data sparsity by aggregating signals from co-expressed genes, stabilizing inputs against technical dropout. The performance plateau is attributed to irreducible constraints: transcriptional lag between surface-protein labels and mRNA profiles, inherent label noise from discretizing a continuous biological process, and uncorrected batch effects causing a gap between internal CV (~0.65) and external test scores.


