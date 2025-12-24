# Paper Tables (journal-ready markdown)

Source folder (CSVs): `/home/dadams/Repos/colorado_redux/analysis_postgis/step2_model_outputs`
Generated: `/home/dadams/Repos/colorado_redux/step2_paper_tables.md`

Significance: * p<0.10, ** p<0.05, *** p<0.01

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
| post_2020 | 15704 | 47.9 |
| pre_2020 | 10672 | 35.4 |

### Table H1-B: Spill-level logit (post effect) + predicted pct_historical
**Panel 1: Logit OR for Post**
| Term | OR [95% CI] | p |
| --- | --- | --- |
| Post | 1.647*** [1.557, 1.743] | <0.001 |

**Panel 2: Model-implied pct_historical (marginal)**
| period | pred_pct_historical |
| --- | --- |
| pre_2020 | 36.8 |
| post_2020 | 46.8 |

### Table H1-C (Appendix): Operator FE LPM (post coefficient)
| Term | Estimate (SE) | p |
| --- | --- | --- |
| Post | 0.107*** (0.032) | <0.001 |

Note: Standard errors are clustered by operator.

## Claim 2: Typical reporting timeliness improves post-2020

### Table H2-A: OLS on log(1+delay) (core terms)
| Term | Estimate (SE) | p |
| --- | --- | --- |
| Post | -0.220*** (0.060) | <0.001 |
| Historical | 0.043 (0.091) | 0.636 |
| Post × Historical | 0.008 (0.081) | 0.923 |

Note: Standard errors are clustered by operator; model includes operator fixed effects and county/rurality controls.

### Table H2-A′ (Appendix): Same model clustered by county
| Term | Estimate (SE) | p |
| --- | --- | --- |
| Post | -0.220*** (0.013) | <0.001 |
| Historical | 0.043*** (0.017) | 0.009 |
| Post × Historical | 0.008 (0.020) | 0.697 |

### Table R1 (Appendix): Robustness (key terms)
| variant | post | post_se | post:historical | int_se |
| --- | --- | --- | --- | --- |
| baseline | -0.220 | 0.060 | 0.008 | 0.081 |
| cap180 | -0.220 | 0.060 | 0.006 | 0.080 |
| exclude_extreme99 | -0.232 | 0.062 | -0.037 | 0.075 |

## Claim 3: Mechanism is mostly fewer any-delay cases; tail behaves differently for Historical

### Table H2-B: Two-part model (core terms)
**Panel 1: any_delay logit (ORs)**
| Term | OR [95% CI] | p |
| --- | --- | --- |
| Post | 0.420*** [0.244, 0.724] | 0.002 |
| Historical | 0.790 [0.520, 1.198] | 0.267 |
| Post × Historical | 0.721 [0.437, 1.190] | 0.200 |

**Panel 2: conditional delay>0 OLS (coefficients)**
| Term | Estimate (SE) | p |
| --- | --- | --- |
| Post | -0.057 (0.048) | 0.237 |
| Historical | 0.108 (0.080) | 0.177 |
| Post × Historical | 0.202*** (0.068) | 0.003 |

### Table H2-C: Mechanism decomposition (by spill type × period)
| spill_type | period | P_any_delay | E_delay_if_pos |
| --- | --- | --- | --- |
| Recent | pre_2020 | 0.745 | 2.03 |
| Recent | post_2020 | 0.573 | 1.86 |
| Historical | pre_2020 | 0.702 | 2.38 |
| Historical | post_2020 | 0.449 | 2.90 |

## Claim 4: Extreme delays remain rare but increase post-2020 and are concentrated in Historical cases

### Table H2-D: Predicted probabilities for late30 and late90 (by spill type × period)
| spill_type | period | P_late30 | P_late90 |
| --- | --- | --- | --- |
| Recent | pre_2020 | 0.003650 | 0.000239 |
| Recent | post_2020 | 0.007531 | 0.003581 |
| Historical | pre_2020 | 0.025917 | 0.008854 |
| Historical | post_2020 | 0.040456 | 0.021834 |

### Table H2-E (Appendix): late30 and late90 logits (core terms)
**Panel 1: late30 logit (ORs)**
| Term | OR [95% CI] | p |
| --- | --- | --- |
| Post | 2.082 [0.827, 5.242] | 0.120 |
| Historical | 7.471*** [2.364, 23.605] | <0.001 |
| Post × Historical | 0.774 [0.275, 2.179] | 0.628 |

