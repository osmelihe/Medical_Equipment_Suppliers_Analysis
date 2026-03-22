# Medical Equipment Suppliers — Analysis Project
# README
# =====================================================

## Overview
Exploratory and predictive analysis of the Medicare Medical Equipment Suppliers dataset.
58,191 supplier records | 17 columns | Source: CMS (Centers for Medicare & Medicaid Services)

## Dataset: Medical-Equipment-Suppliers.csv
Key columns:
  - provider_id              Unique supplier identifier
  - acceptsassignement       TARGET — whether supplier accepts Medicare assignment (True/False)
  - participationbegindate   Programme enrolment date
  - practicestate            US state (2-letter code)
  - specialitieslist         Pipe-delimited speciality tags
  - providertypelist         Pipe-delimited provider type tags
  - supplieslist             Pipe-delimited list of supplied products
  - latitude / longitude     Geographic coordinates

## Notebook: Medical_Equipment_Suppliers_Analysis.ipynb
Answers four analytical questions:

  Q1 — Feature Importance
       Which features matter most and how do they drive assignment acceptance?
       → supplies_count is the #1 predictor; followed by tenure, geography, and pharmacy flag.

  Q2 — Creative Insights
       Four non-obvious findings:
         A. Grocery stores are enrolled as Medicare medical equipment suppliers.
         B. Tenure paradox — oldest suppliers accept assignment least often.
         C. Supply breadth is a leading indicator of Medicare dependency.
         D. State-level acceptance gap exceeds 40 percentage points.

  Q3 — Model Accuracy
       Random Forest vs. Logistic Regression, validated with 5-fold cross-validation.
       → Random Forest ROC-AUC ≈ 0.72 (stable across folds).

  Q4 — Predictive Scenario
       7 hypothetical 2026 entrant profiles scored by the trained model.
       → Pharmacies & broad-portfolio suppliers accept; niche startups decline.
       → Startup tipping point: ~16–18 supply types triggers assignment acceptance.

## Requirements
  Python  >= 3.9
  pandas, numpy, matplotlib, seaborn
  scikit-learn >= 1.2

  Install: pip install pandas numpy matplotlib seaborn scikit-learn

## Usage
  1. Place Medical-Equipment-Suppliers.csv in the same folder as the notebook.
  2. Open Medical_Equipment_Suppliers_Analysis.ipynb in Jupyter or VS Code.
  3. Run All Cells (Kernel → Restart & Run All).

## Notes
  - All visualisations are generated inline within the notebook.
  - Random seed is fixed (random_state=42) for full reproducibility.
  - is_contracted_for_cba column is all-False and excluded from modelling.

=====================================================
