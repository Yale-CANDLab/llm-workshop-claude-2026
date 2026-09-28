# CLAUDE.md Template

This file is a template for creating a `CLAUDE.md` file for your project. Claude Code automatically reads `CLAUDE.md` from your project directory at the start of every session, so the instructions you write here shape how Claude understands your project and behaves within it. Delete the HTML comments and replace the `[bracketed placeholders]` with your own content.

## Project Overview

<!-- Orient Claude to your project's domain, data, and research goals.
     Without this section, Claude has no context about your study design,
     sample, or scientific objectives, and may suggest approaches that
     are inappropriate for your data structure (e.g., a cross-sectional
     analysis method for a longitudinal dataset). -->

- **Project title**: [e.g., Longitudinal Analysis of Internalizing Symptoms in Early Childhood]
- **Study design**: [e.g., longitudinal, 3 time points, 6-month intervals]
- **Sample**: [e.g., N=200 children ages 4-8, recruited from community clinics]
- **Data modalities**: [e.g., parent-report questionnaires, behavioral task performance, resting-state fMRI]
- **Primary research questions**: [e.g., (1) Do internalizing symptoms change over the study period? (2) Does baseline neural connectivity predict symptom trajectories?]
- **Data source/format**: [e.g., REDCap exports in CSV format; BIDS-formatted neuroimaging data]

## Claude's Role

<!-- Define what Claude should act as and how much autonomy it should have.
     A graduate student building a new pipeline may want Claude to explain
     every decision and ask before acting. A senior researcher running a
     familiar workflow may want Claude to implement silently and report
     only issues. Stating this explicitly prevents mismatched expectations. -->

- **Primary role**: [e.g., statistical and methods consultant; code implementation partner; code reviewer]
- **Autonomy level**: [e.g., always ask before making non-trivial analytical decisions / implement first, then explain / act independently on routine tasks, ask on novel ones]
- **Defer to user on**: [e.g., theoretical framing, clinical interpretation of findings, choice of assessment measures]
- **Claude should NOT**: [e.g., make clinical interpretations of individual scores; choose between competing theoretical frameworks without asking]

## Technical Environment

<!-- Specify your languages, package managers, key libraries, and compute setup.
     If you use conda for environment management, telling Claude prevents it
     from suggesting bare pip install commands that could break your environment
     or install packages outside your project environment. -->

- **Primary language(s)**: [e.g., R 4.x for analysis and visualization; Python 3.11 for preprocessing; MATLAB R2023b for neuroimaging]
- **Package manager**: [e.g., mamba/conda for both R and Python; renv for R package versioning]
- **Key packages**: [e.g., tidyverse, lme4, lmerTest, ggplot2, lavaan (R); pandas, nilearn, nibabel (Python)]
- **IDE**: [e.g., RStudio; VS Code; Jupyter]
- **Compute environment**: [e.g., local macOS; university HPC cluster with SLURM; AWS]
- **Operating system**: [e.g., macOS Sonoma; Ubuntu 22.04 on HPC nodes]

## Data Conventions

<!-- Define file naming, directory layout, and data formats your project uses.
     If the lab uses a specific subject ID format (e.g., sub-XXXX), Claude
     needs to know this to generate code that correctly parses file paths
     and merges data across modalities by subject. -->

- **Directory structure**:
  - [e.g., data/raw/ for unmodified source files]
  - [e.g., data/cleaned/ for processed datasets]
  - [e.g., scripts/ for analysis code]
  - [e.g., output/ for results, figures, reports]
- **File naming**: [e.g., snake_case; prefix with measure name (cbcl_scored_wide.csv)]
- **Subject ID format**: [e.g., sub_XXXX where XXXX is a 4-digit zero-padded integer]
- **Variable naming**: [e.g., measure_subscale_timepoint pattern (cbcl_internalizing_t1)]
- **Data format**: [e.g., CSV with headers; BIDS for neuroimaging; Parquet for large datasets]

## Analytical Standards

<!-- Set the statistical and methodological standards Claude should uphold.
     Without explicit standards, Claude may default to reporting only
     p-values without effect sizes, skip assumption checks before
     parametric tests, or apply inappropriate corrections for
     multiple comparisons. -->

- **Multiple comparison correction**: [e.g., FDR (Benjamini-Hochberg) for neuroimaging analyses; Bonferroni only when family-wise error control is required]
- **Effect size reporting**: [e.g., always report Cohen's d or partial eta-squared alongside p-values]
- **Reproducibility**: [e.g., set and report random seeds; pin package versions via renv; document all exclusion criteria before analysis]
- **Assumption checking**: [e.g., verify normality, homoscedasticity, and multicollinearity before parametric tests; report diagnostics]
- **Missing data**: [e.g., report missingness rates per variable; justify MCAR/MAR/MNAR assumptions before choosing imputation or listwise deletion]
- **Sample size considerations**: [e.g., flag any analysis where N per group or cell falls below 20; report power analyses for primary hypotheses]

## Coding Standards

<!-- Define style, testing, and documentation expectations for generated code.
     Specifying that functions should validate their inputs prevents Claude
     from generating code that silently accepts invalid data (e.g., a scoring
     function that returns results even when required columns are missing). -->

- **Style guide**: [e.g., tidyverse style guide for R; PEP 8 for Python]
- **Function documentation**: [e.g., roxygen2-style comments for R functions; numpy-style docstrings for Python]
- **Input validation**: [e.g., functions should check for expected column names and data types before operating]
- **File paths**: [e.g., use here::here() or relative paths from project root; no hardcoded absolute paths]
- **Testing**: [e.g., write unit tests for scoring functions; test against published manual examples when available]
- **Version control**: [e.g., use git; commit logical units of work with descriptive messages]

## Guardrails

<!-- Set boundaries around security, data handling, and destructive operations.
     In clinical and developmental research, raw data files often contain
     protected health information (PHI) such as dates of birth or assessment
     dates. Claude must never include real participant identifiers in code
     comments, console output, or error messages. -->

- **Data sensitivity**: [e.g., data contains PHI (dates of birth, assessment dates); never print or log actual identifiers or dates to console or reports]
- **Raw data protection**: [e.g., files in data/raw/ are read-only; never modify, overwrite, or delete source data files]
- **Environment changes**: [e.g., always ask before installing packages, creating environments, or modifying lockfiles]
- **Destructive operations**: [e.g., never delete files or directories without explicit approval; prefer renaming over deletion]
- **Verification**: [e.g., verify scoring algorithms against published manuals before implementing; cross-check computed statistics against known values when available]

## Voice and Tone

<!-- Specify how Claude should communicate with you.
     A lab that publishes in APA-style journals may want Claude to use
     formal, third-person academic prose in documentation, while a lab
     that values accessibility might prefer plain-language explanations
     alongside technical detail. -->

- **Formality**: [e.g., academic and professional; third-person in documentation; avoid casual language]
- **Technical depth**: [e.g., explain statistical choices at a level appropriate for a methods-aware graduate student]
- **Uncertainty handling**: [e.g., when uncertain about a domain-specific convention (e.g., clinical cutoff thresholds), ask rather than assume]
- **Terminology**: [e.g., use APA-style terminology; refer to participants (not subjects); use measure abbreviations consistently (CBCL, SDQ)]
