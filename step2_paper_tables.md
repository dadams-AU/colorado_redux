# Paper Tables (from exported CSV artifacts + in-memory descriptives)

Source folder (CSVs): `/home/dadams/Repos/colorado_redux/analysis_postgis/step2_model_outputs`
Generated: `/home/dadams/Repos/colorado_redux/step2_paper_tables.md`

## Table D1: Traditional descriptives

(Delay is in days; cells report mean (SD) and median [IQR]. Percentages are percent of spills in group.)

### Table D1-A: Delay descriptives by period
| period | n | pct_historical | mean (SD) | median [IQR] | pct_delay_0 | pct_delay_le1 | pct_any_delay | pct_late30 | pct_late90 | pct_ge99 | n_operators | n_counties | n_rurality |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| post_2020 | 15704 | 47.9 | 3.93 (30.82) | 1 [0, 1] | 48.9 | 81.6 | 51.1 | 1.9 | 1.1 | 1.1 | 86 | 3 | 3 |
| pre_2020 | 10672 | 35.4 | 2.50 (12.39) | 1 [0, 2] | 27.0 | 66.1 | 73.0 | 1.0 | 0.3 | 0.2 | 102 | 3 | 3 |

### Table D1-B: Delay descriptives by spill type × period
| spill_type | period | n | mean (SD) | median [IQR] | pct_delay_0 | pct_delay_le1 | pct_any_delay | pct_late30 | pct_late90 | pct_ge99 | n_operators | n_counties | n_rurality |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Historical | post_2020 | 7518 | 5.56 (35.23) | 0 [0, 1] | 58.0 | 85.5 | 42.0 | 3.2 | 1.9 | 1.8 | 46 | 3 | 3 |
| Historical | pre_2020 | 3776 | 3.59 (19.93) | 1 [0, 2] | 30.3 | 69.4 | 69.7 | 2.0 | 0.7 | 0.6 | 46 | 3 | 3 |
| Recent | post_2020 | 8186 | 2.42 (26.05) | 1 [0, 1] | 40.6 | 78.0 | 59.4 | 0.8 | 0.4 | 0.4 | 71 | 3 | 3 |
| Recent | pre_2020 | 6896 | 1.90 (4.40) | 1 [0, 2] | 25.2 | 64.2 | 74.8 | 0.5 | 0.0 | 0.0 | 90 | 3 | 3 |

## Claim 1: Post-2020 shifts spill composition toward inspection-identified (Historical) spills

### Table H1-A: Descriptive mix by period
| period | n_total | pct_historical |
| --- | --- | --- |
| post_2020 | 15704 | 47.873 |
| pre_2020 | 10672 | 35.382 |

### Table H1-B: Baseline spill-level logit + marginal predicted pct_historical
**Panel 1: OR for post (controls: county + rurality)**
| term | OR | CI95_lo | CI95_hi | p |
| --- | --- | --- | --- | --- |
| post | 1.647 | 1.557 | 1.743 | 0.000 |

**Panel 2: model-implied pct_historical pre vs post (marginal)**
| period | pred_pct_historical |
| --- | --- |
| pre_2020 | 36.826 |
| post_2020 | 46.762 |

### Table H1-C (Appendix): Operator FE LPM (post coefficient; clustered by operator)
| term | coef | se | p |
| --- | --- | --- | --- |
| post | 0.107 | 0.032 | 0.001 |

## Claim 2: Typical reporting timeliness improves post-2020

### Table H2-A: OLS on log(1+delay) (cluster by operator)
| term | coef | se | p |
| --- | --- | --- | --- |
| post | -0.220 | 0.060 | 0.000 |
| historical | 0.043 | 0.091 | 0.636 |
| post:historical | 0.008 | 0.081 | 0.923 |

### Table H2-A′ (Appendix): Same model clustered by county
| term | coef | se | p |
| --- | --- | --- | --- |
| post | -0.220 | 0.013 | 0.000 |
| historical | 0.043 | 0.017 | 0.009 |
| post:historical | 0.008 | 0.020 | 0.697 |

### Table R1 (Appendix): Robustness continuous key terms (baseline vs cap180 vs exclude_extreme99)
| variant | post | post_se | post:historical | int_se |
| --- | --- | --- | --- | --- |
| baseline | -0.220 | 0.060 | 0.008 | 0.081 |
| cap180 | -0.220 | 0.060 | 0.006 | 0.080 |
| exclude_extreme99 | -0.232 | 0.062 | -0.037 | 0.075 |

## Claim 3: Mechanism is mostly fewer any-delay cases; tail behaves differently for Historical

### Table H2-B: Two-part model coefficients
**Panel 1: any_delay logit (ORs)**
| term | OR | CI95_lo | CI95_hi | p |
| --- | --- | --- | --- | --- |
| post | 0.420 | 0.244 | 0.724 | 0.002 |
| historical | 0.790 | 0.520 | 1.198 | 0.267 |
| post:historical | 0.721 | 0.437 | 1.190 | 0.200 |

