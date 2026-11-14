# Project context

## What this is
A portfolio project for wealth management internship recruiting. I'm a sophomore at BU (Finance major, Data Science minor). I build portfolios for 3 hypothetical clients, backtest and stress test them, and write a one-page plain-English proposal for each. Later it goes on my personal website.
Repo: github.com/EgalJ/Client-Portfolio-Proposals (public)

## Plan
1. Data exploration (done)
2. Optimized ETF portfolio for each client within their allocation limits, using PyPortfolioOpt (done)
3. Backtest each portfolio since 2007 (next)
4. Stress tests: 2008, 2020, 2022
5. One-page client proposals in the proposals/ folder
6. README write-up with key charts and results

## What's done
- clients.md: 3 client profiles with goals, risk tolerance and allocation limits
  - Maya, 28: 80% to 95% stocks
  - David, 55: 50% to 65% stocks, at least 15% muni bonds (MUB)
  - Robert and Linda, 68 and 66: 30% to 45% stocks, include inflation-protected bonds (TIP), $80k/year withdrawals
- Notebooks/01_data_exploration.ipynb: pulls 10 ETFs from yfinance since 2007 (SPY, IWM, EFA, EEM, AGG, SHY, TIP, MUB, VNQ, GLD). Data starts late 2007 when MUB launched. Saves data/etf_prices.csv. Calculates annual return, volatility, max drawdown, return/risk, a correlation heatmap and growth of $10k. Charts saved in charts/.
- I was writing my key takeaways in a markdown cell at the bottom of notebook 01.

## Environment (Windows 11, x64 laptop)
- Python 3.14.10 (x64) in .venv. The global "python" command isn't on PATH; use "py" or the venv's Python.
- Use "python -m pip install ..." instead of "pip". Windows Smart App Control blocked pip.exe and unsigned DLLs like pandas. If you see "An Application Control policy has blocked this file," that's the cause.
- Git isn't on the terminal PATH. Use "C:\Program Files\Git\cmd\git.exe" or VS Code's Source Control panel. Git name and email are already configured.
- Notebooks run with the .venv kernel and use relative paths like ../data and ../charts.

## How I want you to work
- I'm still learning. Go one step at a time and explain what each piece of code does in plain English.
- Keep the code simple and readable. I need to be able to explain every line and every assumption in an interview.
- Ask before big decisions, for example whether VNQ counts as "stocks" for the allocation limits.
- Writing style: concise, casual, direct. No em dashes.

## Decisions from notebook 02
- Notebooks/02_portfolio_optimization.ipynb: max Sharpe portfolio per client with PyPortfolioOpt. Saves data/optimized_weights.csv and charts/optimized_weights.png.
- Expected returns = historical CAGR, risk = sample covariance, risk-free rate 2%
- "Stocks" = SPY, IWM, EFA, EEM, VNQ (VNQ counts as stocks)
- Max 40% per ETF, GLD capped at 10% (uncapped, the optimizer put 20% to 35% in gold)
- David: MUB >= 15%. Robert and Linda: SHY >= 5% (about 1.25 years of withdrawals), TIP >= 10%
- Known weakness: optimizer chases past returns, so EFA, EEM, VNQ and AGG get 0%

## Next step
Create Notebooks/03_backtest.ipynb and backtest each client's portfolio since 2007 using data/optimized_weights.csv.
