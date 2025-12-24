# Lung Cancer Multi-Omics Biomarker Discovery  
**Transcriptomics + Proteomics Integration (CPTAC-LUAD)**

## Overview
This project demonstrates a **multi-omics biomarker discovery workflow** for **lung cancer**, integrating **transcriptomic (RNA-seq)** and **proteomic** data from public **CPTAC-LUAD** datasets.  

The goal is to show how **omics integration improves biomarker robustness and interpretability**, which is critical for **molecular diagnostics**, rather than to build a production-ready clinical model.

---

## Scientific Motivation
Single-omics biomarkers often suffer from:
- noise and false positives,
- limited reproducibility,
- weak biological interpretability.

**Multi-omics integration** addresses these limitations by prioritizing biomarkers supported at **multiple biological layers**:
- **Transcriptomics** → gene activity  
- **Proteomics** → functional protein expression  

---

## Data Sources
All data used are **public and pre-processed**, allowing the project to focus on biomarker discovery logic and integration strategy.

### Transcriptomics
- Source: **CPTAC Lung Adenocarcinoma (LUAD)** via LinkedOmics  
- Data type: log2-normalized RNA-seq expression  
- Comparison: Tumor vs Normal lung tissue  

### Proteomics
- Source: **CPTAC LUAD Proteome**  
- Data type: normalized protein abundance  
- Comparison: Tumor vs Normal lung tissue  

---

## Workflow (Step-by-Step)

### 1. Data Preparation
- Loaded transcriptomic and proteomic matrices
- Ensured sample-by-feature format
- Labeled samples as `tumor` or `normal`
- Converted labels to binary values for analysis

---

### 2. Single-Omics Biomarker Discovery (Transcriptomics)
- Compared tumor vs normal samples
- Computed:
  - effect size (mean difference)
  - statistical significance (Welch’s t-test)
- Applied multiple-testing correction (Benjamini–Hochberg FDR)
- Ranked genes by significance and magnitude

**Output:**  
`results/top_transcriptomic_biomarkers.csv`

---

### 3. Single-Omics Biomarker Discovery (Proteomics)
- Repeated the same statistical workflow on protein abundance data
- Identified differentially abundant proteins associated with lung cancer

**Output:**  
`results/top_proteomic_biomarkers.csv`

---

### 4. Multi-Omics Integration
- Integrated RNA and proteomics results at the **gene/protein symbol level**
- Classified biomarkers as:
  - RNA-only
  - Protein-only
  - RNA & Protein (supported in both layers)
- Prioritized biomarkers supported by **both omics layers**

**Output:**  
`results/integrated_biomarker_panel.csv`

---

### 5. Biomarker Panel Construction
Constructed compact panels suitable for diagnostic interpretation:
- RNA-only panel (Top 10 genes)
- Protein-only panel (Top 10 proteins)
- Integrated panel (RNA + Protein features)

---

### 6. Machine-Learning Validation
- Model: Logistic Regression (interpretable baseline)
- Preprocessing:
  - median imputation
  - feature scaling
- Evaluation:
  - 5-fold stratified cross-validation
  - ROC-AUC and Accuracy

ML is used here as a **validation tool**, not as a black-box predictor.

---

## Results

### Model Performance Summary

| Biomarker Panel | Number of Features | ROC-AUC (Mean) | Accuracy (Mean) |
|-----------------|-------------------:|---------------:|----------------:|
| RNA-only        | 10                 | 1.00           | 1.00            |
| Protein-only    | 10                 | 1.00           | 1.00            |
| Integrated      | 16                 | 1.00           | 0.995           |

---

## Results Interpretation
- Near-perfect tumor vs normal separation is **expected** for CPTAC-LUAD due to strong molecular differences.
- RNA-only and protein-only panels already show excellent discrimination.
- The **integrated panel** does not aim to outperform single-omics models, but to:
  - confirm biomarkers across biological layers,
  - increase confidence and robustness,
  - reduce false positives.

> The value of integration lies in **biological validation**, not marginal gains in accuracy.

---

## Key Takeaways
- Transcriptomics captures **disease activity**
- Proteomics captures **functional consequences**
- Multi-omics integration improves biomarker reliability
- Compact biomarker panels are more suitable for diagnostics
- High performance reflects dataset clarity, not overfitting intent

---

## Limitations
- This is a **computational discovery study**
- Clinical deployment requires:
  - independent validation cohorts
  - prospective testing
  - wet-lab or clinical validation

---

## Relevance
This workflow mirrors real-world practices in:
- biomarker discovery
- molecular diagnostics
- precision medicine
- omics integration in biotech and pharma R&D

---

## Author
**Aneesa Abbas**  
Background: Genetics • Bioinformatics • AI  
Focus: Omics integration, biomarker discovery, molecular diagnostics

---

### Interview One-Liner
> “This project demonstrates how integrating transcriptomic and proteomic evidence improves the robustness and interpretability of lung cancer biomarker discovery using public CPTAC data.”
