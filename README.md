# Tanken.fyi

This repository is going to be populated with the source code from [tanken.fyi](https://tanken.fyi), which is the companion website for the apps

- [Spritpreise Österreich for iOS](https://apps.apple.com/at/app/spritpreise-at-clever-tanken/id1613791034)
- [Spritpreise Österreich for Android](https://play.google.com/store/apps/details?id=tech.pertiller.spritpreise.at&hl=de&gl=at&utm_source=tanken.fyi)

## Austria: Historical Fuel Prices

This repository contains a JSON Schema that defines the structure for historical fuel pricing statistics in Austria. The underlying data includes an export of aggregated metrics for Diesel, Super 95, CNG (Compressed Natural Gas), and Crude Oil benchmarks, recorded at regular intervals.

### Overview

The data is designed to support time-series data analysis and visualization, ensuring consistent structure and interpretation across datasets.

**Key features:**

- ISO 8601 timestamps in UTC
- Statistical summaries per fuel type: min, max, mean, median, and quantiles
- Dual crude oil prices: Brent (primary) and WTI
- Percentile-based outlier detection

### Quantile Thresholds Explained

The schema includes four statistical quantiles beyond the standard min/max/mean/median:

| Quantile  | Approx. Value   | Interpretation                               |
| --------- | --------------- | -------------------------------------------- |
| `q-0.01`  | 1st percentile  | Cheapest outlier threshold                   |
| `q-0.159` | 15.9th          | Roughly -1 standard deviation (normal dist.) |
| `q-0.841` | 84.1st          | Roughly +1 standard deviation (normal dist.) |
| `q-0.98`  | 98th percentile | Most expensive outlier threshold             |

### File Structure

- `export/at/stats/at-fuel-stats.schema.json` — The main JSON Schema file
- `export/at/stats/at-fuel-stats.data.json` — Exported data conforming to the schema
