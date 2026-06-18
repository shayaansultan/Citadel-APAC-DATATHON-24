# Citadel APAC Datathon 2024 — Finalist

Statistical study of bidirectional causality between F\&B industry metrics and macroeconomic factors, modeled using Vector Autoregression (VAR).

## Result

**Finalist**, Citadel APAC Datathon 2024

## Research Question

How do soda consumption, US obesity rates, crude oil prices, and fast-food market cap interact with and influence F\&B stock performance?

## Approach

We used **Vector Autoregression (VAR)** to model feedback mechanisms across multiple time series simultaneously — capturing not just how macro variables affect stocks, but how those stocks feed back into the broader system.

### Data sources
- ACS-Nutrition datasets (obesity, soda consumption by state)
- USDA agricultural commodity data
- Fast-food company market cap history
- Crude oil price series
- F\&B public company stock data

### Pipeline
1. Data wrangling and cleaning across heterogeneous sources
2. Exogenous dataset construction (meat production, soda, oil)
3. Stationarity testing and differencing
4. VAR model fitting and lag selection
5. Impulse response analysis and Granger causality testing

## Stack

Python · pandas · statsmodels · Jupyter

## Team

Shayaan Sultan · Yuv Bindal · Deepan
