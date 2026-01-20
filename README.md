# Time Series Analysis of the S&P 500

This project presents an ARIMA-based time series analysis of daily S&P 500 log returns using R. The objective is to assess short-term predictability in equity index returns through classical time series techniques, including stationarity testing, model identification, diagnostic checking, and out-of-sample forecasting.

The work was completed as part of an MSc-level time series analysis module and is presented here for portfolio purposes.

---

## Overview

Daily adjusted closing prices of the S&P 500 index were retrieved from Yahoo Finance and transformed into log returns. Log returns are approximately stationary, stabilise variance, and are suitable for ARIMA modelling. The dataset was split into a training period (2010–2022) and a test period (2023–2025) for forecast evaluation.

The analysis follows the standard Box–Jenkins methodology:
1. Stationarity testing
2. Model identification using ACF/PACF
3. Model estimation and comparison
4. Residual diagnostics
5. Out-of-sample forecasting and performance evaluation

---

## Methodology

### Data Transformation
- Adjusted closing prices were used to account for dividends and splits.
- Prices were transformed into daily log returns to achieve stationarity and interpretability.

### Stationarity Tests
- Augmented Dickey–Fuller (ADF) tests reject the presence of a unit root.
- KPSS tests fail to reject level stationarity.
- Together, these confirm that log returns are stationary, justifying an ARMA (ARIMA with d = 0) framework.

### Model Identification
- Sample ACF and PACF show very weak serial dependence, typical of daily financial returns.
- A grid search over low-order ARIMA(p,0,q) models (p,q ∈ {0,1,2}) was performed.
- Models were compared using AIC and BIC.

### Model Selection
- ARIMA(0,0,2) was selected as the preferred specification.
- Although `auto.arima()` selected ARIMA(4,0,0), the improvement in AIC was marginal and not supported by the ACF/PACF.
- BIC and parsimony favoured ARIMA(0,0,2).

### Residual Diagnostics
- Residuals fluctuate around zero with no visible autocorrelation.
- Ljung–Box tests reject the null due to the large sample size, but residual correlations are practically negligible.
- Shapiro–Wilk tests reject normality, consistent with heavy-tailed financial returns.
- Overall, residuals behave approximately as white noise.

### Forecasting and Evaluation
- Models were refitted on the training set and evaluated on the test period.
- Forecast accuracy (RMSE and MAE) was nearly identical across models.
- A Diebold–Mariano test showed no statistically significant difference in predictive accuracy.
- Forecasts revert quickly to the unconditional mean, consistent with the efficient market hypothesis.

---

## Key Results

- Daily S&P 500 returns exhibit minimal short-term predictability.
- Simple, parsimonious ARIMA models perform as well as more complex alternatives.
- ARIMA(0,0,2) provides an adequate and interpretable representation of return dynamics.
- Forecast performance is comparable to a naïve zero-return benchmark.

---

## Technologies Used

- **R**
- **quantmod** – data retrieval
- **forecast** – ARIMA modelling and forecasting
- **tseries / urca** – stationarity testing
- **Jupyter Notebook (R kernel)** for reproducible analysis and visualisation

---

## Notes

This project focuses on modelling the conditional mean of returns. Volatility clustering and heavy tails suggest that extensions such as GARCH models could be explored for variance dynamics, but these are beyond the scope of this analysis.

---

## Author

Ali Butt  
MSc Data Science  
BEng Software Engineering
