# 🛒 Walmart Sales Forecasting — Time Series Analysis

An end-to-end time series forecasting project on Walmart retail sales data, featuring **ARIMA**, **SARIMAX**, and **Auto ARIMA** models with rich Exploratory Data Analysis (EDA) including seasonal decomposition, correlation analysis, and store performance benchmarking.

---

## 📌 Project Overview

This project analyzes weekly sales data across Walmart stores and builds time series forecasting models to predict future sales. The analysis incorporates external factors such as temperature, fuel price, CPI, unemployment rate, and holiday flags to build more accurate SARIMAX models.

---

## 🚀 Key Highlights

| Metric | Value |
|--------|-------|
| Dataset | Walmart Sales Dataset (`Walmart.csv`) |
| Focus Store | **Store 40** (primary analysis) |
| Time Series Models | **ARIMA**, **SARIMAX**, **Auto ARIMA** |
| Seasonal Period | **52 weeks** (annual seasonality) |
| Evaluation Metric | **RMSE** (Root Mean Squared Error) |
| Exogenous Variables | Temperature, Fuel Price, CPI, Unemployment, Holiday Flag |

---

## 🛠️ Tech Stack

| Category | Tools |
|----------|-------|
| Language | Python |
| Data Processing | Pandas, NumPy |
| Time Series | statsmodels (ARIMA, SARIMAX), pmdarima (Auto ARIMA) |
| Stationarity Test | ADF Test (Augmented Dickey-Fuller) |
| EDA & Visualization | Matplotlib, Seaborn |
| Decomposition | Seasonal Decompose (additive model) |
| Environment | Google Colab / Jupyter Notebook |

---

## 📂 Project Structure

```
Walmart_project/
│
├── Walmart_project.ipynb       # Main notebook — full pipeline
├── Walmart.csv                 # Weekly sales data across stores
└── README.md                   # Project documentation
```

---

## ⚙️ How It Works

### 1. Data Loading & Preprocessing
- Loaded Walmart retail data with columns: `Store`, `Date`, `Weekly_Sales`, `Temperature`, `Fuel_Price`, `CPI`, `Unemployment`, `Holiday_Flag`
- Parsed dates using `pd.to_datetime()` with format `%d-%m-%Y`
- Set `Date` as the DataFrame index for time series operations
- Checked for null values and duplicates — data was clean

### 2. Exploratory Data Analysis (EDA)
- **Time Series Visualization**: Plotted weekly sales for Store 40 to observe trends
- **Rolling Statistics**: 12-week rolling mean and standard deviation to visually assess stationarity
- **Stationarity Test**: Applied ADF (Augmented Dickey-Fuller) test — data confirmed stationary
- **Seasonal Decomposition**: Additive decomposition with 52-week period across all stores to extract trend, seasonality, and residuals
- **Correlation Analysis**:
  - Weekly Sales vs Unemployment (per-store correlation analysis)
  - Weekly Sales vs Temperature
  - Weekly Sales vs CPI
  - Full correlation heatmap across all numeric features
- **Holiday Impact**: Compared average weekly sales on holiday vs non-holiday weeks
- **Store Performance**: Ranked all stores by average weekly sales; identified top 5, best, and worst performing stores

### 3. ACF & PACF Analysis
- Plotted **ACF** and **PACF** on first-differenced series to identify optimal ARIMA parameters (p, d, q)

### 4. Train/Test Split
- 80% training, 20% testing split on Store 40's weekly sales data

### 5. Model 1 — ARIMA(1,0,2)
- Fitted ARIMA model on training data
- Generated predictions on test period using `typ='levels'`
- Visualized: Train vs Test vs Predicted sales

### 6. Model 2 — SARIMAX (without exogenous variables)
- Fitted SARIMAX with `order=(1,0,2)` and `seasonal_order=(1,1,1,52)`
- Captures annual seasonal patterns in weekly sales
- Visualized: Train vs Test vs SARIMA Predicted sales
- Evaluated: RMSE on test set

### 7. Model 3 — SARIMAX (with exogenous variables)
- Used **Temperature**, **Fuel Price**, **CPI**, **Unemployment**, and **Holiday Flag** as exogenous regressors
- Fitted full SARIMAX model incorporating external economic factors
- Generated forecasts on test period with matching exogenous test data
- Evaluated: RMSE on test set
- Visualized: Train vs Test vs SARIMAX Predicted sales

### 8. Model 4 — Auto ARIMA
- Used `pmdarima.auto_arima()` to automatically find the best ARIMA(p,d,q) order
- Generated 24-week future forecast (12 months ahead) using fitted SARIMAX results

---

## 📊 Pipeline Summary

```
Raw Data → Date Parsing → EDA (Rolling Stats, ADF Test, Decomposition)
        → Store 40 Isolation → Train/Test Split → ACF/PACF Analysis
        → ARIMA(1,0,2) → SARIMAX(1,0,2)(1,1,1,52) → SARIMAX + Exogenous
        → Auto ARIMA → 24-Week Future Forecast
```

---

## 📈 Key Findings

- Store 40's weekly sales are **stationary** (ADF test confirmed)
- Annual seasonality (52-week period) is clearly present in the data
- **Unemployment** shows negative correlation with weekly sales for most stores
- **Holiday weeks** generate higher average weekly sales than non-holiday weeks
- SARIMAX with exogenous variables provides richer forecasts by incorporating economic context

---

## 🔧 How to Run

```bash
# Clone the repository
git clone https://github.com/Durgeshkadiyapu/Walmart_project.git
cd Walmart_project

# Install dependencies
pip install pandas numpy matplotlib seaborn statsmodels pmdarima

# Launch the notebook
jupyter notebook Walmart_project.ipynb
```

> **Note:** The dataset (`Walmart.csv`) should be placed in the working directory or Google Drive if running on Colab.

---

## 🧠 What I Learned

- Time series stationarity testing with ADF and visual rolling statistics
- Seasonal decomposition to extract trend, seasonality, and residuals
- Building and comparing ARIMA, SARIMAX, and Auto ARIMA models
- Incorporating exogenous variables (economic factors) into time series forecasting
- RMSE-based evaluation of forecasting model performance
- Store-level performance benchmarking and correlation analysis

---

## 👤 Author

**Kadiyapu Durgesh Kumar**  
B.Tech CSE (AI & ML Minor) | VIT-AP University  
AI & Data Science Trainee | DRISHTI CPS, IIT Indore

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue)](https://linkedin.com/in/durgesh-kumar-37a46a31b)
[![GitHub](https://img.shields.io/badge/GitHub-Follow-black)](https://github.com/Durgeshkadiyapu)

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).
