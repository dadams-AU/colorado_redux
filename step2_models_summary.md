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
| period    |   n_total |   pct_historical |   pct_recent |
|:----------|----------:|-----------------:|-------------:|
| post_2020 |     15704 |           47.873 |       52.127 |
| pre_2020  |     10672 |           35.382 |       64.618 |

Top counties (pre/post rows):
| county_norm   | period    |   n_total |   pct_historical |   pct_recent |
|:--------------|:----------|----------:|-----------------:|-------------:|
| GARFIELD      | post_2020 |      2094 |            8.405 |       91.595 |
| GARFIELD      | pre_2020  |      1384 |           11.85  |       88.15  |
| RIO BLANCO    | post_2020 |       854 |           20.843 |       79.157 |
| RIO BLANCO    | pre_2020  |      1170 |            8.034 |       91.966 |
| WELD          | post_2020 |     12756 |           56.162 |       43.838 |
| WELD          | pre_2020  |      8118 |           43.336 |       56.664 |

Top 25 operators (pre/post rows):
| operator                                   | period    |   n_total |   pct_historical |   pct_recent |
|:-------------------------------------------|:----------|----------:|-----------------:|-------------:|
| BARRETT CORPORATION* BILL                  | pre_2020  |       140 |           35.714 |       64.286 |
| BONANZA CREEK ENERGY OPERATING COMPANY LLC | post_2020 |       638 |           16.928 |       83.072 |
| BONANZA CREEK ENERGY OPERATING COMPANY LLC | pre_2020  |       492 |            7.724 |       92.276 |
| CAERUS PICEANCE LLC                        | post_2020 |      1814 |           11.356 |       88.644 |
| CAERUS PICEANCE LLC                        | pre_2020  |       380 |           21.579 |       78.421 |
| CHEVRON USA INC                            | post_2020 |       234 |           21.368 |       78.632 |
| CHEVRON USA INC                            | pre_2020  |       638 |            4.389 |       95.611 |
| CRESTONE PEAK RESOURCES OPERATING LLC      | post_2020 |       540 |           53.333 |       46.667 |
| CRESTONE PEAK RESOURCES OPERATING LLC      | pre_2020  |       154 |           33.766 |       66.234 |
| DCP MIDSTREAM LP                           | pre_2020  |       208 |           16.346 |       83.654 |
| DCP OPERATING COMPANY LP                   | post_2020 |       276 |           20.29  |       79.71  |
| DCP OPERATING COMPANY LP                   | pre_2020  |       124 |           27.419 |       72.581 |
| EXTRACTION OIL & GAS INC                   | post_2020 |       328 |           21.341 |       78.659 |
| EXTRACTION OIL & GAS INC                   | pre_2020  |       166 |           57.831 |       42.169 |
| FOUNDATION ENERGY MANAGEMENT LLC           | post_2020 |        20 |           30     |       70     |
| FOUNDATION ENERGY MANAGEMENT LLC           | pre_2020  |       140 |            8.571 |       91.429 |
| FUNDARE RESOURCES OPERATING COMPANY LLC    | post_2020 |       196 |            8.163 |       91.837 |
| GRAND RIVER GATHERING LLC                  | post_2020 |       116 |            0     |      100     |
| GRAND RIVER GATHERING LLC                  | pre_2020  |        22 |            0     |      100     |
| GREAT WESTERN OPERATING COMPANY LLC        | post_2020 |        94 |           42.553 |       57.447 |
| GREAT WESTERN OPERATING COMPANY LLC        | pre_2020  |       112 |           21.429 |       78.571 |
| HIGHPOINT OPERATING CORPORATION            | post_2020 |       576 |           12.5   |       87.5   |
| HIGHPOINT OPERATING CORPORATION            | pre_2020  |       280 |            4.286 |       95.714 |
| KERR MCGEE GATHERING LLC                   | post_2020 |       126 |           12.698 |       87.302 |
| KERR MCGEE GATHERING LLC                   | pre_2020  |       124 |           32.258 |       67.742 |
| KERR MCGEE OIL & GAS ONSHORE LP            | post_2020 |      3140 |           73.121 |       26.879 |
| KERR MCGEE OIL & GAS ONSHORE LP            | pre_2020  |      1574 |           56.417 |       43.583 |
| KP KAUFFMAN COMPANY INC                    | post_2020 |       844 |           13.27  |       86.73  |
| KP KAUFFMAN COMPANY INC                    | pre_2020  |        96 |           29.167 |       70.833 |
| LARAMIE ENERGY LLC                         | post_2020 |       150 |            5.333 |       94.667 |
| LARAMIE ENERGY LLC                         | pre_2020  |       136 |            7.353 |       92.647 |
| NOBLE ENERGY INC                           | post_2020 |      3316 |           85.042 |       14.958 |
| NOBLE ENERGY INC                           | pre_2020  |      2114 |           67.171 |       32.829 |
| PDC ENERGY INC                             | post_2020 |      1620 |           67.037 |       32.963 |
| PDC ENERGY INC                             | pre_2020  |       834 |           51.319 |       48.681 |
| SRC ENERGY INC                             | post_2020 |         4 |          100     |        0     |
| SRC ENERGY INC                             | pre_2020  |       154 |           54.545 |       45.455 |
| TEP ROCKY MOUNTAIN LLC                     | post_2020 |       206 |            1.942 |       98.058 |
| TEP ROCKY MOUNTAIN LLC                     | pre_2020  |       386 |            5.699 |       94.301 |
| VERDAD RESOURCES LLC                       | post_2020 |       104 |            5.769 |       94.231 |
| VERDAD RESOURCES LLC                       | pre_2020  |        40 |           20     |       80     |
| WHITING OIL & GAS CORPORATION              | post_2020 |        78 |           15.385 |       84.615 |
| WHITING OIL & GAS CORPORATION              | pre_2020  |       368 |            9.783 |       90.217 |
| WPX ENERGY ROCKY MOUNTAIN LLC              | pre_2020  |       164 |           17.073 |       82.927 |
| XTO ENERGY INC                             | post_2020 |        36 |            5.556 |       94.444 |
| XTO ENERGY INC                             | pre_2020  |       148 |            5.405 |       94.595 |

