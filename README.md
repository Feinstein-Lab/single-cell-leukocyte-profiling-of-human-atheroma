# single-cell-leukocyte-profiling-of-human-atheroma
We perform the analysis of single-cell RNA sequencing data from femoral and carotid samples. The code is written in R and uses the Seurat package.

<a rel="license" href="http://creativecommons.org/licenses/by-nc/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc/4.0/">Creative Commons Attribution-NonCommercial 4.0 International License</a>.

**Installation and Setup**
Before running the code, make sure to install the required R packages:
Seurat
tidyverse
ggpubr
devtools
harmony
You can install these packages using the install.packages() function in R.

**Data Upload and QC on Separate Samples**
The code begins by loading the necessary libraries and dependencies. Next, it uploads the scRNA-seq data for femoral samples and performs QC on each individual sample. The femoral samples are labeled as FEMPIC01, FEMPIC42, FEMPIC45, FEMPIC46, FEMPIC48, FEMPIC50, and FEMPIC53. The data for each sample is read using the Read10X() function from the Seurat package and then converted to a Seurat object using the CreateSeuratObject() function. The individual samples are combined using the merge() function.
Similarly, the code uploads the scRNA-seq data for carotid samples (CARPIC01, CARPIC49, and CARPIC51) and performs QC on each sample. The carotid samples are then combined using the merge() function.
The QC steps include calculating various metrics such as the number of UMI counts, the number of different genes with reads, and the percentage of mitochondrial reads. Histograms and violin plots are generated to visualize the distribution of these metrics. Unwanted cells are filtered out based on specified criteria.

**Combine Samples, Normalize, and Scale**
The code combines the full femoral and carotid datasets and proceeds to normalize and scale the data. The counts are log-transformed, variable features are identified using the FindVariableFeatures() function, and the data is scaled using the ScaleData() function. Mitochondrial and ribosomal genes are removed from the dataset.

**Visualize Carotid vs Femoral with PCA before Integration and Batch Correction**
The code performs principal component analysis (PCA) on the combined dataset and plots the PCA results using the DimPlot() function. Nearest neighbors are identified, and a graph is constructed. Clusters are then determined using the FindClusters() function, and a UMAP embedding is generated using the RunUMAP() function. The resulting clusters are labeled as either "carotid" or "femoral" based on their original identification. The UMAP is visualized with both the original sample groups and the carotid vs. femoral labels.

**Integrate with Harmony**
The code utilizes the Harmony algorithm to integrate the carotid and femoral datasets. The RunHarmony() function is used to perform the integration.

**Perform Clustering**
The code further performs clustering on the integrated dataset using the UMAP representation obtained from Harmony. Nearest neighbors are identified, and clusters are determined using the FindNeighbors() and FindClusters() functions. The resulting clusters are plotted using the DimPlot() function, both with and without splitting by the carotid and femoral labels.

**Cell Calling**
The code includes cell calling using known cell markers. Violin plots and feature plots are generated to visualize the expression of specific markers, such as CD14, CD68, KIT, CSF3R, CLEC4C, HLA-DRA, CD79A, IGHM, IGHG2, CD4, CD3D, CD8A, CD2, NKG7, MYH11, ACTA2, and CCR2.

**Automatic Labeling with Celltypist**
The code uses the Celltypist tool for automatic cell type labeling. The scRNA-seq data is converted to the anndata format, and predicted labels are obtained from Celltypist. The UMAP plot is generated with the predicted cell type labels.

**Generate Dotplot and Heatmap**
The code generates a dot plot and heatmap for the top 5 marker genes in each cluster. The Seurat::DotPlot() and DoHeatmap() functions are used for visualization.

**Generate Proportions and Log Odds Ratios**
The code compares the number of cells and the proportion of cells in each cluster between carotid and femoral samples. The results are presented in a table format. Additionally, odds ratios and Fisher's exact tests are calculated for each cluster.

**Differential Expression with Volcano Plots**
The code performs differential expression analysis between carotid and femoral samples using the FindMarkers() function. Volcano plots are generated to visualize the results.
Note: Please ensure that the necessary data files are present in the specified directories before running the code.
