# Step 2 modeling + robustness summary (Colorado spills)

This report evaluates three hypothesis families: (1) Historical vs Recent mix shifts after 2020, (2) reporting timeliness changes (especially for Recent), (3) rural lag and heterogeneous improvements.
Primary models keep the full sample; sensitivity includes capping and an explicit exclusion check.

## Setup
- Rows before delay non-missing filter: 26,376
- Rows used in models (delay_days non-missing): 26,376
- Operator FE included in OLS: True (unique operators=142)
- Covariance (main): cluster

## H1) Agency outputs: Historical vs Recent mix
### Descriptives
```
   period  n_total  pct_historical  pct_recent
post_2020    15704          47.873      52.127
 pre_2020    10672          35.382      64.618
```

Top counties (pre/post rows):
```
county_norm    period  n_total  pct_historical  pct_recent
   GARFIELD post_2020     2094           8.405      91.595
   GARFIELD  pre_2020     1384          11.850      88.150
 RIO BLANCO post_2020      854          20.843      79.157
 RIO BLANCO  pre_2020     1170           8.034      91.966
       WELD post_2020    12756          56.162      43.838
       WELD  pre_2020     8118          43.336      56.664
```

Top 25 operators (pre/post rows):
```
                                  operator    period  n_total  pct_historical  pct_recent
                 BARRETT CORPORATION* BILL  pre_2020      140          35.714      64.286
BONANZA CREEK ENERGY OPERATING COMPANY LLC post_2020      638          16.928      83.072
BONANZA CREEK ENERGY OPERATING COMPANY LLC  pre_2020      492           7.724      92.276
                       CAERUS PICEANCE LLC post_2020     1814          11.356      88.644
                       CAERUS PICEANCE LLC  pre_2020      380          21.579      78.421
                           CHEVRON USA INC post_2020      234          21.368      78.632
                           CHEVRON USA INC  pre_2020      638           4.389      95.611
     CRESTONE PEAK RESOURCES OPERATING LLC post_2020      540          53.333      46.667
     CRESTONE PEAK RESOURCES OPERATING LLC  pre_2020      154          33.766      66.234
                          DCP MIDSTREAM LP  pre_2020      208          16.346      83.654
                  DCP OPERATING COMPANY LP post_2020      276          20.290      79.710
                  DCP OPERATING COMPANY LP  pre_2020      124          27.419      72.581
                  EXTRACTION OIL & GAS INC post_2020      328          21.341      78.659
                  EXTRACTION OIL & GAS INC  pre_2020      166          57.831      42.169
          FOUNDATION ENERGY MANAGEMENT LLC post_2020       20          30.000      70.000
          FOUNDATION ENERGY MANAGEMENT LLC  pre_2020      140           8.571      91.429
   FUNDARE RESOURCES OPERATING COMPANY LLC post_2020      196           8.163      91.837
                 GRAND RIVER GATHERING LLC post_2020      116           0.000     100.000
                 GRAND RIVER GATHERING LLC  pre_2020       22           0.000     100.000
       GREAT WESTERN OPERATING COMPANY LLC post_2020       94          42.553      57.447
       GREAT WESTERN OPERATING COMPANY LLC  pre_2020      112          21.429      78.571
           HIGHPOINT OPERATING CORPORATION post_2020      576          12.500      87.500
           HIGHPOINT OPERATING CORPORATION  pre_2020      280           4.286      95.714
                  KERR MCGEE GATHERING LLC post_2020      126          12.698      87.302
                  KERR MCGEE GATHERING LLC  pre_2020      124          32.258      67.742
           KERR MCGEE OIL & GAS ONSHORE LP post_2020     3140          73.121      26.879
           KERR MCGEE OIL & GAS ONSHORE LP  pre_2020     1574          56.417      43.583
                   KP KAUFFMAN COMPANY INC post_2020      844          13.270      86.730
                   KP KAUFFMAN COMPANY INC  pre_2020       96          29.167      70.833
                        LARAMIE ENERGY LLC post_2020      150           5.333      94.667
                        LARAMIE ENERGY LLC  pre_2020      136           7.353      92.647
                          NOBLE ENERGY INC post_2020     3316          85.042      14.958
                          NOBLE ENERGY INC  pre_2020     2114          67.171      32.829
                            PDC ENERGY INC post_2020     1620          67.037      32.963
                            PDC ENERGY INC  pre_2020      834          51.319      48.681
                            SRC ENERGY INC post_2020        4         100.000       0.000
                            SRC ENERGY INC  pre_2020      154          54.545      45.455
                    TEP ROCKY MOUNTAIN LLC post_2020      206           1.942      98.058
                    TEP ROCKY MOUNTAIN LLC  pre_2020      386           5.699      94.301
                      VERDAD RESOURCES LLC post_2020      104           5.769      94.231
                      VERDAD RESOURCES LLC  pre_2020       40          20.000      80.000
             WHITING OIL & GAS CORPORATION post_2020       78          15.385      84.615
             WHITING OIL & GAS CORPORATION  pre_2020      368           9.783      90.217
             WPX ENERGY ROCKY MOUNTAIN LLC  pre_2020      164          17.073      82.927
                            XTO ENERGY INC post_2020       36           5.556      94.444
                            XTO ENERGY INC  pre_2020      148           5.405      94.595
```

