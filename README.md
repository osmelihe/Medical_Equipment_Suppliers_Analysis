# Medical Equipment Suppliers — Analysis Project
# README v2
# =====================================================

## Overview
Exploratory and predictive analysis of the Medicare Medical Equipment Suppliers dataset.
58,191 supplier records | 17 columns | Source: CMS (Centers for Medicare & Medicaid Services)
Target variable: acceptsassignement (True/False)


## Files
  Medical-Equipment-Suppliers.csv                  Raw dataset
  https://data.cms.gov/provider-data/dataset/ct36-nrcq
  Medical_Equipment_Suppliers_v5.ipynb             Main analysis notebook (current version)


## Requirements
  Python       >= 3.9
  numpy        >= 2.0
  pandas
  matplotlib
  scikit-learn >= 1.3

  Install:
    pip install numpy pandas matplotlib scikit-learn

  Anaconda users (recommended — avoids NumPy version conflicts):
    conda create -n analysis python=3.11
    conda activate analysis
    conda install numpy pandas matplotlib scikit-learn jupyter


## How to Run
  1. Place Medical-Equipment-Suppliers.csv and the .ipynb in the same folder.
  2. Open terminal in that folder.
  3. Run: jupyter notebook
  4. Open Medical_Equipment_Suppliers_v2.ipynb
  5. Select kernel: Python (analysis)  ← important if using Anaconda
  6. Kernel → Restart & Run All


## Notebook Structure (CRISP-DM)

  This notebook follows the CRISP-DM methodology. Each phase is clearly labelled.

  Phase 0  Imports & Configuration

  Phase 1  Business Understanding
           Problem statement, success criteria, and the four analytical questions.

  Phase 2  Data Understanding
           Load dataset, inspect shape, column types, and value distributions.

  Phase 3  Data Preparation
           Feature engineering and missing value treatment.
           - tenure_years      : days since enrolment / 365.25
           - supplies_count    : pipe-delimited list count
           - speciality_count  : pipe-delimited list count
           - providertype_count: pipe-delimited list count
           - is_pharmacy / is_optician / is_ortho / is_oxygen / is_grocery : binary flags
           - state_encoded     : LabelEncoder on practicestate
           Missing value strategy documented with full justification per column.

  Phase 4  Modelling — Question 1
           What are the most important features and how do they drive the outcome?
           → Random Forest + Permutation Importance + quintile/flag charts
           → Conclusion: supplies_count is the #1 predictor

  Phase 5  Evaluation — Question 3
           How accurate is the model trained to predict the data?
           → RF vs Logistic Regression | ROC-AUC ~0.72 | 5-fold CV
           → Conclusion: stable, actionable accuracy; ceiling set by absent revenue data

  Phase 6  Deployment & Insights — Questions 2 & 4
           Q2: Unusual insights (grocery suppliers, tenure paradox, supply breadth, state gap)
           Q4: Predictive scenario — Post-CMS Reform Entrant Wave 2026
           → Startup tipping point: ~16 supply types


## Functions (with Docstrings)

  engineer_features(dataframe)
      Engineers all model-ready features from the raw dataframe.
      Parameters : dataframe (pd.DataFrame)
      Returns    : pd.DataFrame with 10 new columns

  evaluate_model(model, X_test, y_test, model_name)
      Evaluates a trained classifier and prints a metrics summary.
      Parameters : model, X_test, y_test, model_name (str)
      Returns    : dict with accuracy, precision, recall, f1, roc_auc

  score_supplier_profile(model, features, profile_dict)
      Scores a single hypothetical supplier profile.
      Parameters : model, features (list), profile_dict (dict)
      Returns    : dict with probability, prediction, label
      Raises     : ValueError if features are missing from profile_dict


## Reproducibility
  All models use random_state=42.
  Results are fully reproducible given the same library versions.


## Known Issue — NumPy Version Conflict
  Error: "A module compiled with NumPy 1.x cannot run in NumPy 2.x"
  Cause: Anaconda base environment packages built against NumPy 1.x.

  Fix — use a clean conda environment:
    conda create -n analysis python=3.11
    conda activate analysis
    conda install numpy pandas matplotlib scikit-learn jupyter
    jupyter notebook

  After Jupyter opens, select kernel "Python (analysis)" in the top-right corner.

=====================================================

