# Step 3 — Interrupted Time Series (ITS) models

This section reports segmented-regression ITS models aggregated to monthly time series.

## Specification

Segmented structure:

- $y_t = \beta_0 + \beta_1 t + \beta_2 post_t + \beta_3 (t-t_0) post_t + \gamma_{m} + \epsilon_t$

where $\gamma_m$ are month-of-year fixed effects (seasonality).


Inference uses HAC/Newey–West standard errors (monthly maxlags = 12).


## Settings

- Date column: `Initial Report Date`

- Delay column: `report_delay_days`

- Intervention date: `2020-01-01`

- Intervention month (aligned): `2020-01-31`


## Full coefficient outputs (HAC SEs)

### Overall — Mean log(1+delay) (OLS + HAC)

| Outcome                    | Term   | Coef    | SE     | 95% CI            | p      |
| -------------------------- | ------ | ------- | ------ | ----------------- | ------ |
| Overall: Mean log(1+delay) | const  | 0.8377  | 0.0513 | [0.7372, 0.9382]  | <0.001 |
| Overall: Mean log(1+delay) | t      | -0.0017 | 0.0013 | [-0.0043, 0.0009] | 0.197  |
| Overall: Mean log(1+delay) | post   | -0.1055 | 0.0663 | [-0.2354, 0.0244] | 0.111  |
| Overall: Mean log(1+delay) | t_post | 0.0001  | 0.0020 | [-0.0038, 0.0039] | 0.976  |
| Overall: Mean log(1+delay) | moy_2  | -0.0581 | 0.0487 | [-0.1535, 0.0373] | 0.233  |
| Overall: Mean log(1+delay) | moy_3  | -0.0464 | 0.0426 | [-0.1299, 0.0371] | 0.276  |
| Overall: Mean log(1+delay) | moy_4  | -0.0073 | 0.0550 | [-0.1151, 0.1006] | 0.895  |
| Overall: Mean log(1+delay) | moy_5  | -0.0108 | 0.0527 | [-0.1142, 0.0926] | 0.838  |
| Overall: Mean log(1+delay) | moy_6  | -0.0662 | 0.0542 | [-0.1725, 0.0401] | 0.222  |
| Overall: Mean log(1+delay) | moy_7  | -0.0152 | 0.0527 | [-0.1185, 0.0881] | 0.773  |
| Overall: Mean log(1+delay) | moy_8  | 0.0376  | 0.0496 | [-0.0596, 0.1348] | 0.449  |
| Overall: Mean log(1+delay) | moy_9  | -0.0463 | 0.0595 | [-0.1629, 0.0704] | 0.437  |
| Overall: Mean log(1+delay) | moy_10 | -0.0007 | 0.0409 | [-0.0808, 0.0795] | 0.987  |
| Overall: Mean log(1+delay) | moy_11 | 0.0429  | 0.0405 | [-0.0365, 0.1222] | 0.289  |
| Overall: Mean log(1+delay) | moy_12 | -0.0529 | 0.0542 | [-0.1591, 0.0532] | 0.329  |


**Fit statistics**

| Outcome                    | Model     | N (months) | AIC    | BIC   | LogLik | R²    | Adj R² |
| -------------------------- | --------- | ---------- | ------ | ----- | ------ | ----- | ------ |
| Overall: Mean log(1+delay) | OLS (HAC) | 118        | -120.2 | -78.6 | 75.10  | 0.430 | 0.352  |


### Overall — P(any delay) (Binomial logit with successes/trials + HAC; OR reported)

