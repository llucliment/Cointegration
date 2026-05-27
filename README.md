# Cointegration-Based Statistical Arbitrage Screener

This project implements a Python-based screener for identifying potentially cointegrated stock pairs in the S&P 500. The objective is to detect pairs of assets whose prices exhibit a long-term equilibrium relationship and may therefore be suitable for pairs trading or statistical arbitrage strategies.

The project downloads S&P 500 tickers, retrieves historical adjusted price data, filters assets with insufficient data, applies the Engle-Granger cointegration test to all possible pairs, estimates hedge ratios, calculates spread half-life, and ranks candidate pairs by statistical significance.

---

## Project Motivation

Pairs trading is a market-neutral strategy based on the idea that two related assets may move together over the long term. If their relationship temporarily diverges, a trader may go long the undervalued asset and short the overvalued asset, expecting the spread to revert to its historical equilibrium.

This project focuses on the research and screening stage of a cointegration-based pairs trading pipeline.

The main goals are:

- Build a scalable cointegration screener.
- Identify statistically significant pairs among S&P 500 stocks.
- Estimate hedge ratios for candidate pairs.
- Measure mean-reversion speed using spread half-life.
- Save reproducible results for later backtesting.

---

## Methodology

The workflow is divided into the following steps:

1. Download the current S&P 500 tickers from Wikipedia.
2. Download historical adjusted close prices using `yfinance`.
3. Save the raw price data locally as CSV files.
4. Filter assets with excessive missing data or insufficient observations.
5. Generate all possible stock pairs.
6. Apply the Engle-Granger cointegration test to each pair.
7. Estimate the hedge ratio using ordinary least squares.
8. Construct the spread between the two assets.
9. Calculate the half-life of mean reversion.
10. Rank and save candidate pairs by p-value.

---

## Core Concepts

### Cointegration

Two price series are cointegrated if they are individually non-stationary but a linear combination of them is stationary. In a trading context, this means that the spread between two assets may revert to a long-term equilibrium.

### Engle-Granger Test

The Engle-Granger test is used to test whether two time series are cointegrated.

The hypotheses are:

```text
H0: The two series are not cointegrated.
H1: The two series are cointegrated.