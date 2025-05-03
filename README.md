# Single-cell-Analysis
Single cell Analysis on Non-small cell lung cancer dissociated tumor cell from 7 donors

# 📊 NSCLC Single-cell RNA-seq Analysis using Seurat

This repository contains a comprehensive workflow for analyzing a **single-cell RNA sequencing (scRNA-seq)** dataset of **non-small cell lung cancer (NSCLC)** using the **Seurat** R package. The dataset originates from a 10X Genomics `.h5` file, and the pipeline covers standard preprocessing, quality control, normalization, clustering, and visualization techniques.

---

## 🧠 Project Goal

The goal of this project is to preprocess and explore scRNA-seq data to uncover transcriptional heterogeneity in NSCLC using an end-to-end Seurat pipeline.

---

## 📁 Dataset Description

* **Input File:** A 10X Genomics-formatted `.h5` file containing raw count data.
* **Modalities Present:** Gene expression, antibody capture, and multiplexing capture.
* **Data Type:** Sparse matrix (optimized for memory efficiency).

---

## 🔧 Pipeline Overview (Theoretical Steps)

### 🔹 Step 1: Setup & Data Loading

* Initialize the R environment by clearing previous objects and freeing memory.
* Set the working directory.
* Load required libraries (`tidyverse`, `Seurat`).
* Import the 10X `.h5` file.
* Select the gene expression matrix from multiple modalities in the dataset.

### 🔹 Step 2: Create Seurat Object

* Convert the gene expression matrix into a Seurat object using `CreateSeuratObject()`.
* Apply basic filtering: include only cells with ≥3 genes and genes expressed in ≥200 cells.

### 🔹 Step 3: Quality Control

* Compute **mitochondrial gene percentage** to flag low-quality or dying cells.
* Visualize cell metrics (`nCount_RNA`, `nFeature_RNA`, and `percent.mt`) using violin plots and scatter plots.
* Remove poor-quality cells:

  * Fewer than 200 genes.
  * More than 2500 genes.
  * > 5% mitochondrial content.

### 🔹 Step 4: Normalization

* Apply global-scaling normalization (default: **LogNormalize**).
* Normalize gene expression to 10,000 transcripts per cell, then log-transform.

### 🔹 Step 5: Identify Highly Variable Genes

* Select top 2,000 genes with the highest variance across cells.
* These genes are most informative for downstream clustering and dimensionality reduction.

### 🔹 Step 6: Data Scaling

* Standardize expression levels to remove technical or unwanted biological variation.
* Prepares the data for PCA and clustering by minimizing noise.

### 🔹 Step 7: Principal Component Analysis (PCA)

* Reduce dimensionality using PCA.
* Summarize expression across many genes into principal components (PCs).
* Visualize PCs and determine how many to keep using an **ElbowPlot**.

### 🔹 Step 8: Clustering

* Identify cell clusters using a **graph-based clustering** method (default: Louvain).
* Experiment with different resolution parameters to adjust the number of clusters.

### 🔹 Step 9: UMAP Visualization

* Apply **UMAP** (Uniform Manifold Approximation and Projection) for non-linear dimensionality reduction.
* Visualize clusters in 2D space for intuitive interpretation.

### 🔹 Step 10: Save Output

* Save the processed Seurat object to an `.RDS` file for future use.
* Avoids repeating the full analysis pipeline.

---

## 💾 Output Files

* `nsclc_seu.RDS` – Final Seurat object after preprocessing and clustering.
* Plots for QC, PCA, UMAP, and HVG visualization.

---

🧬 Summary of Biological Insights and Conclusion from UMAP Analysis
The UMAP visualization of NSCLC single-cell RNA-seq data highlights the cellular heterogeneity within the tumor microenvironment. Using Seurat, we identified distinct clusters that likely represent major cell types such as tumor epithelial cells, immune cells (T cells, B cells, NK cells), and stromal cells (fibroblasts, endothelial cells).

This clustering reveals the complex structure of the tumor and provides a foundation for further biological analyses including cell-type identification, immune profiling, and cell-cell communication studies.

Overall, the analysis demonstrates how single-cell RNA-seq can uncover detailed insights into tumor biology, which is essential for advancing personalized cancer research and immunotherapy strategies.

---

## 🧪 Requirements

* R (≥ 4.0)
* Seurat (≥ 4.0)
* tidyverse

---

## 🧰 How to Run

Update file paths and filenames as needed in your script, then run the pipeline sequentially in R or RStudio.

---

## 💡 Notes

* Consider using `SCTransform()` for advanced normalization and batch correction.
* Mitochondrial gene patterns may vary between species (`^MT-` for human, `^mt-` for mouse).
* Adjust QC thresholds depending on tissue type or sequencing platform.

---

## 🙋‍♀️ Questions?

Feel free to open an issue if you have questions or suggestions!

