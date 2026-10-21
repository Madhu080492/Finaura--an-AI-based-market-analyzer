# FINAURA
### AI-Based Financial Market Regime Detection, Risk Forecasting & Portfolio Analytics

FINAURA is an academic integrated project that explores financial-market risk using historical market data, machine learning, statistical analysis, and data visualization. Its main supervised-learning objective is to estimate **next 5-trading-day realized volatility** for selected market assets.

The project is intended to support risk analysis and informed decision-making. It is **not** a guarantee of returns, a recommendation to buy or sell securities, or a system that predicts exact future stock prices.

> **Project status:** Data collection, preprocessing, exploratory data analysis (EDA), and initial model experiments are present in the repository. Model evaluation and validation are ongoing. The complete web application and dashboard are planned and are not yet implemented.

---

## Contents

- [Objectives](#objectives)
- [Datasets](#datasets)
- [Technology Stack](#technology-stack)
- [Repository Structure](#repository-structure)
- [Machine Learning Approach](#machine-learning-approach)
- [Statistical and Risk-Analysis Scope](#statistical-and-risk-analysis-scope)
- [Getting Started](#getting-started)
- [Workflow](#workflow)
- [Current Limitations and Next Steps](#current-limitations-and-next-steps)
- [Responsible Use](#responsible-use)

## Objectives

- Collect and analyze historical financial and cross-asset data.
- Clean datasets and create useful time-series features.
- Explore trends, distributions, volatility, and relationships through EDA.
- Experiment with baseline and machine-learning models for volatility forecasting.
- Build toward portfolio-risk analytics, risk metrics, and scenario analysis.
- Present results through clear visualizations and, in a later phase, a web dashboard.

## Datasets

The repository contains raw and processed files for these eight dataset groups:

| Dataset | Example file in `data/raw/` | Frequency / notes |
|---|---|---|
| NIFTY 50 | `nifty50_raw.csv` | Historical index market data |
| Selected NSE stocks | `nse_stocks_raw.csv` | Historical data for selected stocks; processed data may contain a `symbol` column |
| India VIX | `india_vix_raw.csv` | Market volatility index data |
| Gold | `gold_raw.csv` | Historical gold-price data |
| USD/INR | `usd_inr_raw.csv` | Exchange-rate data |
| Delhi Petrol | `delhi_petrol_raw.csv` | Fuel-price history |
| Delhi Diesel | `delhi_diesel_raw.csv` | Fuel-price history |
| Indian Basket Crude Oil | `indian_basket_crude_raw.xlsx` | Crude-oil data; the source data is monthly |

Data availability, coverage, frequency, and columns vary by dataset. Check each notebook and the corresponding CSV before using a dataset in analysis. Source attribution should be retained alongside the data when the source is known.

## Technology Stack

**Used in the current analysis**
- Python
- Pandas and NumPy
- Scikit-learn
- Matplotlib and Seaborn
- yfinance (for market-data retrieval where configured)
- Jupyter Notebook
- CSV and Excel files for dataset storage

**Planned for the complete application**
- React — frontend
- FastAPI — backend/API
- PostgreSQL — database

The planned application stack is not part of the currently completed notebook workflow.

## Repository Structure

```text
FINAURA/
├── download_data.py
├── data/
│   ├── raw/                 # Original downloaded/source datasets
│   ├── processed/            # Cleaned datasets, EDA summaries and experiment outputs
│   └── raw.zip               # Archived raw data (if retained)
└── notebooks/
    ├── 01_NIFTY50_Preprocessing.ipynb
    ├── 02_NSE_Stocks_Preprocessing.ipynb
    ├── 03_India_VIX_Preprocessing.ipynb
    ├── 04_Gold_Preprocessing.ipynb
    ├── 05_USD_INR_Preprocessing.ipynb
    ├── 06_Delhi_Petrol_Preprocessing.ipynb
    ├── 07_Delhi_Diesel_Preprocessing.ipynb
    ├── 08_Indian_Basket_Crude_Preprocessing.ipynb
    ├── 09_*_EDA.ipynb
    └── 10_*_Initial_Model_Experiments.ipynb
```

The exact notebook names are dataset-specific; see the `notebooks/` folder for the complete list.

## Machine Learning Approach

The main forecasting target is **next 5-trading-day realized volatility** for market assets.

Initial experiments include:
1. **Mean baseline** — predicts the mean target calculated from the training data.
2. **Linear Regression** — a simple supervised-learning benchmark.
3. **Random Forest Regressor** — a non-linear model for comparison.

### Evaluation

- **MAE (Mean Absolute Error):** primary error metric.
- **RMSE (Root Mean Squared Error):** secondary error metric.
- **Chronological train/test split:** preferred for time-series data.
- **Leakage checks:** features must not use information from after the prediction timestamp.

Saved result files in `data/processed/` include dataset-specific initial model metrics, prediction outputs, and feature-importance tables where available. These are preliminary experiment artifacts; verify the target definition, feature construction, split strategy, and metrics before treating any score as final.

Fuel-price and crude-oil experiments may use different forecast targets and frequencies. They should not be assumed to share the five-trading-day volatility target.

## Statistical and Risk-Analysis Scope

The broader project is designed to explore or integrate:

- Asset returns and rolling volatility
- Correlation analysis
- Portfolio return and volatility estimates
- Value at Risk (VaR)
- Monte Carlo simulation
- Stress testing under selected scenarios
- Market-regime analysis

These are project objectives and planned analysis areas; not every item is implemented as a complete application feature yet. Any market-regime labels or risk thresholds must be defined and validated before being presented as reliable outputs.

## Getting Started

### 1. Requirements

Install Python 3 and use a virtual environment if possible. From a terminal opened in the project folder, run:

**Windows PowerShell**
```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install pandas numpy scikit-learn matplotlib seaborn yfinance jupyter openpyxl
```

If PowerShell blocks virtual-environment activation, you can run the environment's Python directly or use the activation method recommended for your setup. Install any additional package required by a specific notebook if it reports a missing dependency.

### 2. Open the notebooks

```powershell
jupyter notebook
```

Alternatively, open the project folder in VS Code and use its Jupyter notebook support.

### 3. Recommended order

1. Review the relevant file in `data/raw/`.
2. Run the matching preprocessing notebook in `notebooks/`.
3. Review the matching EDA notebook.
4. Run the corresponding initial model experiment notebook, if one exists and is ready.
5. Inspect the generated files in `data/processed/`.

Run notebooks in order and check each output before moving to the next. Some notebooks depend on processed files created by earlier notebooks.

### 4. Data download script

`download_data.py` is included for market-data retrieval. Review its date range, symbols, output paths, and data-provider requirements before running it. Data-provider availability and returned historical values can change; compare downloaded data with the existing files before overwriting anything.

## Workflow

```text
Raw datasets
    ↓
Preprocessing and validation
    ↓
Processed datasets
    ↓
Exploratory Data Analysis (EDA)
    ↓
Feature engineering and target creation
    ↓
Baseline and ML experiments
    ↓
MAE / RMSE evaluation and leakage checks
    ↓
Risk analytics and application integration (planned)
    ↓
Dashboard and final validation (planned)
```

## Current Limitations and Next Steps

- Verify and, where necessary, correct target calculations before rerunning experiments.
- Confirm that training and test data are separated chronologically.
- Ensure each model is evaluated on the same valid test period and comparable rows.
- Record actual MAE/RMSE values only after validating the experiment outputs.
- Complete or document any missing dataset-specific experiment notebooks.
- Finalize and validate the market-regime detection method.
- Implement and test the portfolio-risk engine.
- Develop the planned API, database, frontend, and dashboard.
- Add automated tests, dependency versions, and reproducible run instructions as the project matures.

## Responsible Use

FINAURA is an educational research and decision-support project. Forecasts and risk estimates are uncertain, depend on historical data and modelling assumptions, and can perform poorly when market conditions change. Outputs should not be treated as personalized financial advice or as a guarantee of future performance.
