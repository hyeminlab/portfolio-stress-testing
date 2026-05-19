# Portfolio Stress Testing Project
Portfolio stress testing and risk analysis during market crisis periods.

## Objective
Analyze portfolio behavior during market crises.

## Assets
SPY, TLT, GLD, etc.

## Methods
- Historical Simulation
- Maximum Drawdown
- Value at Risk

## 📅 Progress Update (May 19, 2026)

### 1. Implemented Macro Regime Analysis
- Developed a modular risk evaluation function to slice and analyze financial metrics across different macroeconomic environments.
- Evaluated 4 key risk/return metrics: **Annualized Return, Annualized Volatility, Maximum Drawdown (MDD), and 95% Historical Daily VaR**.

### 2. Empirical Results (Multi-Asset Portfolio: SPY 40% / GLD 30% / TLT 30%)

| Metric | Total Period (2020-2026) | COVID-19 Shock (2020.02-2020.04) | Inflation Shock (2022) |
| :--- | :---: | :---: | :---: |
| **Annualized Return** | 11.02% | 16.90% | -15.96% |
| **Annualized Volatility** | 11.63% | 24.43% | 13.91% |
| **Maximum Drawdown (MDD)** | -22.63% | -14.41% | -21.86% |
| **95% Daily VaR** | -1.12% | -2.75% | -1.41% |

### 3. Key Quantitative Insights
- **COVID-19 Shock Regime:** Demonstrated traditional asset diversification mechanics. While equity (SPY) crashed by over 33%, the overall portfolio MDD was strictly contained at **-14.41%** due to aggressive monetary easing that boosted long-term bonds (TLT) and gold (GLD).
- **Inflation Shock Regime:** Experienced a severe performance drawdown (**Return: -15.96%, MDD: -21.86%**). This highlights the vulnerability of traditional asset allocation during rapid rate-hike cycles, implying a structural **'Correlation Breakdown'** between equities and fixed-income assets.

---
Next Step: Implement Rolling Correlation analysis to visually prove the stock-bond correlation breakdown in 2022.