Plot saved: `/home/dadams/Repos/colorado_redux/analysis_postgis/step2_model_outputs/pct_historical_over_time.png`

### Model
Spill-level logit formula used: `historical ~ post + C(county_norm) + C(rurality_3)`
```
        model term  log_odds     se  odds_ratio  or_ci95_lo  or_ci95_hi      p_value
H1_hist_logit post  0.499121 0.0714    1.647273    1.432152    1.894708 2.738355e-12
```

Interrupted time series (monthly pct_historical): pct_historical ~ t + post + post_t + month-of-year FE
```
                  model   term       coef       se    z_or_t      p_value
H1_its_monthly_pct_hist   post -67.878628 7.003186 -9.692536 3.243732e-22
H1_its_monthly_pct_hist post_t   0.984768 0.107711  9.142720 6.090091e-20
```

## H2) Timeliness: reporting delay
### Continuous DV: OLS on log1p_delay
```
       model            term      coef       se    z_or_t      p_value
H2_ols_log1p            post -0.219885 0.024052 -9.142088 6.125768e-20
H2_ols_log1p      historical  0.043168 0.153896  0.280499 7.790944e-01
H2_ols_log1p post:historical  0.007845 0.028785  0.272523 7.852199e-01
```

### Two-part model
Any delay (logit) formula used: `any_delay ~ post + historical + post:historical + C(rurality_3) + C(county_norm)`
```
             model            term  log_odds       se  odds_ratio  or_ci95_lo  or_ci95_hi      p_value
H2_logit_any_delay            post -0.687265 0.073321    0.502950    0.435625    0.580680 7.024476e-21
H2_logit_any_delay      historical -0.134713 0.085901    0.873967    0.738541    1.034226 1.168281e-01
H2_logit_any_delay post:historical -0.472647 0.140966    0.623350    0.472867    0.821722 7.996622e-04
```

Delay length | delay>0 (OLS log1p_delay):
```
                      model            term      coef       se    z_or_t      p_value
H2_ols_log1p_cond_delay_gt0            post -0.057099 0.017413 -3.279143 1.041227e-03
H2_ols_log1p_cond_delay_gt0      historical  0.107903 0.127927  0.843472 3.989646e-01
H2_ols_log1p_cond_delay_gt0 post:historical  0.202392 0.029057  6.965272 3.277704e-12
```

### Threshold models (odds ratios)
late30 formula used: `late30 ~ post + historical + post:historical + C(rurality_3) + C(county_norm)`
```
          model            term  log_odds       se  odds_ratio  or_ci95_lo  or_ci95_hi  p_value
H2_logit_late30            post  0.733227 0.645191    2.081787    0.587812    7.372827 0.255769
H2_logit_late30      historical  2.010974 0.620959    7.470592    2.211993   25.230522 0.001202
H2_logit_late30 post:historical -0.255636 0.571480    0.774424    0.252653    2.373737 0.654643
```

