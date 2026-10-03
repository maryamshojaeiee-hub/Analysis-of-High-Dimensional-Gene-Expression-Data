01_differential_expression
================
Maryam Shojaei Shahrokhabadi
2026-10-03

``` r
knitr::opts_chunk$set(echo = FALSE)
```

## Question 1

- **Title:**Differential gene expression

- **Objective:** Identify genes that are **differentially expressed**
  between **control** and **cancer** subjects

- **Dataset:** Prostate cancer gene expression data

- There were no missing value and no zero

## Group-specific gene expression patterns

- Variance differs between Control and Cancer groups.

- There are some outliers in both groups.

<img src="01_differential_expression_files/figure-gfm/unnamed-chunk-1-1.png" alt="" width="70%" style="display: block; margin: auto;" />
\## Distribution of the top 4 variable genes

- These genes do not follow a normal distribution.

- **Wilcoxon rank-Sum** test for differential expression.

<img src="01_differential_expression_files/figure-gfm/unnamed-chunk-2-1.png" alt="" width="90%" style="display: block; margin: auto;" />

## Wilcoxon test hypothesis for gene expression

**Null hypothesis ($H_0$):** Cancer and control groups have similar
expression distributions.

$$
H_0:\; P(X_C > X_H) = 0.5
$$

**Alternative hypothesis ($H_1$):** Cancer and control groups have
different expression distributions.

$$
P(X_C > X_H) \neq 0.5
$$

## Histogram of the raw p values

- We expect to find a few significant genes after multiplicity
  adjustment

## Volcano plot with adjusted P-values

- Highlights genes with significant differential expression

- Multiple testing corrections applied:
  - Benjamini-Hochberg (BH): dashed line
  - Holm: blue dotted line

<!-- -->

    ##      Gene     Log2FC      P_value         FDR    holm_adj
    ## 411   411 -0.2244608 1.322045e-06 0.003040757 0.007974576
    ## 452   452  0.7952413 1.008550e-06 0.003040757 0.006084584
    ## 739   739 -0.8749383 1.512062e-06 0.003040757 0.009119248
    ## 610   610  0.9068995 4.459442e-06 0.005380763 0.026885976
    ## 4552 4552  0.5609114 3.676185e-06 0.005380763 0.022167394
    ## 81     81  0.5016304 5.401191e-06 0.005430897 0.032558377
    ## 37     37  0.5964814 7.643450e-06 0.005454504 0.046067073
    ## 1720 1720  0.6833282 7.886536e-06 0.005454504 0.047524265
    ## 4331 4331 -0.7620104 8.137002e-06 0.005454504 0.049025440
    ## 3647 3647  0.8074751 1.334055e-05 0.008048355 0.080363484

<img src="01_differential_expression_files/figure-gfm/unnamed-chunk-5-1.png" alt="" width="85%" style="display: block; margin: auto;" />

## Highlighting significant fold-Change genes

- Significance thresholds mark differentially expressed genes.

- Fold-change cutoffs indicate genes with meaningful expression
  differences.
  <img src="01_differential_expression_files/figure-gfm/unnamed-chunk-6-1.png" alt="" width="85%" style="display: block; margin: auto;" />

## Question2

**Title:Differential expression via Limma**

Linear model for detecting genes with differential expression.

For each gene $j$, the expression in sample $i$ is modeled as:

$$X_{ij} = \beta_{0j} + \beta_{1j} Group_i + \epsilon_{ij}$$

$\beta_{0j}$: The gene-specific intercept.

$\beta_{1j}$: log2 fold change between cancer and control.

$Group$: The indicator variable representing the disease status.

$\epsilon_{ij}$: Random error term.

**The Statistical Hypotheses** $$
H_0: \beta_{1j} = 0 
$$ $$
H_1: \beta_{1j} \neq 0  
$$

## Volcano plot of differential expression (Limma)

    ## Warning in cbind(...): number of rows of result is not a multiple of vector
    ## length (arg 1)

    ##                  Length Class  Mode     
    ## coefficients     12066  -none- numeric  
    ## rank                 1  -none- numeric  
    ## assign               0  -none- NULL     
    ## qr                   5  qr     list     
    ## df.residual       6033  -none- numeric  
    ## sigma             6033  -none- numeric  
    ## cov.coefficients     4  -none- numeric  
    ## stdev.unscaled   12066  -none- numeric  
    ## pivot                2  -none- numeric  
    ## Amean             6033  -none- numeric  
    ## method               1  -none- character
    ## design             204  -none- numeric

    ##           logFC      AveExpr         t      P.Value   adj.P.Val        B
    ## 610  -0.9068995 -0.093749817 -5.527293 1.967133e-07 0.001186771 6.676823
    ## 1720 -0.6833282 -0.201815304 -4.801466 4.650686e-06 0.014028794 3.869362
    ## 3940  0.8729599  0.025333822  4.604504 1.048165e-05 0.014295617 3.150596
    ## 914  -0.8348609 -0.018475778 -4.604479 1.048273e-05 0.014295617 3.150506
    ## 364   0.7463900  0.138947980  4.567458 1.218398e-05 0.014295617 3.017643
    ## 332  -0.7319054 -0.314449378 -4.529268 1.421742e-05 0.014295617 2.881347
    ## 4546  0.6492091 -0.202287680  4.337833 3.044114e-05 0.018657199 2.210006
    ## 3647 -0.8074751  0.184804805 -4.334110 3.088880e-05 0.018657199 2.197149
    ## 579  -0.7519201 -0.253946106 -4.314288 3.338089e-05 0.018657199 2.128831
    ## 4331  0.7620104  0.005678114  4.313139 3.353106e-05 0.018657199 2.124879

<img src="01_differential_expression_files/figure-gfm/unnamed-chunk-7-1.png" alt="" width="85%" style="display: block; margin: auto;" />

## Overlap of significant genes between methods

Among 18 shared significant genes, 8 exceeded $|log_2FC| > 0.75$:

**“739”, “610”, “4331”, “3647”, “3940”, “579”, “3991”, and “3375”**
