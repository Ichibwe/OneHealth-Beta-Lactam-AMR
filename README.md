[README_Beta_Lactam_OneHealth_AMR.md](https://github.com/user-attachments/files/33128443/README_Beta_Lactam_OneHealth_AMR.md)
# β-Lactam Resistance Gene Distribution Across One Health Sources

## Overview

This repository contains an **R-based analytical and visualization
workflow** for investigating the distribution of **β-lactam resistance
genes** in antimicrobial-resistant bacterial isolates across **human,
animal, and environmental sources** using a **One Health approach**.

The workflow integrates isolate-level AMR information with
isolation-source and sample-type metadata to summarize β-lactam
resistance gene occurrence, compare patterns across One Health sectors,
and generate publication-quality figures and analytical tables.

The analysis is designed for genomic AMR surveillance data and
demonstrates the application of **R programming, data wrangling,
exploratory data analysis, and scientific visualization** to One Health
antimicrobial resistance research.

## Objectives

The workflow is designed to:

-   classify isolates into **Human, Animal, and Environment** source
    groups;
-   identify and analyse **β-lactam resistance genes**;
-   quantify the number of unique isolates carrying each resistance
    gene;
-   compare β-lactam resistance gene distributions across One Health
    sources;
-   examine resistance-gene distributions across different sample types;
-   visualize individual isolates by sample type within source-specific
    summaries;
-   generate publication-quality figures;
-   export analytical summary tables for reporting and downstream
    interpretation.

## Analysis Workflow

### 1. Data preparation

The script reads the merged AMR dataset, checks required variables, and
prepares the data for analysis.

### 2. One Health source classification

Isolation sources are grouped into three broad categories:

-   **Animal** --- including beef cattle and chicken isolates
-   **Human**
-   **Environment**

### 3. β-Lactam resistance gene identification

The workflow focuses on β-lactam resistance genes recorded in the AMR
dataset. In the underlying data, these determinants are identified using
gene symbols beginning with `bla`.

Only records classified as AMR determinants are retained for the
principal analysis.

### 4. Isolate-level deduplication

To avoid inflating counts, the workflow retains one observation for each
unique combination of:

``` text
isolate
resistance gene
isolation source
sample type
```

Thus, an isolate is counted only once for a given β-lactam resistance
gene within the corresponding source and sample-type combination.

### 5. Gene distribution by One Health source

The script calculates the number of isolates carrying each β-lactam
resistance gene across:

``` text
Animal
Human
Environment
```

Genes can then be ordered according to their overall frequency in the
analysed dataset.

### 6. Sample-type distribution

The workflow evaluates β-lactam resistance genes by sample type and
generates:

-   isolate counts by resistance gene and sample type;
-   percentage distributions within sample types;
-   wide-format gene-by-sample-type summary tables.

### 7. Visualization

The script contains several iterative visualization approaches,
including publication-quality grouped bar charts in which:

-   the **x-axis** represents β-lactam resistance genes;
-   the **y-axis** represents the number of isolates;
-   bar groups represent isolation sources;
-   coloured dots can represent individual isolates according to sample
    type.

Selected versions also include a **radial sample-type wheel** to
summarize sample-type categories.

### 8. Selected gene analysis

The workflow includes a focused analysis of **blaTEM-1**, summarizing
its occurrence according to isolation source and sample type.

## Input Data

A principal version of the workflow reads:

``` text
Merged_AMR_MLST_Mobsuitclean.csv
```

The main analysis requires variables including:

``` text
isolate_id
amr_element_symbol
amr_subtype
amlst_isolation_source_or_host
amlst_sample_type
```

Some iterative sections of the script may use standardized or
alternative column names. Users should therefore confirm that the column
names in their dataset match the relevant analysis block before running
it.

> **Data availability:** The underlying research dataset may not be
> included in this public repository. Users wishing to reproduce the
> workflow should provide an appropriately structured dataset and update
> the input path and column names where required.

## R Packages

Packages used across the script include:

``` r
readr
readxl
readODS
dplyr
tidyr
stringr
ggplot2
forcats
scales
cowplot
ggforce
patchwork
janitor
writexl
openxlsx
flextable
officer
MASS
vegan
lubridate
foreign
```

Not every package is required for every analysis section.

## Running the Analysis

Clone the repository:

``` bash
git clone https://github.com/Ichibwe/OneHealth-ESBL-E.coli-AMR.git
cd OneHealth-ESBL-E.coli-AMR
```

Open the R script in **RStudio** or another R environment.

Load the dataset, for example:

``` r
PLasmid <- readr::read_csv(
  "Merged_AMR_MLST_Mobsuitclean.csv",
  show_col_types = FALSE
)
```

Install any required packages that are not already available, then run
the relevant analysis sections sequentially.

## Outputs

The workflow produces high-resolution scientific figures and analytical
tables. Depending on the analysis block, outputs include:

-   grouped bar charts of β-lactam resistance genes by isolation source;
-   sample-type dot distributions;
-   radial sample-type visualizations;
-   β-lactam resistance gene counts by sample type;
-   percentage distributions by sample type;
-   wide-format gene distribution tables;
-   focused summaries for selected genes such as `blaTEM-1`;
-   high-resolution **PNG** figures;
-   **PDF** figures in selected sections;
-   **CSV** analytical tables.

Figures and tables are primarily written to:

``` text
03_Figures/
```

One of the figure workflows exports publication-quality images at **600
dpi**.

## Suggested Repository Structure

``` text
OneHealth-ESBL-E.coli-AMR/
├── README.md
├── AMR_source_analysis.R
├── data/
│   └── README.md
└── 03_Figures/
```

If the original research data cannot be shared publicly, the `data/`
directory can contain a description of the expected input structure or
an appropriately de-identified example dataset.

## Reproducibility

The workflow implements the analysis programmatically in R so that data
processing, summaries, and figures can be regenerated when the
underlying dataset changes.

The use of isolate-level deduplication is particularly important because
it reduces the risk of repeatedly counting the same isolate for the same
resistance gene, isolation source, and sample type.

## Scientific Context

β-Lactam antibiotics are an important antimicrobial class, and
resistance to these agents is a major component of antimicrobial
resistance surveillance. Examining β-lactam resistance genes across
human, animal, and environmental sources can help describe how
resistance determinants are distributed within interconnected One Health
systems.

This repository provides an R-based approach for converting genomic AMR
and epidemiological metadata into interpretable summaries and
visualizations that can support **One Health AMR surveillance and
research**.

## Interpretation

The workflow describes the **distribution and co-occurrence of
resistance determinants within the analysed dataset**. Detection of the
same β-lactam resistance gene in isolates from different One Health
sources does **not by itself demonstrate transmission or horizontal gene
transfer between sectors**.

Establishing transmission or genetic exchange requires additional
genomic and epidemiological evidence, such as high-resolution
phylogenetic analysis, plasmid reconstruction, long-read or hybrid
sequencing, and appropriate epidemiological metadata.

## Author

**Innocent Chibwe**

Microbiology \| Antimicrobial Resistance \| Genomics \| Bioinformatics
\| Data Analytics \| One Health

GitHub: https://github.com/Ichibwe

## Citation

This repository contains an analytical workflow developed as part of
ongoing AMR research. If you use or adapt the workflow, please
acknowledge the repository. Formal citation details can be added when
the associated research is published.

## License

No license is specified at present. Unless a license is added to the
repository, the code should not be assumed to carry an open-source reuse
license.
