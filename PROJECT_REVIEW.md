# Project cleanup review

## Changes made
- Replaced the misleading CNN/MLP project branding with a title that matches the notebook and report: Real-Time Stock Market Stream Analysis.
- Kept one canonical notebook; the two uploaded notebooks were byte-for-byte identical.
- Renamed the notebook and report to simple, consistent filenames.
- Rewrote the README with purpose, architecture, setup, configuration, and limitations.
- Cleared saved notebook outputs to avoid publishing stale logs or accidental secrets.
- Removed the embedded InfluxDB token from notebook source and replaced it with an environment variable.
- Added requirements, `.env.example`, and `.gitignore`.

## Review before publishing
- Rotate/revoke the previously embedded InfluxDB token if it was ever valid.
- Verify the Spark/Kafka connector version matches the installed Spark version.
- Run each streaming section against a controlled sample stream and confirm expected results.
- Review window aggregation logic, output modes, timestamp parsing, and InfluxDB/Grafana integration.
- Check that the course report is okay to publish publicly.
