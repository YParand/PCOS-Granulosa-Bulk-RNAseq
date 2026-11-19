# PCOS-Granulosa-Bulk-RNAseq
Markdown
# Bulk RNA-seq Transcriptomic Analysis of Granulosa Cells in PCOS (GSE138518)

A reproducible, parameterized R Markdown bioinformatics pipeline for investigating transcriptomic alterations in human ovarian granulosa cells from patients with Polycystic Ovary Syndrome (PCOS) compared to healthy controls.

---

## 📌 Project Overview

Polycystic Ovary Syndrome (PCOS) is a complex endocrine and metabolic disorder associated with chronic low-grade inflammation and impaired folliculogenesis. This pipeline analyzes publicly available bulk RNA-seq count data (**GEO Accession: [GSE138518](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE138518)**) to identify differentially expressed genes, enriched biological pathways, and candidate hub genes for downstream protein-protein interaction (PPI) network modeling.

### Key Analytical Steps
1. **Data Preprocessing & Filtering:** Raw count matrix formatting, sample group assignment (`Control` vs. `PCOS`), and low-count gene filtering.
2. **Differential Expression Analysis (`DESeq2`):** Negative binomial generalized linear modeling to identify significantly upregulated and downregulated genes (`padj < 0.1`, `|log2FoldChange| > 1`).
3. **Publication-Grade Visualizations:**
   - **Volcano Plot:** Highlighting top significantly altered genes (`ggplot2` & `ggrepel`).
   - **Hierarchical Clustering Heatmap:** Z-score scaled variance-stabilized expression (VST) of the top 50 DEGs (`pheatmap`).
4. **Functional Enrichment Analysis (`clusterProfiler`):**
   - Over-Representation Analysis (ORA) for **Gene Ontology (Biological Processes)** and **KEGG Pathways**.
   - **Gene-Concept Network (`cnetplot`)** linking top enriched GO terms to fold-change dynamics.
5. **Gene Set Enrichment Analysis (`GSEA`):** Whole-transcriptome ranked enrichment analysis visualized via **Ridgeplots** (`enrichplot`), revealing coordinated immune and inflammatory pathway activation.
6. **PPI Network Preparation:** Exporting filtered significant DEGs formatted for direct import into **STRING** and **Cytoscape** for Hub Gene identification.

---

## 📂 Repository Structure

```text
├── PCOS_RNAseq_Pipeline.Rmd      # Main parameterized R Markdown analysis pipeline
├── PCOS_RNAseq_Pipeline.html     # Compiled interactive HTML report with outputs & plots
├── data/
│   └── GSE138518_RNA.xlsx        # Input raw gene count matrix (place your dataset here)
├── outputs/                      # Auto-generated directory upon execution
│   ├── results/                  # CSV tables (DEGs, GO, KEGG, GSEA, PPI input)
│   └── figures/                  # High-resolution (300 DPI) JPEG visualizations
└── README.md                     # Project documentation
⚙️ Prerequisites & Package Installation
Ensure you have R (≥ 4.2.0) and RStudio installed. Run the following script in R to install all required CRAN and Bioconductor dependencies:

R
# Install CRAN packages
install.packages(c("readxl", "dplyr", "ggplot2", "ggrepel", "pheatmap", "knitr", "rmarkdown"))

# Install Bioconductor packages
if (!requireNamespace("BiocManager", quietly = TRUE))
    install.packages("BiocManager")

BiocManager::install(c("DESeq2", "clusterProfiler", "org.Hs.eg.db", "enrichplot"))
🚀 How to Run (Dynamic Input & Output Selection)
This pipeline uses R Markdown Parameters (params), eliminating hardcoded file paths so you can select your own input file and output directory at runtime:

Open PCOS_RNAseq_Pipeline.Rmd in RStudio.

Click the small dropdown arrow next to the Knit button at the top of the editor and select Knit with Parameters....

In the dialog window:

Select Input Counts Excel File (.xlsx): Click Browse... to select your count matrix file (defaults to data/GSE138518_RNA.xlsx).

Select Output Directory: Specify the folder name where results/ and figures/ will be automatically created (defaults to outputs).

Click Knit to execute the full workflow and generate the interactive HTML report.

📊 Generated Outputs
Tables (outputs/results/)
DEG_PCOS_vs_Control.csv — Complete differential expression statistics from DESeq2.

GO_BP_Enrichment_Results.csv — Enriched Gene Ontology Biological Process terms.

KEGG_Pathway_Enrichment_Results.csv — Enriched KEGG signaling pathways.

GSEA_GO_Results.csv — Ranked GSEA enrichment scores and core enriched genes.

Hub_Genes_PPI_Input.csv — Filtered significant DEGs formatted for STRING / Cytoscape.

Figures (outputs/figures/, 300 DPI)
Volcano_Plot_PCOS_Clean_Labeled.jpg

Heatmap_Top50_PCOS.jpg

GO_BP_Dotplot.jpg

KEGG_Pathway_Barplot.jpg

GO_Gene_Concept_Network.jpg

GSEA_GO_Ridgeplot.jpg

👤 Author
Mohammad Reza Yavari Parand

Department of Comparative Biosciences, Faculty of Veterinary Medicine, University of Tehran

Research Focus: Clinical Biochemistry, Transcriptomics, Metabolomics & Lipidomics

📄 License
This project is open-source and available under the MIT License.
