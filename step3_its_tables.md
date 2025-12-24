# Step 3 — ITS key terms

Key segmented-regression terms (level and slope change) with HAC standard errors.

## Mean log(1+delay) (OLS)

| Outcome                    | Term (segmented) | Coef    | SE     | 95% CI            | p     |
| -------------------------- | ---------------- | ------- | ------ | ----------------- | ----- |
| Overall: Mean log(1+delay) | post             | -0.1055 | 0.0663 | [-0.2354, 0.0244] | 0.111 |
| Overall: Mean log(1+delay) | t_post           | 0.0001  | 0.0020 | [-0.0038, 0.0039] | 0.976 |


**Fit statistics**

| Outcome                    | Model     | N (months) | AIC    | BIC   | LogLik | R²    | Adj R² |
| -------------------------- | --------- | ---------- | ------ | ----- | ------ | ----- | ------ |
| Overall: Mean log(1+delay) | OLS (HAC) | 118        | -120.2 | -78.6 | 75.10  | 0.430 | 0.352  |

OLS: “Mean log(1+delay) shows a modest post-intervention level drop (−0.106; p=0.111) with no slope change.”


## P(any delay) (Binomial logit; OR)

| Outcome               | Term (segmented) | OR    | 95% CI         | p     |
| --------------------- | ---------------- | ----- | -------------- | ----- |
| Overall: P(any delay) | post             | 0.639 | [0.398, 1.026] | 0.064 |
| Overall: P(any delay) | t_post           | 0.999 | [0.984, 1.014] | 0.879 |


**Fit statistics**

| Outcome               | Model                | N (months) | AIC    | BIC   | LogLik  | R² | Adj R² |
| --------------------- | -------------------- | ---------- | ------ | ----- | ------- | -- | ------ |
| Overall: P(any delay) | Binomial logit (HAC) | 118        | 1551.8 | 367.0 | -760.92 |    |        |

Any delay: “The odds of any delay fall at the intervention (OR=0.639; p=0.064), with no evidence of a post-intervention trend shift.”

## P(late ≥90) (Binomial logit; OR)

| Outcome              | Term (segmented) | OR    | 95% CI         | p     |
| -------------------- | ---------------- | ----- | -------------- | ----- |
| Overall: P(late ≥90) | post             | 1.060 | [0.311, 3.610] | 0.926 |
| Overall: P(late ≥90) | t_post           | 1.027 | [0.998, 1.058] | 0.065 |


**Fit statistics**

| Outcome              | Model                | N (months) | AIC   | BIC    | LogLik  | R² | Adj R² |
| -------------------- | -------------------- | ---------- | ----- | ------ | ------- | -- | ------ |
| Overall: P(late ≥90) | Binomial logit (HAC) | 118        | 520.4 | -113.8 | -245.18 |    |        |

Late90: “Extreme-delay odds show no level break but a gradual post-intervention increase in trend (OR=1.027 per month; p=0.065).”
