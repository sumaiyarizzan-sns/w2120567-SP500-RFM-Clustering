# 6BUIS017W Coursework 1: Market Analysis and Stock Segmentation Using RFM

Business intelligence analysis of S&P 500 shares (1 Jan 2021 to 1 Jan 2025, end exclusive). It compares clusters built on **risk and return** (mean weekly return, weekly beta vs `^GSPC`) with clusters built on **adapted RFM trading activity** (Recency, Frequency and Monetary of unusually high-volume days).

## How to run
1. Open `w2120567_SP500_RFM_Clustering.ipynb` in Google Colab.
2. Run all cells. With `USE_CACHE = True`, the notebook reads the saved snapshot in `data/raw/` and every result is reproduced exactly. If the snapshot is missing, it downloads fresh data and saves it.

## Repository contents
| Path | Contents |
|---|---|
| `w2120567_SP500_RFM_Clustering.ipynb` | Full analysis (Tasks 1 and 2, plus the exports used for Task 3) |
| `data/raw/sp500_constituents.csv` | Wikipedia constituent list as retrieved |
| `data/raw/daily_*.csv.gz` | Daily Adj Close, Close, Volume, splits and dividends from yfinance |
| `data/raw/retrieval_metadata.json` | Source URLs and retrieval timestamps |
| `outputs/feature_table_with_clusters.csv` | One row per share: features plus all cluster assignments |
| `outputs/exclusion_log.csv` | Every excluded share and the rule it failed |
| `outputs/run_metadata.json` | Observation date, windows, selected k, ARI results |
| `outputs/package_versions.txt` | Exact package versions |
| `outputs/figures/` | All report figures |

## Key definitions
- **Weekly return:** Friday-ending weeks on Adj Close, with incomplete edge weeks removed and no filling.
- **Weekly beta:** cov(share, benchmark) / var(benchmark), calculated over aligned weeks.
- **Event:** volume > 2 × mean volume of the preceding 20 sessions, excluding the event day.
- **R:** calendar days from the latest event to the observation date. **F:** event days in the last 60 sessions. **M:** Σ Close × Volume over the last 60 sessions, in USD.

RFM here describes trading activity. It is not a measure of company value or a prediction of future returns.
