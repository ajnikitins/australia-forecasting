# Forecasting Australian GDP Growth

Econometrics project, Bocconi University, 2025–2026.

This project develops and evaluates econometric models for Australian year-on-year real GDP growth, with a focus on recursive out-of-sample forecasting.

The analysis compares conventional autoregressive benchmarks with richer dynamic specifications incorporating inflation, monetary policy, and labour-market information. It combines model selection, structural-stability analysis, residual diagnostics, and recursive one-step-ahead forecast evaluation over 2016Q1–2025Q4.

**[View the final presentation](australia_forecasting_slides.pdf)**

## Project overview

The analysis uses Australian macroeconomic data from 1993Q1 to 2025Q4 and models quarterly year-on-year real GDP growth.

The main predictors are:

* year-on-year inflation;
* the cash rate and changes in the cash rate;
* the unemployment rate.

Several model classes are considered:

1. **AR(2)** — univariate autoregressive benchmark;
2. **VAR(2)** — multivariate benchmark including GDP growth, inflation, and the cash rate;
3. **ARDL models** — distributed-lag specifications combining GDP dynamics with macroeconomic predictors;
4. **ARDL models with ARMA errors** — allowing residual dynamics, including seasonal components, to capture persistence not explained by the regressors;
5. **ARMAX models** — alternative dynamic specifications in which autoregressive behaviour is modelled through the error process.

Candidate models are estimated using data available before the forecast-evaluation period and shortlisted using AIC and BIC before diagnostic and forecast-performance comparisons.

Parameter-stability tests indicate changes in Australian output dynamics around the Global Financial Crisis. The main specifications therefore include a post-2008Q4 level shift, while recursive CUSUM tests provide little evidence of substantial remaining instability after accounting for this break.

## Forecast evaluation

Models are evaluated using recursive one-quarter-ahead forecasts from 2016Q1 to 2025Q4.

At each forecast origin, the model is re-estimated using only information available before the quarter being forecast. Performance is assessed using:

* mean forecast error;
* mean squared forecast error (MSFE);
* root mean squared forecast error (RMSFE);
* mean absolute forecast error (MAFE);
* forecast-bias tests;
* forecast-error autocorrelation tests;
* Diebold–Mariano tests;
* HAC-robust loss-difference tests.

Because the COVID period dominates squared forecast losses, performance is also evaluated excluding 2020Q1–2022Q4.

## Main findings

* Plain ARDL models improve on the basic AR(2) and VAR(2) benchmarks, but retain substantial residual dynamics associated partly with the year-on-year construction of GDP growth.
* Allowing for ARMA and seasonal residual dynamics produces considerably stronger forecast performance. ARDL-ARMA and ARMAX specifications generally outperform the benchmark models.
* The best full-sample specification, `ARDL_ARMA5010`, reduces MSFE by approximately **44% relative to the AR(2) benchmark**.
* A richer specification, `ARDL_ARMA5250`, incorporates GDP persistence, inflation, changes in the cash rate, and unemployment while retaining similar forecasting performance.
* The relative advantage of the ARDL-ARMA specifications remains when the COVID period is excluded, suggesting that their performance is not driven exclusively by the extreme pandemic observations.
* Despite economically large MSFE reductions, formal Diebold–Mariano and HAC loss-difference tests provide only marginal statistical evidence of superior predictive accuracy. The evaluation sample contains only 40 quarters, and a relatively small number of COVID-era observations account for a large share of total forecast loss.
* The preferred models generally show little evidence of forecast bias or remaining forecast-error autocorrelation.

The results therefore favour richer dynamic models over simple autoregressive benchmarks, while also illustrating the uncertainty involved in statistically distinguishing forecast performance over a relatively short evaluation sample.

## Methods

The project uses:

* autoregressive and distributed-lag models
* vector autoregressions
* ARMA and seasonal ARMA error processes
* ARMAX models
* AIC and BIC model selection
* structural-break and recursive CUSUM tests
* heteroskedasticity and serial-correlation diagnostics
* parameter-stability and joint-significance tests
* recursive pseudo-out-of-sample forecasting
* forecast bias and efficiency diagnostics
* Diebold–Mariano forecast-comparison tests
* HAC-robust loss-difference tests

The analysis is implemented in **R**, primarily using `forecast`, `vars`, `strucchange`, `lmtest`, `sandwich`, and the tidyverse ecosystem.

## Repository structure

```text
.
├── analysis.Rmd                       # Full empirical analysis and forecasting code
├── australia_forecasting_slides.pdf  # Final presentation
├── presentation/
│   └── australia_forecasting_slides.tex
└── data/
    └── data_raw.xlsx                  # Source macroeconomic data
```

## Reproducibility

The repository uses [`renv`](https://rstudio.github.io/renv/) to record the R package environment.

After cloning the repository, restore the package environment with:

```r
renv::restore()
```

The complete analysis is contained in `analysis.Rmd`.

On the first run, the script estimates the candidate model set and recursively re-estimates the selected models over the forecast-evaluation sample. Model objects, forecasts, tables, and figures are generated under `output/`.

## Data

The analysis combines data from the **Australian Bureau of Statistics (ABS)** and the **Reserve Bank of Australia (RBA)**.

The underlying series include:

* quarterly real GDP;
* quarterly consumer prices;
* monthly unemployment;
* daily cash-rate observations.

The series are converted to a common quarterly frequency. GDP and prices are expressed as year-on-year log changes, while monthly unemployment and daily cash-rate observations are aggregated to quarterly frequency.

The dataset used for the analysis is included under `data/`.

## Project context

This repository documents my implementation and empirical analysis for a group assignment completed with C. Buttignon and D. Mauri as part of the Econometrics course at Bocconi University.