Plot saved: `/home/dadams/Repos/colorado_redux/analysis_postgis/step2_model_outputs/pct_historical_over_time.png`

### Model
Spill-level logit formula used: `historical ~ post + C(county_norm) + C(rurality_3)`
| model         | term   |   log_odds |        se |   odds_ratio |   or_ci95_lo |   or_ci95_hi |     p_value |
|:--------------|:-------|-----------:|----------:|-------------:|-------------:|-------------:|------------:|
| H1_hist_logit | post   |   0.499121 | 0.0713996 |      1.64727 |      1.43215 |      1.89471 | 2.73836e-12 |

Interrupted time series (monthly pct_historical): pct_historical ~ t + post + post_t + month-of-year FE
| model                   | term   |       coef |       se |   z_or_t |     p_value |
|:------------------------|:-------|-----------:|---------:|---------:|------------:|
| H1_its_monthly_pct_hist | post   | -67.8786   | 7.00319  | -9.69254 | 3.24373e-22 |
| H1_its_monthly_pct_hist | post_t |   0.984768 | 0.107711 |  9.14272 | 6.09009e-20 |

## H2) Timeliness: reporting delay
### Continuous DV: OLS on log1p_delay
| model        | term            |        coef |        se |    z_or_t |     p_value |
|:-------------|:----------------|------------:|----------:|----------:|------------:|
| H2_ols_log1p | post            | -0.219885   | 0.0240519 | -9.14209  | 6.12577e-20 |
| H2_ols_log1p | historical      |  0.0431676  | 0.153896  |  0.280499 | 0.779094    |
| H2_ols_log1p | post:historical |  0.00784468 | 0.0287854 |  0.272523 | 0.78522     |

