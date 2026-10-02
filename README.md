# Rossmann Sales & Seasonality — Time Series Case Study

An end-to-end time series analysis of Rossmann drug store sales: exploratory analysis, stationarity testing, seasonal decomposition, feature engineering, and forecasting (SARIMA, Prophet, XGBoost) with business recommendations for promotions, staffing, and inventory planning.

This project was completed as a case study on **Marketing — Sales Performance and Seasonality Trends**, covering time series EDA, decomposition, modeling, and translating model outputs into actionable marketing decisions.

## Dataset

Source: [Rossmann Store Sales (Kaggle)](https://www.kaggle.com/competitions/rossmann-store-sales)

| File | Included in repo? | Description |
|---|---|---|
| `train.csv` |  Not included (exceeds GitHub's file size limit) | Daily sales history per store — download separately from Kaggle and place in the project folder before running the notebook |
| `test.csv` | Yes | Store-day records to generate predictions for |
| `store.csv` | Yes | Store metadata (type, assortment, competition distance, promo participation) |
| `sample_submission.csv` | Yes | Kaggle's expected submission format |

**To run this notebook yourself:** download `train.csv` from the Kaggle competition page above and place it in the same folder as the notebook — the code expects it at `train.csv` relative to the notebook's working directory.

## Project Structure

```
├── Untitled.ipynb          # Main analysis notebook (all 22 tasks)
├── test.csv                 # Provided
├── store.csv                 # Provided
├── sample_submission.csv     # Provided
├── train.csv                 # NOT included — download from Kaggle
└── README.md
```

## What's Covered

The notebook works through the full time series workflow:

- **Data understanding** — data dictionary, daily aggregation, raw sales plots
- **Descriptive statistics** — mean/median/variance/skewness/kurtosis, overall and by month
- **Seasonality** — subseries plots by month and day-of-week
- **Stationarity** — ACF/PACF analysis, ADF and KPSS tests, log transform, Box-Cox, non-seasonal and seasonal differencing
- **Decomposition** — additive, multiplicative, and STL decomposition compared
- **Data quality** — missing date handling, store-closure logic, outlier and structural break detection
- **Feature engineering** — 13 features including lags, rolling statistics, cyclical date encodings, and interaction terms
- **Modeling** — expanding-window train/validation/test split; SARIMA, Prophet, and XGBoost models compared via rolling-origin cross-validation (MAE/RMSE)
- **Uncertainty & interpretation** — prediction intervals and coverage rates, XGBoost feature importance, a +20% promo-uplift scenario simulation
- **Reporting** — observed-vs-forecast dashboard, executive summary, and documented limitations

## Key Findings

- **Promotions and day-of-week are the strongest sales drivers** — `is_weekend`, `is_holiday`, and `dow` dominate XGBoost's feature importance, ahead of lag/rolling features.
- **Strong weekly seasonality** — ACF/PACF show clear spikes at lag 7; seasonal differencing at lag 7 is needed to fully stabilize the series.
- **XGBoost outperformed SARIMA and Prophet** on validation RMSE/MAE, while SARIMA and Prophet gave better-calibrated 80% prediction intervals (93% and 92% coverage vs. XGBoost's 23%, indicating the XGBoost intervals need recalibration).
- **December shows a clear seasonal sales peak**, useful for timing inventory ramp-up and staffing.

## Tools & Libraries

`pandas`, `numpy`, `matplotlib`, `seaborn`, `scipy`, `statsmodels`, `prophet`, `xgboost`, `scikit-learn`

## How to Run

1. Clone this repo
2. Download `train.csv` from the [Kaggle Rossmann competition](https://www.kaggle.com/competitions/rossmann-store-sales) and place it in the project folder
3. Install dependencies: `pip install pandas numpy matplotlib seaborn scipy statsmodels prophet xgboost scikit-learn`
4. Open `Untitled.ipynb` in Jupyter and run all cells
