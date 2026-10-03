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
[Read the full report →](https://maryamshojaeiee-hub.github.io/Analysis-of-High-Dimensional-Gene-Expression-Data/reports/01_differential_expression.html) · [View the code →](code/01_differential_expression.Rmd)

### 2. Predictive Modelling (leukemia data)
Single-gene logistic regression compared with supervised principal components (SPCA). SPCA reduced the misclassification error from 7% to 3%.
[Read the full report →](02_predictive_modelling.md)

### 3. Gene Signature for Classification (leukemia data)
Comparison of LDA, DLDA, SVM, LASSO and Random Forest with cross-validation. A 23-gene signature with DLDA achieved a 2% error rate.
[Read the full report →](03_gene_signature.md)

### 4. Cluster Analysis (leukemia data)
Hierarchical clustering and k-means with the gap statistic. Clustering without labels largely recovered the two leukemia subtypes.
[Read the full report →](04_cluster_analysis.md)

## Tools
R, R Markdown, limma, CMA, glmnet, randomForest, e1071, ggplot2

## Author
Maryam Shojaei Shahrokhabadi · [LinkedIn URL] · [Email]