**Panel 2: late90 logit (ORs)**
| Term | OR [95% CI] | p |
| --- | --- | --- |
| Post | 15.055** [1.631, 139.000] | 0.017 |
| Historical | 37.544*** [3.303, 426.734] | 0.003 |
| Post × Historical | 0.167 [0.016, 1.751] | 0.136 |

### Table E99 (Appendix): Ridge extreme99 predicted probabilities
| spill_type | p_pre | p_post | risk_ratio | risk_diff |
| --- | --- | --- | --- | --- |
| Recent | 0.1 | 0.3 | 3.17 | 0.21 |
| Historical | 0.4 | 0.7 | 1.89 | 0.33 |

## Claim 5: Geography moderates improvement (tempered rural lag)

### Table H3-A: Joint tests for post×rurality
| Outcome | Test | Statistic | df | p |
| --- | --- | --- | --- | --- |
| Any delay | χ² | 1.667 | 2 | 0.434 |
| log(1+delay) | F | 3.278 | (2, 141) | 0.041 |
| Late ≥90 | χ² | 0.685 | 2 | 0.710 |

### Table H3-B: Rurality gradient (Recent spills only)
| rurality_3 | period | P_any_delay | implied_mean_delay | P_late30 | P_late90 |
| --- | --- | --- | --- | --- | --- |
| Rural | pre_2020 | 0.757073 | 1.47 | 0.005869 | 0.000344 |
| Rural | post_2020 | 0.645204 | 1.12 | 0.012055 | 0.005139 |
| Suburban | pre_2020 | 0.71421 | 1.54 | 0.002721 | 0.000188 |
| Suburban | post_2020 | 0.540791 | 0.87 | 0.005649 | 0.002819 |
| Urban | pre_2020 | 0.735393 | 1.22 | 0.002262 | 0.000167 |
| Urban | post_2020 | 0.536487 | 0.66 | 0.004697 | 0.002508 |

## Claim 6: Operator + geography variation (profiling deliverables)

### Table VAR-A: County adjusted predicted probabilities
| county_norm | n_total | p_late30_adj | p_late90_adj |
| --- | --- | --- | --- |
| GARFIELD | 3478 | 0.57 | 0.17 |
| RIO BLANCO | 2024 | 4.35 | 1.28 |
| WELD | 20874 | 1.46 | 0.81 |

### Operator risk profiles (Appendix): Top/Bottom 15
**Top 15 any_delay**
| Rank | Operator | N | Adj. P(any delay) (%) |
| --- | --- | --- | --- |
| 1 | SYNERGY RESOURCES CORPORATION | 100 | 96.0 |
| 2 | BARRETT CORPORATION* BILL | 140 | 91.4 |
| 3 | VANGUARD OPERATING LLC | 68 | 91.1 |
| 4 | BISON OIL & GAS II LLC | 52 | 88.4 |
| 5 | BAYSWATER EXPLORATION & PRODUCTION LLC | 116 | 88.0 |
| 6 | BNN WESTERN LLC | 50 | 87.9 |
| 7 | FUNDARE RESOURCES OPERATING COMPANY LLC | 196 | 87.7 |
| 8 | XTO ENERGY INC | 184 | 84.8 |
| 9 | NOBLE MIDSTREAM SERVICES LLC | 78 | 84.6 |
| 10 | BERRY PETROLEUM COMPANY LLC | 64 | 84.2 |
| 11 | URSA OPERATING COMPANY LLC | 110 | 83.6 |
| 12 | BAYSWATER EXPLORATION AND PRODUCTION LLC | 76 | 81.6 |
| 13 | CHEVRON USA INC | 872 | 81.0 |
| 14 | FOUNDATION ENERGY MANAGEMENT LLC | 160 | 80.0 |
| 15 | LARAMIE ENERGY LLC | 286 | 79.8 |

