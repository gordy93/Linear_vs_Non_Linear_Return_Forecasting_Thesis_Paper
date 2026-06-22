# Linear_vs_Non_Linear_Return_Forecasting_Thesis_Paper

This project is a condenced version of my MSc thesis in Quantitative Finance for the CFA Quant Awards 2026. This asset-pricing research compares whether non-linear machine-learning models provide incremental value over dimension-reduced linear models in equity return forecasting.

The research evaluates both **statistical predictive accuracy** and **economic portfolio value** using a large-scale U.S. equity panel of approximately **3.4 million stock-month observations** and **150+ firm-level characteristics**.

## Research Question

Do non-linear machine-learning models genuinely improve equity return forecasts, or do their gains mainly reflect better processing of high-dimensional firm characteristics?

Rather than comparing flexible models only against simple OLS benchmarks, this project tests non-linear models against linear models that are explicitly designed to handle high-dimensional predictors through dimension reduction.

## Methodology

The forecasting target is the one-month-ahead excess return of stock (i) at time (t+1), estimated from firm characteristics observed at time (t).

The empirical framework compares four model groups:

| Model Class                     | Models                                                                         |
| ------------------------------- | ------------------------------------------------------------------------------ |
| Simple linear                   | OLS, OLS-FF3                                                                   |
| Dimension-reduced linear models | PCR, IPCA, PLS                                                                 |
| Non-linear models               | GBRT, RF, FFNN                                                                 |
| Ensembles                       | Equal-weighted linear and non-linear forecast ensembles                        |

All models are evaluated using an expanding-window training design with a rolling validation sample and a fully out-of-sample test period.

## Data and Preprocessing

The analysis uses the Jensen et al. (2022) Global Factor Data library accessed through WRDS.

Key preprocessing steps:

* Cross-sectional rank transformation of firm characteristics to the interval ([-1, 1])
* One-month lag of firm-level characteristics to avoid look-ahead bias
* Median imputation for missing characteristic values
* Industry demeaning using two-digit SIC industry classifications
* Annual model refitting with expanding training windows
* Out-of-sample testing over 1999–2024

The raw data are not included in this repository because WRDS data are subject to licensing restrictions.

## Evaluation Framework

### Statistical Performance

Forecasting accuracy is evaluated using:

* Out-of-sample (R^2)
* Clark-West tests against the zero-return benchmark
* Adjusted Diebold-Mariano tests for pairwise model comparison
* Bonferroni correction for multiple testing

### Economic Performance

Predicted returns are converted into monthly long-short decile portfolios:

* Long top predicted-return decile
* Short bottom predicted-return decile
* Equal-weighted and value-weighted implementations
* Realistic transaction-cost adjustment
* Sharpe Ratio and Probabilistic Sharpe Ratio
* Capital Asset Pricing Model and Fama-French 5-Factor alpha
* Turnover, maximum drawdown and downside-risk analysis

## Key Findings

1. **Non-linear models do not deliver a statistically robust forecasting advantage once linear models are strengthened with dimension reduction.**
   Dimension-reduced linear models remain statistically competitive with non-linear specifications after adjusted forecast-comparison tests.

2. **Model complexity matters more economically than statistically.**
   Non-linear models generate stronger value-weighted long-short portfolio performance, while linear models remain competitive under equal-weighting.

3. **Predictive information is concentrated in economically interpretable signal themes.**
   The strongest predictive content comes from low risk, quality, momentum, value and profitability characteristics.

4. **Signal importance is time-varying.**
   Predictive themes shift across market regimes, with a pronounced change around the Global Financial Crisis.

5. **Portfolio construction determines whether machine-learning complexity adds value.**
   Similar stock-level predictive accuracy can translate into different realised portfolio outcomes once forecasts are ranked, weighted and traded.

## Main Contribution

This project provides a stricter test of non-linearity in empirical asset pricing.

The results suggest that the value of machine-learning complexity should not be judged only by predictive accuracy. A flexible model is useful only when it adds value beyond disciplined feature processing, robust validation and economically realistic portfolio construction.

In short:

> Complexity is not a substitute for economic discipline; it is only useful when it improves realised investment outcomes.
