
<!-- README.md is generated from README.Rmd. Please edit that file -->

# 3PodR

<!-- badges: start -->
[![R Markdown](https://img.shields.io/badge/RMarkdown-Analysis-blue.svg)](https://rmarkdown.rstudio.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
<!-- badges: end -->

## Introduction
This template generates a comprehensive differential gene expression analysis report from one or more CSV files. Each CSV should contain differentially expressed genes (first column), log fold change (second column), and p-values (third column), and only those columns in that exact order. The first column should be a character vector, and the second and third columns should be numeric vectors.

Once built, the template files are rendered producing the following analyses: 
1. Volcano plots with thresholds for both p-value and adjusted p-value.
2. Gene Set Enrichment Analysis (GSEA) tables for Gene Ontology (GO) Biological Process (BP), Cellular Component (CC), and Molecular Function (MF) pathways, summarized using PAVER integration.
3. Gene Ontology (GO) pathway analysis (like in (#2)) via EnrichR, also summarized using PAVER.
4. A table of concordant and discordant drugs, derived from querying iLINCS with the input gene signature, and a separate table counting the most common mechanisms of action.

## Installation
To install 3podR, perform the following steps:

1. Clone the repository via `git clone https://github.com/willgryan/3PodR_bookdown.git`.
2. Change directory into the repository, via `cd 3podR_bookdown` (or open `3podR_bookdown.Rproj` in [Rstudio](https://posit.co/download/rstudio-desktop/) ).
3. Restore the environment via renv:
```r 
renv::restore()
```
4. Once all packages have been installed, you may try to render the report with the template data and default settings via the command:
```r
rmarkdown::render_site(encoding = 'UTF-8')
```

## Troubleshooting
To troubleshoot 3podR, use the following steps:
1. Always ensure your installation is correct by using the example data files in extdata. If these are running, the problem is almost certainly not with 3podR. If the report is not successfully generated, there may be a problem with your installation. Be sure that all files in the `renv.lock` file are installed before proceeding. As a general rule, always try to install from binary. If there is some request to install from source, try to change the repository that the package is downloaded from. It may be necessary to install from github using the `devtools` package and the `install_github()` function (and please ensure you are using the correct remote SHA at the end of the repository name, e.g. `install_github("willgryan/PAVER@REMOTE_SHA")` ) for the following packages: `PAVER`, `drugfindR`, `BioPathNet`.
2. If the installation seems to have been correct and the report is successfully generated with the example data, the next likely suspect is the input differential gene expression CSV file. Ensure that there are three and *only* three columns in the following order: gene symbols (character vector), logFC (numeric vector), and p-value (numeric vector).
3. If the input file is certainly the issue, one of the most common problems is the gene symbol column. Note that the gene symbols must have i) one gene symbol per line, and ii) it must be findable in the annotation file corresponding to the species that the analysis is being run on (either hgnc for homo sapiens, rgd for rat, or mgi for mouse). Files with these gene symbol annotations can be found in the assets folder. 3podR *cannot* accept anything other than HGNC symbols (e.g. Ensembl or Entrez gene IDs are unacceptable and will result in errors).
