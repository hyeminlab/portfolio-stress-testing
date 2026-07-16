# Multi-Asset Portfolio Stress Testing & Macro Risk Analysis

A quantitative risk-management project examining the resilience of diversified multi-asset portfolios across contrasting macroeconomic stress regimes. The analysis extends beyond aggregate backtesting by evaluating time-varying volatility, cross-asset correlation instability, historical tail losses, and volatility-responsive allocation.

---

## Research Motivation (Synergy with Factor Alpha Generation)

While actively developing and passing mathematical alpha expressions during the **WorldQuant BRAIN International Quant Championship (IQC) 2026 (Stage 02)**, I heavily focused on extracting statistical anomalies from large-scale corporate fundamental datasets. For instance, I successfully implemented expressions targeting asset mispricing based on multi-day historical Z-scores of balance sheet and income statement dynamics (e.g., formulations capturing intangible asset overvaluation like `-1 * ts_zscore(goodwill / sales, 500)`).

Through this rigorous competitive process, I recognized a critical structural limitation inherent in cross-sectional alpha generation platforms: they operate in macro-level silos. While simulators efficiently generate traditional, aggregated performance metrics—such as the Sharpe Ratio, Turnover, and generic Maximum Drawdown (MDD)—they heavily restrict customized downstream risk modeling and non-linear risk diagnostics under shifting macroeconomic regimes.

To bridge this crucial analytical gap between **Alpha Sourcing** and **Institutional Risk Architecture**, I independently engineered this Python-based multi-asset stress-testing framework. The core objective of this project is to construct an autonomous risk engine capable of ingesting arbitrary tactical strategies or synthetic portfolio returns, subsequently exposing them to historical liquidity crunches and inflationary macro shocks. By computing complementary tail-risk metrics—specifically **95% Historical Value at Risk (VaR)** and **95% Expected Shortfall (ES)**—this framework serves as an independent validation layer for evaluating the downside boundaries of diversified capital allocation. The 95% confidence level is used for transparent portfolio comparison, while the Basel market-risk framework applies Expected Shortfall at a 97.5% one-tailed confidence level for regulatory capital calculations.

---

## Objective
- Synthesize a diversified asset portfolio and evaluate its empirical performance from 2020 to 2026.
- Quantify portfolio tail risk under varying macroeconomic regimes (e.g., liquidity shocks vs. inflationary rate-hike cycles).
- Empirically illustrate how the diversification benefits assumed by static mean-variance allocation can weaken when cross-asset correlations shift during inflationary stress.
- Implement a dynamic inverse-volatility allocation strategy to examine whether volatility-responsive rebalancing can reduce portfolio drawdowns and tail-loss severity.

---

## Portfolio Architecture
To avoid look-ahead bias, portfolio weights are lagged by one trading day before being applied to realized returns.
The framework evaluates three distinct progressive asset allocation strategies:
1. **Baseline Portfolio (3 Assets):** Tactical asset mix focused on core diversification.
   - Equities (Growth): SPY (S&P 500 ETF) — 40%
   - Alternatives (Inflation Hedge): GLD (SPDR Gold Shares) — 30%
   - Fixed Income (Defensive): TLT (iShares 20+ Year Treasury Bond ETF) — 30%
2. **Extended Fixed Portfolio (5 Assets):** Expanded universe to capture idiosyncratic growth and industrial commodities.
   - SPY (30%) / PLTR (10%) / GLD (20%) / SLV (10%) / TLT (30%)
3. **Dynamic Inverse-Volatility Portfolio (5 Assets):** Portfolio weights are adjusted using the inverse of each asset’s trailing 60-day realized volatility, such that lower-volatility assets receive larger allocations and higher-volatility assets receive smaller allocations ($\omega_{i,t} \propto 1/\sigma_{i,t}$).
---

