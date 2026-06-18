# Citadel APAC Datathon 2024 — Finalist

**Team 17**: Shayaan Sultan · Yuv Bindal · Pranav Gupta · Dhasarathan Deepan Krishnaa

📄 [Full Report (PDF)](./Team_17_report.pdf)

---

## Research Question

*Exploring the relationships of the carbonated beverages industry with teenage obesity and sugar consumption.*

Two independent analyses:
1. **Soda ↔ Obesity**: Does soda consumption drive teenage obesity rates — and does obesity drive soda consumption in return?
2. **Sugar Economics ↔ Beverage Stocks**: Do sugar prices and import levels affect KO/PEP stock performance?

---

## Analysis 1 — PanelVAR: Soda Consumption and Teenage Obesity

**Finding**: Statistically significant bidirectional relationship confirmed. Soda consumption and obesity rates form a positive feedback loop among US teenagers.

### Data
- CDC Nutrition, Physical Activity, and Obesity dataset (2007–2019)
- USDA Meat Production data (used as exogenous control)
- Panel: 897 observations across 204 State × Race/Ethnicity panels

### Model
Panel Vector Autoregression (PanelVAR) with exogenous variables — chosen to capture bidirectional causality and cross-sectional heterogeneity simultaneously.

- **Fixed effects**: Removed via forward mean-differencing (Helmert procedure / forward orthogonal deviations) to avoid Nickell bias from standard mean-differencing
- **Estimation**: System GMM, using lagged values as instruments
- **Robustness**: Hansen Test for overidentification (p = 0.193 — instruments valid)
- **Stationarity**: ADF tests on meat production; seasonal differencing applied

```
Z_it = β·Z_{it-1} + γ1·X_{t-1} + γ2·X_{t-2} + f_i + e_it

Z = {Soda_Percentage, Obesity_Percentage}  [endogenous]
X = meat_prod_diff                          [exogenous, lagged]
f_i = fixed effects
```

### Results

| | Soda_Percentage | Obesity_Percentage |
|---|---|---|
| lag1_Soda_Percentage | 0.7191 *** | 0.1801 *** |
| lag1_Obesity_Percentage | 0.1411 * | 0.7859 *** |
| Meat_prod_lag1 | -0.0082 *** | 0.0050 *** |

Both cross-effects are significant — soda predicts future obesity and obesity predicts future soda consumption. Orthogonalized Impulse Response Functions (OIRF) and Forecast Error Variance Decomposition (FEVD) confirm a sustained positive feedback loop.

---

## Analysis 2 — VARX: Sugar Economics and Beverage Stock Returns

**Finding**: No statistically significant link between KO/PEP excess returns and sugar prices or imports. Mega-cap beverage companies appear insulated from short-term sugar cost fluctuations, likely through hedging and diversified cost structures.

### Variables

| Feature | Type | Source |
|---|---|---|
| KO & PEP excess log returns | Endogenous | Yahoo Finance |
| Sugar price log returns | Endogenous | Provided |
| US sugar import (monthly, seasonal decomposition) | Endogenous | FRED |
| Crude oil prices | Exogenous | FRED |
| CPI growth rate | Exogenous | FRED |
| Retail sales | Exogenous | FRED |
| COVID binary (Mar 2020 – Jan 2022) | Exogenous | Engineered |

Granger causality tests confirmed bidirectional causality between sugar imports and sugar prices at 4+ lags (p < 0.001), justifying their treatment as jointly endogenous.

---

## Stack

Python · pandas · statsmodels · yfinance · Jupyter