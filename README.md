# AQR "Hold the Dip" Replication

This repository contains a simplified, SPY-based replication of the buy-the-dip analysis discussed in AQR's "Hold the Dip." The project tests whether systematic dip-buying rules improve on buy-and-hold when applied to SPY data from 1993 onward.

The current implementation is a conceptual replication rather than an exact reproduction of AQR's paper. It uses public Yahoo Finance data, a rolling-window drawdown definition, and a simplified execution model.

## What Is Implemented

- Downloads SPY price data from 1993 onward with `yfinance`.
- Builds a buy-and-hold baseline.
- Computes daily returns, equity curves, and drawdowns.
- Implements drawdown-triggered buy-the-dip strategies.
- Tests a grid of 196 strategy variants:
  - Dip depths: 5%, 10%, 15%, 20%
  - Lookback windows: 1W, 2W, 3W, 1M, 3M, 6M, 1Y
  - Holding periods: 1M, 2M, 3M, 6M, 1Y, 3Y, 5Y
- Compares strategies using:
  - CAGR
  - Annualized volatility
  - Sharpe ratio
  - Max drawdown
  - Beta to SPY
  - Annual alpha
  - Correlation
  - R-squared
  - Average market exposure

## Main Takeaway

In this SPY-only implementation, the strongest buy-the-dip variant by CAGR is close to buy-and-hold but does not clearly dominate it. Many of the better-performing variants remain highly correlated with SPY, which suggests that the strategy's returns are still largely driven by equity market exposure.

The result is directionally consistent with the idea that simple dip-buying rules are not obviously superior to staying invested, especially after considering implementation details that are not yet modeled here.

## Current Limitations

- Uses SPY from 1993 onward rather than AQR's broader historical dataset.
- Uses a rolling-window drawdown definition, which may differ from AQR's exact methodology.
- Assumes uninvested capital earns 0%.
- Does not include transaction costs.
- Does not include taxes or slippage.
- Does not yet include trend-following benchmarks such as 10-month moving average or 12-month time-series momentum.

## Next Steps

- Add transaction cost assumptions based on position changes.
- Add cash returns for periods when the strategy is out of the market.
- Add 10-month moving-average and 12-month time-series momentum benchmarks.
- Compare buy-and-hold, dip-buying, and trend-following on the same performance table.
- Test the framework on longer historical index data or additional asset classes.

## Files

- `01_data_baseline.ipynb`: Main analysis notebook.
- `requirements.txt`: Python package list for the notebook environment.
- `notes.md`: Scratch notes.

## Setup

Create and activate a virtual environment, then install the dependencies:

```bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

Open the notebook:

```bash
jupyter notebook 01_data_baseline.ipynb
```
