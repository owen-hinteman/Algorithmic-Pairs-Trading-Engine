# Pairs Trading & Statistical Arbitrage Analysis

A quantitative finance project designed to test cointegration between financial assets, verify spread stationarity, and backtest a Z-score-based mean-reversion algorithmic trading strategy.

---

## 📌 Project Overview

Statistical arbitrage uses quantitative models to identify pricing inefficiencies between correlated assets. This project focuses on **Pairs Trading**, a strategy that:
1. Identifies co-integrated or highly correlated asset pairs.
2. Tracks the historical spread between the assets.
3. Generates **BUY** or **SELL** signals when the spread deviates significantly from its moving average (measured via Z-Score).
4. Exits positions when the spread reverts back to its historical mean.

---

## 🛠️ Tech Stack & Dependencies

* **Language:** Python 3.8+
* **Data Retrieval:** [`yfinance`](https://github.com/ranaroussi/yfinance)
* **Data Manipulation:** [`pandas`](https://pandas.pydata.org/), [`numpy`](https://numpy.org/)
* **Statistical Modeling:** [`statsmodels`](https://www.statsmodels.org/)

---

## 🚀 Key Workflow & Features

### 1. Data Ingestion
Retrieves daily closing prices across distinct asset classes:
* **Energy / Equities:** EOG Resources (`EOG`) vs. ConocoPhillips (`COP`)
* **Precious Metals / ETFs:** SPDR Gold Shares (`GLD`) vs. iShares Silver Trust (`SLV`)
* **Dual-Class Shares:** Alphabet Inc. (`GOOGL` vs. `GOOG`)

### 2. Statistical Testing
* **Engle-Granger Cointegration Test:** Applied to `EOG`/`COP` and `GLD`/`SLV` to test for long-term equilibrium relationships.
* **Augmented Dickey-Fuller (ADF) Test:** Applied to the `GOOGL`/`GOOG` ratio spread to confirm mean-reverting stationarity.

### 3. Strategy & Signal Generation
Using a **30-day rolling window**, the algorithm calculates the dynamic Z-Score of the spread:

$$\text{Z-Score} = \frac{\text{Spread} - \mu_{30}}{\sigma_{30}}$$

* **BUY Signal (Position = 1):** $\text{Z-Score} < -2.0$ (Spread is undervalued)
* **SELL Signal (Position = -1):** $\text{Z-Score} > 2.0$ (Spread is overvalued)
* **HOLD / FLAT (Position = 0):** $-2.0 \le \text{Z-Score} \le 2.0$

### 4. Backtesting
Evaluates cumulative returns by applying position signals to the daily percentage change of the spread, adjusting for lookahead bias by shifting signals by $t+1$.

---

## 📈 Summary Results

* **Stationarity:** The `GOOGL`/`GOOG` spread demonstrated strong stationarity ($p = 0.0036$).
* **Strategy Performance:** Over the tested period, the Z-score mean-reversion strategy achieved a **10.96% cumulative return**.

---

## 📂 Repository Structure

```text
pairs-trading-analysis/
│
├── .gitignore          # File exclusions for Git
├── README.md           # Project documentation
├── requirements.txt    # Python library dependencies
└── pairs_trading.ipynb # Main Jupyter Notebook containing code & analysis