**Bottom 15 any_delay**
| Rank | Operator | N | Adj. P(any delay) (%) |
| --- | --- | --- | --- |
| 1 | KERR MCGEE OIL & GAS ONSHORE LP | 4714 | 34.0 |
| 2 | CHEVRON PRODUCTION COMPANY | 72 | 36.1 |
| 3 | WPX ENERGY ROCKY MOUNTAIN LLC | 164 | 36.5 |
| 4 | NGL WATER SOLUTIONS DJ LLC | 138 | 49.3 |
| 5 | HIGHPOINT OPERATING CORPORATION | 856 | 50.2 |
| 6 | K P KAUFFMAN COMPANY INC | 72 | 52.9 |
| 7 | CAERUS PICEANCE LLC | 2194 | 53.7 |
| 8 | EXTRACTION OIL & GAS INC | 494 | 54.6 |
| 9 | BONANZA CREEK ENERGY OPERATING COMPANY LLC | 1130 | 55.8 |
| 10 | SUMMIT MIDSTREAM PARTNERS LLC | 78 | 56.4 |
| 11 | KERR MCGEE GATHERING LLC | 250 | 56.8 |
| 12 | TAPROOT ROCKIES MIDSTREAM LLC | 52 | 57.5 |
| 13 | VERDAD RESOURCES LLC | 144 | 58.3 |
| 14 | NOBLE ENERGY INC | 5430 | 61.8 |
| 15 | UTAH GAS OP LTD DBA UTAH GAS CORP | 122 | 62.3 |

**Top 15 late30**
| Rank | Operator | N | Adj. P(late ≥30) (%) | Adj. P(any delay) (%) |
| --- | --- | --- | --- | --- |
| 1 | UTAH GAS OP LTD DBA UTAH GAS CORP | 122 | 9.2 | 62.3 |
| 2 | SCOUT ENERGY MANAGEMENT LLC | 106 | 4.0 | 79.2 |
| 3 | CHEVRON USA INC | 872 | 3.5 | 81.0 |
| 4 | URSA OPERATING COMPANY LLC | 110 | 3.0 | 83.6 |
| 5 | XTO ENERGY INC | 184 | 2.8 | 84.8 |
| 6 | NOBLE ENERGY INC | 5430 | 2.0 | 61.8 |
| 7 | CHEVRON PRODUCTION COMPANY | 72 | 1.8 | 36.1 |
| 8 | KERR MCGEE OIL & GAS ONSHORE LP | 4714 | 1.8 | 34.0 |
| 9 | PDC ENERGY INC | 2454 | 1.7 | 66.9 |
| 10 | CRESTONE PEAK RESOURCES OPERATING LLC | 694 | 1.6 | 62.5 |
| 11 | CAERUS PICEANCE LLC | 2194 | 1.5 | 53.7 |
| 12 | SYNERGY RESOURCES CORPORATION | 100 | 1.3 | 96.0 |
| 13 | SRC ENERGY INC | 158 | 1.1 | 65.8 |
| 14 | WHITING OIL & GAS CORPORATION | 446 | 1.1 | 62.8 |
| 15 | EXTRACTION OIL & GAS INC | 494 | 1.0 | 54.6 |

**Bottom 15 late30**
| Rank | Operator | N | Adj. P(late ≥30) (%) | Adj. P(any delay) (%) |
| --- | --- | --- | --- | --- |
| 1 | EOG RESOURCES INC | 104 | 0.3 | 75.0 |
| 2 | VANGUARD OPERATING LLC | 68 | 0.3 | 91.1 |
| 3 | BNN WESTERN LLC | 50 | 0.3 | 87.9 |
| 4 | BERRY PETROLEUM COMPANY LLC | 64 | 0.3 | 84.2 |
| 5 | NGL WATER SOLUTIONS DJ LLC | 138 | 0.4 | 49.3 |
| 6 | NOBLE MIDSTREAM SERVICES LLC | 78 | 0.4 | 84.6 |
| 7 | BISON OIL & GAS II LLC | 52 | 0.5 | 88.4 |
| 8 | GRAND RIVER GATHERING LLC | 138 | 0.5 | 63.7 |
| 9 | WPX ENERGY ROCKY MOUNTAIN LLC | 164 | 0.5 | 36.5 |
| 10 | DCP MIDSTREAM LP | 208 | 0.5 | 75.0 |
| 11 | SUMMIT MIDSTREAM PARTNERS LLC | 78 | 0.5 | 56.4 |
| 12 | TALLGRASS WATER WESTERN LLC | 56 | 0.6 | 78.6 |
| 13 | BISON IV OPERATING LLC | 70 | 0.6 | 77.2 |
| 14 | TAPROOT ROCKIES MIDSTREAM LLC | 52 | 0.6 | 57.5 |
| 15 | LARAMIE ENERGY LLC | 286 | 0.6 | 79.8 |

