# From Words to Curves: Bayesian Modeling of Early Vocabulary Growth

**A Bayesian Hierarchical Negative Binomial Approach to Modeling Early Vocabulary Growth**

**Author:** Antonietta De Lucia  
**Course:** Fundamentals of Statistical Learning II  
**Program:** MSc in Data Science, Sapienza University of Rome  
**Academic year:** 2025–2026

## Overview

How does productive vocabulary develop between 16 and 30 months of age, and how can we quantify the substantial variability between children? This project studies early vocabulary acquisition using Bayesian count-data models, focusing on nonlinear growth, overdispersion, age-group heterogeneity, and demographic covariates.

The analysis uses **WordBank** data from the MacArthur–Bates Communicative Development Inventories (CDI), focusing on the English (American) *Words and Sentences* form and the Marchman sample. The report describes **5,031 observations** in the cleaned analysis dataset and a **random subsample of 500 children** for MCMC model fitting.

## Research objectives

- Characterize the nonlinear trajectory and variability of productive vocabulary between 16 and 30 months.
- Evaluate why a Poisson likelihood is inadequate for strongly overdispersed word counts.
- Fit and compare Bayesian Negative Binomial models, including a hierarchical specification with partial pooling across monthly age groups.
- Investigate sex, caregiver education, and age-by-sex effects on the modeled growth process.
- Assess MCMC convergence, model fit, posterior predictions, and uncertainty.

## Methods

The modeling framework combines a **Brody–Bertalanffy asymptotic mean function** with Poisson and Negative Binomial likelihoods. Candidate models include a population-level baseline, an age-group hierarchical model, and extensions for demographic effects.

Inference is performed with **JAGS through R**, using Markov chain Monte Carlo (MCMC). Model assessment includes convergence diagnostics (R-hat, effective sample size, and traceplots), posterior predictive checks, and **Deviance Information Criterion (DIC)** comparisons. The report also includes a parameter recovery experiment and a frequentist comparison.

## Selected findings

- Vocabulary counts are highly overdispersed, motivating a Negative Binomial rather than a simple Poisson observation model.
- The hierarchical Negative Binomial model (**NB2**) substantially improves on the population-level Negative Binomial baseline (**NB1**): the report gives **DIC 6,412.5 vs. 6,499.8**.
- The analysis explores sex-specific growth patterns; estimated effect magnitudes have meaningful uncertainty and should not be interpreted causally.
- Posterior predictive analysis illustrates uncertainty and heterogeneity in vocabulary development across ages.

These are results reported in the accompanying coursework report; they have not been independently rerun as part of this GitHub packaging.

## Repository contents

```text
bayesian-vocabulary-growth/
├── README.md                  # Project overview and instructions
├── vocabulary_growth.Rmd      # Original R Markdown analysis (renamed only)
├── Project_Report.pdf         # Original academic report (renamed only)
└── .gitignore                 # Excludes local caches and generated files
```

## Requirements

- R and RStudio (recommended)
- JAGS installed separately on the operating system
- R packages: `wordbankr`, `dplyr`, `ggplot2`, `tidyr`, `moments`, `R2jags`, `rjags`, `coda`, `minpack.lm`, `bookdown`, `knitr`
- For PDF rendering, a working LaTeX installation supporting XeLaTeX

Install the listed R packages as appropriate for your R/JAGS environment. The analysis has not been tested in a clean environment for this repository upload.

## Data and reproducibility

The R Markdown file first looks for a local cache named `data_full.rds`. If that file is absent, it attempts to retrieve the WordBank administration data using `wordbankr::get_administration_data()` for **English (American)** and form **WS**, with demographic information.

The cached dataset is **not included** in this repository. Availability of the upstream WordBank service, package versions, and local JAGS configuration can affect reproducibility. See the R Markdown source for the data-loading logic and analysis steps.

To render the analysis after installing the dependencies and obtaining the data:

```r
rmarkdown::render("vocabulary_growth.Rmd")
```

The document's configured HTML output uses `bookdown::html_document2`; PDF output additionally requires XeLaTeX.

## Limitations

The underlying data are cross-sectional rather than longitudinal, so modeled age differences should not be interpreted as observed within-child trajectories. The CDI instrument also has a 680-word measurement ceiling, and demographic associations do not establish causality. For detailed assumptions, model diagnostics, and interpretation, see [`Project_Report.pdf`](Project_Report.pdf).

## Data source

WordBank: https://wordbank.stanford.edu/  
Frank et al. (2017), *Wordbank: An open repository for developmental vocabulary data*. See the academic report for the complete bibliography.

## Academic context

Individual final project submitted for **Fundamentals of Statistical Learning II**, MSc Data Science, Sapienza University of Rome (2025–2026).
