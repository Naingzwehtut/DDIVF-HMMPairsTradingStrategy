# DDIVF-HMM Pairs Trading Strategy

An implementation of **"A Novel Algorithmic Trading Strategy using Hidden Markov Model for Kalman Filtering Innovations"** (Johnson-Skinner, Liang, Yu & Morariu — IEEE COMPSAC 2021, [DOI: 10.1109/COMPSAC51774.2021.00264](https://doi.org/10.1109/COMPSAC51774.2021.00264)).

## What's inside

`ddivf_hmm_pairs_trading.ipynb` reproduces the paper's pipeline end-to-end:

1. **Kalman Filter** — tracks a time-varying hedge ratio between two cointegrated stocks and produces prediction-error "innovations."
2. **DDIVF** — a robust, distribution-free volatility forecast for those innovations (DD-EWMA with data-driven sign correlation), instead of the Kalman filter's own variance estimate.
3. **Baseline strategy** — a single-threshold mean-reversion trading rule on the innovation z-score, with train/test split evaluation.
4. **Hidden Markov Model** — detects hidden volatility regimes directly from the innovations and lets the trading threshold adapt per regime (2-state and 3-state versions).
5. **Results comparison** — Buy & Hold vs. DDIVF vs. DDIVF-HMM, replicating the paper's tables and figures.

## Running it

```bash
pip install numpy pandas matplotlib statsmodels hmmlearn yfinance
jupyter notebook ddivf_hmm_pairs_trading.ipynb
```

The notebook downloads live daily prices for a cointegrated pair (default: `KO`/`PEP`) via `yfinance`. If there's no internet access, it automatically falls back to a simulated cointegrated pair with realistic fat-tailed, regime-switching noise, so every cell still runs.

## Disclaimer

This is an educational reproduction of a research paper, not investment advice. The backtest ignores transaction costs, slippage, and borrowing costs, and thresholds are fit and evaluated on a single static train/test split.
