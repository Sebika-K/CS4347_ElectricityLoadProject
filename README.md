# Electricity Load Forecasting

This project applies machine learning methods to model and forecast household electricity consumption using the OpenML Electricity Load Diagrams 2011–2014 dataset. The dataset contains over 105,000 observations with 316 meter readings collected at uniform time intervals.

## Project Overview
The objective is to predict the target meter value (value_0) based on the readings of the remaining meters. The task involves high dimensionality, skewed distributions across features, and weak linear relationships, making it a suitable case for regularized and nonlinear models.

The project includes data cleaning, exploratory data analysis, baseline modeling, regularized regression methods, dimensionality reduction, and nonlinear modeling with XGBoost.

## Authors
Sebika Khulal  
Ananta Aryal  
Anubhav Bhetuwal

## Dataset
Source: OpenML dataset 46214  
Rows: 105,217  
Features: 319  
Includes 316 numeric meter readings plus timestamp, id_series, and time index.  
The dataset contains no missing numerical values but exhibits large variation in scales, right-skewed distributions, and nonlinear patterns.

Dataset link: https://www.openml.org/d/46214


## Structure

```text
CS4347_ElectricityLoadProject/
│
├── data/                     # Raw and cleaned data
│   ├── electricity.csv
│   └── cleaned_data.pkl
│
├── notebooks/
│   ├── download_dataset.ipynb
│   ├── 01_load_clean_data.ipynb
│   ├── 01_EDA.ipynb
│   ├── 02_baseline_model.ipynb
│   ├── 03_hyperparameter_tuning.ipynb
│   ├── 04_time_series_forecasting.ipynb
│   ├── 05_normalization_analysis.ipynb
│   └── FinalReport.ipynb
│
├── report/
│   └── FinalReport.pdf
│
├── results/
│   ├── baseline_results.json
│   ├── ridge_results.json
│   ├── lasso_results.json
│   ├── gbr_results.json
│   └── xgb_results.json
│
├── README.md
└── requirements.txt

```

Additional resources:

- Final report PDF: report/FinalReport.pdf

- Main notebook: notebooks/FinalReport.ipynb
## Exploratory Data Analysis
Main findings:

- Strong right-skew across all meter readings.
- Many features contain long stretches of zeros, indicating sparse consumption.
- Pairwise correlations with the target are weak (maximum below 0.22).
- Scatterplots show banding caused by repeated meter readings and nonlinear relationships.
- The magnitude differences across features justify feature normalization.
- Weak linear structure implies that linear models will underperform, motivating the use of nonlinear and dimensionality reduction methods.

## Modeling

### Normalization

Feature normalization was applied using StandardScaler to address the large scale imbalance across meter readings. This ensured that features with large magnitudes did not dominate the model during training.

### Baseline: Linear Regression
Chronological 80/20 split without shuffling.  
RMSE: approximately 7.33  

Linear regression underperforms because correlations with the target are weak, feature distributions are skewed, and the data exhibits nonlinear structure.

### Regularized Models
Ridge Regression  
RMSE: approximately 7.33  

Lasso Regression  
RMSE: approximately 6.35  

Lasso improves performance by removing noisy or irrelevant features in the high-dimensional setting.

### Dimensionality Reduction + Nonlinear Model
Sparse Random Projection (316 → 50 components)  
XGBoost trained on SRP outputs  
Test RMSE: approximately 6.42  

SRP reduces dimensionality efficiently while approximately preserving distances.  
XGBoost handles nonlinearity and interactions, resulting in strong performance.

## Model Comparison
| Model | RMSE |
|-------|-------|
| Linear Regression | ~7.33 |
| Ridge Regression | ~7.33 |
| Lasso Regression | ~6.35 |
| SRP + XGBoost | ~6.42 |

Lasso achieves the best overall RMSE.  
XGBoost performs slightly worse but remains competitive and better suited for nonlinear structure.

## Future Work
- Introduce lag features for true forecasting (t−1, t−24, etc.).
- Add cyclical encodings for hour and day.
- Build multi-step forecasting models.
- Explore more advanced nonlinear models.

## How to Run

Install dependencies:

```bash
pip install -r requirements.txt
```

Then open the main notebook:

```bash
jupyter notebook notebooks/FinalReport.ipynb
```

## Notes
This project was completed as part of CS 4347, Introduction to Machine Learning, at Texas State University.
