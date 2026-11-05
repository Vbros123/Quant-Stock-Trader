# Quant Stock Trader

Python stock-ranking research and a local company-research API. This repository
preserves the recovered ranking v4 and Analyst Lab v4.1 packages, including their
tests, methodology, historical results, and known limitations.

## Start here

- [Ranking model and backtests](nasdaq_ranker_v4/README.md): configurable monthly
  top-five screening, momentum and defensive factors, trading costs, and SPY comparisons.
- [Research backend](analyst_backend_free_v4/README.md): authenticated local
  FastAPI service, SQLite snapshots, SEC, NASDAQ directory, GDELT, economic data,
  optional local AI commentary, and Cboe VIX ingestion.
- [API guide](analyst_backend_free_v4/API_GUIDE.md).
- [Point-in-time and VIX guide](analyst_backend_free_v4/PIT_VIX_GUIDE.md).
- [Measured failures and repairs](nasdaq_ranker_v4/results_v4/FAILURE_ANALYSIS_V4.md).
- [Free data catalog](analyst_backend_free_v4/FREE_SOURCE_CATALOG.md).

## Run the ranker

Use Python 3.11+ and run each component from its own directory.

```bash
cd nasdaq_ranker_v4
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
python -m pytest -q
python run_model_v4.py --help
```

The component README explains how to download research inputs and provide fresh
canonical data for screening. No current recommendations are implied by the
historical result files. The large historical price archive is downloaded
separately using `download_data.py`.

## Run the backend

In a separate terminal, from the repository root:

```bash
cd analyst_backend_free_v4
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
python validate.py
python serve.py
```

The default address is `http://127.0.0.1:8765`. From the same component directory
in another activated terminal, run `python client.py demo`. The service creates
a private local token; do not commit it or your runtime database. SEC ingestion
requires your own honest contact identity in `SEC_USER_AGENT`.

## Research status

The model has not demonstrated consistent, validated risk-adjusted outperformance
of SPY. The archived price study uses a survivor directory and is illustrative
development evidence, not a survivorship-free out-of-sample test. Negative results
are intentionally retained. Point-in-time infrastructure does not fill missing
historical delistings, terminal returns, or fundamental vintages.

These are two separately runnable components. The backend's news and VIX data
are not automatically integrated into or proven to improve the ranking model.
There is no brokerage connection or live automated trading in this release.
Optional AI commentary is not a replica of ChatGPT or a validated trading signal.

Original manifests and validation records describe the saved releases, not a new
market-data run. Personal portfolio screenshots and account data are excluded.
Provider data remains subject to its original terms; this repository grants no
additional rights to redistribute third-party datasets.

Research and screening only, not financial advice. Backtested performance does
not guarantee future results.