late90 formula used: `late90 ~ post + historical + post:historical + C(rurality_3) + C(county_norm)`
```
          model            term  log_odds       se  odds_ratio  or_ci95_lo  or_ci95_hi      p_value
H2_logit_late90            post  2.711705 0.259629   15.054922    9.050612   25.042579 1.552004e-25
H2_logit_late90      historical  3.625521 1.131162   37.544276    4.089581  344.674128 1.350023e-03
H2_logit_late90 post:historical -1.788334 0.341862    0.167239    0.085573    0.326840 1.684580e-07
```

extreme99 formula used: `extreme99 ~ post + historical + post:historical + C(rurality_3) + C(county_norm)`
```
             model            term  log_odds       se   odds_ratio  or_ci95_lo   or_ci95_hi      p_value
H2_logit_extreme99            post  8.891533 1.095314  7270.158776  849.560160 62214.791946 4.747221e-16
H2_logit_extreme99      historical  9.490816 0.829431 13237.589800 2604.850903 67272.097423 2.562118e-30
H2_logit_extreme99 post:historical -7.745245 1.352117     0.000433    0.000031     0.006127 1.014807e-08
```

Predicted P(late30) by spill type × period (marginal standardization):
```
   period spill_type     mean  ci95_lo  ci95_hi
 pre_2020     Recent 0.003650 0.002516 0.005803
 pre_2020 Historical 0.025917 0.011911 0.055095
post_2020     Recent 0.007531 0.001719 0.036008
post_2020 Historical 0.040456 0.025171 0.066593
```
Plot saved: `/home/dadams/Repos/colorado_redux/analysis_postgis/step2_model_outputs/pred_late30_pre_post_by_type.png`

## H3) Rural lag + heterogeneity
late30 with post×rurality interaction (core + interaction terms):
```
                          model                           term  log_odds       se  odds_ratio  or_ci95_lo  or_ci95_hi  p_value
H3_logit_late30_post_x_rurality                           post  0.764282 0.639336    2.147452    0.613351    7.518607 0.231919
H3_logit_late30_post_x_rurality post:C(rurality_3)[T.Suburban] -1.155046 0.671184    0.315043    0.084537    1.174067 0.085267
H3_logit_late30_post_x_rurality    post:C(rurality_3)[T.Urban]  0.216575 0.447007    1.241817    0.517080    2.982341 0.628030
H3_logit_late30_post_x_rurality                     historical  2.059610 0.718533    7.842909    1.918004   32.070445 0.004152
H3_logit_late30_post_x_rurality                post:historical -0.338292 0.560403    0.712987    0.237715    2.138485 0.546070
```

Predicted P(late30) by rurality × period for Recent (historical=0):
```
rurality_3    period     mean  ci95_lo  ci95_hi
     Rural  pre_2020 0.003888 0.002920 0.005291
     Rural post_2020 0.008273 0.001659 0.044027
  Suburban  pre_2020 0.008794 0.003148 0.027430
  Suburban post_2020 0.005985 0.001151 0.028051
     Urban  pre_2020 0.002616 0.000923 0.007801
     Urban post_2020 0.006914 0.001084 0.043393
```
Plot saved: `/home/dadams/Repos/colorado_redux/analysis_postgis/step2_model_outputs/pred_late30_pre_post_by_rurality_recent.png`

Top 15 operators by adjusted predicted P(late30) (min n>=50):
```
                             operator  n_total  p_late30_adj
    UTAH GAS OP LTD DBA UTAH GAS CORP      122         9.191
          SCOUT ENERGY MANAGEMENT LLC      106         4.021
                      CHEVRON USA INC      872         3.470
           URSA OPERATING COMPANY LLC      110         2.990
                       XTO ENERGY INC      184         2.779
                     NOBLE ENERGY INC     5430         1.973
           CHEVRON PRODUCTION COMPANY       72         1.807
      KERR MCGEE OIL & GAS ONSHORE LP     4714         1.801
                       PDC ENERGY INC     2454         1.690
CRESTONE PEAK RESOURCES OPERATING LLC      694         1.568
                  CAERUS PICEANCE LLC     2194         1.478
        SYNERGY RESOURCES CORPORATION      100         1.304
                       SRC ENERGY INC      158         1.111
        WHITING OIL & GAS CORPORATION      446         1.090
             EXTRACTION OIL & GAS INC      494         1.037
```

