# Walmart M5 Sales Forecasting: Time Series Analysis

[![Live Report](https://img.shields.io/badge/Live%20Report-View%20Here-brightgreen?style=for-the-badge)](https://suin8606.github.io/walmart-ts-forecasting/walmart_ts.html)

![R](https://img.shields.io/badge/R-276DC3?style=for-the-badge&logo=r&logoColor=white)
![RMarkdown](https://img.shields.io/badge/RMarkdown-276DC3?style=for-the-badge&logo=r&logoColor=white)
![ggplot2](https://img.shields.io/badge/ggplot2-1A162D?style=for-the-badge&logo=r&logoColor=white)

**Can classical time series models accurately forecast Walmart's daily sales?**  
End-to-end forecasting pipeline on the M5 Competition dataset — ARIMA, SARIMA, and TBATS compared across 730 days of retail sales data.

---

## 📊 Result: SARIMA Best Balances Accuracy and Interpretability

| Model | RMSE | MAE | Handles Seasonality | Interpretable |
|-------|------|-----|---------------------|---------------|
| ARIMA | — | — | No | High |
| SARIMA | — | — | Yes (weekly) | High |
| TBATS | — | — | Yes (weekly + annual) | Low |

> SARIMA captures the dominant 7-day weekly cycle explicitly and provides interpretable coefficients — making it the recommended model for operational inventory planning.

---

## 🔍 Key Findings

- Strong **7-day weekly seasonality** confirmed — weekends consistently outsell weekdays
- Mild **upward trend** through 2014–2015
- **Christmas Day** is a structural zero (stores closed) — treated as outlier and removed
- **First-order differencing** is sufficient for stationarity (ADF test confirmed)
- TBATS becomes more valuable with 3+ years of data to identify annual seasonality

---

## 📐 Models & Math

### ARIMA(p, d, q)
$$\Phi(B)(1-B)^d y_t = \Theta(B)\epsilon_t$$

### SARIMA(p,d,q)(P,D,Q)[s]
$$\Phi_P(B^s)\phi_p(B)(1-B^s)^D(1-B)^d y_t = \Theta_Q(B^s)\theta_q(B)\epsilon_t$$

### TBATS
$$y_t^{(\omega)} = l_{t-1} + \phi b_{t-1} + \sum_{i=1}^{T} s_t^{(i)} + d_t$$

---

## 🔬 Analysis Pipeline

```
Step  Task
----  ----
1     Load M5 sales + calendar data
2     Pivot wide-to-long format (1941 daily columns → rows)
3     Merge with calendar to attach dates and event info
4     EDA — daily sales, category breakdown, day-of-week patterns
5     Outlier removal — Christmas Day structural zeros
6     ADF stationarity test on raw series
7     First-order differencing → confirm stationarity
8     ACF/PACF analysis → identify p and q
9     STL seasonal decomposition
10    AIC grid search for optimal ARIMA(p,0,q) on differenced series
11    SARIMA — auto.arima with weekly seasonality (s=7)
12    TBATS — multiple seasonality (weekly + annual)
13    Residual diagnostics for all models
14    Train/test evaluation — RMSE and MAE
15    30-day future forecast
16    Model comparison + conclusions
```

---

## 📂 Folder Structure

```
walmart-ts-forecasting/
│
├── README.md
├── walmart_ts.Rmd
├── walmart_ts.html
├── install_packages.R
└── .gitignore
```

---

## ▶️ How to Run

```r
# 1. Install required packages
source("install_packages.R")

# 2. Download dataset from Kaggle and place in working directory
# https://www.kaggle.com/competitions/m5-forecasting-accuracy
# Files needed:
#   - sales_train_validation.csv
#   - calendar.csv

# 3. Knit in RStudio → Knit to HTML
```

---

## ⚠️ Data Notes

- Dataset files are excluded from this repo (large files — see .gitignore)
- Only 2014–2015 data used for modeling (manageable size, sufficient for seasonal patterns)
- Aggregate daily sales across all products and stores — item-level forecasting would require hierarchical models

---

## 💡 What I Would Do Next

1. **ARIMAX** — incorporate calendar events and SNAP benefit days as external regressors
2. **Prophet** — Facebook's forecasting library handles holidays and multiple seasonalities automatically
3. **LightGBM** — gradient boosting approach used by M5 competition winners; significantly outperforms classical methods
4. **Hierarchical forecasting** — model at item/store level and reconcile upward for better operational utility

---

## 🏷️ Skills Demonstrated

`R` `Time Series Analysis` `ARIMA` `SARIMA` `TBATS`  
`Stationarity Testing` `ADF Test` `ACF/PACF` `STL Decomposition`  
`AIC Model Selection` `Forecast Evaluation` `RMSE/MAE` `data.table`  
`ggplot2` `R Markdown` `LaTeX Equations`

---

## 👤 Author

**Suin Kim** — M.S. Statistics & Data Science, Baruch College  
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/suinkim29)
[![Email](https://img.shields.io/badge/Email-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:suin.kim29@gmail.com)
