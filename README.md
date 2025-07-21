
🧠 Quantitative Volatility Modeling Using ARCH, GARCH & EWMA
This repository contains a detailed implementation of volatility forecasting techniques used in quantitative finance. The models used are:

ARCH (Autoregressive Conditional Heteroskedasticity)

GARCH (Generalized ARCH)

EWMA (Exponentially Weighted Moving Average)

You’ll also find real vs. predicted volatility comparison, full Python code (in Jupyter Notebook), and step-by-step implementation.

📁 Files Included
File Name	Description
volatilitymodeling.ipynb	Main Jupyter Notebook implementing ARCH, GARCH, and EWMA models on JPMorgan stock data

📌 Table of Contents

##Project Objective

Data Source

ARCH Model

GARCH Model

EWMA Model

## 📊 Project Objective

To model and forecast the volatility of JPMorgan Chase (JPM) stock returns using time-series econometric techniques, and to compare predicted volatility with actual realized market volatility.

---

## 🔹 Data Source

Two data sources are used for price information:

* **Yahoo Finance** via the `yfinance` Python API
* **Alpha Vantage API** (free key used)

**Date Range:** 2015-01-01 to 2025-01-01
**Stock Ticker:** JPM (JPMorgan Chase)

---

## 🔄 ARCH Model

### ✅ What is ARCH?

The ARCH (1) model assumes that today's volatility depends on the **squared return from the previous day**.

### ⚖️ Formula:

$\sigma^2_t = \omega + \alpha_1 r_{t-1}^2$

Where:

* $\omega$ is the long-term base level of variance
* $\alpha_1$ is the coefficient on yesterday's squared return

### ⚙️ Steps:

1. Calculate daily returns
2. Fit ARCH(1) using `arch_model` from the `arch` package
3. Forecast 5-day ahead variance
4. Convert to volatility (sqrt of variance)
5. Compare with 5-day realized volatility

### 📊 Example Result:

```
Predicted Volatility (5-day): ~1.56%
Realized Volatility (5-day): ~1.69%
```

---

## 🔄 GARCH Model

### ✅ What is GARCH?

The GARCH(1,1) model extends ARCH by including past variance in addition to past squared returns. It captures **volatility clustering** better than ARCH.

### ⚖️ Formula:

$\sigma^2_t = \omega + \alpha_1 r_{t-1}^2 + \beta_1 \sigma^2_{t-1}$

Where:

* $\omega$: base variance
* $\alpha_1$: impact of last return shock
* $\beta_1$: impact of past variance

### ⚙️ Steps:

1. Calculate daily returns
2. Fit GARCH(1,1) using `arch_model`
3. Forecast 5-day volatility horizon
4. Compare with actual volatility of that period

### 📊 Example Result:

```
Predicted Volatility (5-day): ~1.62%
Realized Volatility (5-day): ~1.69%
```

---

## 🔄 EWMA Model

### ✅ What is EWMA?

EWMA estimates volatility by assigning **exponentially decreasing weights to past squared returns**. It's widely used due to its simplicity and responsiveness to recent data.

### ⚖️ Formula:

$\sigma^2_t = \lambda \cdot \sigma^2_{t-1} + (1 - \lambda) \cdot r^2_{t-1}$

Where:

* $\lambda$: decay factor (commonly 0.94 for daily data)
* $r^2_{t-1}$: squared return from previous day
* $\sigma^2_{t-1}$: previous day’s variance

### ⚙️ Steps:

1. Set lambda value (e.g. 0.94)
2. Calculate variance recursively from return series
3. Take square root to get volatility
4. Forecast is **only for 1 day ahead**

### 📊 Example Result:

```
Predicted Volatility (2025-01-02): 0.14
Realized Return (absolute): 0.12
```

Note: Since it's a 1-day forecast, we compare to **absolute return** instead of standard deviation.

---

## 👀 Realized vs Predicted Volatility

* **Predicted Volatility:** Output of ARCH/GARCH/EWMA model
* **Realized Volatility:**

  * For ARCH/GARCH: std deviation of next 5 daily returns (annualized)
  * For EWMA: abs(return on next day)

This comparison helps evaluate **model accuracy** in practical terms.

---

## 📚 Libraries Used

* `pandas`
* `numpy`
* `yfinance`
* `arch`
* `matplotlib`
* `requests`

---

## 🔧 How to Run

1. Install required libraries:

```bash
pip install yfinance arch pandas numpy matplotlib
```

2. Open `volatilitymodeling.ipynb` in Jupyter or VS Code
3. Run all cells

---

## 🚀 Conclusion

This project demonstrates how to:

* Apply volatility models on real-world stock data
* Compare predicted vs actual market movements
* Understand the dynamics of conditional heteroskedasticity in finance

Useful for:

* Quantitative finance enthusiasts
* Students of econometrics
* Risk analysts and traders

---

Feel free to fork, star, or contribute!