| Outcome               | Term   | OR    | 95% CI         | p      |
| --------------------- | ------ | ----- | -------------- | ------ |
| Overall: P(any delay) | const  | 3.421 | [2.033, 5.754] | <0.001 |
| Overall: P(any delay) | t      | 0.993 | [0.980, 1.005] | 0.246  |
| Overall: P(any delay) | post   | 0.639 | [0.398, 1.026] | 0.064  |
| Overall: P(any delay) | t_post | 0.999 | [0.984, 1.014] | 0.879  |
| Overall: P(any delay) | moy_2  | 0.929 | [0.717, 1.202] | 0.575  |
| Overall: P(any delay) | moy_3  | 0.874 | [0.660, 1.157] | 0.346  |
| Overall: P(any delay) | moy_4  | 1.061 | [0.820, 1.372] | 0.654  |
| Overall: P(any delay) | moy_5  | 0.951 | [0.743, 1.218] | 0.691  |
| Overall: P(any delay) | moy_6  | 0.950 | [0.714, 1.265] | 0.725  |
| Overall: P(any delay) | moy_7  | 1.010 | [0.771, 1.324] | 0.941  |
| Overall: P(any delay) | moy_8  | 1.212 | [0.952, 1.545] | 0.119  |
| Overall: P(any delay) | moy_9  | 0.970 | [0.736, 1.278] | 0.829  |
| Overall: P(any delay) | moy_10 | 0.908 | [0.709, 1.163] | 0.444  |
| Overall: P(any delay) | moy_11 | 1.029 | [0.848, 1.248] | 0.771  |
| Overall: P(any delay) | moy_12 | 1.005 | [0.750, 1.345] | 0.975  |


**Fit statistics**

| Outcome               | Model                | N (months) | AIC    | BIC   | LogLik  | R² | Adj R² |
| --------------------- | -------------------- | ---------- | ------ | ----- | ------- | -- | ------ |
| Overall: P(any delay) | Binomial logit (HAC) | 118        | 1551.8 | 367.0 | -760.92 |    |        |


### Overall — P(late ≥90) (Binomial logit with successes/trials + HAC; OR reported)

| Outcome              | Term   | OR    | 95% CI         | p      |
| -------------------- | ------ | ----- | -------------- | ------ |
| Overall: P(late ≥90) | const  | 0.003 | [0.001, 0.018] | <0.001 |
| Overall: P(late ≥90) | t      | 1.004 | [0.981, 1.028] | 0.748  |
| Overall: P(late ≥90) | post   | 1.060 | [0.311, 3.610] | 0.926  |
| Overall: P(late ≥90) | t_post | 1.027 | [0.998, 1.058] | 0.065  |
| Overall: P(late ≥90) | moy_2  | 0.576 | [0.092, 3.591] | 0.554  |
| Overall: P(late ≥90) | moy_3  | 0.701 | [0.201, 2.445] | 0.577  |
| Overall: P(late ≥90) | moy_4  | 0.285 | [0.029, 2.774] | 0.279  |
| Overall: P(late ≥90) | moy_5  | 1.122 | [0.272, 4.628] | 0.873  |
| Overall: P(late ≥90) | moy_6  | 0.932 | [0.151, 5.753] | 0.940  |
| Overall: P(late ≥90) | moy_7  | 0.718 | [0.110, 4.698] | 0.730  |
| Overall: P(late ≥90) | moy_8  | 0.574 | [0.099, 3.341] | 0.537  |
| Overall: P(late ≥90) | moy_9  | 0.954 | [0.200, 4.556] | 0.953  |
| Overall: P(late ≥90) | moy_10 | 0.900 | [0.256, 3.162] | 0.870  |
| Overall: P(late ≥90) | moy_11 | 0.615 | [0.153, 2.467] | 0.493  |
| Overall: P(late ≥90) | moy_12 | 0.311 | [0.026, 3.734] | 0.357  |


**Fit statistics**

| Outcome              | Model                | N (months) | AIC   | BIC    | LogLik  | R² | Adj R² |
| -------------------- | -------------------- | ---------- | ----- | ------ | ------- | -- | ------ |
| Overall: P(late ≥90) | Binomial logit (HAC) | 118        | 520.4 | -113.8 | -245.18 |    |        |


