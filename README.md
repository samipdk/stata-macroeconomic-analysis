# Equity Markets and Inflation Dynamics
### A VAR and Granger Causality Analysis of DJIA and CPI (2000–2025)

> **Course:** ECON 803 — Quantitative Analysis of Business Conditions and Forecasting  
> **Institution:** Wichita State University | May 2025  
> **Authors:** Samip K. Thakuri · Shimriya Pyakurel · Labesh Raj Giri  
> **Instructor:** Dr. Xiaoyang Zhu  

---

## Overview

This study investigates the dynamic relationship between U.S. equity market performance and consumer inflation, examining whether movements in the **Dow Jones Industrial Average (DJIA)** can forecast changes in the **Consumer Price Index (CPI)**, and vice versa.

Using monthly data from **January 2000 to March 2025**, the analysis spans major macroeconomic episodes including the 2008 Global Financial Crisis, the COVID-19 pandemic shock, and the post-pandemic inflationary surge. A time series econometric framework is employed — including unit root testing, Granger causality analysis, Vector Autoregression (VAR) modeling, and Impulse Response Functions (IRFs) — to uncover the directional predictive relationships between equity markets and inflation.

---

## Research Questions

1. Do equity market movements help forecast U.S. consumer inflation?
2. Does consumer inflation help forecast the Dow Jones Industrial Average?

---

## Data

| Variable | Source | Frequency | Period |
|----------|--------|-----------|--------|
| Dow Jones Industrial Average (DJIA) | Yahoo Finance | Monthly | Jan 2000 – Mar 2025 |
| Consumer Price Index (CPI, All Urban Consumers) | FRED, Federal Reserve Bank of St. Louis | Monthly | Jan 2000 – Mar 2025 |

Both series are **log-transformed** and **first-differenced** to ensure stationarity prior to modeling, approximating monthly growth rates.

---

## Methodology

### 1. Stationarity Testing
Augmented Dickey-Fuller (ADF) tests confirmed both series are non-stationary in levels but stationary in first differences — integrated of order one, I(1).

| Variable | ADF Statistic | p-Value | Stationary? |
|----------|--------------|---------|-------------|
| Log DJIA | -1.65 | 0.76 | No |
| ΔLog DJIA | -9.32 | 0.000 | Yes |
| Log CPI | -1.98 | 0.62 | No |
| ΔLog CPI | -6.87 | 0.000 | Yes |

### 2. Lag Order Selection
AIC and BIC criteria both identified **VAR(2)** as the optimal model specification.

| Lag | AIC | BIC | HQC |
|-----|-----|-----|-----|
| 1 | -7.18 | -6.99 | -7.10 |
| **2** | **-7.33** | **-7.04** | **-7.21** |
| 3 | -7.25 | -6.85 | -7.10 |

### 3. Granger Causality Testing
Tested directional predictability between DJIA and CPI within the VAR(2) framework.

| Null Hypothesis | F-Statistic | p-Value | Result |
|----------------|-------------|---------|--------|
| DJIA does not Granger-cause CPI | 4.37 | 0.014 | Reject H₀ |
| CPI does not Granger-cause DJIA | 2.01 | 0.137 | Fail to Reject H₀ |

### 4. Vector Autoregression (VAR)
A VAR(2) model was estimated to capture the joint dynamics of ΔLog(DJIA) and ΔLog(CPI), allowing for contemporaneous and lagged cross-variable effects.

| Dependent Variable | Lagged Variable | Coefficient | p-Value |
|-------------------|----------------|-------------|---------|
| ΔLog(CPI) | ΔLog(DJIA)₍ₜ₋₁₎ | 0.172 | 0.011 |
| ΔLog(CPI) | ΔLog(DJIA)₍ₜ₋₂₎ | -0.094 | 0.081 |
| ΔLog(DJIA) | ΔLog(CPI)₍ₜ₋₁₎ | 0.019 | 0.213 |
| ΔLog(DJIA) | ΔLog(CPI)₍ₜ₋₂₎ | 0.003 | 0.721 |