### Two-part model
Any delay (logit) formula used: `any_delay ~ post + historical + post:historical + C(rurality_3) + C(county_norm)`
| model              | term            |   log_odds |        se |   odds_ratio |   or_ci95_lo |   or_ci95_hi |     p_value |
|:-------------------|:----------------|-----------:|----------:|-------------:|-------------:|-------------:|------------:|
| H2_logit_any_delay | post            |  -0.687265 | 0.0733209 |     0.50295  |     0.435625 |     0.58068  | 7.02448e-21 |
| H2_logit_any_delay | historical      |  -0.134713 | 0.0859012 |     0.873967 |     0.738541 |     1.03423  | 0.116828    |
| H2_logit_any_delay | post:historical |  -0.472647 | 0.140966  |     0.62335  |     0.472867 |     0.821722 | 0.000799662 |

Delay length | delay>0 (OLS log1p_delay):
| model                       | term            |       coef |        se |    z_or_t |    p_value |
|:----------------------------|:----------------|-----------:|----------:|----------:|-----------:|
| H2_ols_log1p_cond_delay_gt0 | post            | -0.0570987 | 0.0174127 | -3.27914  | 0.00104123 |
| H2_ols_log1p_cond_delay_gt0 | historical      |  0.107903  | 0.127927  |  0.843472 | 0.398965   |
| H2_ols_log1p_cond_delay_gt0 | post:historical |  0.202392  | 0.0290573 |  6.96527  | 3.2777e-12 |

### Threshold models (odds ratios)
late30 formula used: `late30 ~ post + historical + post:historical + C(rurality_3) + C(county_norm)`
| model           | term            |   log_odds |       se |   odds_ratio |   or_ci95_lo |   or_ci95_hi |    p_value |
|:----------------|:----------------|-----------:|---------:|-------------:|-------------:|-------------:|-----------:|
| H2_logit_late30 | post            |   0.733227 | 0.645191 |     2.08179  |     0.587812 |      7.37283 | 0.255769   |
| H2_logit_late30 | historical      |   2.01097  | 0.620959 |     7.47059  |     2.21199  |     25.2305  | 0.00120162 |
| H2_logit_late30 | post:historical |  -0.255636 | 0.57148  |     0.774424 |     0.252653 |      2.37374 | 0.654643   |

late90 formula used: `late90 ~ post + historical + post:historical + C(rurality_3) + C(county_norm)`
| model           | term            |   log_odds |       se |   odds_ratio |   or_ci95_lo |   or_ci95_hi |     p_value |
|:----------------|:----------------|-----------:|---------:|-------------:|-------------:|-------------:|------------:|
| H2_logit_late90 | post            |    2.7117  | 0.259629 |    15.0549   |    9.05061   |     25.0426  | 1.552e-25   |
| H2_logit_late90 | historical      |    3.62552 | 1.13116  |    37.5443   |    4.08958   |    344.674   | 0.00135002  |
| H2_logit_late90 | post:historical |   -1.78833 | 0.341862 |     0.167239 |    0.0855731 |      0.32684 | 1.68458e-07 |

extreme99 formula used: `extreme99 ~ post + historical + post:historical + C(rurality_3) + C(county_norm)`
| model              | term            |   log_odds |       se |      odds_ratio |    or_ci95_lo |     or_ci95_hi |     p_value |
|:-------------------|:----------------|-----------:|---------:|----------------:|--------------:|---------------:|------------:|
| H2_logit_extreme99 | post            |    8.89153 | 1.09531  |  7270.16        |  849.56       | 62214.8        | 4.74722e-16 |
| H2_logit_extreme99 | historical      |    9.49082 | 0.829431 | 13237.6         | 2604.85       | 67272.1        | 2.56212e-30 |
| H2_logit_extreme99 | post:historical |   -7.74524 | 1.35212  |     0.000432796 |    3.0573e-05 |     0.00612672 | 1.01481e-08 |

Predicted P(late30) by spill type × period (marginal standardization):
| period    | spill_type   |       mean |    ci95_lo |    ci95_hi |
|:----------|:-------------|-----------:|-----------:|-----------:|
| pre_2020  | Recent       | 0.00365003 | 0.0024855  | 0.00627317 |
| pre_2020  | Historical   | 0.0259166  | 0.0121502  | 0.0547058  |
| post_2020 | Recent       | 0.00753063 | 0.00179263 | 0.0334635  |
| post_2020 | Historical   | 0.0404562  | 0.0253026  | 0.0631995  |
Plot saved: `/home/dadams/Repos/colorado_redux/analysis_postgis/step2_model_outputs/pred_late30_pre_post_by_type.png`

