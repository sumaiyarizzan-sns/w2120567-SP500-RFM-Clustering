# 6BUIS017W Coursework 1 – S&P 500 Stock Segmentation Using RFM

**Student:** Sumaiya Rizan (w2120567)
**Module:** 6BUIS017W CRM & CM with Business Intelligence, University of Westminster

This repo has the code and data for my CW1 report. I clustered S&P 500 shares in two different ways and compared them:

1. **Risk and return**: mean weekly return and weekly beta against the S&P 500 (^GSPC)
2. **Trading activity**: an adapted RFM based on unusually high-volume days (Recency, Frequency and Monetary)

The study period is 1 January 2021 to 1 January 2025 (end date not included).

## How to run it

1. Open `w2120567_SP500_RFM_Clustering.ipynb` in Google Colab.
2. Click **Runtime → Run all**.

The notebook first looks for the saved data in `data/raw/`. If it finds it, it uses that snapshot, so you get exactly the same results as in my report. If the folder is missing, it downloads fresh data from Wikipedia and Yahoo Finance instead (this takes about 5 minutes).

## What's in the repo

- `w2120567_SP500_RFM_Clustering.ipynb` – the full analysis with all outputs (Tasks 1 and 2, plus the tables used in Task 3)
- `data/raw/` – the data snapshot I used: the S&P 500 list from Wikipedia and daily prices, volume, splits and dividends from yfinance, plus the retrieval dates
- `outputs/feature_table_with_clusters.csv` – one row per share with all the features and cluster labels
- `outputs/exclusion_log.csv` – the shares I excluded and why
- `outputs/run_metadata.json` – observation date, windows, chosen k values and main results
- `outputs/package_versions.txt` – the library versions I used
- `outputs/figures/` – all the charts in the report
- `outputs/sp500_datamart.sqlite` – a small prototype of the data mart from Task 3.1
- `requirements.txt` – the Python packages needed

## Main definitions

- **Weekly return**: Friday-ending weeks using Adjusted Close. Incomplete first and last weeks are removed, and missing prices are never filled.
- **Beta**: covariance of the share's and the benchmark's weekly returns, divided by the variance of the benchmark's returns.
- **High-volume day**: volume is more than 2× the average of the previous 20 trading days (the day itself isn't included in the average).
- **R**: calendar days from the last high-volume day to 31 Dec 2024. **F**: number of high-volume days in the last 60 sessions. **M**: sum of Close × Volume over those 60 sessions, in USD.

Note: RFM here describes trading activity only. It doesn't measure company value and isn't a prediction of future returns.
