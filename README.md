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

When rendered, the report:
1. **Loads and validates the data**: shape, data types, missing values and unique IDs.
2. **Sets up the matrices**: standardizes the three predictors with broadcasting and builds
   the design matrix `X` with an intercept column.
3. **Fits the model by least squares** with `np.linalg.lstsq()`, then computes the fitted
   values, residuals and RMSE.
4. **Runs matrix diagnostics**: QR decomposition and SVD, each verified with
   `np.allclose()`, the matrix rank, and condition numbers for the standardized and raw
   design matrices.
5. **Ends with a written reflection** on reproducibility and numerical computing.

## Main Findings
- The intercept (50.61) equals the mean of `streamflow_index`, as expected with
  standardized predictors.
- Snowpack has the largest standardized coefficient (13.29), followed by precipitation
  (4.74) and mean temperature (−4.11). Streamflow is higher with more snowpack and
  precipitation, and lower in warmer conditions.
- The residuals average to zero (up to rounding), and the RMSE is 7.51.
- The QR and SVD reconstructions match `X`, and the design matrix has full rank (4).
- Standardization reduced the condition number from about 3321 (raw) to 3.30, so the raw
  design was badly scaled rather than truly collinear.