### 5. Impulse Response Functions (IRF)
IRFs visualized the dynamic response of each variable to a one-standard deviation shock in the other over a 12-month horizon.

### 6. Diagnostic Testing

| Test | Purpose | Result |
|------|---------|--------|
| Portmanteau & Ljung-Box Q | Residual autocorrelation | No autocorrelation |
| Jarque-Bera | Residual normality | CPI normal; DJIA marginally non-normal |
| ARCH LM | Heteroskedasticity | DJIA exhibits volatility clustering |
| Companion Matrix | VAR stability | All eigenvalues inside unit circle |

### 7. Forecasting
In-sample and out-of-sample forecasts generated for **April 2023 to March 2025** using the VAR(2) model.

| Variable | RMSE | MAE | MAPE (%) |
|----------|------|-----|----------|
| ΔLog(CPI) | 0.00271 | 0.00201 | 1.18 |
| ΔLog(DJIA) | 0.03740 | 0.02821 | 4.92 |

---

## Key Findings

- **Unidirectional Granger causality** runs from DJIA to CPI — equity market movements significantly help forecast inflation, but not the reverse
- **A 1% increase in DJIA growth** leads to a statistically significant positive effect on CPI growth one month later (coefficient: 0.172, p = 0.011), with a partial reversal at two months (-0.094)
- **Impulse Response Analysis** shows a positive DJIA shock produces a sustained increase in CPI growth over 2–4 months, gradually tapering off — consistent with demand-side inflationary transmission
- **CPI shocks** have negligible and statistically insignificant effects on DJIA, confirming that inflation is largely a backward-looking indicator
- **VAR model is dynamically stable** — all eigenvalues of the companion matrix lie inside the unit circle
- **Forecasting accuracy** is strong for CPI (MAPE: 1.18%) and reasonable for DJIA (MAPE: 4.92%), given its inherent volatility

---

## Policy Implications

- **For policymakers:** Equity market trends can serve as early warning signals of inflation, offering a real-time leading indicator ahead of official CPI releases and supporting more agile monetary policy responses
- **For investors:** Understanding the lead-lag dynamics between DJIA and CPI can inform inflation-sensitive portfolio allocation and hedging strategies
- **For researchers:** Results support further exploration of nonlinear models, structural breaks, and the inclusion of additional financial variables such as interest rates and commodity prices

---

## Tools & Technologies

| Tool | Purpose |
|------|---------|
| STATA | Data cleaning, time series modeling, VAR estimation, Granger causality testing, IRF, diagnostics, forecasting |
| FRED (Federal Reserve Economic Data) | CPI data retrieval |
| Yahoo Finance | DJIA historical price data |

---

## Limitations

- Structural breaks such as wars, pandemics, and monetary regime shifts are not explicitly modeled
- DJIA residuals exhibit significant volatility clustering — a GARCH extension could improve equity return forecast precision
- The model assumes linearity and symmetric responses, which may oversimplify real-world macroeconomic dynamics
- Analysis is bivariate; incorporating additional variables (interest rates, commodity prices, global indices) could enrich the model

---

## References

- Enders, W. (2014). *Applied Econometric Time Series* (4th ed.). Wiley.
- Stock, J. H., & Watson, M. W. (2019). *Introduction to Econometrics* (4th ed.). Pearson.
- Hamilton, J. D. (1994). *Time Series Analysis*. Princeton University Press.
- Lutkepohl, H. (2005). *New Introduction to Multiple Time Series Analysis*. Springer.
- Granger, C. W. J. (1969). Investigating causal relations by econometric models and cross-spectral methods. *Econometrica*, 37(3), 424–438.
- Sims, C. A. (1980). Macroeconomics and reality. *Econometrica*, 48(1), 1–48.
- Federal Reserve Bank of St. Louis. (2025). Consumer Price Index for All Urban Consumers (CPIAUCNS). https://fred.stlouisfed.org
- Yahoo Finance. (2025). Dow Jones Industrial Average historical data. https://finance.yahoo.com