**Panel 2: conditional delay>0 OLS (coefficients)**
| term | coef | se | p |
| --- | --- | --- | --- |
| post | -0.057 | 0.048 | 0.237 |
| historical | 0.108 | 0.080 | 0.177 |
| post:historical | 0.202 | 0.068 | 0.003 |

### Table H2-C: Mechanism decomposition (P(any_delay) + E(delay|delay>0) by spill type × period)
| spill_type | period | P_any_delay | E_delay_if_pos |
| --- | --- | --- | --- |
| Recent | pre_2020 | 0.745 | 2.030 |
| Recent | post_2020 | 0.573 | 1.862 |
| Historical | pre_2020 | 0.702 | 2.376 |
| Historical | post_2020 | 0.449 | 2.904 |

## Claim 4: Extreme delays remain rare but increase post-2020 and are concentrated in Historical cases

### Table H2-D: Predicted probabilities for late30 and late90 by spill type × period
| spill_type | period | P_late30 | P_late90 |
| --- | --- | --- | --- |
| Recent | pre_2020 | 0.004 | 0.000 |
| Recent | post_2020 | 0.008 | 0.004 |
| Historical | pre_2020 | 0.026 | 0.009 |
| Historical | post_2020 | 0.040 | 0.022 |

### Table H2-E (Appendix): late30 and late90 logit coefficients (ORs)
**Panel 1: late30 logit (ORs)**
| term | OR | CI95_lo | CI95_hi | p |
| --- | --- | --- | --- | --- |
| post | 2.082 | 0.827 | 5.242 | 0.120 |
| historical | 7.471 | 2.364 | 23.605 | 0.001 |
| post:historical | 0.774 | 0.275 | 2.179 | 0.628 |

**Panel 2: late90 logit (ORs)**
| term | OR | CI95_lo | CI95_hi | p |
| --- | --- | --- | --- | --- |
| post | 15.055 | 1.631 | 139.000 | 0.017 |
| historical | 37.544 | 3.303 | 426.734 | 0.003 |
| post:historical | 0.167 | 0.016 | 1.751 | 0.136 |

### Table E99 (Appendix): Ridge extreme99 predicted probabilities and risk ratios
| spill_type | p_pre | p_post | risk_ratio | risk_diff |
| --- | --- | --- | --- | --- |
| Recent | 0.095 | 0.303 | 3.169 | 0.207 |
| Historical | 0.374 | 0.707 | 1.888 | 0.333 |

## Claim 5: Geography moderates improvement (tempered rural lag)

### Table H3-A: Interaction/joint tests summary
| outcome | test | stat | df | p_value |
| --- | --- | --- | --- | --- |
| any_delay | χ² | 1.667 | 2 | 0.434483 |
| log1p_delay | F | 3.278 | (2, 141) | 0.0405981 |
| late90 | χ² | 0.685 | 2 | 0.709937 |

### Table H3-B: Rurality gradient (Recent spills only)
| rurality_3 | period | P_any_delay | implied_mean_delay | P_late30 | P_late90 |
| --- | --- | --- | --- | --- | --- |
| Rural | pre_2020 | 0.757 | 1.470 | 0.006 | 0.000 |
| Rural | post_2020 | 0.645 | 1.119 | 0.012 | 0.005 |
| Suburban | pre_2020 | 0.714 | 1.544 | 0.003 | 0.000 |
| Suburban | post_2020 | 0.541 | 0.867 | 0.006 | 0.003 |
| Urban | pre_2020 | 0.735 | 1.216 | 0.002 | 0.000 |
| Urban | post_2020 | 0.536 | 0.664 | 0.005 | 0.003 |

## Claim 6: Operator + geography variation (profiling deliverables)

### Table VAR-A: County adjusted predicted probabilities
| county_norm | n_total | p_late30_adj | p_late90_adj |
| --- | --- | --- | --- |
| GARFIELD | 3478 | 0.575 | 0.171 |
| RIO BLANCO | 2024 | 4.349 | 1.284 |
| WELD | 20874 | 1.456 | 0.805 |

### Operator risk profiles (Appendix): Top/Bottom 15
**Top 15 any_delay**
| operator | n_total | p_late30_adj | p_any_adj |
| --- | --- | --- | --- |
| SYNERGY RESOURCES CORPORATION | 100 | 1.304 | 95.994 |
| BARRETT CORPORATION* BILL | 140 | 0.817 | 91.400 |
| VANGUARD OPERATING LLC | 68 | 0.301 | 91.132 |
| BISON OIL & GAS II LLC | 52 | 0.472 | 88.411 |
| BAYSWATER EXPLORATION & PRODUCTION LLC | 116 | 0.820 | 88.007 |
| BNN WESTERN LLC | 50 | 0.308 | 87.927 |
| FUNDARE RESOURCES OPERATING COMPANY LLC | 196 | 0.812 | 87.736 |
| XTO ENERGY INC | 184 | 2.779 | 84.785 |
| NOBLE MIDSTREAM SERVICES LLC | 78 | 0.414 | 84.593 |
| BERRY PETROLEUM COMPANY LLC | 64 | 0.329 | 84.214 |
| URSA OPERATING COMPANY LLC | 110 | 2.990 | 83.626 |
| BAYSWATER EXPLORATION AND PRODUCTION LLC | 76 | 0.709 | 81.611 |
| CHEVRON USA INC | 872 | 3.470 | 80.964 |
| FOUNDATION ENERGY MANAGEMENT LLC | 160 | 0.705 | 79.963 |
| LARAMIE ENERGY LLC | 286 | 0.595 | 79.758 |

