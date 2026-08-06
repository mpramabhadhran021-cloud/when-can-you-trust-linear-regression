# When Can You Trust Linear Regression?

An investigation of the robustness of Ordinary Least Squares (OLS) under real-world data conditions.

## Overview

OLS returns coefficients, standard errors, and p-values whether or not the data satisfy the conditions that make those numbers meaningful. This project treats OLS as a scientific instrument and asks, empirically, when it can be trusted.

Four controlled Monte Carlo experiments — each varying one property of the data while holding a common baseline model fixed — quantify how OLS's coefficients, confidence intervals, and predictive accuracy respond to:

1. Shrinking sample size
2. Response outliers
3. Predictor multicollinearity
4. Unmodeled curvature (nonlinearity)

Two of these are then extended into head-to-head method comparisons against a standard robust alternative (Huber regression vs. outliers, Ridge regression vs. multicollinearity), to test whether switching methods helps as much as the diagnostics suggest it should. Finally, the resulting diagnostic checklist is applied to a real dataset with unknown ground truth (the scikit-learn diabetes cohort) to test whether the simulation-derived intuitions transfer.

## Key finding

Three of the four violations (sample size, outliers under symmetric contamination, multicollinearity short of near-perfect correlation) leave the average coefficient estimate essentially unbiased — the damage is to precision or prediction, not the point estimate. Nonlinearity is the exception: it can bias coefficients outright when omitted curvature correlates with an included predictor, and even when it doesn't, it quietly destroys predictive accuracy. The diagnostic checklist built from the simulations (VIF, Breusch–Pagan, Ramsey RESET, Cook's distance) transfers cleanly to the real-data case study.

## Structure

```
when_can_you_trust_linear_regression.ipynb   # primary notebook — full workflow
figures/                                      # exported figures (1, 2, 2b, 3, 3b, 4, 5, 6)
requirements.txt
report.pdf                                    # rendered report
```

## Methods

Monte Carlo simulation (1,000 replications per condition) around a fixed baseline data-generating process, one-factor-at-a-time design, `statsmodels.OLS` as the primary estimator, `HuberRegressor` and `Ridge` (scikit-learn) for the robust-method comparisons. Diagnostics: Variance Inflation Factor, Breusch–Pagan test, Ramsey RESET test, Cook's distance. Real-data validation on the scikit-learn diabetes cohort (n=442, 10 predictors).

## Reproducing

```
pip install -r requirements.txt
jupyter notebook when_can_you_trust_linear_regression.ipynb
```

All randomness is seeded (NumPy's `default_rng`), so re-running the notebook end to end reproduces every number and figure exactly. No external datasets are required — all data are either simulated or loaded from scikit-learn.