Bottom 15 operators by adjusted predicted P(late30) (min n>=50):
```
                     operator  n_total  p_late30_adj
            EOG RESOURCES INC      104         0.301
       VANGUARD OPERATING LLC       68         0.301
              BNN WESTERN LLC       50         0.308
  BERRY PETROLEUM COMPANY LLC       64         0.329
   NGL WATER SOLUTIONS DJ LLC      138         0.359
 NOBLE MIDSTREAM SERVICES LLC       78         0.414
       BISON OIL & GAS II LLC       52         0.472
    GRAND RIVER GATHERING LLC      138         0.473
WPX ENERGY ROCKY MOUNTAIN LLC      164         0.491
             DCP MIDSTREAM LP      208         0.493
SUMMIT MIDSTREAM PARTNERS LLC       78         0.503
  TALLGRASS WATER WESTERN LLC       56         0.589
       BISON IV OPERATING LLC       70         0.589
TAPROOT ROCKIES MIDSTREAM LLC       52         0.589
           LARAMIE ENERGY LLC      286         0.595
```

Top 15 counties by adjusted predicted P(late30) (min n>=50):
```
county_norm  n_total  p_late30_adj
 RIO BLANCO     2024         4.349
       WELD    20874         1.456
   GARFIELD     3478         0.575
```

## Robustness / sensitivity
### OLS (log1p_delay): baseline vs cap180 vs exclude extreme99
```
                       model            term      coef       se    z_or_t      p_value
         robust_ols_baseline            post -0.219885 0.024052 -9.142088 6.125768e-20
         robust_ols_baseline      historical  0.043168 0.153896  0.280499 7.790944e-01
         robust_ols_baseline post:historical  0.007845 0.028785  0.272523 7.852199e-01
           robust_ols_cap180            post -0.219943 0.023916 -9.196626 3.693661e-20
           robust_ols_cap180      historical  0.041076 0.154035  0.266667 7.897254e-01
           robust_ols_cap180 post:historical  0.005602 0.028736  0.194947 8.454346e-01
robust_ols_exclude_extreme99            post -0.231604 0.024248 -9.551665 1.276287e-21
robust_ols_exclude_extreme99      historical  0.003735 0.144605  0.025828 9.793942e-01
robust_ols_exclude_extreme99 post:historical -0.036970 0.024389 -1.515881 1.295495e-01
```

Exclude-extreme99 variant removes 0.713% of rows (extreme99==1).

### late30 (logit): baseline vs exclude extreme99
```
                          model            term  log_odds       se  odds_ratio  or_ci95_lo  or_ci95_hi  p_value
         robust_late30_baseline            post  0.733227 0.645191    2.081787    0.587812    7.372827 0.255769
         robust_late30_baseline      historical  2.010974 0.620959    7.470592    2.211993   25.230522 0.001202
         robust_late30_baseline post:historical -0.255636 0.571480    0.774424    0.252653    2.373737 0.654643
robust_late30_exclude_extreme99            post  0.147381 0.622270    1.158796    0.342231    3.923683 0.812777
robust_late30_exclude_extreme99      historical  1.846107 0.967478    6.335110    0.951086   42.197650 0.056370
robust_late30_exclude_extreme99 post:historical -0.152764 0.514639    0.858332    0.313030    2.353556 0.766590
```

## Outputs
- Report: `/home/dadams/Repos/colorado_redux/step2_models_summary.md`
- Output directory: `/home/dadams/Repos/colorado_redux/analysis_postgis/step2_model_outputs`