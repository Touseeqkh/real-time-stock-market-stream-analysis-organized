# Real-Time Stock Market Stream Analysis

A course project demonstrating real-time stock-price processing with **Apache Kafka** and **Apache Spark Structured Streaming**, with optional output to **InfluxDB** for monitoring in Grafana.

> **Scope note:** This repository contains a streaming analytics notebook. It does not implement CNNs or MLPs, so the previous `CNN-and-MLP` repository name and description were inaccurate.

## Project goals

- Ingest stock-price events from a Kafka topic.
- Parse streaming events into a structured Spark DataFrame.
- Calculate windowed average prices by stock.
- Explore top-priced stocks and falling/rising price movements.
- Visualize selected results with Matplotlib.
- Optionally write windowed results to InfluxDB for dashboarding with Grafana.

## Technology stack

- Python
- Apache Kafka
- Apache Spark Structured Streaming (PySpark)
- Pandas and Matplotlib
- InfluxDB Python client (optional)
- Grafana (optional dashboard layer)

## Repository contents

```text
.
├── stock_market_stream_analysis.ipynb  # Main notebook
├── report.pdf                           # Original course report
├── requirements.txt                     # Python packages
├── .env.example                         # Example configuration keys
├── .gitignore
└── README.md
```

## Requirements

- Python 3.9+ (the notebook was originally created with Python 3.9)
- A compatible Java runtime for your chosen Spark version
- A running Kafka broker and a topic named `stock`
- Optional: InfluxDB and Grafana

The notebook originally references Spark's Kafka connector for Spark 3.0.0 / Scala 2.12. Connector versions must match your installed Spark version. Check the Spark documentation before changing versions.

## Setup

1. Create and activate a virtual environment.
2. Install Python dependencies:

   ```bash
   pip install -r requirements.txt
   ```

3. Start Kafka and ensure the `stock` topic receives events with fields matching the notebook schema:

   ```json
   {
     "name": "AAPL",
     "price": 187.25,
     "timestamp": "2026-10-11T12:00:00"
   }
   ```

   Adapt timestamp parsing to the actual producer format and the schema expected by your Kafka stream.

4. Configure the Kafka bootstrap address with `KAFKA_BOOTSTRAP_SERVERS` if it differs from `localhost:9092`.
5. Open `stock_market_stream_analysis.ipynb` in Jupyter and run the cells in order, after reviewing each streaming query's timeout and stop behavior.

## Optional InfluxDB configuration

Set these environment variables before running the InfluxDB cells:

- `INFLUXDB_URL`
- `INFLUXDB_TOKEN`
- `INFLUXDB_ORG`
- `INFLUXDB_BUCKET`

Copy `.env.example` as a local reference if useful, but **never commit real credentials or `.env` files**. The notebook has been changed to read the token from an environment variable rather than embedding it.

## Important limitations and next improvements

- The notebook contains several separate streaming queries; run them one at a time to avoid competing consumers and duplicate processing.
- Some tasks are exploratory and should be validated against a known sample stream before treating their output as definitive.
- Spark aggregation semantics, ordering within windows, watermarks, and output modes need review for the specific Kafka data and Spark version.
- The notebook uses `collect()` / `toPandas()` in places, which is appropriate only for small batches.
- The optional InfluxDB integration needs to be tested against your local InfluxDB version and configured organization/bucket.
- The original report is retained as submitted course documentation.

## Security

A credential was embedded in the original notebook. It has been removed from this cleaned copy and replaced with `INFLUXDB_TOKEN`. If the old token was ever valid, revoke or rotate it in InfluxDB before publishing the repository. Removing a token from the current file does not erase it from Git history.

## Author

Danish Touseeq

## Academic context

Data Processing and Analytics (DPA), International Master's in Data and Intelligence for Smart Systems (DISS), Université Claude Bernard Lyon 1.
