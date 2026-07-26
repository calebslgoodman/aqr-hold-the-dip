# Hold the Dip: Replication of AQR's Market Timing Analysis

This project is a simplified replication of AQR's "Hold the Dip" analysis using SPY data. The notebook tests whether systematic buy-the-dip rules can improve on a basic buy-and-hold approach.

The project is not meant to exactly reproduce AQR's published numbers. AQR uses a broader historical dataset and likely has different implementation details. This version focuses on building the core idea in Python and seeing whether the same general conclusion shows up in a simpler SPY-only setting.

## What the Main Notebook Does

- Downloads SPY price data from Yahoo Finance.
- Computes daily returns, cumulative returns, and drawdowns.
- Builds a buy-and-hold benchmark.
- Implements drawdown-triggered buy-the-dip rules.
- Tests a grid of dip depths, lookback windows, and holding periods.
- Compares strategies using CAGR, annualized volatility, Sharpe ratio, and max drawdown.
- Computes beta, annual alpha, correlation, and R-squared versus SPY.
- Discusses why the results differ from AQR's exact paper.

## Completed Extension Notebook

The second notebook, `02_costs_trend_following_comparison.ipynb`, adds the missing implementation pieces needed for a fuller comparison:

- Transaction costs.
- Cash returns while out of the market.
- 10-month moving-average trend following.
- 12-month time-series momentum.
- A final comparison table across buy-and-hold, buy-the-dip, and trend-following strategies.

This keeps the original notebook intact while making the project support a broader strategy comparison.

## Policy-Shock Event Study

The third notebook, `03_policy_shock_event_study.ipynb`, starts connecting the strategy to recent market volatility. It currently implements:

- A sourced event calendar of Trump policy changes and remarks tied to market dips or reversals.
- Event-triggered SPY holding-period returns after each policy shock.
- Fixed-horizon returns for 5, 10, 20, 30, and 60 trading-day holds.
- A grouped summary and plot of average returns by event type.
- A written interpretation of the results, including the caveat that positive post-event returns may partly reflect normal SPY drift.

The key unfinished piece is a placebo test against random non-event dates. That would show whether SPY rose more after these policy-shock events than it usually does after ordinary dates in the same period.

## Current Scope

The first notebook is intentionally simple:

- SPY is the only asset.
- The data starts in 1993.
- Dip signals are based on rolling-window drawdowns.
- Uninvested capital is treated as earning 0%.
- Transaction costs, taxes, slippage, and cash yields are not modeled.

The second notebook relaxes some of those assumptions by adding cash returns, transaction costs, and trend-following benchmarks. The project should still be viewed as a conceptual replication rather than an exact reproduction of AQR's paper.

The third notebook is an exploratory event study. It is useful for connecting the project to current markets, but it does not prove a trading strategy on its own.

## Main Takeaway

The notebook finds that simple buy-the-dip rules do not clearly dominate buy-and-hold in this SPY-only setup. Some parameter choices reduce exposure or change the drawdown profile, but the stronger strategies remain closely tied to equity market beta.

That is broadly consistent with the idea that "buying the dip" sounds intuitive, but does not automatically create a better strategy than staying invested.

## Files

- `01_data_baseline.ipynb`: Main analysis notebook.
- `02_costs_trend_following_comparison.ipynb`: Extension notebook with costs, cash returns, trend-following benchmarks, and the final comparison table.
- `03_policy_shock_event_study.ipynb`: Policy-shock event calendar and SPY event-window notebook.
- `notes.md`: Scratch project notes.
- `pandas_notes.md`: Pandas notes from working through the project.
- `requirements.txt`: Python dependencies.

## Setup

Create and activate a virtual environment:

```bash
python3 -m venv venv
source venv/bin/activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Open the notebook:

```bash
jupyter notebook 01_data_baseline.ipynb
```

Open the extension notebook:

```bash
jupyter notebook 02_costs_trend_following_comparison.ipynb
```

Open the policy-shock event study:

```bash
jupyter notebook 03_policy_shock_event_study.ipynb
```

## Next Steps

Possible improvements:

- Add a random-date placebo test to the policy-shock notebook.
- Test other equity indexes or longer historical datasets.
- Split the analysis into in-sample and out-of-sample periods.
- Try alternative transaction cost assumptions.
- Compare against AQR's exact signal definitions if more detail is available.
