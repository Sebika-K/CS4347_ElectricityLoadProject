# Electricity Load Forecasting — Project Progress Report

This repository contains the progress for our CS 4347 project on modeling and forecasting household electricity consumption using the OpenML Electricity Load Diagrams (2011–2014) dataset. The dataset includes 105,000+ rows and 316 smart-meter features.

## Team Members & Roles
- **Sebika Khulal** — Data cleaning, full EDA, baseline Linear Regression, normalization pipeline  
- **Ananta Aryal** — Feature engineering, cyclical features, forecasting preparation  
- **Anubhav Bhetuwal** — Dimensionality reduction (SRP), Ridge tuning, Gradient Boosting improvement model  

## Dataset
- **Source:** OpenML #46214  
- **Rows:** 105,217  
- **Features:** 319 (value_0–value_315, timestamp, meter ID, time index)  
- No missing numeric values; highly skewed distributions; >33M numeric entries total.  
- Cleaned dataset stored as `cleaned_data.pkl`.

## EDA Summary
- Strong right-skew across all meter readings  
- Very weak linear correlations with target (`< 0.22`)  
- Scatterplots show nonlinear, banded structure  
- High variance across features → normalization required  
- Confirms need for nonlinear models and dimensionality reduction

## Baseline Model
- **Model:** Linear Regression  
- **Split:** 80/20 chronological (shuffle=False)  
- **RMSE:** 7.96  
- Underfitting due to nonlinear relationships and high dimensionality

## Normalization
- StandardScaler used (fit on train only)  
- Scaling does not change Linear Regression RMSE (OLS-invariant)  
- Required for Ridge, Lasso, SRP, and Gradient Boosting models

## Improvement Model: SRP + Gradient Boosting
- **SRP:** Reduced 316 → 50 components  
- **GBR RMSE:** 6.85 (significant improvement over baseline)  
- Nonlinear modeling handles skewness and weak correlations effectively

## Upcoming Work (Forecasting)
- Create lag features (t−1, t−2, t−24)  
- Add cyclical encodings (hour/day)  
- Build baseline + improved forecasting models  
- Compare forecasting RMSE

## Next Steps
- Complete Ridge/Lasso/GBR tuning  
- Finalize SRP dimensionality  
- Build forecasting pipeline  
- Prepare final comparison tables, slides, and report
