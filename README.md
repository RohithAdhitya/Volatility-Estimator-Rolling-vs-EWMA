# Volatility-Estimator-Rolling-vs-EWMA
### Overview

This project explores time-varying volatility by computing and comparing multiple volatility estimators on a liquid financial asset (SPY).
The goal is to demonstrate how different modeling assumptions affect risk measurement, especially during market stress and regime transitions.

Rather than treating volatility as a single fixed number, this project analyzes volatility as a dynamic risk metric.

### Objectives

- Compute historical volatility using multiple rolling windows

- Implement EWMA (Exponentially Weighted Moving Average) volatility

- Compare estimator behavior across calm and stressed market regimes

- Visualize and diagnose estimator disagreement during volatility transitions

### Data

- Asset: SPY (S&P 500 ETF)

- Frequency: Daily trading data

- Source: Yahoo Finance (via yfinance)

- Prices: Adjusted close prices (dividends and splits adjusted)

The data updates automatically with new trading days but can be frozen locally for reproducibility.

### Methodology
#### 1. Log Returns

Daily log returns are computed as:
              
              r_t = ln(P_t / P_{t-1})

Log returns are used because they are additive over time and more statistically stable than simple returns.


#### 2. Rolling Historical Volatility

Rolling volatility is calculated as the standard deviation of daily log returns over fixed windows and annualized using √252:

- 20-day rolling volatility (short-term, highly responsive)

- 60-day rolling volatility (medium-term)

- 120-day rolling volatility (long-term, stable)

This highlights the trade-off between responsiveness and stability.


#### 3. EWMA Volatility

EWMA volatility applies exponentially decaying weights to past returns:

            sigma_t^2 = lambda * sigma_{t-1}^2 + (1 - lambda) * r_{t-1}^2


- Decay factor: λ = 0.94 (RiskMetrics convention for daily data)

- Recent returns receive higher weight

- Older information fades smoothly over time

EWMA is commonly used in risk management due to its stability and responsiveness.


### Visual Analysis

The project includes the following visualizations:

- Full comparison plot
  Rolling (20/60/120) vs EWMA volatility across the full sample

- Focused comparison (zoomed view)
  EWMA vs 20-day rolling volatility during recent years

- Difference plot (EWMA − 20d rolling)
  Highlights periods where volatility estimators disagree, typically during regime transitions

- Distribution comparison\
  Compares the statistical behavior of EWMA and rolling volatility estimates


### Key Observations

- Volatility is clearly time-varying, with clustering during market stress.
  
- Short rolling windows react quickly but are noisy; longer windows are smoother but lag.

- EWMA provides a balance between responsiveness and stability.

- Estimator disagreement is minimal during calm periods but spikes during crises.

- Large deviations between estimators coincide with volatility regime transitions, where risk estimation is most sensitive.


### Future Extensions

- Event-based volatility analysis (CPI / FOMC announcements)

- OHLC-based volatility estimators (Parkinson, Garman–Klass)

- Volatility forecasting evaluation against realized volatility

- Application to multiple asset classes (FX, crypto, rates)

### Technologies Used
- Python
- pandas, numpy
- matplotlib
- yfinance
- Jupyter Notebook
