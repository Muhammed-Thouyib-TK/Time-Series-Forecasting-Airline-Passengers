# ✈️ Time Series Forecasting — Airline Passengers

## Overview
This notebook implements classical time-series forecasting experiments on the **AirPassengers** dataset (Jan 1949 — Dec 1960). The goal is to compare different forecasting approaches and identify which methods best capture trend and seasonality for monthly passenger counts.

---

## What I did (exact steps implemented)
1. **Data loading**
   - Loaded CSV from `https://raw.githubusercontent.com/jbrownlee/Datasets/master/airline-passengers.csv`.
   - Converted `Month` to `DatetimeIndex`.

2. **Exploratory Data Analysis (EDA)**
   - Time-series plot of passengers.
   - Lag plots for lags = 3, 10, 50, 100.
   - AutoCorrelation Function (ACF) for nlags = 10, 50, 100.

3. **Train/Test split**
   - `train = df[:-12]`; `test = df[-12:]`.

4. **Baseline & simple models**
   - Naïve forecast (repeat last train value).
   - Moving Average forecasts (window = 3, 12).
   - Simple Exponential Smoothing (SimpleExpSmoothing).

5. **AutoRegressive models**
   - `AutoReg` fitted with various lag settings (lags=10, 12, 24). Forecasted the test period and plotted results. Also used to produce extended forecasts.

6. **ARIMA / SARIMA**
   - Fitted ARIMA (example `order=(2,1,1)`), printed AIC.
   - Grid search across ARIMA orders to minimize AIC — **best_order printed: (3,1,3)** with best AIC = `1214.9100602856486`.
   - Fitted ARIMA with best order; forecasted test window.
   - Fitted SARIMAX with `seasonal_order=(3,1,3,6)` and `(3,1,3,12)` and forecasted.

7. **Evaluation**
   - RMSE (using `sklearn.metrics.root_mean_squared_error`) reported for each model.

---

## Results (test RMSE — as computed in the notebook)
| Model / config                               | Test RMSE |
|---------------------------------------------:|----------:|
| Naïve                                        |    102.98 |
| Moving Average (window=3)                    |     88.84 |
| Moving Average (window=12)                   |     74.43 |
| SimpleExpSmoothing                           |    102.98 |
| AutoReg (lags=12)                            |     17.49 |
| AutoReg (lags=24)                            |     14.04 |
| ARIMA (best_order = (3,1,3))                 |     58.31 |
| SARIMAX (seasonal_order=(3,1,3,6))           |     26.95 |
| SARIMAX (seasonal_order=(3,1,3,12))          |     15.03 |

**Best result in this notebook:** `AutoReg(lags=24)` → RMSE **14.04**.

---

## Plots included
- Passenger time-series plot.  
- Lag plots (3 / 10 / 50 / 100).  
- ACF charts.  
- Forecast vs Actual figures for each model (Naïve, MA, SimpleExp, AutoReg, ARIMA, SARIMAX).  
- Extended AutoReg forecasts (future dates beyond test).

---

## Libraries used
- pandas, matplotlib, warnings  
- statsmodels: `AutoReg`, `SimpleExpSmoothing`, `ARIMA`, `SARIMAX`  
- scikit-learn: `root_mean_squared_error` (for RMSE)
