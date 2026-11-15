# portfolio-optimizer

Python portfolio optimizer based on Modern Portfolio Theory. It downloads historical prices for a basket of stocks, simulates thousands of random portfolios, and identifies the maximum-Sharpe-ratio and minimum-volatility portfolios on the efficient frontier. Results are exported to a formatted Excel workbook and a chart.

> Built with Claude Code.

## What it does

1. **Fetches data:** downloads 3 years of daily adjusted closing prices with `yfinance` for 15 tickers across 5 sectors (technology, financials, energy, healthcare, consumer).
2. **Computes statistics:** annualised expected returns, volatilities and the covariance matrix.
3. **Simulates portfolios:** generates 10,000 random long-only portfolios (weights drawn from a Dirichlet distribution, so they are non-negative and sum to 1) and calculates each portfolio's return, volatility and Sharpe ratio.
4. **Finds the key portfolios:** the maximum-Sharpe portfolio and the minimum-volatility portfolio.
5. **Outputs results:** an efficient frontier chart (`efficient_frontier.png`) and an Excel workbook (`portfolio_results.xlsx`).

The Excel workbook has four sheets: Optimal Portfolio (with a plain-English interpretation), Efficient Frontier Data, Stock Statistics, and the embedded Efficient Frontier Chart.

## Method note

The optimal portfolios are found by Monte Carlo simulation (picking the best of 10,000 random portfolios) rather than by an analytical or numerical optimizer, so results are approximate and improve with more simulated portfolios.

## Setup

```bash
pip install -r requirements.txt
python src/main.py
```

## Configuration

Edit `src/config.py` to change the stock universe, the data window (`YEARS_OF_DATA`), the number of simulated portfolios (`NUM_PORTFOLIOS`), the risk-free rate (`RISK_FREE_RATE`, set to 4.3%), and output file names.

## Files

| File | Purpose |
| --- | --- |
| `requirements.txt` | Python dependencies |
| `src/main.py` | Entry point that runs the full pipeline |
| `src/config.py` | Tickers, data window and simulation settings |
| `src/data_fetcher.py` | Downloads prices and computes return statistics |
| `src/optimizer.py` | Monte Carlo simulation and optimal portfolio selection |
| `src/visualizer.py` | Efficient frontier chart |
| `src/excel_output.py` | Excel workbook export |
