# Step 2B final models (Colorado spills mission-change study)

This notebook cell produces the final, defensible model set for H1–H3 while keeping the full sample and avoiding separation in the extreme tail (>=99 days).



## H1: Historical vs Recent mix (agency outputs)

### Descriptive mix

```
   period  n_total  pct_historical
post_2020    15704          47.873
 pre_2020    10672          35.382
```

### Models

Baseline spill-level logit formula used: `historical ~ post + C(county_norm) + C(rurality_3)`

```
            model term  log_odds       se  odds_ratio  or_ci95_lo  or_ci95_hi      p_value
H1_logit_baseline post  0.499121 0.028681    1.647273    1.557228    1.742526 7.873288e-68
```

Marginal predicted pct_historical (pre vs post):

```
   period  pred_pct_historical
 pre_2020               36.826
post_2020               46.762
```

Operator-structure robustness: LPM with operator FE, clustered by operator. Formula: `historical ~ post + C(county_norm) + C(rurality_3) + C(operator)`

```
             model term     coef       se        t  p_value
H1_LPM_operator_FE post 0.106654 0.031796 3.354377 0.000795
```

Plots saved:

- `/home/dadams/Repos/colorado_redux/analysis_postgis/step2_model_outputs/h1_pct_historical_monthly.png`
- `/home/dadams/Repos/colorado_redux/analysis_postgis/step2_model_outputs/h1_pct_historical_monthly_top3counties.png`



## H2: Reporting timeliness (regulated entities)

### A) Continuous DV (primary)

OLS formula: `log1p_delay ~ post + historical + post:historical + C(county_norm) + C(rurality_3) + C(operator)`

Cluster by operator (main):

```
                        model            term      coef       se         t  p_value
H2_OLS_log1p_cluster_operator            post -0.219885 0.060210 -3.651970 0.000260
H2_OLS_log1p_cluster_operator      historical  0.043168 0.091194  0.473360 0.635957
H2_OLS_log1p_cluster_operator post:historical  0.007845 0.080962  0.096894 0.922811
```

Cluster by county (robustness):

```
                      model            term      coef       se          t      p_value
H2_OLS_log1p_cluster_county            post -0.219885 0.012972 -16.950874 1.896133e-64
H2_OLS_log1p_cluster_county      historical  0.043168 0.016638   2.594523 9.472216e-03
H2_OLS_log1p_cluster_county post:historical  0.007845 0.020156   0.389197 6.971306e-01
```

### B) Two-part model

any_delay logit formula used: `any_delay ~ post + historical + post:historical + C(rurality_3) + C(county_norm) + C(operator)`

```
             model            term  log_odds       se  odds_ratio  or_ci95_lo  or_ci95_hi  p_value
H2_logit_any_delay            post -0.866859 0.277734    0.420270    0.243846    0.724335 0.001801
H2_logit_any_delay      historical -0.236037 0.212766    0.789751    0.520451    1.198397 0.267269
H2_logit_any_delay post:historical -0.327067 0.255409    0.721036    0.437067    1.189502 0.200348
```

Conditional positive delay model (delay>0), OLS on log1p_delay; clustered by operator:

```
                                  model            term      coef       se         t  p_value
H2_OLS_log1p_delay_gt0_cluster_operator            post -0.057099 0.048314 -1.181823 0.237276
H2_OLS_log1p_delay_gt0_cluster_operator      historical  0.107903 0.079906  1.350382 0.176893
H2_OLS_log1p_delay_gt0_cluster_operator post:historical  0.202392 0.068181  2.968463 0.002993
```

Mechanism decomposition table (marginal standardized):

```
spill_type    period  P_any_delay  E_delay_if_pos
    Recent  pre_2020     0.745056           2.030
    Recent post_2020     0.572983           1.862
Historical  pre_2020     0.702362           2.376
Historical post_2020     0.449043           2.904
```

### C) Threshold models

late30 formula used: `late30 ~ post + historical + post:historical + C(rurality_3) + C(county_top3)`

```
          model            term  log_odds       se  odds_ratio  or_ci95_lo  or_ci95_hi  p_value
H2_logit_late30            post  0.733227 0.471128    2.081787    0.826808    5.241651 0.119631
H2_logit_late30      historical  2.010974 0.586986    7.470592    2.364301   23.605183 0.000613
H2_logit_late30 post:historical -0.255636 0.527887    0.774424    0.275190    2.179340 0.628200
```

late90 formula used: `late90 ~ post + historical + post:historical + C(rurality_3) + C(county_top3)`

```
          model            term  log_odds       se  odds_ratio  or_ci95_lo  or_ci95_hi  p_value
H2_logit_late90            post  2.711705 1.134067   15.054922    1.630577  139.000243 0.016796
H2_logit_late90      historical  3.625521 1.240123   37.544276    3.303164  426.734091 0.003461
H2_logit_late90 post:historical -1.788334 1.198220    0.167239    0.015973    1.750982 0.135570
```

Predicted P(late30) and P(late90) pre vs post (marginal standardized):

```
spill_type    period  P_late30  P_late90
    Recent  pre_2020  0.003650  0.000239
    Recent post_2020  0.007531  0.003581
Historical  pre_2020  0.025917  0.008854
Historical post_2020  0.040456  0.021834
```



## H3: Rural lag and heterogeneous improvements

### Interaction models

any_delay model formula used: `any_delay ~ post + historical + post:historical + C(rurality_3) + post:C(rurality_3) + C(county_norm)`

