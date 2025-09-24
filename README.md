# Python SMA Crossover Strategy Backtester

A Python-based backtesting framework implementing Simple Moving Average (SMA) crossover strategy for systematic trading with comprehensive performance analysis.

![Python](https://img.shields.io/badge/python-v3.7+-blue.svg)
![Pandas](https://img.shields.io/badge/pandas-latest-green.svg)
![yfinance](https://img.shields.io/badge/yfinance-latest-orange.svg)
![Matplotlib](https://img.shields.io/badge/matplotlib-latest-red.svg)

## Overview

This backtesting system downloads historical market data, implements technical trading strategies, executes simulated trades, and provides detailed performance analytics comparing strategy returns against buy-and-hold benchmarks.

## Features

- **Automated Data Retrieval**: Historical stock data from Yahoo Finance API
- **SMA Crossover Strategy**: 50-day and 200-day moving average crossover signals
- **Signal Generation**: Automated buy/sell signal identification
- **Performance Analytics**: Comprehensive return analysis and risk metrics
- **Visual Backtesting**: Price charts with signal overlays and performance graphs
- **Comparative Analysis**: Strategy vs. benchmark performance evaluation

## Strategy Implementation

### Simple Moving Average Crossover Logic

- **Long Signal**: 50-day SMA crosses above 200-day SMA (Golden Cross)
- **Short Signal**: 50-day SMA crosses below 200-day SMA (Death Cross)
- **Position Execution**: Trades executed day after signal generation
- **Asset**: NIFTY BEES ETF (NIFTYBEES.NS)

### Mathematical Framework

```
Signal(t) = {
    1   if SMA50(t) > SMA200(t)  [Long Position]
    -1  if SMA50(t) < SMA200(t)  [Short Position]
    0   otherwise                [No Position]
}

Strategy Return(t) = Signal(t-1) × Market Return(t)
```

## Technical Implementation

### Core Components

```python
# Data acquisition and preprocessing
ticker = 'NIFTYBEES.NS'
data = yf.download(ticker, start='2020-01-01', end='2025-01-01')

# Moving average calculations
data['SMA50'] = data['Close'].rolling(window=50).mean()
data['SMA200'] = data['Close'].rolling(window=200).mean()

# Signal generation
data['Signal'] = 0
data.loc[data['SMA50'] > data['SMA200'], 'Signal'] = 1
data.loc[data['SMA50'] < data['SMA200'], 'Signal'] = -1

# Performance calculation
data['Market Returns'] = data['Close'].pct_change()
data['Strategy Returns'] = data['Market Returns'] * data['Signal'].shift(1)
```

### Performance Metrics

- **Cumulative Returns**: Compound growth over backtesting period
- **Total Return Comparison**: Strategy vs. buy-and-hold performance
- **Signal Analysis**: Crossover point identification and timing
- **Risk Assessment**: Return volatility and drawdown analysis

## Installation

```bash
pip install pandas yfinance matplotlib numpy
```

## Usage

```python
import pandas as pd
import yfinance as yf
import matplotlib.pyplot as plt

# Execute complete backtesting workflow
python backtest_strategy.py
```

## Results Analysis

The system outputs:
- Total buy-and-hold return percentage
- Total strategy return percentage  
- Performance comparison metrics
- Visual charts with price action and signals
- Trade execution points visualization

### Sample Output
```
Total Buy-and-Hold Return: 45.67%
Total Strategy Return: 52.34%
```

## Visualization Components

- **Price Chart**: Historical closing prices with moving averages
- **Signal Overlay**: Buy/sell markers at crossover points
- **Performance Tracking**: Cumulative return comparisons
- **Interactive Charts**: Matplotlib-based financial visualizations

## Code Structure

```
├── Data Download (yfinance)
├── Technical Indicators (SMA calculations)
├── Signal Generation (Crossover detection)
├── Backtesting Engine (Return calculations)
├── Performance Analysis (Metrics computation)
└── Visualization (Charts and plots)
```

## Technical Requirements

- Python 3.7+
- pandas for data manipulation
- yfinance for market data
- matplotlib for visualization
- numpy for numerical computations

## Algorithm Workflow

1. **Data Acquisition**: Download historical OHLC data
2. **Indicator Calculation**: Compute 50-day and 200-day SMAs
3. **Signal Detection**: Identify crossover events
4. **Position Management**: Generate buy/sell signals
5. **Return Calculation**: Compute strategy and market returns
6. **Performance Analysis**: Compare cumulative returns
7. **Visualization**: Generate charts and performance plots

This backtesting framework provides a foundation for systematic trading strategy development and quantitative analysis of technical trading rules.
