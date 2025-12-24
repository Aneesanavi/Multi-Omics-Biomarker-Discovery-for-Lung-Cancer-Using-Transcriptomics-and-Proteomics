Lung Cancer Multi-Omics Biomarker Discovery

Transcriptomics + Proteomics Integration (CPTAC-LUAD)

Project Overview

This project demonstrates a multi-omics biomarker discovery workflow for lung cancer, integrating transcriptomic (RNA-seq) and proteomic data from public CPTAC datasets.

The objective is not to build a production-ready diagnostic model, but to:

show how biomarkers are discovered from each omics layer,

integrate signals across omics to increase biological confidence,

and evaluate compact biomarker panels using simple, interpretable machine-learning models.

Scientific Motivation

Single-omics biomarkers often suffer from:

noise,

lack of reproducibility,

and limited biological interpretability.

Multi-omics integration improves robustness by retaining biomarkers that are supported at multiple biological layers:

RNA → gene activity

Protein → functional expression

This approach is particularly relevant for molecular diagnostics, where biomarkers must be both biologically meaningful and clinically measurable.

Data Used
Transcriptomics (RNA-seq)

Source: CPTAC Lung Adenocarcinoma (LUAD) via LinkedOmics

Data type: log2-normalized RNA expression

Samples: Tumor vs Normal lung tissue

Rows: Samples

Columns: Genes

Proteomics

Source: CPTAC LUAD Proteome

Data type: normalized protein abundance

Samples: Tumor vs Normal lung tissue

Rows: Samples

Columns: Proteins (gene symbols)

All datasets are public and pre-processed, allowing the project to focus on biomarker discovery, integration strategy, and interpretation, rather than raw sequencing or mass-spectrometry preprocessing.

Project Workflow (Step-by-Step)
Step 1: Data Preparation

Load transcriptomic and proteomic expression matrices

Ensure consistent formatting:

rows = samples

columns = features

labels = tumor / normal

Convert labels to binary values for modeling

Why this matters:
Correct formatting and labeling are essential before any statistical or ML analysis.

Step 2: Single-Omics Biomarker Discovery (Transcriptomics)

For RNA data:

Compare tumor vs normal samples

For each gene:

compute effect size (mean difference)

compute statistical significance (Welch’s t-test)

Rank genes by:

low p-value

high absolute effect size

Apply multiple-testing correction (Benjamini–Hochberg FDR)

Output:
top_transcriptomic_biomarkers.csv

Interpretation:
These genes represent transcriptional changes associated with lung cancer.

Step 3: Single-Omics Biomarker Discovery (Proteomics)

For protein data:

Repeat the same analysis strategy:

tumor vs normal comparison

effect size + statistical testing

ranking by significance and magnitude

Output:
top_proteomic_biomarkers.csv

Interpretation:
These proteins represent functional molecular changes and are closer to clinically measurable biomarkers.

Step 4: Multi-Omics Integration

Integration is performed at the gene/protein symbol level.

Biomarkers are classified as:

RNA-only: supported only at transcript level

Protein-only: supported only at protein level

RNA & Protein: supported at both levels

Priority is given to biomarkers supported by both omics layers, as these are more likely to be:

biologically meaningful

reproducible

clinically relevant

Output:
integrated_biomarker_panel.csv

Step 5: Biomarker Panel Construction

Three compact panels are defined:

RNA-only panel (top 10 genes)

Protein-only panel (top 10 proteins)

Integrated panel (genes/proteins supported by both layers)

Why compact panels?
Clinical diagnostics favor small, interpretable biomarker sets rather than thousands of features.

Step 6: Machine-Learning Evaluation

A simple, interpretable ML model is used:

Logistic Regression

Median imputation for missing values

Feature scaling

5-fold stratified cross-validation

Performance metrics:

ROC-AUC

Accuracy

Important:
ML is used here as a validation tool, not a black-box predictor.

Results
Model Performance Summary
Panel	Features	ROC-AUC (mean)	Accuracy (mean)
RNA-only	10	1.00	1.00
Protein-only	10	1.00	1.00
Integrated	16	1.00	0.995
Interpretation of Results

Near-perfect tumor vs normal separation is expected for CPTAC lung cancer data due to strong molecular differences.

RNA-only and protein-only panels already show excellent discrimination.

The integrated panel does not aim to outperform single-omics, but to:

confirm biomarkers across multiple biological layers

increase confidence and robustness

reduce false positives

The value of integration lies in biological validation, not marginal gains in accuracy.

Key Takeaways

Transcriptomics captures disease activity

Proteomics captures functional consequences

Integration confirms true disease-associated biomarkers

Compact panels are more relevant for molecular diagnostics

High performance here reflects dataset clarity, not overfitting intent

Limitations

This is a computational discovery project

Clinical deployment requires:

independent cohorts

prospective validation

wet-lab or clinical testing

Performance in real-world settings will be lower due to heterogeneity

How This Project Is Relevant

This workflow mirrors real-world practices in:

biomarker discovery

precision medicine

molecular diagnostics

omics integration in biotech and pharma R&D