## Methodology & Core Metrics
1. **Annualized Geometric Return:** Captured compounded growth normalized on a 252-day trading year.
2. **Annualized Volatility:** Quantified asset price dispersion applying the square-root-of-time rule ($\sigma \times \sqrt{252}$).
3. **Maximum Drawdown (MDD):** Measured the peak-to-trough decline to evaluate worst-case scenario wealth destruction.
4. **95% Historical Value at Risk (VaR):** Determined the threshold daily loss at a 95% confidence level.
5. **95% Historical Expected Shortfall (ES):** Calculated the average daily return among observations falling below the 95% Historical VaR threshold. This metric measures the severity of losses beyond VaR and is reported at the 95% level for consistency with the portfolio comparison framework. It should not be interpreted as a direct regulatory Basel capital measure, which uses a 97.5% one-tailed ES under the internal models approach.

---

## Comprehensive Empirical Results

### 1. Macro Regime Breakdown Summary (Baseline Portfolio)
The table below highlights how the core 3-asset mixed portfolio reacted across distinct historical stress environments:

| Metric | Total Period (2020-2026) | COVID-19 Shock (2020.02 - 2020.04) | Inflation Shock (2022.01 - 2022.12) |
| :--- | :---: | :---: | :---: |
| **Period Return** | [Full Period Return] | [COVID Return] | -15.96% |
| **Annualized Volatility** | **11.63%** | 24.43% | 13.91% |
| **Maximum Drawdown (MDD)** | **-22.63%** | -14.41% | -21.86% |
| **95% Daily VaR** | **-1.12%** | -2.75% | -1.35% |
| **95% Expected Shortfall (ES)** | **-1.68%** | [calculated COVID ES] | [calculated 2022 ES] |

*Standalone Asset Vulnerability (Full-Period MDD reference):* SPY: **-33.72%** | GLD: **-22.00%** | TLT: **-48.35%**

### 2. Strategy Optimization Scoreboard (The Core Comparison)
The table below maps the complete progression from the baseline portfolio to asset universe expansion and dynamic algorithmic optimization:

| Portfolio Architecture | Annualized Return | Annualized Volatility | Maximum Drawdown (MDD) | 95% Daily VaR | 95% Daily ES |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Baseline (3 Assets)** | 11.02% | 11.63% | -22.63% | -1.12% | -1.68% |
| **Extended Fixed (5 Assets)** | 16.12% | 14.63% | -29.03% | -1.42% | -2.02% |
| **Dynamic Inverse-Volatility (5 Assets)** | **13.15%** | **12.64%** | **-25.75%** | **-1.25%** | **-1.73%** |

---

## Advanced Algorithmic & Macro Diagnostics

### 1. The Asset Universe Expansion Trade-off
Adding concentrated exposure to the high-volatility growth stock **PLTR** and the industrial precious-metal ETF **SLV** increased the portfolio’s annualized return by **5.10 percentage points** relative to the baseline over the observed sample. However, this higher return was accompanied by materially greater downside risk: Maximum Drawdown deteriorated from **-22.63% to -29.03%**, while 95% Expected Shortfall declined from **-1.68% to -2.02%**. The result illustrates the return–risk trade-off created by adding concentrated satellite exposures to an otherwise diversified portfolio.

### 2. Dynamic Tail-Risk Mitigation via Inverse-Volatility Allocation
Transitioning from a static asset mix to a dynamic inverse-volatility allocation reduced the influence of assets experiencing elevated realized volatility. Relative to the Extended Fixed Portfolio, the strategy improved Maximum Drawdown by **3.28 percentage points**, from **-29.03% to -25.75%**, and reduced 95% Expected Shortfall from **-2.02% to -1.73%**. These results indicate partial tail-risk mitigation over the observed sample, although the strategy did not eliminate drawdown risk and should not be interpreted as evidence of universal outperformance.

### 3. The 2020 Pandemic Shock: Classic Non-Linear Diversification
During the COVID-19 liquidity shock, SPY experienced a drawdown of more than 33%. Within the selected stress window, the inclusion of long-duration Treasuries and gold reduced the baseline portfolio’s drawdown to **-14.41%**, despite annualized volatility rising to **24.43%**. The result is consistent with the diversification benefit observed when equity returns diverged from defensive asset returns during parts of the crisis period.

