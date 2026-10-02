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