## H3) Rural lag + heterogeneity
late30 with post×rurality interaction (core + interaction terms):
| model                           | term                           |   log_odds |       se |   odds_ratio |   or_ci95_lo |   or_ci95_hi |    p_value |
|:--------------------------------|:-------------------------------|-----------:|---------:|-------------:|-------------:|-------------:|-----------:|
| H3_logit_late30_post_x_rurality | post                           |   0.764282 | 0.639336 |     2.14745  |     0.613351 |      7.51861 | 0.231919   |
| H3_logit_late30_post_x_rurality | post:C(rurality_3)[T.Suburban] |  -1.15505  | 0.671184 |     0.315043 |     0.084537 |      1.17407 | 0.0852674  |
| H3_logit_late30_post_x_rurality | post:C(rurality_3)[T.Urban]    |   0.216575 | 0.447007 |     1.24182  |     0.51708  |      2.98234 | 0.62803    |
| H3_logit_late30_post_x_rurality | historical                     |   2.05961  | 0.718533 |     7.84291  |     1.918    |     32.0704  | 0.00415158 |
| H3_logit_late30_post_x_rurality | post:historical                |  -0.338292 | 0.560403 |     0.712987 |     0.237715 |      2.13848 | 0.54607    |

Predicted P(late30) by rurality × period for Recent (historical=0):
| rurality_3   | period    |       mean |     ci95_lo |    ci95_hi |
|:-------------|:----------|-----------:|------------:|-----------:|
| Rural        | pre_2020  | 0.0038878  | 0.0029556   | 0.00519953 |
| Rural        | post_2020 | 0.00827299 | 0.00186044  | 0.0365342  |
| Suburban     | pre_2020  | 0.00879439 | 0.00276839  | 0.0211865  |
| Suburban     | post_2020 | 0.0059846  | 0.0012201   | 0.0332954  |
| Urban        | pre_2020  | 0.00261609 | 0.000782753 | 0.00716594 |
| Urban        | post_2020 | 0.00691419 | 0.00143749  | 0.0408529  |
Plot saved: `/home/dadams/Repos/colorado_redux/analysis_postgis/step2_model_outputs/pred_late30_pre_post_by_rurality_recent.png`

Top 15 operators by adjusted predicted P(late30) (min n>=50):
| operator                              |   n_total |   p_late30_adj |
|:--------------------------------------|----------:|---------------:|
| UTAH GAS OP LTD DBA UTAH GAS CORP     |       122 |          9.191 |
| SCOUT ENERGY MANAGEMENT LLC           |       106 |          4.021 |
| CHEVRON USA INC                       |       872 |          3.47  |
| URSA OPERATING COMPANY LLC            |       110 |          2.99  |
| XTO ENERGY INC                        |       184 |          2.779 |
| NOBLE ENERGY INC                      |      5430 |          1.973 |
| CHEVRON PRODUCTION COMPANY            |        72 |          1.807 |
| KERR MCGEE OIL & GAS ONSHORE LP       |      4714 |          1.801 |
| PDC ENERGY INC                        |      2454 |          1.69  |
| CRESTONE PEAK RESOURCES OPERATING LLC |       694 |          1.568 |
| CAERUS PICEANCE LLC                   |      2194 |          1.478 |
| SYNERGY RESOURCES CORPORATION         |       100 |          1.304 |
| SRC ENERGY INC                        |       158 |          1.111 |
| WHITING OIL & GAS CORPORATION         |       446 |          1.09  |
| EXTRACTION OIL & GAS INC              |       494 |          1.037 |

