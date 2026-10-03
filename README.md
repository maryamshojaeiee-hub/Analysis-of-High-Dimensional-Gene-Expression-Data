# Analysis-of-High-Dimensional-Gene-Expression-Data
Statistical analysis of two public microarray datasets (prostate cancer and leukemia) covering differential expression testing, predictive modelling, gene signature development, and cluster analysis in R.

## Overview

Gene expression studies measure thousands of genes on only a few dozen patients, so standard statistical methods break down: multiple testing inflates false discoveries, and predictive models overfit easily. This project applies methods designed for this "large p, small n" setting to answer four types of questions:

1. Which genes are differentially expressed between prostate cancer patients and healthy controls?
2. How well can a single gene predict leukemia subtype, and does combining genes through supervised PCA do better?
3. What is the smallest gene signature that reliably classifies leukemia subtypes, and which classifier works best?
4. Do patients form natural groups based on their expression profiles alone, and do these match the known subtypes?

## Data

| Dataset | Genes | Samples | Groups |
|---|---|---|---|
| Prostate cancer (Singh et al., 2002) | 6,033 | 102 | 50 healthy controls, 52 prostate cancer |
| Leukemia (Golub et al., 1999) | 7,128 | 72 | 47 ALL, 25 AML |

Both datasets are well-known benchmarks, used in Efron & Hastie, [*Computer Age Statistical Inference*](https://hastie.su.domains/CASI/), and Efron, [*Large-Scale Inference*](https://www.cambridge.org/core/books/largescale-inference/contents/7E866460BD3DD85A266ACD167727500E).

## Analyses

### 1. Differential Expression Analysis (prostate data)
**Objective:** Identify genes that are differentially expressed between control and cancer subjects.

To identify genes that differ between cancer patients and controls, we compared a classical gene-by-gene test (Wilcoxon rank-sum) with limma, which also fits a model per gene but uses empirical Bayes moderation to borrow information across genes. Both methods agreed on 18 genes, 8 of which also showed large fold changes (|log₂FC| > 0.75).
[Read the full report →](https://maryamshojaeiee-hub.github.io/Analysis-of-High-Dimensional-Gene-Expression-Data/reports/01_differential_expression.html) · [View the code →](codes/01_differential_expression.Rmd)


### 2. Predictive Modelling of Leukemia Subtype (leukemia data)
To predict whether a patient has AML or ALL from gene expression, we first fitted a separate logistic regression model for each gene and evaluated the best single-gene predictors. To use information from several correlated genes at once, we then applied supervised principal components (SPCA): the top-ranked genes were summarised by their first principal component, which was used as the predictor in a logistic model. SPCA reduced the misclassification error from 7% for the best single gene to 3%, with 96% sensitivity and 98% specificity.[Read the full report →](https://maryamshojaeiee-hub.github.io/Analysis-of-High-Dimensional-Gene-Expression-Data/reports/02_predictive_modelling.html) · [View the code →](code/02_predictive_modelling.Rmd)

### 3. Gene Signature for Classification (leukemia data)
To develop a small set of genes that distinguishes AML from ALL, we compared five classifiers (LDA, DLDA, SVM, LASSO and Random Forest) using Monte Carlo cross-validation, with gene selection repeated inside each training set to avoid selection bias. DLDA performed best, with a cross-validated error of about 2.5% using 30 genes, while LDA became unstable as genes were added. Genes selected in at least half of the cross-validation splits formed a final 23-gene signature.
[Read the full report →](https://maryamshojaeiee-hub.github.io/Analysis-of-High-Dimensional-Gene-Expression-Data/reports/03_gene_signature.html) · [View the code →](code/03_gene_signature.Rmd)

### 4. Cluster Analysis (leukemia data)
We used hierarchical clustering and k-means clustering on the 100 most variable genes to see whether the patients naturally separated into different groups, without using their known leukemia types. The gap statistic indicated that two clusters were optimal. K-means then identified two groups of 26 and 46 patients, closely corresponding to the actual numbers of AML (25) and ALL (47) patients. This suggests that leukemia subtype is the main source of variation in the gene expression data.
[Read the full report →](https://maryamshojaeiee-hub.github.io/Analysis-of-High-Dimensional-Gene-Expression-Data/reports/04_cluster_analysis.html) · [View the code →](code/04_cluster_analysis.Rmd)

## Tools
R, R Markdown, limma, CMA, glmnet, randomForest, e1071, ggplot2

## Reproducing the Analysis

Install the required R packages:

```r
# CRAN packages
install.packages(c("tidyverse", "knitr", "kableExtra", "patchwork", "gridExtra",
                   "ggplotify", "UpSetR", "e1071", "glmnet", "randomForest",
                   "clusterGenomics"))

# Bioconductor packages
if (!requireNamespace("BiocManager", quietly = TRUE)) install.packages("BiocManager")
BiocManager::install(c("Biobase", "multtest", "limma", "CMA"))
```

Then open any `.Rmd` file in the `codes` folder in RStudio and click **Knit**. The prostate data are downloaded automatically from the authors' website.
## Author
Maryam Shojaei Shahrokhabadi · [LinkedIn](https://www.linkedin.com/in/maryam-shojaei-210740250)· [maryam.shojaei.ee@gmail.com]
