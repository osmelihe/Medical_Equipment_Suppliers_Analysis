# Medical Equipment Suppliers — Analysis Project
# README
# =====================================================

## Overview
Exploratory and predictive analysis of the Medicare Medical Equipment Suppliers dataset.
58,191 supplier records | 17 columns | Source: CMS (Centers for Medicare & Medicaid Services)
Target variable: acceptsassignement (True/False)


## Files
  Medical-Equipment-Suppliers.csv               Raw dataset (place in same folder as notebook)
  Medical_Equipment_Suppliers_Analysis.ipynb    Main analysis notebook


## Requirements
  Python       >= 3.9
  numpy        >= 2.0
  pandas
  matplotlib
  scikit-learn >= 1.3

  Install all at once:
    pip install numpy pandas matplotlib scikit-learn

  Anaconda users (recommended to avoid version conflicts):
    conda create -n analysis python=3.11
    conda activate analysis
    conda install numpy pandas matplotlib scikit-learn jupyter


## How to Run
  1. Place Medical-Equipment-Suppliers.csv and the .ipynb file in the same folder.
  2. Open terminal in that folder.
  3. Run: jupyter notebook
  4. Open Medical_Equipment_Suppliers_Analysis.ipynb
  5. Kernel → Restart & Run All


## Notebook Structure
  Section 0  Imports
             pandas, numpy, matplotlib, scikit-learn only — no extra dependencies.

  Section 1  Data Loading & Feature Engineering
             tenure_years      : days since enrolment / 365.25
             supplies_count    : number of distinct supply types (pipe-delimited count)
             speciality_count  : number of speciality tags
             providertype_count: number of provider type tags
             is_pharmacy / is_optician / is_ortho / is_oxygen / is_grocery : binary flags
             state_encoded     : LabelEncoder on practicestate

  Q1  Feature Importance
      - RandomForestClassifier Gini importance
      - Permutation importance (more robust)
      - Acceptance rate by feature quintile
      - Acceptance rate by binary flag
      Top finding: supplies_count is the #1 predictor.

  Q2  Creative & Unusual Insights
      - Insight A: Grocery stores enrolled as Medicare equipment suppliers
      - Insight B: Tenure paradox — oldest suppliers accept assignment least often
      - Insight C: Supply breadth is a leading indicator of Medicare dependency
      - Insight D: State-level acceptance gap exceeds 40 percentage points

  Q3  Model Accuracy
      - Random Forest vs Logistic Regression (Pipeline + StandardScaler)
      - Metrics: Accuracy, Precision, Recall, F1, ROC-AUC
      - 5-fold Stratified Cross-Validation
      - ROC Curve + CV Boxplot + Confusion Matrix
      Top finding: Random Forest ROC-AUC ~ 0.72, stable across folds.

  Q4  Predictive Scenario — Post-CMS Reform Entrant Wave 2026
      - 7 hypothetical new supplier profiles scored by the trained model
      - Sensitivity analysis: startup supply tipping point (~16 supply types)
      Top finding: Pharmacies & broad-portfolio suppliers accept; niche startups decline.


## Reproducibility
  All models use random_state=42.
  Results are fully reproducible given the same library versions.


## Known Issue — NumPy Version Conflict
  Error: "A module compiled with NumPy 1.x cannot run in NumPy 2.x"
  Cause: Outdated Anaconda packages (matplotlib, gensim, numba) built against NumPy 1.x.

  Fix — create a clean environment:
    conda create -n analysis python=3.11
    conda activate analysis
    conda install numpy pandas matplotlib scikit-learn jupyter
    jupyter notebook

=====================================================