Bottom 15 operators by adjusted predicted P(late30) (min n>=50):
| operator                      |   n_total |   p_late30_adj |
|:------------------------------|----------:|---------------:|
| EOG RESOURCES INC             |       104 |          0.301 |
| VANGUARD OPERATING LLC        |        68 |          0.301 |
| BNN WESTERN LLC               |        50 |          0.308 |
| BERRY PETROLEUM COMPANY LLC   |        64 |          0.329 |
| NGL WATER SOLUTIONS DJ LLC    |       138 |          0.359 |
| NOBLE MIDSTREAM SERVICES LLC  |        78 |          0.414 |
| BISON OIL & GAS II LLC        |        52 |          0.472 |
| GRAND RIVER GATHERING LLC     |       138 |          0.473 |
| WPX ENERGY ROCKY MOUNTAIN LLC |       164 |          0.491 |
| DCP MIDSTREAM LP              |       208 |          0.493 |
| SUMMIT MIDSTREAM PARTNERS LLC |        78 |          0.503 |
| TALLGRASS WATER WESTERN LLC   |        56 |          0.589 |
| BISON IV OPERATING LLC        |        70 |          0.589 |
| TAPROOT ROCKIES MIDSTREAM LLC |        52 |          0.589 |
| LARAMIE ENERGY LLC            |       286 |          0.595 |

Top 15 counties by adjusted predicted P(late30) (min n>=50):
| county_norm   |   n_total |   p_late30_adj |
|:--------------|----------:|---------------:|
| RIO BLANCO    |      2024 |          4.349 |
| WELD          |     20874 |          1.456 |
| GARFIELD      |      3478 |          0.575 |

## Robustness / sensitivity
### OLS (log1p_delay): baseline vs cap180 vs exclude extreme99
| model                        | term            |        coef |        se |     z_or_t |     p_value |
|:-----------------------------|:----------------|------------:|----------:|-----------:|------------:|
| robust_ols_baseline          | post            | -0.219885   | 0.0240519 | -9.14209   | 6.12577e-20 |
| robust_ols_baseline          | historical      |  0.0431676  | 0.153896  |  0.280499  | 0.779094    |
| robust_ols_baseline          | post:historical |  0.00784468 | 0.0287854 |  0.272523  | 0.78522     |
| robust_ols_cap180            | post            | -0.219943   | 0.0239156 | -9.19663   | 3.69366e-20 |
| robust_ols_cap180            | historical      |  0.0410761  | 0.154035  |  0.266667  | 0.789725    |
| robust_ols_cap180            | post:historical |  0.00560195 | 0.0287358 |  0.194947  | 0.845435    |
| robust_ols_exclude_extreme99 | post            | -0.231604   | 0.0242475 | -9.55166   | 1.27629e-21 |
| robust_ols_exclude_extreme99 | historical      |  0.00373491 | 0.144605  |  0.0258284 | 0.979394    |
| robust_ols_exclude_extreme99 | post:historical | -0.0369703  | 0.0243886 | -1.51588   | 0.12955     |

Exclude-extreme99 variant removes 0.713% of rows (extreme99==1).

### late30 (logit): baseline vs exclude extreme99
| model                           | term            |   log_odds |       se |   odds_ratio |   or_ci95_lo |   or_ci95_hi |    p_value |
|:--------------------------------|:----------------|-----------:|---------:|-------------:|-------------:|-------------:|-----------:|
| robust_late30_baseline          | post            |   0.733227 | 0.645191 |     2.08179  |     0.587812 |      7.37283 | 0.255769   |
| robust_late30_baseline          | historical      |   2.01097  | 0.620959 |     7.47059  |     2.21199  |     25.2305  | 0.00120162 |
| robust_late30_baseline          | post:historical |  -0.255636 | 0.57148  |     0.774424 |     0.252653 |      2.37374 | 0.654643   |
| robust_late30_exclude_extreme99 | post            |   0.147381 | 0.62227  |     1.1588   |     0.342231 |      3.92368 | 0.812777   |
| robust_late30_exclude_extreme99 | historical      |   1.84611  | 0.967478 |     6.33511  |     0.951086 |     42.1976  | 0.05637    |
| robust_late30_exclude_extreme99 | post:historical |  -0.152764 | 0.514639 |     0.858332 |     0.31303  |      2.35356 | 0.76659    |

## Outputs
- Report: `/home/dadams/Repos/colorado_redux/step2_models_summary.md`
- Output directory: `/home/dadams/Repos/colorado_redux/analysis_postgis/step2_model_outputs`