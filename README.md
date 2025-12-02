# Electricity Load Forecasting — Final Project Summary

This repository contains the full progress and results for our CS 4347 project on forecasting household electricity consumption using the **OpenML Electricity Load Diagrams (2011–2014)** dataset. The dataset contains over 105,000 timestamped observations and 316 smart-meter features.

## Team Members and Roles
- **Sebika Khulal** — Data cleaning, full EDA, baseline Linear Regression, normalization  
- **Ananta Aryal** — Feature engineering, cyclical encodings, forecasting preparation  
- **Anubhav Bhetuwal** — Dimensionality reduction (SRP), Ridge/Lasso tuning, XGBoost improvement model  

---

## Dataset
- **Source:** OpenML dataset #46214  
- **Rows:** 105,217  
- **Features:** 319 total  
  - 316 smart-meter readings (`value_0`–`value_315`)  
  - Timestamp, series ID, time index  
- No missing numerical values  
- Heavy right-skew across all meters  
- Cleaned dataset saved as `cleaned_data.pkl`

---

## EDA Summary

### Distribution Patterns
- All meter readings show strong right-skew.
- Frequent zeros (low consumption periods) and rare spikes (high-usage events).

### Correlation Structure
- Target meter `value_0` has **very weak correlations** with other meters (< 0.22).
- Indicates limited usability of pure linear relationships.

### Nonlinear Structure
- Scatterplots reveal curved and banded shapes.
- Confirms presence of nonlinear interactions and heteroskedasticity.

### Modeling Implications
- Normalization is required due to large variance differences.
- Dimensionality reduction helps control noise in high dimensions.
- Nonlinear models (tree-based, boosting) are expected to outperform linear