```
                             model                           term  log_odds       se  odds_ratio  or_ci95_lo  or_ci95_hi  p_value
H3_logit_any_delay_post_x_rurality                           post -0.540584 0.255156    0.582408    0.353211    0.960329 0.034120
H3_logit_any_delay_post_x_rurality post:C(rurality_3)[T.Suburban] -0.212933 0.417008    0.808211    0.356912    1.830158 0.609617
H3_logit_any_delay_post_x_rurality    post:C(rurality_3)[T.Urban] -0.335366 0.260434    0.715076    0.429207    1.191347 0.197844
H3_logit_any_delay_post_x_rurality                post:historical -0.353541 0.214533    0.702197    0.461153    1.069236 0.099362
```
Joint test post×rurality (χ²): chi2=1.667, df=2, p=0.434483; terms=['post:C(rurality_3)[T.Suburban]', 'post:C(rurality_3)[T.Urban]']

log1p_delay model formula: `log1p_delay ~ post + historical + post:historical + C(rurality_3) + post:C(rurality_3) + C(county_norm) + C(operator)`

```
                                        model                           term      coef       se         t  p_value
H3_OLS_log1p_post_x_rurality_cluster_operator                           post -0.153236 0.056882 -2.693939 0.007061
H3_OLS_log1p_post_x_rurality_cluster_operator post:C(rurality_3)[T.Suburban] -0.156486 0.105184 -1.487735 0.136821
H3_OLS_log1p_post_x_rurality_cluster_operator    post:C(rurality_3)[T.Urban] -0.132796 0.056804 -2.337794 0.019398
H3_OLS_log1p_post_x_rurality_cluster_operator                post:historical  0.050618 0.085441  0.592437 0.553558
```
Joint test post×rurality (F): F=3.278, df=(2, 141), p=0.0405981; terms=['post:C(rurality_3)[T.Suburban]', 'post:C(rurality_3)[T.Urban]']

late90 model formula used: `late90 ~ post + historical + post:historical + C(rurality_3) + post:C(rurality_3) + C(county_top3)`

```
                          model                           term  log_odds       se  odds_ratio  or_ci95_lo  or_ci95_hi  p_value
H3_logit_late90_post_x_rurality                           post  2.992725 1.087601   19.939945    2.365589  168.077150 0.005929
H3_logit_late90_post_x_rurality post:C(rurality_3)[T.Suburban] -0.442241 1.038556    0.642594    0.083927    4.920099 0.670237
H3_logit_late90_post_x_rurality    post:C(rurality_3)[T.Urban] -0.766637 0.936833    0.464573    0.074064    2.914086 0.413170
H3_logit_late90_post_x_rurality                post:historical -1.522369 1.455527    0.218194    0.012586    3.782802 0.295597
```
Joint test post×rurality (χ²): chi2=0.685, df=2, p=0.709937; terms=['post:C(rurality_3)[T.Suburban]', 'post:C(rurality_3)[T.Urban]']

### Rurality gradient (Recent spills only; model-implied median delay = exp(lp)-1)

```
rurality_3    period  P_any_delay  median_delay_implied  P_late30  P_late90
     Rural  pre_2020     0.757073                 1.470  0.005869  0.000344
     Rural post_2020     0.645204                 1.119  0.012055  0.005139
  Suburban  pre_2020     0.714210                 1.544  0.002721  0.000188
  Suburban post_2020     0.540791                 0.867  0.005649  0.002819
     Urban  pre_2020     0.735393                 1.216  0.002262  0.000167
     Urban post_2020     0.536487                 0.664  0.004697  0.002508
```



## Extreme tail (>=99 days): rare-events strategy

Used ridge (L2) logistic regression with CV on C, class_weight='balanced'.

```
 chosen_C  event_rate     n
 0.012328    0.007128 26376
```

Stable predicted probabilities (marginal standardized) and pre/post risk ratios:

```
spill_type    p_pre   p_post  risk_ratio  risk_diff
    Recent 0.095476 0.302575    3.169117   0.207099
Historical 0.374337 0.706926    1.888477   0.332589
```



## Operator + geography variation (Aim 3 deliverables)

### Operators (min n>=50): adjusted predicted probabilities

Top/bottom 15 for late30 and any_delay saved as CSVs under `step2_model_outputs/operator_adjusted/`.

### Counties (min n>=50): adjusted predicted P(late30) and P(late90)

```
county_norm  n_total  p_late30_adj  p_late90_adj
 RIO BLANCO     2024         4.349         1.284
       WELD    20874         1.456         0.805
   GARFIELD     3478         0.575         0.171
```

Choropleth map skipped (no county geometry join detected in this notebook).



## Robustness set (must include)

### Continuous model (cluster by operator): compare key terms

```
          variant      post  post_se  post:historical   int_se
         baseline -0.219885 0.060210         0.007845 0.080962
           cap180 -0.219943 0.060322         0.005602 0.080049
exclude_extreme99 -0.231604 0.061896        -0.036970 0.074799
```

### Key logit (late30): compare key terms

```
                                             variant     post  post_se  post:historical   int_se
                                            baseline 0.733227 0.471128        -0.255636 0.527887
cap180 (affects DV only via delay; late30 unchanged) 0.733227 0.471128        -0.255636 0.527887
                                   exclude_extreme99 0.147381 0.633244        -0.152764 0.766658
```



## Outputs

- Report: `/home/dadams/Repos/colorado_redux/step2_final_models.md`

- Plots/tables: `/home/dadams/Repos/colorado_redux/analysis_postgis/step2_model_outputs`
