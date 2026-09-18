# When Can You Trust Linear Regression?

## What is this project?

This project studies how ordinary least squares (OLS) behaves when the data are not ideal.

I use simulated data so that the true model is known. This lets me see how different problems affect estimates and predictions.

## Research Question

> How do common problems in the data affect OLS estimates, uncertainty, and prediction?

## Experiments

I study four situations:
1. Small sample sizes
2. Outliers
3. Correlated predictors
4. Nonlinear relationships

I also compare OLS with Huber regression for outliers and Ridge regression for multicollinearity.

Finally, I apply some of the same diagnostics to the scikit-learn diabetes dataset.

## Method

The main part uses Monte Carlo simulation. For each experiment, I generate many datasets from a known model and change one feature at a time.

I also use VIF, the Breusch-Pagan test, the Ramsey RESET test, and Cook's distance.

## Main Findings

The different problems do not affect OLS in the same way. Small samples and multicollinearity mainly reduce precision. Outliers can affect estimates and predictions. Nonlinearity can cause problems when a linear model is used for a curved relationship.

The main lesson is that a regression result should be checked before it is interpreted.

## Repository

when_can_you_trust_linear_regression.ipynb — main notebook
figures/ — figures
requirements.txt — required packages
report.pdf — project report

## How to Run

pip install -r requirements.txt
jupyter notebook when_can_you_trust_linear_regression.ipynb

## Limitations

Simulation results depend on the data-generating process chosen for the experiments. The real-data example does not have a known true model.