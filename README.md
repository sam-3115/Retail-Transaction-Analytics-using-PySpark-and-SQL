# Retail Sales Analytics (PySpark + PostgreSQL)

End-to-end sales analytics on ~1M retail transactions.
Dataset: Online Retail II (UCI / Kaggle).

## Architecture

    Raw CSV (~1M rows)
          |
          v
    PySpark: clean, deduplicate, derive revenue
          |
          v
    Partitioned Parquet (year/month)
          |
          v
    PostgreSQL (sales table + indexes) via Spark JDBC
          |
          v
    SQL analysis (CTEs, window functions)
          |
          v
    CSV results + Matplotlib charts

## Setup

Requirements: Python 3.9+, Java 11 or 17 (needed by Spark), Docker.

    pip install -r requirements.txt
    docker compose up -d

Download `online_retail_II.csv` from Kaggle ("Online Retail II UCI")
and place it at `data/online_retail_II.csv`.

## Run (always from the project root)

    python src/01_clean_with_spark.py
    python src/02_load_to_postgres.py
    python src/03_run_analysis.py

Results (CSV + charts) are saved in `outputs/`.

## Analyses

- Monthly sales trend with month-over-month growth
- Top 10 products by revenue
- Revenue by country
- Repeat customer rate
- Top 10 customers by spend