**Bottom 15 any_delay**
| operator | n_total | p_late30_adj | p_any_adj |
| --- | --- | --- | --- |
| KERR MCGEE OIL & GAS ONSHORE LP | 4714 | 1.801 | 34.028 |
| CHEVRON PRODUCTION COMPANY | 72 | 1.807 | 36.083 |
| WPX ENERGY ROCKY MOUNTAIN LLC | 164 | 0.491 | 36.518 |
| NGL WATER SOLUTIONS DJ LLC | 138 | 0.359 | 49.310 |
| HIGHPOINT OPERATING CORPORATION | 856 | 0.709 | 50.234 |
| K P KAUFFMAN COMPANY INC | 72 | 0.778 | 52.895 |
| CAERUS PICEANCE LLC | 2194 | 1.478 | 53.702 |
| EXTRACTION OIL & GAS INC | 494 | 1.037 | 54.632 |
| BONANZA CREEK ENERGY OPERATING COMPANY LLC | 1130 | 0.755 | 55.773 |
| SUMMIT MIDSTREAM PARTNERS LLC | 78 | 0.503 | 56.398 |
| KERR MCGEE GATHERING LLC | 250 | 0.756 | 56.773 |
| TAPROOT ROCKIES MIDSTREAM LLC | 52 | 0.589 | 57.472 |
| VERDAD RESOURCES LLC | 144 | 0.643 | 58.332 |
| NOBLE ENERGY INC | 5430 | 1.973 | 61.807 |
| UTAH GAS OP LTD DBA UTAH GAS CORP | 122 | 9.191 | 62.260 |

**Top 15 late30**
| operator | n_total | p_late30_adj | p_any_adj |
| --- | --- | --- | --- |
| UTAH GAS OP LTD DBA UTAH GAS CORP | 122 | 9.191 | 62.260 |
| SCOUT ENERGY MANAGEMENT LLC | 106 | 4.021 | 79.231 |
| CHEVRON USA INC | 872 | 3.470 | 80.964 |
| URSA OPERATING COMPANY LLC | 110 | 2.990 | 83.626 |
| XTO ENERGY INC | 184 | 2.779 | 84.785 |
| NOBLE ENERGY INC | 5430 | 1.973 | 61.807 |
| CHEVRON PRODUCTION COMPANY | 72 | 1.807 | 36.083 |
| KERR MCGEE OIL & GAS ONSHORE LP | 4714 | 1.801 | 34.028 |
| PDC ENERGY INC | 2454 | 1.690 | 66.911 |
| CRESTONE PEAK RESOURCES OPERATING LLC | 694 | 1.568 | 62.527 |
| CAERUS PICEANCE LLC | 2194 | 1.478 | 53.702 |
| SYNERGY RESOURCES CORPORATION | 100 | 1.304 | 95.994 |
| SRC ENERGY INC | 158 | 1.111 | 65.833 |
| WHITING OIL & GAS CORPORATION | 446 | 1.090 | 62.769 |
| EXTRACTION OIL & GAS INC | 494 | 1.037 | 54.632 |

**Bottom 15 late30**
| operator | n_total | p_late30_adj | p_any_adj |
| --- | --- | --- | --- |
| EOG RESOURCES INC | 104 | 0.301 | 74.973 |
| VANGUARD OPERATING LLC | 68 | 0.301 | 91.132 |
| BNN WESTERN LLC | 50 | 0.308 | 87.927 |
| BERRY PETROLEUM COMPANY LLC | 64 | 0.329 | 84.214 |
| NGL WATER SOLUTIONS DJ LLC | 138 | 0.359 | 49.310 |
| NOBLE MIDSTREAM SERVICES LLC | 78 | 0.414 | 84.593 |
| BISON OIL & GAS II LLC | 52 | 0.472 | 88.411 |
| GRAND RIVER GATHERING LLC | 138 | 0.473 | 63.678 |
| WPX ENERGY ROCKY MOUNTAIN LLC | 164 | 0.491 | 36.518 |
| DCP MIDSTREAM LP | 208 | 0.493 | 75.010 |
| SUMMIT MIDSTREAM PARTNERS LLC | 78 | 0.503 | 56.398 |
| TALLGRASS WATER WESTERN LLC | 56 | 0.589 | 78.557 |
| BISON IV OPERATING LLC | 70 | 0.589 | 77.213 |
| TAPROOT ROCKIES MIDSTREAM LLC | 52 | 0.589 | 57.472 |
| LARAMIE ENERGY LLC | 286 | 0.595 | 79.758 |