### 4. The 2022 Inflationary Regime: Structural Correlation Breakdown
The asset allocation framework faced its most critical vulnerability during the 2022 monetary tightening cycle. The **60-day rolling correlation** analysis showed that the relationship between SPY and TLT was time-varying. During parts of the sample, the correlation was materially negative, reaching approximately **-0.4 to -0.6**, whereas it moved toward positive territory and reached approximately **+0.3** during the 2022 tightening regime. As equities and long-duration bonds declined concurrently during the tightening cycle, the diversification benefit of the baseline allocation weakened. The portfolio recorded a **2022 period return of -15.96%** and a **Maximum Drawdown of -21.86%**, illustrating the vulnerability of static stock-bond diversification when inflation and interest-rate shocks affect both asset classes simultaneously.

### 5. Risk Non-Stationarity & Volatility Clustering
The **60-day rolling volatility** analysis illustrates that realized portfolio risk varied substantially over time rather than remaining constant throughout the sample. The historical returns show distinct risk patterns: short-lived, explosive spikes during sudden liquidity events (2020) versus persistent, elevated risk plateaus during fundamental macroeconomic regime shifts (2022). This illustrates why Expected Shortfall can provide additional information beyond VaR by capturing the average severity of losses once the VaR threshold has been exceeded. The result is conceptually consistent with the broader regulatory shift from VaR toward Expected Shortfall in the Basel market-risk framework, although this project uses a simplified 95% historical implementation rather than the full regulatory specification.

---

## Tech Stack & Libraries
- **Language:** Python
- **Data Source:** Yahoo Finance API (`yfinance`)
- **Data Engineering:** `pandas`, `numpy`
- **Visualization:** `matplotlib`

## Repository Structure
- `Project_01_Stress_Testing.ipynb`: 
Core Jupyter Notebook containing data sourcing,
portfolio construction,
dynamic inverse-volatility weighting,
rolling risk diagnostics,
and historical tail-risk calculations.
- `README.md`: Institutional-grade research documentation and macro risk diagnostics.

---
## Images
# 1. 3대 개별 자산 취약성(Individual Asset Vulnerability) 
![SPY Stock Price](./images/no1.SPY_stock_price.png)
![Individual Stand-alone MDD](./images/no3.drawdown_comparison.png)

# 2. 1. Macro Regime Breakdown Summary 
![Macro Regime Analysis](./images/no4.macro_regime_analysis.jpeg)

# 3. 2. Strategy Optimization Scoreboard 
![Cumulative Returns Comparison](./images/no2.culmulative_returns_comparison.png)
![Extended Portfolio Risk Summary](./images/no7.extended_portfolio_risk_summary.jpeg)
![Static vs Dynamic Inverse-Volatility Allocation](./images/no8.static_portfolio_vs_dyanmic_risk_parity.jpeg)

# 4. The 2022 Inflationary Regime: Structural Correlation Breakdown 
![Correlation Breakdown](./images/no5.correlation_breakdown.png)

# 5. Risk Dynamics & Volatility Clustering 
![Portfolio Risk Dynamics](./images/no6.portfolio_risk_dynamics.png)

---
## Limitations

- The analysis is based on a relatively short sample beginning in 2020 and therefore covers only a limited number of macroeconomic regimes.
- Historical VaR and Expected Shortfall are estimated from realized returns and do not constitute full regulatory Basel capital models.
- The dynamic allocation is an inverse-volatility strategy rather than a full covariance-based risk-parity optimization.
- Results may be sensitive to the selected assets, lookback window, rebalancing frequency, and transaction-cost assumptions.
- The analysis is retrospective and does not guarantee comparable performance under future market conditions.
- The analysis assumes frictionless execution and does not explicitly model transaction costs, taxes, or market impact.
