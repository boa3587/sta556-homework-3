# STA 556 Homework 3: Reproducibility & Matrix Computation

## Purpose
A reproducible Quarto report that fits and diagnoses a linear model using NumPy matrix
computation. The report standardizes the predictors, builds the design matrix, fits the model
by least squares, and checks the fit with QR decomposition, SVD and condition numbers.

## Data
This project uses **Option C, the watershed conditions dataset** (`data/watershed.csv`),
provided with the assignment. The data are synthetic, so no causal claims are made.

- **Observations:** 125 (one row per watershed observation, no missing values, unique IDs)
- **Response:** `streamflow_index`
- **Predictors:** `snowpack_pct_normal` (snowpack as % of normal), `precip_mm`
  (precipitation in millimetres), `mean_temp_c` (mean temperature in °C)

## Project Structure
```
sta556-homework-3/
├── data/
│   └── watershed.csv         # provided dataset, read by the report, not modified
├── reports/
│   ├── homework3.qmd         # report source: all code, output and written responses
│   └── homework3.html        # rendered report produced from homework3.qmd
├── .gitignore
└── README.md
```

The report reads the data with the relative path `../data/watershed.csv`, so keep this
folder structure as it is.

## How to Run
From the repository root, render the report with:

```bash
quarto render reports/homework3.qmd
```

This runs every code cell in order in a fresh Python session and writes
`reports/homework3.html`. Every number in the report comes from the code; no results are
typed in by hand.

When