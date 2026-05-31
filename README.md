# Multi-Asset Portfolio Stress Testing & Macro Risk Analysis

A quantitative risk management project designed to evaluate the empirical resilience of a traditional diversified multi-asset portfolio under extreme macroeconomic stress regimes. This project goes beyond basic historical backtesting to analyze structural flaws in asset allocation—specifically focusing on volatility clustering and inter-asset correlation breakdowns.

## Objective
- Synthesize a diversified asset portfolio and evaluate its performance from 2020 to 2026.
- Quantify portfolio tail risk under varying macroeconomic regimes (e.g., liquidity shocks vs. inflationary rate-hike cycles).
- Statistically prove the limitations of Modern Portfolio Theory (MPT) during high-inflation crises.

## Portfolio Architecture
The portfolio utilizes an optimized baseline multi-asset allocation:
- **Equities (Growth):** SPY (S&P 500 ETF) — 40%
- **Alternatives (Inflation Hedge):** GLD (SPDR Gold Shares) — 30%
- **Fixed Income (Defensive):** TLT (iShares 20+ Year Treasury Bond ETF) — 30%

---

## Methodology & Core Metrics
1. **Annualized Geometric Return:** Captured compounded growth normalized on a 252-day trading year.
2. **Annualized Volatility:** Quantified asset price dispersion applying the square-root-of-time rule ($\sigma \times \sqrt{252}$).
3. **Maximum Drawdown (MDD):** Measured the peak-to-trough decline to evaluate worst-case scenario wealth destruction.
4. **95% Historical Value at Risk (VaR):** Determined the threshold daily loss at a 95% confidence level.
5. **95% Expected Shortfall (ES / Conditional VaR):** Calculated the mean loss conditional on the portfolio breaching its 95% VaR parameter to measure systemic tail-risk depth.

---

## Comprehensive Empirical Results

### 1. Macro Regime Breakdown Summary
The table below highlights how the mixed portfolio reacted across distinct macro environments:

| Metric | Total Period (2020-2026) | COVID-19 Shock (2020.02 - 2020.04) | Inflation Shock (2022.01 - 2022.12) |
| :--- | :---: | :---: | :---: |
| **Annualized Return** | **11.02%** | 16.90% | -15.96% |
| **Annualized Volatility** | **11.63%** | 24.43% | 13.91% |
| **Maximum Drawdown (MDD)** | **-22.63%** | -14.41% | -21.86% |
| **95% Daily VaR** | **-1.12%** | -2.75% | -1.35% |
| **95% Expected Shortfall (ES)** | **-1.68%** | *Breached* | *Breached* |

### 2. Individual Asset Vulnerability (Stand-alone MDD)
To understand diversification mechanics, individual maximum drawdowns over the full period were mapped:
- **SPY (Equities):** -33.72%
- **GLD (Gold):** -22.00%
- **TLT (Long-term Bonds):** -48.35%

### 3. Extended Portfolio Analysis (Asset Universe Expansion)
To enhance the portfolio's return profile and stress-test the inclusion of high-beta growth equities and industrial alternatives, the universe was expanded with **Palantir (PLTR, 10%)** and **Silver (SLV, 10%)**, reducing core assets proportionally (SPY 30% / GLD 20% / TLT 30%).

| Portfolio Type | Annualized Return | Annualized Volatility | Maximum Drawdown (MDD) | 95% Daily VaR | 95% Daily ES |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Baseline (3 Assets)** | 11.02% | 11.63% | -22.63% | -1.12% | -1.68% |
| **Extended (5 Assets)** | **16.12%** | **14.63%** | **-29.03%** | **-1.42%** | **-2.02%** |

**Quantitative Revision Insights:**
- **Risk-Return Trade-off:** Incorporating idiosyncratic growth assets (PLTR) amplified the portfolio's compounded return by **+5.10%p**. 
- **Tail Risk Amplification:** The trade-off is materialized in the structural degradation of downstream risk metrics. The Maximum Drawdown worsened by **-6.40%p**, and the **Expected Shortfall (ES)** extended beyond the -2% threshold (**-2.02%**). This empirically confirms that adding tactical satellite assets shifts the portfolio along the efficient frontier toward a high-beta regime, demanding more rigorous liquidity buffers during systematic crises.
---

## Key Quantitative Insights & Macro Diagnostics

### 1. The 2020 Pandemic Shock: Classic Non-Linear Diversification
During the COVID-19 crash, equity markets plummeted (SPY single-asset crash >33%). However, aggressive central bank intervention and interest rate cuts initiated an immediate surge in fixed-income duration (TLT) and gold (GLD). 
- **Result:** The **negative rolling correlation** between stock and bond returns successfully mitigated downside risk, strictly containing the overall portfolio MDD to **-14.41%**, despite short-term annualized volatility spiking to **24.43%**.

### 2. The 2022 Inflationary Regime: Structural Correlation Breakdown
The portfolio faced its most critical vulnerability during the 2022 monetary tightening cycle. As the Federal Reserve aggressively raised interest rates to combat inflation, a simultaneous repricing occurred in both equity valuations and fixed-income assets.
- **The MPT Failure:** Implementing a **60-day Rolling Correlation** analysis mathematically demonstrated that the stock-bond correlation shifted abruptly from a defensive negative territory ($-0.4$ to $-0.6$) to a highly positive territory ($+0.3$). 
- **Result:** Because both asset classes fell in tandem, traditional diversification failed, resulting in a severe performance drawdown (**Return: -15.96%, MDD: -21.86%**).

### 3. Risk Dynamics & Volatility Clustering
Applying a **60-day Rolling Volatility** filter proved that financial risk is non-stationary. The portfolio experienced distinct risk regimes—short, explosive spikes during liquidity events (2020) versus persistent, elevated risk plateaus during macroeconomic regime shifts (2022). 

### 4. Tail Risk Quantification via Expected Shortfall
While the daily baseline 95% VaR stands at **-1.12%**, our **Expected Shortfall (ES)** shows a deeper tail risk of **-1.68%**. This indicates that when black swan events break our statistical defensive lines, the portfolio faces an average conditional daily loss of 1.68%, highlighting the vital importance of incorporating conditional risk metrics over simple VaR constraints under Basel III standards.

---

## Tech Stack & Libraries
- **Language:** Python
- **Data Source:** Yahoo Finance API (`yfinance`)
- **Data Engineering:** `pandas`, `numpy`
- **Visualization:** `matplotlib`

## Repository Structure
- `Project_01_Stress_Testing.ipynb`: Core Jupyter Notebook containing data sourcing, portfolio synthesis, rolling statistics, and risk metric calculation logic.
- `README.md`: Professional research and documentation.

- 
