# AdShield Trust & Safety Dashboard

AdShield is a self-contained Trust & Safety analytics prototype for ad platforms. It simulates advertiser activity, computes platform health KPIs, detects anomalies using a rolling 7-day baseline, and provides decision-ready views for investigation and executive reporting.

## Overview

This project was built to demonstrate how Trust & Safety metrics can be translated into a working product surface for risk monitoring. The dashboard combines KPI scorecards, trend analysis, anomaly detection, and advertiser-level exploration in a single static prototype.

## Features

- KPI scorecards for Violation Prevalence, False Positive Rate, Action Rate, and Precision.
- Trend chart for recent platform health movement.
- Rolling-baseline anomaly detection using mean, standard deviation, and z-score logic.
- Explorer view with category filters and anomaly-only mode.
- Weekly executive-style summary generated from KPI movement and top anomalies.
- Synthetic advertiser activity data for demo and prototyping purposes.

## Metrics used

### 1. Violation Prevalence (‰)
Measures how many confirmed violations occur per 1,000 impressions.

Formula:

`Prevalence = (confirmed_violations / impressions) * 1000`

### 2. False Positive Rate (FPR)
Measures how many flagged cases were incorrect, based on the dashboard's current definition.

Formula:

`FPR = false_positive_flags / (false_positive_flags + confirmed_violations)`

### 3. Action Rate
Measures how many reviewed cases resulted in an action.

Formula:

`Action Rate = action_taken_count / human_reviewed_count`

### 4. Precision
Measures how many flagged cases were actually correct.

Formula:

`Precision = confirmed_violations / (confirmed_violations + false_positive_flags)`

## Anomaly logic

The anomaly engine compares current advertiser-level behavior with the previous 7-day baseline.

Steps used in the prototype:

1. Take the previous 7 days of values for a monitored metric.
2. Calculate the rolling mean.
3. Calculate the rolling standard deviation.
4. Compute the z-score:

`z = (current_value - rolling_mean) / rolling_standard_deviation`

5. Flag the record as anomalous when `|z| >= 2.5`.

Severity buckets used:

- Medium: `|z| >= 2.5`
- High: `|z| >= 3.2`
- Critical: `|z| >= 4.0`

Metrics monitored for anomaly detection in this prototype:

- Ad Spend
- Reported Violations
- CPM-like Ratio

## Explorer behavior

The explorer supports category filters and an **Anomalies only** mode.

When anomaly-only mode is enabled, the table shows advertiser-day rows whose `date + advertiser_id` exists in the anomaly set. This means a row may appear because one monitored metric crossed the anomaly threshold, even if not every visible value in that row looks unusual on its own.

## How to run

This is a static HTML prototype.

### Option 1: Open directly

- Download the repository.
- Open the HTML file in a browser.

### Option 2: Run a local server

If you prefer serving it locally:

```bash
python -m http.server 8000
```

Then open:

```text
http://localhost:8000/
```

## Project structure

```text
.
├── adshield.html
└── README.md
```

## Why this project

This prototype was created to demonstrate:

- Product thinking for Trust & Safety workflows.
- KPI design for risk monitoring.
- Practical anomaly detection using rolling baselines.
- Ability to communicate data to both technical and non-technical stakeholders.

## Limitations

- Uses synthetic data, not live production data.
- Built as a self-contained prototype, not a production deployment.
- Current FPR definition is dashboard-specific and may differ from strict statistical definitions.
- Anomaly results are designed for demonstration and exploratory investigation.

## Possible next improvements

- Add a Triggered Metric column in anomaly-only mode.
- Add tooltips for KPI definitions and formulas.
- Export weekly summaries to CSV or PDF.
- Replace synthetic data with API-driven or database-backed ingestion.
- Add reviewer workflow and case-level drill-downs.

## Screenshots

Add screenshots here after pushing the project to GitHub.

## Resume-ready summary

Built a static Trust & Safety analytics dashboard for ad platforms with KPI scorecards, advertiser-level anomaly detection, and executive-ready weekly reporting.
