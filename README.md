# 📈 Rossmann Store Sales Forecasting (Capstone Project)

## 🔍 Project Overview

Rossmann is a large European drugstore chain operating over 3,000 stores across multiple countries.  
Accurate sales forecasting is critical due to the short shelf life of many products and the operational impact of over- or under-stocking.

In this project, we build a **robust daily sales forecasting system** for selected key Rossmann stores using historical sales data, promotional information, and customer footfall.

The goal is to **forecast daily sales for the next 6 weeks (42 days)** with high accuracy and strong business interpretability.

---

## 🎯 Business Objectives

- Forecast daily sales for individual Rossmann stores
- Understand the impact of:
  - Customer footfall
  - Promotions
  - Temporal patterns
- Compare classical time-series and machine-learning approaches
- Evaluate performance using **MAPE (Mean Absolute Percentage Error)**

---

## 📊 Dataset Description

The project uses two datasets:

### `train.csv`
Daily store-level sales data:
- `Store`
- `Date`
- `Sales`
- `Customers`
- `Promo`
- `Promo2`
- `StateHoliday`
- `SchoolHoliday`
- `Open`

### `store.csv`
Store metadata:
- `StoreType`
- `Assortment`
- `CompetitionDistance`
- `Promo2SinceYear`
- `PromoInterval`

**Scope**:  
The analysis focuses on **key high-value stores** (e.g., Store 1, 3, 8, 9, 13, 25, 29, 31, 46).

---

## 🧠 Approach & Methodology

### 1️⃣ Exploratory Data Analysis (EDA)
- Univariate analysis of Sales and Customers
- Bivariate analysis:
  - Customers vs Sales
  - Promo vs Sales
- Correlation heatmaps
- Outlier treatment (99th percentile)

### 2️⃣ Time-Series Analysis
- Stationarity testing using **ADF test**
- Differencing to ensure stationarity
- Cointegration testing using **Johansen Test**

> VAR modeling was explored but abandoned due to numerical instability caused by strong deterministic relationships between Sales and Customers — a known limitation in retail datasets.

---

## 🔄 Model Pivot Strategy

Given the instability of VAR, the modeling approach was pivoted to:

### ✅ SARIMAX (Primary Model)
- Captures temporal structure
- Incorporates external drivers:
  - Customers
  - Promotions
- Highly interpretable
- Stable and production-ready

### ✅ XGBoost (Benchmark Model)
- Lag-based feature engineering
- Captures non-linear patterns
- Used for accuracy comparison

---

## 🤖 Models Implemented

### SARIMAX
- Configuration: `SARIMAX(1,1,1)`
- Exogenous variables:
  - Customers
  - Promo
- Diagnostics:
  - No residual autocorrelation
  - Stable variance
  - Strong statistical significance

### XGBoost
- Lag features: 1, 7, 14 days
- Calendar features:
  - Day of Week
  - Month
- Gradient-boosted regression trees

---

## 📏 Model Evaluation

Evaluation was performed on a **time-based holdout set (last 42 days)**.

| Model     | MAPE |
|----------|------|
| SARIMAX  | **4.25%** |
| XGBoost  | **4.01%** |

✅ Both models achieved **excellent forecasting accuracy (<5%)**.

---

## 📈 Forecast Visualization

The final comparison plot shows:
- Actual sales
- SARIMAX forecast (smooth & interpretable)
- XGBoost forecast (sharper, reactive)

Shaded error regions and demand spike annotations were added to improve interpretability and business storytelling.

---

## 🏆 Final Model Selection

Although XGBoost marginally outperformed SARIMAX in terms of raw accuracy, **SARIMAX was selected as the final model** due to:

- Comparable accuracy
- Superior interpretability
- Clear linkage to business drivers
- Easier explainability for stakeholders

XGBoost is retained as a **high-performing benchmark**.

---

## 🛠️ Tech Stack

- **Python**
- **Pandas / NumPy**
- **Matplotlib / Seaborn**
- **Statsmodels**
- **XGBoost**
- **Scikit-learn**
- **Google Colab**

---

## 📁 Project Structure
├── data/
│ ├── train.csv
│ ├── store.csv
├── notebooks/
│ └── Rossmann_Sales_Forecasting.ipynb
├── README.md


---

## 🚀 Key Takeaways

- Customer footfall is the strongest driver of sales
- Promotions provide consistent short-term uplift
- Retail sales forecasting benefits from combining:
  - Time-series models (SARIMAX)
  - Machine-learning models (XGBoost)
- Model selection should balance **accuracy + interpretability**

---

## 📌 Future Enhancements

- Incorporate holiday calendars explicitly
- Extend to multi-store hierarchical forecasting
- Add probabilistic forecasts (confidence intervals)
- Deploy as an automated forecasting pipeline

---

## 👤 Author

**Nitish Narayanan**  
Solution Engineering Chapter Lead @Infobip | AI & Data Science Enthusiast  

---

⭐ If you found this project useful, feel free to star the repository!

