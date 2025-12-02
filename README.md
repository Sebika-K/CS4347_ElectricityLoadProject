
---

## 📊 Dataset

- **Source:** OpenML #46214  
- **Rows:** 105,217  
- **Features:** 319  
  - 316 numeric smart-meter readings  
  - timestamp, id_series, time_step  
- **Missing values:** None  
- **Properties:**  
  - High-dimensional  
  - Strong right-skew  
  - Weak pairwise correlations  

---

## 🔍 Exploratory Data Analysis (EDA)

Key findings:

### **Distribution**
- All meter features show strong right-skew.
- Many zeros (periods of low consumption).
- Rare spikes represent unusual high-usage events.

### **Correlation**
- `value_0` has **no strong correlation** with any other feature (< 0.22).
- Confirms that **linear models will struggle**.

### **Scatterplots**
- Show nonlinear, banded patterns.
- Indicates strong nonlinear structure across meters.

### **Implications**
- Normalization required  
- Dimensionality reduction helps  
- Nonlinear models (e.g., XGBoost) expected to outperform linear models  

---

## 🤖 Models and Results

### **Baseline Model: Linear Regression**
- Split: 80/20 chronological  
- RMSE: **7.33**  
- Underfits due to:
  - Weak correlations  
  - High nonlinearity  
  - Very high dimension  

---

### **Improved Models**

| Model | RMSE | Notes |
|-------|------|-------|
| **Ridge Regression** | ~7.33 | Scaling helps stability but not accuracy |
| **Lasso Regression** | **6.35** | Removes noisy features, good improvement |
| **SRP + XGBoost** | **6.42** | Best nonlinear model; robust to skew |

**Best overall model:**  
✔ **Lasso Regression (RMSE ≈ 6.35)**  
✔ XGBoost (RMSE ≈ 6.42) close behind but slower and heavier

---

## 🧪 Final Comparison Plot

A bar chart comparing Baseline, Ridge, Lasso, and XGBoost RMSE values is included in the report.  

This confirms:
- Linear models perform poorly  
- Regularization helps  
- Nonlinear + dimensionality reduction gives the strongest improvements  

---

## 🧠 Contributions

### **Sebika Khulal**
- Loaded & cleaned dataset  
- Full EDA (histograms, correlations, scatterplots)  
- Baseline model  
- Normalization pipeline  

### **Ananta Aryal**
- Feature engineering  
- Time-based feature creation  
- Forecasting preparation  

### **Anubhav Bhetuwal**
- SRP dimensionality reduction  
- Ridge and Lasso tuning  
- XGBoost modeling and final evaluation  

---

## 📌 Future Work
- Add lagged features (t-1, t-24, etc)  
- Build multi-step forecasting models  
- Evaluate advanced methods (LSTM, Temporal Convnets)  
- Create a full dashboard for consumption analytics  

---

## 📄 License
This project is completed for academic purposes as part of **CS 4347 — Introduction to Machine Learning** at Texas State University.

