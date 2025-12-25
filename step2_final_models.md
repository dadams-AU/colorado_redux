# Step 2B final models (Colorado spills mission-change study)

This notebook cell produces the final, defensible model set for H1–H3 while keeping the full sample and avoiding separation in the extreme tail (>=99 days).



## H1: Historical vs Recent mix (agency outputs)

### Descriptive mix

| period    |   n_total |   pct_historical |
|:----------|----------:|-----------------:|
| post_2020 |     15704 |           47.873 |
| pre_2020  |     10672 |           35.382 |

### Models

Baseline spill-level logit formula used: `historical ~ post + C(county_norm) + C(rurality_3)`

| model             | term                         |   log_odds |    se |   odds_ratio |   or_ci95_lo |   or_ci95_hi | p_value   |
|:------------------|:-----------------------------|-----------:|------:|-------------:|-------------:|-------------:|:----------|
| H1_logit_baseline | Intercept                    |     -2.801 | 0.07  |        0.061 |        0.053 |        0.07  | <0.001    |
| H1_logit_baseline | C(county_norm)[T.RIO BLANCO] |      0.705 | 0.093 |        2.024 |        1.688 |        2.428 | <0.001    |
| H1_logit_baseline | C(county_norm)[T.WELD]       |      1.555 | 0.067 |        4.733 |        4.148 |        5.4   | <0.001    |
| H1_logit_baseline | C(rurality_3)[T.Suburban]    |      0.731 | 0.062 |        2.077 |        1.84  |        2.345 | <0.001    |
| H1_logit_baseline | C(rurality_3)[T.Urban]       |      1.42  | 0.033 |        4.138 |        3.878 |        4.414 | <0.001    |
| H1_logit_baseline | post                         |      0.499 | 0.029 |        1.647 |        1.557 |        1.743 | <0.001    |

Marginal predicted pct_historical (pre vs post):

| period    |   pred_pct_historical |
|:----------|----------------------:|
| pre_2020  |                36.826 |
| post_2020 |                46.762 |

Operator-structure robustness: LPM with operator FE, clustered by operator. Formula: `historical ~ post + C(county_norm) + C(rurality_3) + C(operator)`

| model              | term                                                       |   coef |    se |             t | p_value   |
|:-------------------|:-----------------------------------------------------------|-------:|------:|--------------:|:----------|
| H1_LPM_operator_FE | Intercept                                                  | -0.055 | 0.18  |  -0.307       | 0.759     |
| H1_LPM_operator_FE | C(county_norm)[T.RIO BLANCO]                               |  0.088 | 0.033 |   2.706       | 0.007     |
| H1_LPM_operator_FE | C(county_norm)[T.WELD]                                     | -0.184 | 0.171 |  -1.079       | 0.281     |
| H1_LPM_operator_FE | C(rurality_3)[T.Suburban]                                  |  0.125 | 0.034 |   3.679       | <0.001    |
| H1_LPM_operator_FE | C(rurality_3)[T.Urban]                                     |  0.133 | 0.031 |   4.359       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.31 OPERATING]                                | -0.14  | 0.18  |  -0.776       | 0.437     |
| H1_LPM_operator_FE | C(operator)[T.4-H OPERATING CORPORATION]                   |  1.107 | 0.032 |  34.805       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.8 NORTH LLC]                                 |  0.62  | 0.039 |  15.935       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.AKA ENERGY GROUP LLC]                        |  0.075 | 0.022 |   3.354       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.ANADARKO DJ GAS PROCESSING LLC]              | -0     | 0     |  -0.01        | 0.992     |
| H1_LPM_operator_FE | C(operator)[T.ANADARKO WATTENBERG OIL COMPLEX LLC]         |  0.094 | 0.025 |   3.831       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.ANSCHUTZ EXPLORATION CORP]                   | -0.04  | 0.18  |  -0.221       | 0.825     |
| H1_LPM_operator_FE | C(operator)[T.BARGATH LLC]                                 |  0.22  | 0.174 |   1.266       | 0.205     |
| H1_LPM_operator_FE | C(operator)[T.BARRETT CORPORATION* BILL]                   |  0.559 | 0.049 |  11.344       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.BARRETT RESOURCES CORP]                      | -0     | 0     |  -0.043       | 0.966     |
| H1_LPM_operator_FE | C(operator)[T.BAYLESS PRODUCER, LLC* ROBERT L]             | -0.033 | 0.186 |  -0.177       | 0.859     |
| H1_LPM_operator_FE | C(operator)[T.BAYSWATER EXPLORATION & PRODUCTION LLC]      |  0.229 | 0.014 |  16.555       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.BAYSWATER EXPLORATION AND PRODUCTION LLC]    |  0.489 | 0.044 |  11.211       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.BERRY PETROLEUM COMPANY LLC]                 |  0.012 | 0.176 |   0.067       | 0.947     |
| H1_LPM_operator_FE | C(operator)[T.BISON IV OPERATING LLC]                      |  0.133 | 0.031 |   4.359       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.BISON OIL & GAS II LLC]                      |  0.174 | 0.04  |   4.368       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.BLACK HILLS PLATEAU PRODUCTION LLC]          |  0.055 | 0.18  |   0.307       | 0.759     |
| H1_LPM_operator_FE | C(operator)[T.BLUE CHIP OIL INC]                           |  1.005 | 0.033 |  30.722       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.BNN WESTERN LLC]                             |  0.231 | 0.055 |   4.221       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.BONANZA CREEK ENERGY OPERATING COMPANY LLC]  |  0.289 | 0.037 |   7.854       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.CAERUS PICEANCE LLC]                         |  0.062 | 0.173 |   0.355       | 0.722     |
| H1_LPM_operator_FE | C(operator)[T.CAPTIVA ENERGY PARTNERS LLC]                 |  0.24  | 0.057 |   4.198       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.CARRIZO NIOBRARA LLC]                        |  0.24  | 0.057 |   4.198       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.CCRP OPERATING INC]                          |  0.24  | 0.057 |   4.198       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.CHACO ENERGY COMPANY]                        |  1.133 | 0.031 |  37.14        | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.CHEVRON PIPELINE COMPANY]                    | -0.033 | 0.186 |  -0.177       | 0.859     |
| H1_LPM_operator_FE | C(operator)[T.CHEVRON PRODUCTION COMPANY]                  | -0.033 | 0.186 |  -0.177       | 0.859     |
| H1_LPM_operator_FE | C(operator)[T.CHEVRON USA INC]                             |  0.028 | 0.184 |   0.151       | 0.880     |
| H1_LPM_operator_FE | C(operator)[T.CIVITAS NORTH LLC]                           |  0.36  | 0.031 |  11.809       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.COACHMAN ENERGY OPERATING COMPANY LLC]       | -0.07  | 0.174 |  -0.405       | 0.686     |
| H1_LPM_operator_FE | C(operator)[T.COLORADO OIL & GAS CONSERVATION COMMISSION]  |  0.483 | 0.093 |   5.186       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.COMPLETE ENERGY SERVICES INC]                |  0.107 | 0.032 |   3.354       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.CONFLUENCE DJ LLC]                           |  0.107 | 0.032 |   3.354       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.CRESTONE PEAK RESOURCES OPERATING LLC]       |  0.525 | 0.011 |  46.242       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.CUB CREEK ENERGY]                            |  0.086 | 0.02  |   4.198       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.CUB CREEK ENERGY LLC]                        |  0.106 | 0.024 |   4.359       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.DAN A HUGHES COMPANY LP]                     |  0.24  | 0.057 |   4.198       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.DCP MIDSTREAM LP]                            |  0.291 | 0.035 |   8.294       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.DCP OPERATING COMPANY LP]                    |  0.281 | 0.014 |  20.006       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.DIAMOND OPERATING INC]                       |  0.133 | 0.031 |   4.359       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.EDGE ENERGY II LLC]                          |  0.333 | 0.019 |  17.471       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.ENCANA OIL & GAS (USA) INC]                  |  0.109 | 0.146 |   0.744       | 0.457     |
| H1_LPM_operator_FE | C(operator)[T.ENERPLUS RESOURCES (USA) CORPORATION]        |  0.092 | 0.028 |   3.354       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.EOG RESOURCES INC]                           |  0.233 | 0.055 |   4.214       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.EWS 13 DJ BASIN LLC]                         |  1     | 0     |   9.08215e+12 | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.EWS 4 DJ BASIN LLC]                          |  0.107 | 0.032 |   3.354       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.EXPEDITION WATER SOLUTIONS COLORADO LLC]     |  0.107 | 0.032 |   3.354       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.EXTRACTION OIL & GAS INC]                    |  0.392 | 0.014 |  27.512       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.EXTRACTION OIL & GAS LLC]                    |  0.441 | 0.034 |  12.857       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.FIFTH CREEK ENERGY OPERATING COMPANY LLC]    |  0.24  | 0.057 |   4.198       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.FOUNDATION ENERGY MANAGEMENT LLC]            |  0.274 | 0.056 |   4.919       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.FRITZLER RESOURCES INC]                      |  0.133 | 0.031 |   4.359       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.FUNDARE RESOURCES OPERATING COMPANY LLC]     |  0.215 | 0.031 |   7.035       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.GADECO LLC]                                  |  1.24  | 0.057 |  21.717       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.GENESIS GAS & OIL COLORADO LLC]              | -0.14  | 0.18  |  -0.776       | 0.437     |
| H1_LPM_operator_FE | C(operator)[T.GRAND RIVER GATHERING LLC]                   | -0.14  | 0.171 |  -0.818       | 0.413     |
| H1_LPM_operator_FE | C(operator)[T.GREAT WESTERN OPERATING COMPANY LLC]         |  0.401 | 0.023 |  17.458       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.GRIZZLY OPERATING LLC]                       | -0.162 | 0.171 |  -0.945       | 0.344     |
| H1_LPM_operator_FE | C(operator)[T.GRYNBERG* JACK DBA GRYNBERG PETROLEUM CO]    |  1.24  | 0.057 |  21.717       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.HIGHPOINT ENERGY LLC]                        |  0.107 | 0.032 |   3.354       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.HIGHPOINT OPERATING CORPORATION]             |  0.243 | 0.033 |   7.317       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.HRM RESOURCES II LLC]                        |  0.107 | 0.032 |   3.354       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.HUNTER RIDGE ENERGY SERVICES LLC]            | -0.007 | 0.178 |  -0.039       | 0.969     |
| H1_LPM_operator_FE | C(operator)[T.HYNDREX RESOURCES]                           |  0.107 | 0.032 |   3.354       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.INDUSTRIAL GAS SERVICES INC]                 |  1.133 | 0.031 |  37.14        | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.K P KAUFFMAN COMPANY INC]                    |  0.447 | 0.038 |  11.783       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.KERR MCGEE GATHERING LLC]                    |  0.29  | 0.018 |  16.187       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.KERR MCGEE OIL & GAS ONSHORE LP]             |  0.722 | 0.013 |  57.679       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.KOCH EXPLORATION COMPANY LLC]                |  0.967 | 0.186 |   5.186       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.KOCH EXPLORATION COMPANY, LLC]               |  0.467 | 0.186 |   2.504       | 0.012     |
| H1_LPM_operator_FE | C(operator)[T.KP KAUFFMAN COMPANY INC]                     |  0.179 | 0.013 |  13.836       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.KT RESOURCES LLC]                            | -0.14  | 0.18  |  -0.776       | 0.437     |
| H1_LPM_operator_FE | C(operator)[T.LARAMIE ENERGY LLC]                          |  0.056 | 0.176 |   0.319       | 0.749     |
| H1_LPM_operator_FE | C(operator)[T.LASSO OIL & GAS LLC]                         | -0.14  | 0.18  |  -0.776       | 0.437     |
| H1_LPM_operator_FE | C(operator)[T.LINN OPERATING INC]                          |  0.055 | 0.18  |   0.307       | 0.759     |
| H1_LPM_operator_FE | C(operator)[T.LINN OPERATING LLC]                          |  0.055 | 0.18  |   0.307       | 0.759     |
| H1_LPM_operator_FE | C(operator)[T.LONGS PEAK RESOURCES LLC]                    |  0.158 | 0.036 |   4.39        | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.MACHII-ROSS PETROLEUM CO]                    |  1.107 | 0.032 |  34.805       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.MAGPIE OPERATING INC]                        |  1.133 | 0.031 |  37.14        | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.MARALEX RESOURCES, INC]                      |  0.055 | 0.18  |   0.307       | 0.759     |
| H1_LPM_operator_FE | C(operator)[T.MARATHON OIL COMPANY]                        |  0.055 | 0.18  |   0.307       | 0.759     |
| H1_LPM_operator_FE | C(operator)[T.MARKUS PRODUCTION, INC]                      |  1.133 | 0.031 |  37.14        | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.MDS ENERGY DEVELOPMENT LLC]                  |  0.133 | 0.031 |   4.359       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.MERRION OIL & GAS CORP]                      | -0.033 | 0.186 |  -0.177       | 0.859     |
| H1_LPM_operator_FE | C(operator)[T.MONAHAN GAS & OIL INC]                       |  0.107 | 0.032 |   3.354       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.MUSTANG RESOURCES LLC]                       |  0.358 | 0.174 |   2.062       | 0.039     |
| H1_LPM_operator_FE | C(operator)[T.NGL WATER SOLUTIONS DJ LLC]                  |  0.147 | 0.035 |   4.177       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.NICKEL ROAD OPERATING LLC]                   |  0.014 | 0.004 |   3.354       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.NOBLE ENERGY INC]                            |  0.851 | 0.017 |  48.699       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.NOBLE MIDSTREAM SERVICES LLC]                |  0.099 | 0.023 |   4.232       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.NORTHSTAR GAS COMPANY INC]                   | -0.033 | 0.186 |  -0.177       | 0.859     |
| H1_LPM_operator_FE | C(operator)[T.O'BRIEN ENERGY RESOURCES CORP]               |  0.107 | 0.032 |   3.354       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.OXY USA INC]                                 |  0.055 | 0.18  |   0.307       | 0.759     |
| H1_LPM_operator_FE | C(operator)[T.OXY USA WTP LP]                              |  0.055 | 0.18  |   0.307       | 0.759     |
| H1_LPM_operator_FE | C(operator)[T.PAINTED PEGASUS PETROLEUM LLC]               |  1.007 | 0.033 |  30.847       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.PDC ENERGY INC]                              |  0.68  | 0.016 |  43.484       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.PETERSON ENERGY OPERATING INC]               |  1.076 | 0.022 |  48.034       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.PETRO MEX RESOURCES]                         |  0.234 | 0.173 |   1.355       | 0.175     |
| H1_LPM_operator_FE | C(operator)[T.PETRO OPERATING COMPANY LLC]                 |  0.481 | 0.008 |  56.808       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.PETROSHARE CORPORATION]                      |  1.107 | 0.032 |  34.805       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.PLUG NICKEL OIL COMPANY INC]                 | -0.033 | 0.186 |  -0.177       | 0.859     |
| H1_LPM_operator_FE | C(operator)[T.PRAIRIE OPERATING CO LLC]                    | -0     | 0     |  -0.097       | 0.922     |
| H1_LPM_operator_FE | C(operator)[T.PROVIDENCE OPERATING LLC DBA POCO OPERATING] | -0     | 0     |  -0.067       | 0.947     |
| H1_LPM_operator_FE | C(operator)[T.RED HAWK PETROLEUM LLC]                      |  0.167 | 0.038 |   4.38        | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.RED ROCK GATHERING COMPANY LLC]              |  0.202 | 0.183 |   1.104       | 0.270     |
| H1_LPM_operator_FE | C(operator)[T.REP PROCESSING LLC]                          |  0.133 | 0.031 |   4.359       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.RIO MESA RESOURCES INC]                      | -0.14  | 0.18  |  -0.776       | 0.437     |
| H1_LPM_operator_FE | C(operator)[T.ROBERT L BAYLESS PRODUCER LLC]               | -0.14  | 0.18  |  -0.776       | 0.437     |
| H1_LPM_operator_FE | C(operator)[T.ROCKY MOUNTAIN MIDSTREAM LLC]                |  0.053 | 0.016 |   3.354       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.ROCKY MOUNTAIN NATURAL GAS LLC]              | -0.033 | 0.186 |  -0.177       | 0.859     |
| H1_LPM_operator_FE | C(operator)[T.RWL ENTERPRISES]                             |  1.107 | 0.032 |  34.805       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.SAMSON RESOURCES COMPANY]                    |  0.967 | 0.186 |   5.186       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.SCHNEIDER ENERGY SERVICES INC]               |  1.133 | 0.031 |  37.14        | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.SCOUT ENERGY MANAGEMENT LLC]                 | -0.09  | 0.18  |  -0.498       | 0.618     |
| H1_LPM_operator_FE | C(operator)[T.SMITH ENERGY CORP]                           |  1.085 | 0.019 |  55.872       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.SMITH OIL PROPERTIES INC]                    |  1.107 | 0.032 |  34.805       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.SRC ENERGY INC]                              |  0.691 | 0.036 |  19.162       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.SUMMIT DJ-S LLC]                             |  0.133 | 0.031 |   4.359       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.SUMMIT MIDSTREAM NIOBRARA LLC]               |  0.24  | 0.057 |   4.198       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.SUMMIT MIDSTREAM PARTNERS LLC]               | -0.126 | 0.171 |  -0.734       | 0.463     |
| H1_LPM_operator_FE | C(operator)[T.SYNERGY RESOURCES CORPORATION]               |  0.831 | 0.036 |  23.265       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.TALLGRASS WATER WESTERN LLC]                 |  0.133 | 0.031 |   4.359       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.TAPROOT ROCKIES MIDSTREAM LLC]               |  0.133 | 0.031 |   4.359       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.TEP ROCKY MOUNTAIN LLC]                      |  0.003 | 0.176 |   0.015       | 0.988     |
| H1_LPM_operator_FE | C(operator)[T.TEXAS TEA OF COLORADO LLC DBA TEXAS TEA LLC] |  1     | 0     |   9.04194e+12 | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.TINDALL OPERATING COMPANY]                   |  1.133 | 0.031 |  37.14        | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.TOP OPERATING COMPANY]                       |  1.022 | 0.005 | 201.045       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.UPLAND EXPLORATION LLC]                      |  0.133 | 0.031 |   4.359       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.URSA OPERATING COMPANY LLC]                  |  0.196 | 0.179 |   1.099       | 0.272     |
| H1_LPM_operator_FE | C(operator)[T.UTAH GAS OP LTD DBA UTAH GAS CORP]           |  0.445 | 0.18  |   2.466       | 0.014     |
| H1_LPM_operator_FE | C(operator)[T.VANGUARD OPERATING LLC]                      | -0.014 | 0.159 |  -0.085       | 0.932     |
| H1_LPM_operator_FE | C(operator)[T.VERDAD OIL & GAS CORPORATION]                |  0.107 | 0.032 |   3.354       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.VERDAD RESOURCES LLC]                        |  0.21  | 0.026 |   8.11        | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.VISION ENERGY LLC]                           | -0.177 | 0.171 |  -1.035       | 0.301     |
| H1_LPM_operator_FE | C(operator)[T.WARD PETROLEUM CORPORATION]                  |  0.173 | 0.044 |   3.97        | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.WEXPRO COMPANY]                              |  0.967 | 0.186 |   5.186       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.WHITING OIL & GAS CORPORATION]               |  0.313 | 0.053 |   5.922       | <0.001    |
| H1_LPM_operator_FE | C(operator)[T.WINDSOR ENERGY GROUP LLC]                    | -0.033 | 0.186 |  -0.177       | 0.859     |
| H1_LPM_operator_FE | C(operator)[T.WOODARD* SANDRA K]                           | -0.033 | 0.186 |  -0.177       | 0.859     |
| H1_LPM_operator_FE | C(operator)[T.WPX ENERGY ROCKY MOUNTAIN LLC]               |  0.18  | 0.177 |   1.017       | 0.309     |
| H1_LPM_operator_FE | C(operator)[T.XTO ENERGY INC]                              |  0     | 0.185 |   0.002       | 0.998     |
| H1_LPM_operator_FE | post                                                       |  0.107 | 0.032 |   3.354       | <0.001    |

Plots saved:

- `/home/dadams/Repos/colorado_redux/analysis_postgis/step2_model_outputs/h1_pct_historical_monthly.png`
- `/home/dadams/Repos/colorado_redux/analysis_postgis/step2_model_outputs/h1_pct_historical_monthly_top3counties.png`



## H2: Reporting timeliness (regulated entities)

### A) Continuous DV (primary)

OLS formula: `log1p_delay ~ post + historical + post:historical + C(county_norm) + C(rurality_3) + C(operator)`

Cluster by operator (main):

| model                         | term                                                       |   coef |    se |             t | p_value   |
|:------------------------------|:-----------------------------------------------------------|-------:|------:|--------------:|:----------|
| H2_OLS_log1p_cluster_operator | Intercept                                                  |  1.59  | 0.362 |   4.386       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(county_norm)[T.RIO BLANCO]                               |  0.024 | 0.037 |   0.659       | 0.510     |
| H2_OLS_log1p_cluster_operator | C(county_norm)[T.WELD]                                     | -0.6   | 0.366 |  -1.637       | 0.102     |
| H2_OLS_log1p_cluster_operator | C(rurality_3)[T.Suburban]                                  | -0.039 | 0.033 |  -1.199       | 0.230     |
| H2_OLS_log1p_cluster_operator | C(rurality_3)[T.Urban]                                     | -0.077 | 0.024 |  -3.195       | 0.001     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.31 OPERATING]                                |  0.803 | 0.378 |   2.127       | 0.033     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.4-H OPERATING CORPORATION]                   |  0.99  | 0.102 |   9.664       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.8 NORTH LLC]                                 | -0.503 | 0.08  |  -6.315       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.AKA ENERGY GROUP LLC]                        |  0.037 | 0.042 |   0.879       | 0.380     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.ANADARKO DJ GAS PROCESSING LLC]              |  0.405 | 0     |   1.11486e+12 | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.ANADARKO WATTENBERG OIL COMPLEX LLC]         | -0.052 | 0.038 |  -1.344       | 0.179     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.ANSCHUTZ EXPLORATION CORP]                   | -0.517 | 0.377 |  -1.374       | 0.170     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.BARGATH LLC]                                 | -1.021 | 0.362 |  -2.819       | 0.005     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.BARRETT CORPORATION* BILL]                   |  0.041 | 0.071 |   0.577       | 0.564     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.BARRETT RESOURCES CORP]                      |  0     | 0     |   0.05        | 0.960     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.BAYLESS PRODUCER, LLC* ROBERT L]             | -0.921 | 0.38  |  -2.426       | 0.015     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.BAYSWATER EXPLORATION & PRODUCTION LLC]      |  0.259 | 0.034 |   7.705       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.BAYSWATER EXPLORATION AND PRODUCTION LLC]    | -0.216 | 0.067 |  -3.213       | 0.001     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.BERRY PETROLEUM COMPANY LLC]                 | -0.45  | 0.362 |  -1.244       | 0.214     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.BISON IV OPERATING LLC]                      |  0.328 | 0.024 |  13.584       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.BISON OIL & GAS II LLC]                      |  0.004 | 0.035 |   0.128       | 0.898     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.BLACK HILLS PLATEAU PRODUCTION LLC]          | -1.59  | 0.362 |  -4.386       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.BLUE CHIP OIL INC]                           |  1.599 | 0.095 |  16.786       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.BNN WESTERN LLC]                             | -0.171 | 0.063 |  -2.734       | 0.006     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.BONANZA CREEK ENERGY OPERATING COMPANY LLC]  | -0.37  | 0.043 |  -8.691       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.CAERUS PICEANCE LLC]                         | -0.856 | 0.364 |  -2.352       | 0.019     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.CAPTIVA ENERGY PARTNERS LLC]                 |  0.396 | 0.067 |   5.898       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.CARRIZO NIOBRARA LLC]                        |  0.325 | 0.067 |   4.833       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.CCRP OPERATING INC]                          | -0.297 | 0.067 |  -4.42        | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.CHACO ENERGY COMPANY]                        |  3.941 | 0.144 |  27.453       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.CHEVRON PIPELINE COMPANY]                    | -0.228 | 0.38  |  -0.6         | 0.549     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.CHEVRON PRODUCTION COMPANY]                  | -1.199 | 0.38  |  -3.159       | 0.002     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.CHEVRON USA INC]                             | -0.555 | 0.378 |  -1.471       | 0.141     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.CIVITAS NORTH LLC]                           | -0.014 | 0.044 |  -0.316       | 0.752     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.COACHMAN ENERGY OPERATING COMPANY LLC]       |  0.721 | 0.367 |   1.965       | 0.049     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.COLORADO OIL & GAS CONSERVATION COMMISSION]  | -0.63  | 0.199 |  -3.166       | 0.002     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.COMPLETE ENERGY SERVICES INC]                |  0.186 | 0.06  |   3.082       | 0.002     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.CONFLUENCE DJ LLC]                           | -0.22  | 0.06  |  -3.652       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.CRESTONE PEAK RESOURCES OPERATING LLC]       | -0.222 | 0.067 |  -3.324       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.CUB CREEK ENERGY]                            | -0.354 | 0.024 | -14.737       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.CUB CREEK ENERGY LLC]                        |  0.158 | 0.019 |   8.195       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.DAN A HUGHES COMPANY LP]                     |  0.109 | 0.067 |   1.616       | 0.106     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.DCP MIDSTREAM LP]                            | -0.08  | 0.062 |  -1.281       | 0.200     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.DCP OPERATING COMPANY LP]                    | -0.039 | 0.035 |  -1.102       | 0.270     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.DIAMOND OPERATING INC]                       |  0.328 | 0.024 |  13.62        | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.EDGE ENERGY II LLC]                          |  0.821 | 0.041 |  20.128       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.ENCANA OIL & GAS (USA) INC]                  | -0.673 | 0.298 |  -2.257       | 0.024     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.ENERPLUS RESOURCES (USA) CORPORATION]        | -0.057 | 0.052 |  -1.092       | 0.275     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.EOG RESOURCES INC]                           | -0.268 | 0.064 |  -4.197       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.EWS 13 DJ BASIN LLC]                         | -0.051 | 0.134 |  -0.38        | 0.704     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.EWS 4 DJ BASIN LLC]                          |  1.284 | 0.06  |  21.329       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.EXPEDITION WATER SOLUTIONS COLORADO LLC]     | -0.913 | 0.06  | -15.164       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.EXTRACTION OIL & GAS INC]                    | -0.231 | 0.043 |  -5.328       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.EXTRACTION OIL & GAS LLC]                    | -0.134 | 0.067 |  -1.998       | 0.046     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.FIFTH CREEK ENERGY OPERATING COMPANY LLC]    | -0.096 | 0.067 |  -1.435       | 0.151     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.FOUNDATION ENERGY MANAGEMENT LLC]            |  0.052 | 0.081 |   0.643       | 0.520     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.FRITZLER RESOURCES INC]                      |  3.435 | 0.024 | 142.426       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.FUNDARE RESOURCES OPERATING COMPANY LLC]     | -0.043 | 0.029 |  -1.455       | 0.146     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.GADECO LLC]                                  |  0.675 | 0.113 |   5.989       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.GENESIS GAS & OIL COLORADO LLC]              |  1.346 | 0.378 |   3.566       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.GRAND RIVER GATHERING LLC]                   | -0.748 | 0.364 |  -2.054       | 0.040     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.GREAT WESTERN OPERATING COMPANY LLC]         |  0.026 | 0.054 |   0.491       | 0.623     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.GRIZZLY OPERATING LLC]                       | -0.372 | 0.365 |  -1.02        | 0.308     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.GRYNBERG* JACK DBA GRYNBERG PETROLEUM CO]    |  0.312 | 0.113 |   2.772       | 0.006     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.HIGHPOINT ENERGY LLC]                        | -0.913 | 0.06  | -15.164       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.HIGHPOINT OPERATING CORPORATION]             | -0.357 | 0.036 |  -9.958       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.HRM RESOURCES II LLC]                        | -0.913 | 0.06  | -15.164       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.HUNTER RIDGE ENERGY SERVICES LLC]            | -0.17  | 0.365 |  -0.464       | 0.642     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.HYNDREX RESOURCES]                           |  0.186 | 0.06  |   3.082       | 0.002     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.INDUSTRIAL GAS SERVICES INC]                 |  0.788 | 0.144 |   5.491       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.K P KAUFFMAN COMPANY INC]                    | -0.289 | 0.069 |  -4.208       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.KERR MCGEE GATHERING LLC]                    | -0.119 | 0.039 |  -3.06        | 0.002     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.KERR MCGEE OIL & GAS ONSHORE LP]             | -0.449 | 0.087 |  -5.176       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.KOCH EXPLORATION COMPANY LLC]                |  1.287 | 0.387 |   3.328       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.KOCH EXPLORATION COMPANY, LLC]               |  0.641 | 0.38  |   1.686       | 0.092     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.KP KAUFFMAN COMPANY INC]                     |  0.199 | 0.025 |   7.927       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.KT RESOURCES LLC]                            | -0.701 | 0.378 |  -1.857       | 0.063     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.LARAMIE ENERGY LLC]                          | -0.508 | 0.362 |  -1.402       | 0.161     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.LASSO OIL & GAS LLC]                         |  1.55  | 0.378 |   4.106       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.LINN OPERATING INC]                          | -0.516 | 0.362 |  -1.424       | 0.154     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.LINN OPERATING LLC]                          | -1.243 | 0.362 |  -3.43        | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.LONGS PEAK RESOURCES LLC]                    | -0.234 | 0.029 |  -8.062       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.MACHII-ROSS PETROLEUM CO]                    |  1.816 | 0.102 |  17.736       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.MAGPIE OPERATING INC]                        |  4.925 | 0.144 |  34.307       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.MARALEX RESOURCES, INC]                      | -0.897 | 0.362 |  -2.474       | 0.013     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.MARATHON OIL COMPANY]                        | -1.041 | 0.362 |  -2.871       | 0.004     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.MARKUS PRODUCTION, INC]                      | -0.821 | 0.144 |  -5.72        | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.MDS ENERGY DEVELOPMENT LLC]                  | -0.77  | 0.024 | -31.939       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.MERRION OIL & GAS CORP]                      |  0.784 | 0.38  |   2.065       | 0.039     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.MONAHAN GAS & OIL INC]                       |  1.86  | 0.06  |  30.885       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.MUSTANG RESOURCES LLC]                       | -1.098 | 0.368 |  -2.988       | 0.003     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.NGL WATER SOLUTIONS DJ LLC]                  | -0.235 | 0.042 |  -5.542       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.NICKEL ROAD OPERATING LLC]                   | -0.049 | 0.008 |  -6.185       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.NOBLE ENERGY INC]                            | -0.237 | 0.099 |  -2.4         | 0.016     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.NOBLE MIDSTREAM SERVICES LLC]                |  0.091 | 0.026 |   3.425       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.NORTHSTAR GAS COMPANY INC]                   |  0.332 | 0.38  |   0.875       | 0.382     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.O'BRIEN ENERGY RESOURCES CORP]               | -0.913 | 0.06  | -15.164       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.OXY USA INC]                                 |  0.02  | 0.362 |   0.054       | 0.957     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.OXY USA WTP LP]                              | -0.893 | 0.362 |  -2.464       | 0.014     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.PAINTED PEGASUS PETROLEUM LLC]               |  1.964 | 0.134 |  14.632       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.PDC ENERGY INC]                              | -0.092 | 0.081 |  -1.129       | 0.259     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.PETERSON ENERGY OPERATING INC]               |  0.379 | 0.11  |   3.458       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.PETRO MEX RESOURCES]                         |  0.965 | 0.363 |   2.66        | 0.008     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.PETRO OPERATING COMPANY LLC]                 |  0.852 | 0.062 |  13.719       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.PETROSHARE CORPORATION]                      |  0.43  | 0.102 |   4.2         | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.PLUG NICKEL OIL COMPANY INC]                 | -0.515 | 0.38  |  -1.358       | 0.174     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.PRAIRIE OPERATING CO LLC]                    |  0.439 | 0     |   1.18109e+12 | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.PROVIDENCE OPERATING LLC DBA POCO OPERATING] | -0.173 | 0     |  -4.64599e+11 | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.RED HAWK PETROLEUM LLC]                      |  0.197 | 0.032 |   6.106       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.RED ROCK GATHERING COMPANY LLC]              | -0.781 | 0.372 |  -2.098       | 0.036     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.REP PROCESSING LLC]                          |  0.616 | 0.024 |  25.55        | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.RIO MESA RESOURCES INC]                      |  0.685 | 0.378 |   1.815       | 0.069     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.ROBERT L BAYLESS PRODUCER LLC]               | -0.008 | 0.378 |  -0.021       | 0.983     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.ROCKY MOUNTAIN MIDSTREAM LLC]                |  0.322 | 0.03  |  10.691       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.ROCKY MOUNTAIN NATURAL GAS LLC]              |  1.025 | 0.38  |   2.701       | 0.007     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.RWL ENTERPRISES]                             |  1.371 | 0.102 |  13.391       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.SAMSON RESOURCES COMPANY]                    |  0.135 | 0.387 |   0.348       | 0.728     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.SCHNEIDER ENERGY SERVICES INC]               | -0.475 | 0.144 |  -3.306       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.SCOUT ENERGY MANAGEMENT LLC]                 | -0.699 | 0.377 |  -1.855       | 0.064     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.SMITH ENERGY CORP]                           |  0.65  | 0.14  |   4.651       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.SMITH OIL PROPERTIES INC]                    |  2.627 | 0.102 |  25.655       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.SRC ENERGY INC]                              | -0.185 | 0.075 |  -2.454       | 0.014     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.SUMMIT DJ-S LLC]                             |  4.91  | 0.024 | 203.613       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.SUMMIT MIDSTREAM NIOBRARA LLC]               | -0.297 | 0.067 |  -4.42        | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.SUMMIT MIDSTREAM PARTNERS LLC]               | -0.616 | 0.364 |  -1.694       | 0.090     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.SYNERGY RESOURCES CORPORATION]               |  0.198 | 0.084 |   2.37        | 0.018     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.TALLGRASS WATER WESTERN LLC]                 | -0.226 | 0.024 |  -9.354       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.TAPROOT ROCKIES MIDSTREAM LLC]               | -0.324 | 0.024 | -13.415       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.TEP ROCKY MOUNTAIN LLC]                      | -0.74  | 0.366 |  -2.021       | 0.043     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.TEXAS TEA OF COLORADO LLC DBA TEXAS TEA LLC] | -0.051 | 0.134 |  -0.38        | 0.704     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.TINDALL OPERATING COMPANY]                   | -0.128 | 0.144 |  -0.892       | 0.372     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.TOP OPERATING COMPANY]                       |  0.312 | 0.136 |   2.301       | 0.021     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.UPLAND EXPLORATION LLC]                      |  2.488 | 0.024 | 103.172       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.URSA OPERATING COMPANY LLC]                  | -0.594 | 0.369 |  -1.611       | 0.107     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.UTAH GAS OP LTD DBA UTAH GAS CORP]           |  0.26  | 0.377 |   0.69        | 0.490     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.VANGUARD OPERATING LLC]                      | -0.439 | 0.335 |  -1.311       | 0.190     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.VERDAD OIL & GAS CORPORATION]                | -0.22  | 0.06  |  -3.652       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.VERDAD RESOURCES LLC]                        | -0.283 | 0.028 | -10.082       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.VISION ENERGY LLC]                           |  0.867 | 0.365 |   2.375       | 0.018     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.WARD PETROLEUM CORPORATION]                  | -0.402 | 0.063 |  -6.421       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.WEXPRO COMPANY]                              |  0.645 | 0.387 |   1.668       | 0.095     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.WHITING OIL & GAS CORPORATION]               | -0.426 | 0.061 |  -6.976       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.WINDSOR ENERGY GROUP LLC]                    |  2.356 | 0.38  |   6.209       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.WOODARD* SANDRA K]                           | -0.921 | 0.38  |  -2.426       | 0.015     |
| H2_OLS_log1p_cluster_operator | C(operator)[T.WPX ENERGY ROCKY MOUNTAIN LLC]               | -1.329 | 0.364 |  -3.653       | <0.001    |
| H2_OLS_log1p_cluster_operator | C(operator)[T.XTO ENERGY INC]                              | -0.722 | 0.378 |  -1.91        | 0.056     |
| H2_OLS_log1p_cluster_operator | post                                                       | -0.22  | 0.06  |  -3.652       | <0.001    |
| H2_OLS_log1p_cluster_operator | historical                                                 |  0.043 | 0.091 |   0.473       | 0.636     |
| H2_OLS_log1p_cluster_operator | post:historical                                            |  0.008 | 0.081 |   0.097       | 0.923     |

Cluster by county (robustness):

| model                       | term                                                       |   coef |    se |             t | p_value   |
|:----------------------------|:-----------------------------------------------------------|-------:|------:|--------------:|:----------|
| H2_OLS_log1p_cluster_county | Intercept                                                  |  1.59  | 0.117 |  13.578       | <0.001    |
| H2_OLS_log1p_cluster_county | C(county_norm)[T.RIO BLANCO]                               |  0.024 | 0.039 |   0.616       | 0.538     |
| H2_OLS_log1p_cluster_county | C(county_norm)[T.WELD]                                     | -0.6   | 0.116 |  -5.151       | <0.001    |
| H2_OLS_log1p_cluster_county | C(rurality_3)[T.Suburban]                                  | -0.039 | 0.021 |  -1.889       | 0.059     |
| H2_OLS_log1p_cluster_county | C(rurality_3)[T.Urban]                                     | -0.077 | 0.013 |  -5.734       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.31 OPERATING]                                |  0.803 | 0.119 |   6.776       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.4-H OPERATING CORPORATION]                   |  0.99  | 0.017 |  57.261       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.8 NORTH LLC]                                 | -0.503 | 0.062 |  -8.156       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.AKA ENERGY GROUP LLC]                        |  0.037 | 0.231 |   0.16        | 0.873     |
| H2_OLS_log1p_cluster_county | C(operator)[T.ANADARKO DJ GAS PROCESSING LLC]              |  0.405 | 0     |   1.55009e+13 | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.ANADARKO WATTENBERG OIL COMPLEX LLC]         | -0.052 | 0.146 |  -0.355       | 0.722     |
| H2_OLS_log1p_cluster_county | C(operator)[T.ANSCHUTZ EXPLORATION CORP]                   | -0.517 | 0.186 |  -2.776       | 0.006     |
| H2_OLS_log1p_cluster_county | C(operator)[T.BARGATH LLC]                                 | -1.021 | 0.176 |  -5.81        | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.BARRETT CORPORATION* BILL]                   |  0.041 | 0.072 |   0.566       | 0.572     |
| H2_OLS_log1p_cluster_county | C(operator)[T.BARRETT RESOURCES CORP]                      |  0     | 0     |   0.758       | 0.449     |
| H2_OLS_log1p_cluster_county | C(operator)[T.BAYLESS PRODUCER, LLC* ROBERT L]             | -0.921 | 0.119 |  -7.723       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.BAYSWATER EXPLORATION & PRODUCTION LLC]      |  0.259 | 0.076 |   3.413       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.BAYSWATER EXPLORATION AND PRODUCTION LLC]    | -0.216 | 0.054 |  -4.023       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.BERRY PETROLEUM COMPANY LLC]                 | -0.45  | 0.146 |  -3.073       | 0.002     |
| H2_OLS_log1p_cluster_county | C(operator)[T.BISON IV OPERATING LLC]                      |  0.328 | 0.14  |   2.348       | 0.019     |
| H2_OLS_log1p_cluster_county | C(operator)[T.BISON OIL & GAS II LLC]                      |  0.004 | 0.063 |   0.071       | 0.943     |
| H2_OLS_log1p_cluster_county | C(operator)[T.BLACK HILLS PLATEAU PRODUCTION LLC]          | -1.59  | 0.117 | -13.578       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.BLUE CHIP OIL INC]                           |  1.599 | 0.17  |   9.415       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.BNN WESTERN LLC]                             | -0.171 | 0.063 |  -2.734       | 0.006     |
| H2_OLS_log1p_cluster_county | C(operator)[T.BONANZA CREEK ENERGY OPERATING COMPANY LLC]  | -0.37  | 0.02  | -18.149       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.CAERUS PICEANCE LLC]                         | -0.856 | 0.117 |  -7.3         | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.CAPTIVA ENERGY PARTNERS LLC]                 |  0.396 | 0.019 |  20.888       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.CARRIZO NIOBRARA LLC]                        |  0.325 | 0.162 |   2.009       | 0.045     |
| H2_OLS_log1p_cluster_county | C(operator)[T.CCRP OPERATING INC]                          | -0.297 | 0.019 | -15.652       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.CHACO ENERGY COMPANY]                        |  3.941 | 0.023 | 172.556       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.CHEVRON PIPELINE COMPANY]                    | -0.228 | 0.119 |  -1.91        | 0.056     |
| H2_OLS_log1p_cluster_county | C(operator)[T.CHEVRON PRODUCTION COMPANY]                  | -1.199 | 0.139 |  -8.652       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.CHEVRON USA INC]                             | -0.555 | 0.123 |  -4.517       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.CIVITAS NORTH LLC]                           | -0.014 | 0.073 |  -0.192       | 0.848     |
| H2_OLS_log1p_cluster_county | C(operator)[T.COACHMAN ENERGY OPERATING COMPANY LLC]       |  0.721 | 0.572 |   1.261       | 0.207     |
| H2_OLS_log1p_cluster_county | C(operator)[T.COLORADO OIL & GAS CONSERVATION COMMISSION]  | -0.63  | 0.497 |  -1.267       | 0.205     |
| H2_OLS_log1p_cluster_county | C(operator)[T.COMPLETE ENERGY SERVICES INC]                |  0.186 | 0.013 |  14.306       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.CONFLUENCE DJ LLC]                           | -0.22  | 0.013 | -16.951       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.CRESTONE PEAK RESOURCES OPERATING LLC]       | -0.222 | 0.025 |  -8.874       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.CUB CREEK ENERGY]                            | -0.354 | 0.114 |  -3.092       | 0.002     |
| H2_OLS_log1p_cluster_county | C(operator)[T.CUB CREEK ENERGY LLC]                        |  0.158 | 0.194 |   0.816       | 0.414     |
| H2_OLS_log1p_cluster_county | C(operator)[T.DAN A HUGHES COMPANY LP]                     |  0.109 | 0.019 |   5.722       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.DCP MIDSTREAM LP]                            | -0.08  | 0.052 |  -1.523       | 0.128     |
| H2_OLS_log1p_cluster_county | C(operator)[T.DCP OPERATING COMPANY LP]                    | -0.039 | 0.037 |  -1.053       | 0.292     |
| H2_OLS_log1p_cluster_county | C(operator)[T.DIAMOND OPERATING INC]                       |  0.328 | 0.013 |  24.448       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.EDGE ENERGY II LLC]                          |  0.821 | 0.399 |   2.057       | 0.040     |
| H2_OLS_log1p_cluster_county | C(operator)[T.ENCANA OIL & GAS (USA) INC]                  | -0.673 | 0.114 |  -5.902       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.ENERPLUS RESOURCES (USA) CORPORATION]        | -0.057 | 0.099 |  -0.574       | 0.566     |
| H2_OLS_log1p_cluster_county | C(operator)[T.EOG RESOURCES INC]                           | -0.268 | 0.05  |  -5.392       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.EWS 13 DJ BASIN LLC]                         | -0.051 | 0.017 |  -2.99        | 0.003     |
| H2_OLS_log1p_cluster_county | C(operator)[T.EWS 4 DJ BASIN LLC]                          |  1.284 | 0.013 |  98.998       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.EXPEDITION WATER SOLUTIONS COLORADO LLC]     | -0.913 | 0.013 | -70.385       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.EXTRACTION OIL & GAS INC]                    | -0.231 | 0.037 |  -6.217       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.EXTRACTION OIL & GAS LLC]                    | -0.134 | 0.071 |  -1.905       | 0.057     |
| H2_OLS_log1p_cluster_county | C(operator)[T.FIFTH CREEK ENERGY OPERATING COMPANY LLC]    | -0.096 | 0.106 |  -0.908       | 0.364     |
| H2_OLS_log1p_cluster_county | C(operator)[T.FOUNDATION ENERGY MANAGEMENT LLC]            |  0.052 | 0.086 |   0.603       | 0.546     |
| H2_OLS_log1p_cluster_county | C(operator)[T.FRITZLER RESOURCES INC]                      |  3.435 | 0.013 | 255.657       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.FUNDARE RESOURCES OPERATING COMPANY LLC]     | -0.043 | 0.046 |  -0.921       | 0.357     |
| H2_OLS_log1p_cluster_county | C(operator)[T.GADECO LLC]                                  |  0.675 | 0.34  |   1.985       | 0.047     |
| H2_OLS_log1p_cluster_county | C(operator)[T.GENESIS GAS & OIL COLORADO LLC]              |  1.346 | 0.12  |  11.255       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.GRAND RIVER GATHERING LLC]                   | -0.748 | 0.129 |  -5.802       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.GREAT WESTERN OPERATING COMPANY LLC]         |  0.026 | 0.055 |   0.477       | 0.634     |
| H2_OLS_log1p_cluster_county | C(operator)[T.GRIZZLY OPERATING LLC]                       | -0.372 | 0.154 |  -2.407       | 0.016     |
| H2_OLS_log1p_cluster_county | C(operator)[T.GRYNBERG* JACK DBA GRYNBERG PETROLEUM CO]    |  0.312 | 0.238 |   1.313       | 0.189     |
| H2_OLS_log1p_cluster_county | C(operator)[T.HIGHPOINT ENERGY LLC]                        | -0.913 | 0.013 | -70.385       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.HIGHPOINT OPERATING CORPORATION]             | -0.357 | 0.022 | -16.486       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.HRM RESOURCES II LLC]                        | -0.913 | 0.013 | -70.385       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.HUNTER RIDGE ENERGY SERVICES LLC]            | -0.17  | 0.15  |  -1.129       | 0.259     |
| H2_OLS_log1p_cluster_county | C(operator)[T.HYNDREX RESOURCES]                           |  0.186 | 0.013 |  14.306       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.INDUSTRIAL GAS SERVICES INC]                 |  0.788 | 0.023 |  34.513       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.K P KAUFFMAN COMPANY INC]                    | -0.289 | 0.101 |  -2.854       | 0.004     |
| H2_OLS_log1p_cluster_county | C(operator)[T.KERR MCGEE GATHERING LLC]                    | -0.119 | 0.052 |  -2.287       | 0.022     |
| H2_OLS_log1p_cluster_county | C(operator)[T.KERR MCGEE OIL & GAS ONSHORE LP]             | -0.449 | 0.016 | -28.797       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.KOCH EXPLORATION COMPANY LLC]                |  1.287 | 0.121 |  10.659       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.KOCH EXPLORATION COMPANY, LLC]               |  0.641 | 0.258 |   2.482       | 0.013     |
| H2_OLS_log1p_cluster_county | C(operator)[T.KP KAUFFMAN COMPANY INC]                     |  0.199 | 0.036 |   5.482       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.KT RESOURCES LLC]                            | -0.701 | 0.119 |  -5.914       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.LARAMIE ENERGY LLC]                          | -0.508 | 0.127 |  -4           | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.LASSO OIL & GAS LLC]                         |  1.55  | 0.119 |  13.081       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.LINN OPERATING INC]                          | -0.516 | 0.246 |  -2.102       | 0.036     |
| H2_OLS_log1p_cluster_county | C(operator)[T.LINN OPERATING LLC]                          | -1.243 | 0.17  |  -7.325       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.LONGS PEAK RESOURCES LLC]                    | -0.234 | 0.05  |  -4.663       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.MACHII-ROSS PETROLEUM CO]                    |  1.816 | 0.017 | 105.09        | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.MAGPIE OPERATING INC]                        |  4.925 | 0.023 | 215.641       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.MARALEX RESOURCES, INC]                      | -0.897 | 0.117 |  -7.658       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.MARATHON OIL COMPANY]                        | -1.041 | 0.227 |  -4.579       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.MARKUS PRODUCTION, INC]                      | -0.821 | 0.023 | -35.956       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.MDS ENERGY DEVELOPMENT LLC]                  | -0.77  | 0.013 | -57.33        | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.MERRION OIL & GAS CORP]                      |  0.784 | 0.119 |   6.575       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.MONAHAN GAS & OIL INC]                       |  1.86  | 0.013 | 143.353       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.MUSTANG RESOURCES LLC]                       | -1.098 | 0.183 |  -6.008       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.NGL WATER SOLUTIONS DJ LLC]                  | -0.235 | 0.061 |  -3.849       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.NICKEL ROAD OPERATING LLC]                   | -0.049 | 0.046 |  -1.064       | 0.287     |
| H2_OLS_log1p_cluster_county | C(operator)[T.NOBLE ENERGY INC]                            | -0.237 | 0.016 | -14.57        | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.NOBLE MIDSTREAM SERVICES LLC]                |  0.091 | 0.07  |   1.298       | 0.194     |
| H2_OLS_log1p_cluster_county | C(operator)[T.NORTHSTAR GAS COMPANY INC]                   |  0.332 | 0.119 |   2.784       | 0.005     |
| H2_OLS_log1p_cluster_county | C(operator)[T.O'BRIEN ENERGY RESOURCES CORP]               | -0.913 | 0.013 | -70.385       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.OXY USA INC]                                 |  0.02  | 0.117 |   0.167       | 0.867     |
| H2_OLS_log1p_cluster_county | C(operator)[T.OXY USA WTP LP]                              | -0.893 | 0.136 |  -6.57        | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.PAINTED PEGASUS PETROLEUM LLC]               |  1.964 | 0.338 |   5.804       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.PDC ENERGY INC]                              | -0.092 | 0.019 |  -4.935       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.PETERSON ENERGY OPERATING INC]               |  0.379 | 0.284 |   1.332       | 0.183     |
| H2_OLS_log1p_cluster_county | C(operator)[T.PETRO MEX RESOURCES]                         |  0.965 | 0.129 |   7.477       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.PETRO OPERATING COMPANY LLC]                 |  0.852 | 0.39  |   2.184       | 0.029     |
| H2_OLS_log1p_cluster_county | C(operator)[T.PETROSHARE CORPORATION]                      |  0.43  | 0.017 |  24.884       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.PLUG NICKEL OIL COMPANY INC]                 | -0.515 | 0.119 |  -4.323       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.PRAIRIE OPERATING CO LLC]                    |  0.439 | 0.081 |   5.442       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.PROVIDENCE OPERATING LLC DBA POCO OPERATING] | -0.173 | 0.061 |  -2.82        | 0.005     |
| H2_OLS_log1p_cluster_county | C(operator)[T.RED HAWK PETROLEUM LLC]                      |  0.197 | 0.148 |   1.326       | 0.185     |
| H2_OLS_log1p_cluster_county | C(operator)[T.RED ROCK GATHERING COMPANY LLC]              | -0.781 | 0.191 |  -4.087       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.REP PROCESSING LLC]                          |  0.616 | 0.013 |  45.862       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.RIO MESA RESOURCES INC]                      |  0.685 | 0.119 |   5.783       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.ROBERT L BAYLESS PRODUCER LLC]               | -0.008 | 0.119 |  -0.066       | 0.947     |
| H2_OLS_log1p_cluster_county | C(operator)[T.ROCKY MOUNTAIN MIDSTREAM LLC]                |  0.322 | 0.084 |   3.831       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.ROCKY MOUNTAIN NATURAL GAS LLC]              |  1.025 | 0.119 |   8.598       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.RWL ENTERPRISES]                             |  1.371 | 0.222 |   6.186       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.SAMSON RESOURCES COMPANY]                    |  0.135 | 0.121 |   1.114       | 0.265     |
| H2_OLS_log1p_cluster_county | C(operator)[T.SCHNEIDER ENERGY SERVICES INC]               | -0.475 | 0.175 |  -2.708       | 0.007     |
| H2_OLS_log1p_cluster_county | C(operator)[T.SCOUT ENERGY MANAGEMENT LLC]                 | -0.699 | 0.127 |  -5.508       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.SMITH ENERGY CORP]                           |  0.65  | 0.247 |   2.635       | 0.008     |
| H2_OLS_log1p_cluster_county | C(operator)[T.SMITH OIL PROPERTIES INC]                    |  2.627 | 0.017 | 152.008       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.SRC ENERGY INC]                              | -0.185 | 0.082 |  -2.26        | 0.024     |
| H2_OLS_log1p_cluster_county | C(operator)[T.SUMMIT DJ-S LLC]                             |  4.91  | 0.013 | 365.488       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.SUMMIT MIDSTREAM NIOBRARA LLC]               | -0.297 | 0.019 | -15.652       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.SUMMIT MIDSTREAM PARTNERS LLC]               | -0.616 | 0.157 |  -3.932       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.SYNERGY RESOURCES CORPORATION]               |  0.198 | 0.098 |   2.02        | 0.043     |
| H2_OLS_log1p_cluster_county | C(operator)[T.TALLGRASS WATER WESTERN LLC]                 | -0.226 | 0.04  |  -5.582       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.TAPROOT ROCKIES MIDSTREAM LLC]               | -0.324 | 0.057 |  -5.628       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.TEP ROCKY MOUNTAIN LLC]                      | -0.74  | 0.118 |  -6.278       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.TEXAS TEA OF COLORADO LLC DBA TEXAS TEA LLC] | -0.051 | 0.017 |  -2.99        | 0.003     |
| H2_OLS_log1p_cluster_county | C(operator)[T.TINDALL OPERATING COMPANY]                   | -0.128 | 0.023 |  -5.606       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.TOP OPERATING COMPANY]                       |  0.312 | 0.092 |   3.411       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.UPLAND EXPLORATION LLC]                      |  2.488 | 0.013 | 185.195       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.URSA OPERATING COMPANY LLC]                  | -0.594 | 0.128 |  -4.633       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.UTAH GAS OP LTD DBA UTAH GAS CORP]           |  0.26  | 0.201 |   1.295       | 0.195     |
| H2_OLS_log1p_cluster_county | C(operator)[T.VANGUARD OPERATING LLC]                      | -0.439 | 0.136 |  -3.219       | 0.001     |
| H2_OLS_log1p_cluster_county | C(operator)[T.VERDAD OIL & GAS CORPORATION]                | -0.22  | 0.013 | -16.951       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.VERDAD RESOURCES LLC]                        | -0.283 | 0.046 |  -6.086       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.VISION ENERGY LLC]                           |  0.867 | 0.117 |   7.422       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.WARD PETROLEUM CORPORATION]                  | -0.402 | 0.182 |  -2.214       | 0.027     |
| H2_OLS_log1p_cluster_county | C(operator)[T.WEXPRO COMPANY]                              |  0.645 | 0.121 |   5.344       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.WHITING OIL & GAS CORPORATION]               | -0.426 | 0.031 | -13.693       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.WINDSOR ENERGY GROUP LLC]                    |  2.356 | 0.119 |  19.763       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.WOODARD* SANDRA K]                           | -0.921 | 0.119 |  -7.723       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.WPX ENERGY ROCKY MOUNTAIN LLC]               | -1.329 | 0.119 | -11.125       | <0.001    |
| H2_OLS_log1p_cluster_county | C(operator)[T.XTO ENERGY INC]                              | -0.722 | 0.125 |  -5.77        | <0.001    |
| H2_OLS_log1p_cluster_county | post                                                       | -0.22  | 0.013 | -16.951       | <0.001    |
| H2_OLS_log1p_cluster_county | historical                                                 |  0.043 | 0.017 |   2.595       | 0.009     |
| H2_OLS_log1p_cluster_county | post:historical                                            |  0.008 | 0.02  |   0.389       | 0.697     |

### B) Two-part model

any_delay logit formula used: `any_delay ~ post + historical + post:historical + C(rurality_3) + C(county_norm) + C(operator)`

| model              | term                                                       |   log_odds |    se |   odds_ratio |   or_ci95_lo |   or_ci95_hi | p_value   |
|:-------------------|:-----------------------------------------------------------|-----------:|------:|-------------:|-------------:|-------------:|:----------|
| H2_logit_any_delay | Intercept                                                  |      5.474 | 1.441 |      238.335 |       14.135 |     4018.54  | <0.001    |
| H2_logit_any_delay | C(rurality_3)[T.Suburban]                                  |     -0.39  | 0.158 |        0.677 |        0.497 |        0.922 | 0.013     |
| H2_logit_any_delay | C(rurality_3)[T.Urban]                                     |     -0.384 | 0.061 |        0.681 |        0.604 |        0.768 | <0.001    |
| H2_logit_any_delay | C(county_norm)[T.RIO BLANCO]                               |     -0.216 | 0.211 |        0.806 |        0.533 |        1.219 | 0.307     |
| H2_logit_any_delay | C(county_norm)[T.WELD]                                     |     -1.433 | 0.941 |        0.239 |        0.038 |        1.507 | 0.128     |
| H2_logit_any_delay | C(operator)[T.31 OPERATING]                                |      2.367 | 1.731 |       10.663 |        0.359 |      316.929 | 0.171     |
| H2_logit_any_delay | C(operator)[T.4-H OPERATING CORPORATION]                   |      5.11  | 1.487 |      165.687 |        8.984 |     3055.54  | <0.001    |
| H2_logit_any_delay | C(operator)[T.8 NORTH LLC]                                 |     -3.213 | 1.083 |        0.04  |        0.005 |        0.336 | 0.003     |
| H2_logit_any_delay | C(operator)[T.AKA ENERGY GROUP LLC]                        |     -3.413 | 1.087 |        0.033 |        0.004 |        0.277 | 0.002     |
| H2_logit_any_delay | C(operator)[T.ANADARKO DJ GAS PROCESSING LLC]              |      5.801 | 1.468 |      330.528 |       18.614 |     5869.25  | <0.001    |
| H2_logit_any_delay | C(operator)[T.ANADARKO WATTENBERG OIL COMPLEX LLC]         |     -3.41  | 1.083 |        0.033 |        0.004 |        0.276 | 0.002     |
| H2_logit_any_delay | C(operator)[T.ANSCHUTZ EXPLORATION CORP]                   |     -3.486 | 1.404 |        0.031 |        0.002 |        0.48  | 0.013     |
| H2_logit_any_delay | C(operator)[T.BARGATH LLC]                                 |     -5.211 | 1.427 |        0.005 |        0     |        0.089 | <0.001    |
| H2_logit_any_delay | C(operator)[T.BARRETT CORPORATION* BILL]                   |     -1.452 | 1.095 |        0.234 |        0.027 |        2.004 | 0.185     |
| H2_logit_any_delay | C(operator)[T.BARRETT RESOURCES CORP]                      |      5.801 | 1.468 |      330.528 |       18.614 |     5869.25  | <0.001    |
| H2_logit_any_delay | C(operator)[T.BAYLESS PRODUCER, LLC* ROBERT L]             |      1.456 | 1.741 |        4.29  |        0.141 |      130.205 | 0.403     |
| H2_logit_any_delay | C(operator)[T.BAYSWATER EXPLORATION & PRODUCTION LLC]      |     -0.922 | 1.072 |        0.398 |        0.049 |        3.25  | 0.390     |
| H2_logit_any_delay | C(operator)[T.BAYSWATER EXPLORATION AND PRODUCTION LLC]    |     -2.259 | 1.096 |        0.104 |        0.012 |        0.895 | 0.039     |
| H2_logit_any_delay | C(operator)[T.BERRY PETROLEUM COMPANY LLC]                 |     -3.385 | 1.424 |        0.034 |        0.002 |        0.552 | 0.017     |
| H2_logit_any_delay | C(operator)[T.BISON IV OPERATING LLC]                      |     -1.953 | 1.07  |        0.142 |        0.017 |        1.155 | 0.068     |
| H2_logit_any_delay | C(operator)[T.BISON OIL & GAS II LLC]                      |     -1.41  | 1.072 |        0.244 |        0.03  |        1.998 | 0.189     |
| H2_logit_any_delay | C(operator)[T.BLACK HILLS PLATEAU PRODUCTION LLC]          |    -13.246 | 1.758 |        0     |        0     |        0     | <0.001    |
| H2_logit_any_delay | C(operator)[T.BLUE CHIP OIL INC]                           |      6.502 | 1.48  |      666.268 |       36.6   |    12128.6   | <0.001    |
| H2_logit_any_delay | C(operator)[T.BNN WESTERN LLC]                             |     -1.962 | 1.098 |        0.141 |        0.016 |        1.208 | 0.074     |
| H2_logit_any_delay | C(operator)[T.BONANZA CREEK ENERGY OPERATING COMPANY LLC]  |     -3.185 | 1.076 |        0.041 |        0.005 |        0.341 | 0.003     |
| H2_logit_any_delay | C(operator)[T.CAERUS PICEANCE LLC]                         |     -4.432 | 1.416 |        0.012 |        0.001 |        0.191 | 0.002     |
| H2_logit_any_delay | C(operator)[T.CAPTIVA ENERGY PARTNERS LLC]                 |      4.346 | 1.496 |       77.194 |        4.113 |     1448.94  | 0.004     |
| H2_logit_any_delay | C(operator)[T.CARRIZO NIOBRARA LLC]                        |      5.901 | 1.496 |      365.585 |       19.481 |     6860.48  | <0.001    |
| H2_logit_any_delay | C(operator)[T.CCRP OPERATING INC]                          |      4.677 | 1.496 |      107.497 |        5.727 |     2017.57  | 0.002     |
| H2_logit_any_delay | C(operator)[T.CHACO ENERGY COMPANY]                        |      5.621 | 1.498 |      276.132 |       14.661 |     5200.89  | <0.001    |
| H2_logit_any_delay | C(operator)[T.CHEVRON PIPELINE COMPANY]                    |      3.113 | 1.741 |       22.48  |        0.742 |      681.496 | 0.074     |
| H2_logit_any_delay | C(operator)[T.CHEVRON PRODUCTION COMPANY]                  |     -5.83  | 1.42  |        0.003 |        0     |        0.048 | <0.001    |
| H2_logit_any_delay | C(operator)[T.CHEVRON USA INC]                             |     -3.475 | 1.406 |        0.031 |        0.002 |        0.487 | 0.013     |
| H2_logit_any_delay | C(operator)[T.CIVITAS NORTH LLC]                           |     -1.181 | 1.074 |        0.307 |        0.037 |        2.518 | 0.271     |
| H2_logit_any_delay | C(operator)[T.COACHMAN ENERGY OPERATING COMPANY LLC]       |      3.425 | 1.772 |       30.707 |        0.952 |      990.453 | 0.053     |
| H2_logit_any_delay | C(operator)[T.COLORADO OIL & GAS CONSERVATION COMMISSION]  |     -3.678 | 1.157 |        0.025 |        0.003 |        0.244 | 0.001     |
| H2_logit_any_delay | C(operator)[T.COMPLETE ENERGY SERVICES INC]                |      4.34  | 1.494 |       76.712 |        4.104 |     1433.83  | 0.004     |
| H2_logit_any_delay | C(operator)[T.CONFLUENCE DJ LLC]                           |      4.34  | 1.494 |       76.712 |        4.104 |     1433.83  | 0.004     |
| H2_logit_any_delay | C(operator)[T.CRESTONE PEAK RESOURCES OPERATING LLC]       |     -2.205 | 1.078 |        0.11  |        0.013 |        0.912 | 0.041     |
| H2_logit_any_delay | C(operator)[T.CUB CREEK ENERGY]                            |     -3.528 | 1.074 |        0.029 |        0.004 |        0.241 | 0.001     |
| H2_logit_any_delay | C(operator)[T.CUB CREEK ENERGY LLC]                        |     -1.704 | 1.069 |        0.182 |        0.022 |        1.48  | 0.111     |
| H2_logit_any_delay | C(operator)[T.DAN A HUGHES COMPANY LP]                     |      4.346 | 1.496 |       77.194 |        4.113 |     1448.94  | 0.004     |
| H2_logit_any_delay | C(operator)[T.DCP MIDSTREAM LP]                            |     -2.57  | 1.101 |        0.077 |        0.009 |        0.662 | 0.020     |
| H2_logit_any_delay | C(operator)[T.DCP OPERATING COMPANY LP]                    |     -2.106 | 1.071 |        0.122 |        0.015 |        0.994 | 0.049     |
| H2_logit_any_delay | C(operator)[T.DIAMOND OPERATING INC]                       |      5.663 | 1.469 |      287.95  |       16.176 |     5125.71  | <0.001    |
| H2_logit_any_delay | C(operator)[T.EDGE ENERGY II LLC]                          |     -2.374 | 1.072 |        0.093 |        0.011 |        0.761 | 0.027     |
| H2_logit_any_delay | C(operator)[T.ENCANA OIL & GAS (USA) INC]                  |     -3.612 | 1.277 |        0.027 |        0.002 |        0.33  | 0.005     |
| H2_logit_any_delay | C(operator)[T.ENERPLUS RESOURCES (USA) CORPORATION]        |     -2.512 | 1.093 |        0.081 |        0.01  |        0.69  | 0.021     |
| H2_logit_any_delay | C(operator)[T.EOG RESOURCES INC]                           |     -2.884 | 1.102 |        0.056 |        0.006 |        0.484 | 0.009     |
| H2_logit_any_delay | C(operator)[T.EWS 13 DJ BASIN LLC]                         |      6.484 | 1.496 |      654.588 |       34.883 |    12283.5   | <0.001    |
| H2_logit_any_delay | C(operator)[T.EWS 4 DJ BASIN LLC]                          |      4.34  | 1.494 |       76.712 |        4.104 |     1433.83  | 0.004     |
| H2_logit_any_delay | C(operator)[T.EXPEDITION WATER SOLUTIONS COLORADO LLC]     |    -10.295 | 1.495 |        0     |        0     |        0.001 | <0.001    |
| H2_logit_any_delay | C(operator)[T.EXTRACTION OIL & GAS INC]                    |     -2.813 | 1.072 |        0.06  |        0.007 |        0.491 | 0.009     |
| H2_logit_any_delay | C(operator)[T.EXTRACTION OIL & GAS LLC]                    |     -2.517 | 1.1   |        0.081 |        0.009 |        0.697 | 0.022     |
| H2_logit_any_delay | C(operator)[T.FIFTH CREEK ENERGY OPERATING COMPANY LLC]    |     -1.373 | 1.107 |        0.253 |        0.029 |        2.218 | 0.215     |
| H2_logit_any_delay | C(operator)[T.FOUNDATION ENERGY MANAGEMENT LLC]            |     -2.52  | 1.092 |        0.08  |        0.009 |        0.684 | 0.021     |
| H2_logit_any_delay | C(operator)[T.FRITZLER RESOURCES INC]                      |      5.373 | 1.469 |      215.501 |       12.106 |     3836.32  | <0.001    |
| H2_logit_any_delay | C(operator)[T.FUNDARE RESOURCES OPERATING COMPANY LLC]     |     -1.15  | 1.071 |        0.317 |        0.039 |        2.581 | 0.283     |
| H2_logit_any_delay | C(operator)[T.GADECO LLC]                                  |      5.845 | 1.488 |      345.666 |       18.71  |     6386.12  | <0.001    |
| H2_logit_any_delay | C(operator)[T.GENESIS GAS & OIL COLORADO LLC]              |      3.273 | 1.73  |       26.384 |        0.888 |      783.567 | 0.059     |
| H2_logit_any_delay | C(operator)[T.GRAND RIVER GATHERING LLC]                   |     -3.829 | 1.423 |        0.022 |        0.001 |        0.354 | 0.007     |
| H2_logit_any_delay | C(operator)[T.GREAT WESTERN OPERATING COMPANY LLC]         |     -2.054 | 1.077 |        0.128 |        0.016 |        1.059 | 0.057     |
| H2_logit_any_delay | C(operator)[T.GRIZZLY OPERATING LLC]                       |      5.901 | 1.744 |      365.514 |       11.977 |    11154.4   | <0.001    |
| H2_logit_any_delay | C(operator)[T.GRYNBERG* JACK DBA GRYNBERG PETROLEUM CO]    |      6.465 | 1.488 |      641.971 |       34.75  |    11859.8   | <0.001    |
| H2_logit_any_delay | C(operator)[T.HIGHPOINT ENERGY LLC]                        |    -10.295 | 1.495 |        0     |        0     |        0.001 | <0.001    |
| H2_logit_any_delay | C(operator)[T.HIGHPOINT OPERATING CORPORATION]             |     -3.329 | 1.073 |        0.036 |        0.004 |        0.294 | 0.002     |
| H2_logit_any_delay | C(operator)[T.HRM RESOURCES II LLC]                        |    -10.068 | 1.495 |        0     |        0     |        0.001 | <0.001    |
| H2_logit_any_delay | C(operator)[T.HUNTER RIDGE ENERGY SERVICES LLC]            |      4.714 | 1.738 |      111.446 |        3.693 |     3363.47  | 0.007     |
| H2_logit_any_delay | C(operator)[T.HYNDREX RESOURCES]                           |      4.34  | 1.494 |       76.712 |        4.104 |     1433.83  | 0.004     |
| H2_logit_any_delay | C(operator)[T.INDUSTRIAL GAS SERVICES INC]                 |      5.621 | 1.498 |      276.132 |       14.661 |     5200.89  | <0.001    |
| H2_logit_any_delay | C(operator)[T.K P KAUFFMAN COMPANY INC]                    |     -3.561 | 1.101 |        0.028 |        0.003 |        0.246 | 0.001     |
| H2_logit_any_delay | C(operator)[T.KERR MCGEE GATHERING LLC]                    |     -2.893 | 1.075 |        0.055 |        0.007 |        0.456 | 0.007     |
| H2_logit_any_delay | C(operator)[T.KERR MCGEE OIL & GAS ONSHORE LP]             |     -3.503 | 1.082 |        0.03  |        0.004 |        0.251 | 0.001     |
| H2_logit_any_delay | C(operator)[T.KOCH EXPLORATION COMPANY LLC]                |      1.675 | 1.735 |        5.341 |        0.178 |      160.168 | 0.334     |
| H2_logit_any_delay | C(operator)[T.KOCH EXPLORATION COMPANY, LLC]               |      3.268 | 1.734 |       26.268 |        0.878 |      786.024 | 0.059     |
| H2_logit_any_delay | C(operator)[T.KP KAUFFMAN COMPANY INC]                     |     -1.508 | 1.07  |        0.221 |        0.027 |        1.802 | 0.159     |
| H2_logit_any_delay | C(operator)[T.KT RESOURCES LLC]                            |      4.801 | 1.73  |      121.643 |        4.098 |     3611.14  | 0.006     |
| H2_logit_any_delay | C(operator)[T.LARAMIE ENERGY LLC]                          |     -3.548 | 1.42  |        0.029 |        0.002 |        0.465 | 0.012     |
| H2_logit_any_delay | C(operator)[T.LASSO OIL & GAS LLC]                         |      2.367 | 1.731 |       10.663 |        0.359 |      316.929 | 0.171     |
| H2_logit_any_delay | C(operator)[T.LINN OPERATING INC]                          |     -3.641 | 1.442 |        0.026 |        0.002 |        0.443 | 0.012     |
| H2_logit_any_delay | C(operator)[T.LINN OPERATING LLC]                          |     -5.489 | 1.441 |        0.004 |        0     |        0.07  | <0.001    |
| H2_logit_any_delay | C(operator)[T.LONGS PEAK RESOURCES LLC]                    |     -1.624 | 1.071 |        0.197 |        0.024 |        1.607 | 0.129     |
| H2_logit_any_delay | C(operator)[T.MACHII-ROSS PETROLEUM CO]                    |      5.11  | 1.487 |      165.687 |        8.984 |     3055.54  | <0.001    |
| H2_logit_any_delay | C(operator)[T.MAGPIE OPERATING INC]                        |      4.912 | 1.498 |      135.889 |        7.212 |     2560.37  | 0.001     |
| H2_logit_any_delay | C(operator)[T.MARALEX RESOURCES, INC]                      |      2.51  | 1.758 |       12.305 |        0.392 |      385.999 | 0.153     |
| H2_logit_any_delay | C(operator)[T.MARATHON OIL COMPANY]                        |     -5.489 | 1.441 |        0.004 |        0     |        0.07  | <0.001    |
| H2_logit_any_delay | C(operator)[T.MARKUS PRODUCTION, INC]                      |     -9.45  | 1.498 |        0     |        0     |        0.001 | <0.001    |
| H2_logit_any_delay | C(operator)[T.MDS ENERGY DEVELOPMENT LLC]                  |     -9.589 | 1.47  |        0     |        0     |        0.001 | <0.001    |
| H2_logit_any_delay | C(operator)[T.MERRION OIL & GAS CORP]                      |      2.724 | 1.741 |       15.237 |        0.503 |      461.984 | 0.118     |
| H2_logit_any_delay | C(operator)[T.MONAHAN GAS & OIL INC]                       |      4.808 | 1.494 |      122.501 |        6.555 |     2289.28  | 0.001     |
| H2_logit_any_delay | C(operator)[T.MUSTANG RESOURCES LLC]                       |     -5.279 | 1.45  |        0.005 |        0     |        0.087 | <0.001    |
| H2_logit_any_delay | C(operator)[T.NGL WATER SOLUTIONS DJ LLC]                  |     -3.604 | 1.085 |        0.027 |        0.003 |        0.228 | <0.001    |
| H2_logit_any_delay | C(operator)[T.NICKEL ROAD OPERATING LLC]                   |     -0.98  | 1.068 |        0.375 |        0.046 |        3.047 | 0.359     |
| H2_logit_any_delay | C(operator)[T.NOBLE ENERGY INC]                            |     -2.322 | 1.088 |        0.098 |        0.012 |        0.828 | 0.033     |
| H2_logit_any_delay | C(operator)[T.NOBLE MIDSTREAM SERVICES LLC]                |     -1.502 | 1.071 |        0.223 |        0.027 |        1.816 | 0.161     |
| H2_logit_any_delay | C(operator)[T.NORTHSTAR GAS COMPANY INC]                   |      1.456 | 1.741 |        4.29  |        0.141 |      130.205 | 0.403     |
| H2_logit_any_delay | C(operator)[T.O'BRIEN ENERGY RESOURCES CORP]               |    -10.068 | 1.495 |        0     |        0     |        0.001 | <0.001    |
| H2_logit_any_delay | C(operator)[T.OXY USA INC]                                 |      1.295 | 1.759 |        3.652 |        0.116 |      114.678 | 0.461     |
| H2_logit_any_delay | C(operator)[T.OXY USA WTP LP]                              |     -4.218 | 1.441 |        0.015 |        0.001 |        0.248 | 0.003     |
| H2_logit_any_delay | C(operator)[T.PAINTED PEGASUS PETROLEUM LLC]               |      6.913 | 1.492 |     1004.89  |       53.952 |    18716.6   | <0.001    |
| H2_logit_any_delay | C(operator)[T.PDC ENERGY INC]                              |     -2.099 | 1.083 |        0.123 |        0.015 |        1.023 | 0.053     |
| H2_logit_any_delay | C(operator)[T.PETERSON ENERGY OPERATING INC]               |     -2.639 | 1.091 |        0.071 |        0.008 |        0.607 | 0.016     |
| H2_logit_any_delay | C(operator)[T.PETRO MEX RESOURCES]                         |      5.659 | 1.745 |      286.878 |        9.38  |     8773.93  | 0.001     |
| H2_logit_any_delay | C(operator)[T.PETRO OPERATING COMPANY LLC]                 |     -2.874 | 1.075 |        0.056 |        0.007 |        0.465 | 0.008     |
| H2_logit_any_delay | C(operator)[T.PETROSHARE CORPORATION]                      |      5.829 | 1.487 |      340.153 |       18.447 |     6272.14  | <0.001    |
| H2_logit_any_delay | C(operator)[T.PLUG NICKEL OIL COMPANY INC]                 |      2.724 | 1.741 |       15.237 |        0.503 |      461.984 | 0.118     |
| H2_logit_any_delay | C(operator)[T.PRAIRIE OPERATING CO LLC]                    |      6.422 | 1.468 |      615.321 |       34.656 |    10925.1   | <0.001    |
| H2_logit_any_delay | C(operator)[T.PROVIDENCE OPERATING LLC DBA POCO OPERATING] |     -1.691 | 1.068 |        0.184 |        0.023 |        1.495 | 0.113     |
| H2_logit_any_delay | C(operator)[T.RED HAWK PETROLEUM LLC]                      |     -2.879 | 1.073 |        0.056 |        0.007 |        0.46  | 0.007     |
| H2_logit_any_delay | C(operator)[T.RED ROCK GATHERING COMPANY LLC]              |     -3.916 | 1.42  |        0.02  |        0.001 |        0.322 | 0.006     |
| H2_logit_any_delay | C(operator)[T.REP PROCESSING LLC]                          |      5.373 | 1.469 |      215.501 |       12.106 |     3836.32  | <0.001    |
| H2_logit_any_delay | C(operator)[T.RIO MESA RESOURCES INC]                      |      3.877 | 1.73  |       48.282 |        1.626 |     1433.56  | 0.025     |
| H2_logit_any_delay | C(operator)[T.ROBERT L BAYLESS PRODUCER LLC]               |      2.367 | 1.731 |       10.663 |        0.359 |      316.929 | 0.171     |
| H2_logit_any_delay | C(operator)[T.ROCKY MOUNTAIN MIDSTREAM LLC]                |      6.633 | 1.47  |      759.7   |       42.597 |    13548.9   | <0.001    |
| H2_logit_any_delay | C(operator)[T.ROCKY MOUNTAIN NATURAL GAS LLC]              |      2.216 | 1.741 |        9.172 |        0.302 |      278.153 | 0.203     |
| H2_logit_any_delay | C(operator)[T.RWL ENTERPRISES]                             |      5.11  | 1.487 |      165.687 |        8.984 |     3055.54  | <0.001    |
| H2_logit_any_delay | C(operator)[T.SAMSON RESOURCES COMPANY]                    |      2.48  | 1.735 |       11.947 |        0.399 |      357.976 | 0.153     |
| H2_logit_any_delay | C(operator)[T.SCHNEIDER ENERGY SERVICES INC]               |     -2.532 | 1.112 |        0.08  |        0.009 |        0.703 | 0.023     |
| H2_logit_any_delay | C(operator)[T.SCOUT ENERGY MANAGEMENT LLC]                 |     -3.103 | 1.405 |        0.045 |        0.003 |        0.705 | 0.027     |
| H2_logit_any_delay | C(operator)[T.SMITH ENERGY CORP]                           |     -0.961 | 1.108 |        0.383 |        0.044 |        3.354 | 0.386     |
| H2_logit_any_delay | C(operator)[T.SMITH OIL PROPERTIES INC]                    |      3.746 | 1.487 |       42.347 |        2.295 |      781.556 | 0.012     |
| H2_logit_any_delay | C(operator)[T.SRC ENERGY INC]                              |     -2.917 | 1.093 |        0.054 |        0.006 |        0.461 | 0.008     |
| H2_logit_any_delay | C(operator)[T.SUMMIT DJ-S LLC]                             |      4.104 | 1.469 |       60.579 |        3.401 |     1079.14  | 0.005     |
| H2_logit_any_delay | C(operator)[T.SUMMIT MIDSTREAM NIOBRARA LLC]               |      3.823 | 1.496 |       45.744 |        2.437 |      858.8   | 0.011     |
| H2_logit_any_delay | C(operator)[T.SUMMIT MIDSTREAM PARTNERS LLC]               |     -4.117 | 1.421 |        0.016 |        0.001 |        0.264 | 0.004     |
| H2_logit_any_delay | C(operator)[T.SYNERGY RESOURCES CORPORATION]               |     -0.367 | 1.094 |        0.693 |        0.081 |        5.91  | 0.737     |
| H2_logit_any_delay | C(operator)[T.TALLGRASS WATER WESTERN LLC]                 |     -1.875 | 1.07  |        0.153 |        0.019 |        1.249 | 0.080     |
| H2_logit_any_delay | C(operator)[T.TAPROOT ROCKIES MIDSTREAM LLC]               |     -2.872 | 1.07  |        0.057 |        0.007 |        0.461 | 0.007     |
| H2_logit_any_delay | C(operator)[T.TEP ROCKY MOUNTAIN LLC]                      |     -3.751 | 1.42  |        0.023 |        0.001 |        0.38  | 0.008     |
| H2_logit_any_delay | C(operator)[T.TEXAS TEA OF COLORADO LLC DBA TEXAS TEA LLC] |      6.057 | 1.496 |      427.287 |       22.768 |     8019.06  | <0.001    |
| H2_logit_any_delay | C(operator)[T.TINDALL OPERATING COMPANY]                   |      5.621 | 1.498 |      276.132 |       14.661 |     5200.89  | <0.001    |
| H2_logit_any_delay | C(operator)[T.TOP OPERATING COMPANY]                       |      0.173 | 1.108 |        1.189 |        0.135 |       10.434 | 0.876     |
| H2_logit_any_delay | C(operator)[T.UPLAND EXPLORATION LLC]                      |      5.373 | 1.469 |      215.501 |       12.106 |     3836.32  | <0.001    |
| H2_logit_any_delay | C(operator)[T.URSA OPERATING COMPANY LLC]                  |     -3.451 | 1.424 |        0.032 |        0.002 |        0.517 | 0.015     |
| H2_logit_any_delay | C(operator)[T.UTAH GAS OP LTD DBA UTAH GAS CORP]           |     -3.866 | 1.401 |        0.021 |        0.001 |        0.326 | 0.006     |
| H2_logit_any_delay | C(operator)[T.VANGUARD OPERATING LLC]                      |     -2.613 | 1.355 |        0.073 |        0.005 |        1.044 | 0.054     |
| H2_logit_any_delay | C(operator)[T.VERDAD OIL & GAS CORPORATION]                |      4.34  | 1.494 |       76.712 |        4.104 |     1433.83  | 0.004     |
| H2_logit_any_delay | C(operator)[T.VERDAD RESOURCES LLC]                        |     -2.886 | 1.071 |        0.056 |        0.007 |        0.455 | 0.007     |
| H2_logit_any_delay | C(operator)[T.VISION ENERGY LLC]                           |      4.225 | 1.744 |       68.392 |        2.243 |     2085.34  | 0.015     |
| H2_logit_any_delay | C(operator)[T.WARD PETROLEUM CORPORATION]                  |     -3.843 | 1.105 |        0.021 |        0.002 |        0.187 | <0.001    |
| H2_logit_any_delay | C(operator)[T.WEXPRO COMPANY]                              |      2.48  | 1.735 |       11.947 |        0.399 |      357.976 | 0.153     |
| H2_logit_any_delay | C(operator)[T.WHITING OIL & GAS CORPORATION]               |     -3.384 | 1.092 |        0.034 |        0.004 |        0.289 | 0.002     |
| H2_logit_any_delay | C(operator)[T.WINDSOR ENERGY GROUP LLC]                    |      2.216 | 1.741 |        9.172 |        0.302 |      278.153 | 0.203     |
| H2_logit_any_delay | C(operator)[T.WOODARD* SANDRA K]                           |      2.216 | 1.741 |        9.172 |        0.302 |      278.153 | 0.203     |
| H2_logit_any_delay | C(operator)[T.WPX ENERGY ROCKY MOUNTAIN LLC]               |     -5.849 | 1.442 |        0.003 |        0     |        0.049 | <0.001    |
| H2_logit_any_delay | C(operator)[T.XTO ENERGY INC]                              |     -3.308 | 1.409 |        0.037 |        0.002 |        0.58  | 0.019     |
| H2_logit_any_delay | post                                                       |     -0.867 | 0.278 |        0.42  |        0.244 |        0.724 | 0.002     |
| H2_logit_any_delay | historical                                                 |     -0.236 | 0.213 |        0.79  |        0.52  |        1.198 | 0.267     |
| H2_logit_any_delay | post:historical                                            |     -0.327 | 0.255 |        0.721 |        0.437 |        1.19  | 0.200     |

Conditional positive delay model (delay>0), OLS on log1p_delay; clustered by operator:

| model                                   | term                                                       |   coef |    se |             t | p_value   |
|:----------------------------------------|:-----------------------------------------------------------|-------:|------:|--------------:|:----------|
| H2_OLS_log1p_delay_gt0_cluster_operator | Intercept                                                  |  1.186 | 0.275 |   4.318       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(county_norm)[T.RIO BLANCO]                               |  0.125 | 0.113 |   1.104       | 0.270     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(county_norm)[T.WELD]                                     | -0.458 | 0.274 |  -1.675       | 0.094     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(rurality_3)[T.Suburban]                                  |  0.092 | 0.032 |   2.901       | 0.004     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(rurality_3)[T.Urban]                                     |  0.022 | 0.041 |   0.534       | 0.593     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.31 OPERATING]                                |  0.943 | 0.287 |   3.287       | 0.001     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.4-H OPERATING CORPORATION]                   |  1.088 | 0.104 |  10.489       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.8 NORTH LLC]                                 | -0.146 | 0.096 |  -1.532       | 0.126     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.AKA ENERGY GROUP LLC]                        |  1.018 | 0.048 |  21.07        | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.ANADARKO DJ GAS PROCESSING LLC]              |  0.405 | 0     |   3.31187e+12 | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.ANADARKO WATTENBERG OIL COMPLEX LLC]         |  0.843 | 0.05  |  17.029       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.ANSCHUTZ EXPLORATION CORP]                   | -0.039 | 0.286 |  -0.135       | 0.892     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.BARGATH LLC]                                 | -0.043 | 0.273 |  -0.158       | 0.875     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.BARRETT CORPORATION* BILL]                   |  0.348 | 0.073 |   4.781       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.BARRETT RESOURCES CORP]                      |  0     | 0     |   0.142       | 0.887     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.BAYLESS PRODUCER, LLC* ROBERT L]             | -0.618 | 0.295 |  -2.096       | 0.036     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.BAYSWATER EXPLORATION & PRODUCTION LLC]      |  0.432 | 0.029 |  14.916       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.BAYSWATER EXPLORATION AND PRODUCTION LLC]    |  0.135 | 0.068 |   2.004       | 0.045     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.BERRY PETROLEUM COMPANY LLC]                 |  0.08  | 0.273 |   0.294       | 0.769     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.BISON IV OPERATING LLC]                      |  0.752 | 0.041 |  18.126       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.BISON OIL & GAS II LLC]                      |  0.276 | 0.048 |   5.689       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.BLUE CHIP OIL INC]                           |  1.677 | 0.094 |  17.861       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.BNN WESTERN LLC]                             |  0.187 | 0.064 |   2.95        | 0.003     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.BONANZA CREEK ENERGY OPERATING COMPANY LLC]  |  0.145 | 0.05  |   2.932       | 0.003     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.CAERUS PICEANCE LLC]                         | -0.189 | 0.271 |  -0.699       | 0.484     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.CAPTIVA ENERGY PARTNERS LLC]                 |  0.658 | 0.067 |   9.838       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.CARRIZO NIOBRARA LLC]                        |  0.587 | 0.067 |   8.769       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.CCRP OPERATING INC]                          | -0.035 | 0.067 |  -0.522       | 0.601     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.CHACO ENERGY COMPANY]                        |  3.781 | 0.125 |  30.179       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.CHEVRON PIPELINE COMPANY]                    |  0.075 | 0.295 |   0.255       | 0.799     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.CHEVRON PRODUCTION COMPANY]                  | -0.162 | 0.295 |  -0.55        | 0.583     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.CHEVRON USA INC]                             | -0.079 | 0.292 |  -0.272       | 0.786     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.CIVITAS NORTH LLC]                           |  0.136 | 0.053 |   2.558       | 0.011     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.COACHMAN ENERGY OPERATING COMPANY LLC]       |  0.993 | 0.279 |   3.559       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.COLORADO OIL & GAS CONSERVATION COMMISSION]  |  0.095 | 0.115 |   0.829       | 0.407     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.COMPLETE ENERGY SERVICES INC]                |  0.348 | 0.048 |   7.21        | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.CONFLUENCE DJ LLC]                           | -0.057 | 0.048 |  -1.182       | 0.237     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.CRESTONE PEAK RESOURCES OPERATING LLC]       |  0.027 | 0.066 |   0.406       | 0.685     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.CUB CREEK ENERGY]                            |  0.322 | 0.026 |  12.462       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.CUB CREEK ENERGY LLC]                        |  0.465 | 0.031 |  14.93        | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.DAN A HUGHES COMPANY LP]                     |  0.371 | 0.067 |   5.538       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.DCP MIDSTREAM LP]                            |  0.37  | 0.057 |   6.507       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.DCP OPERATING COMPANY LP]                    |  0.293 | 0.039 |   7.586       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.DIAMOND OPERATING INC]                       |  0.428 | 0.041 |  10.307       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.EDGE ENERGY II LLC]                          |  1.724 | 0.064 |  26.777       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.ENCANA OIL & GAS (USA) INC]                  | -0.172 | 0.232 |  -0.739       | 0.460     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.ENERPLUS RESOURCES (USA) CORPORATION]        |  0.377 | 0.048 |   7.805       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.EOG RESOURCES INC]                           |  0.222 | 0.064 |   3.462       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.EWS 13 DJ BASIN LLC]                         | -0.31  | 0.115 |  -2.703       | 0.007     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.EWS 4 DJ BASIN LLC]                          |  1.447 | 0.048 |  29.949       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.EXTRACTION OIL & GAS INC]                    |  0.286 | 0.029 |   9.895       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.EXTRACTION OIL & GAS LLC]                    |  0.284 | 0.063 |   4.508       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.FIFTH CREEK ENERGY OPERATING COMPANY LLC]    |  0.229 | 0.067 |   3.429       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.FOUNDATION ENERGY MANAGEMENT LLC]            |  0.555 | 0.075 |   7.432       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.FRITZLER RESOURCES INC]                      |  3.534 | 0.041 |  85.172       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.FUNDARE RESOURCES OPERATING COMPANY LLC]     |  0.134 | 0.044 |   3.063       | 0.002     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.GADECO LLC]                                  |  0.872 | 0.116 |   7.547       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.GENESIS GAS & OIL COLORADO LLC]              |  1.486 | 0.287 |   5.18        | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.GRAND RIVER GATHERING LLC]                   | -0.233 | 0.275 |  -0.847       | 0.397     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.GREAT WESTERN OPERATING COMPANY LLC]         |  0.367 | 0.055 |   6.706       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.GRIZZLY OPERATING LLC]                       | -0.239 | 0.276 |  -0.867       | 0.386     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.GRYNBERG* JACK DBA GRYNBERG PETROLEUM CO]    |  0.51  | 0.116 |   4.41        | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.HIGHPOINT OPERATING CORPORATION]             |  0.216 | 0.048 |   4.537       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.HUNTER RIDGE ENERGY SERVICES LLC]            |  0.148 | 0.273 |   0.541       | 0.589     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.HYNDREX RESOURCES]                           |  0.348 | 0.048 |   7.21        | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.INDUSTRIAL GAS SERVICES INC]                 |  0.628 | 0.125 |   5.014       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.K P KAUFFMAN COMPANY INC]                    |  0.471 | 0.065 |   7.209       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.KERR MCGEE GATHERING LLC]                    |  0.469 | 0.046 |  10.104       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.KERR MCGEE OIL & GAS ONSHORE LP]             |  0.23  | 0.066 |   3.467       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.KOCH EXPLORATION COMPANY LLC]                |  1.525 | 0.298 |   5.125       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.KOCH EXPLORATION COMPANY, LLC]               |  0.912 | 0.294 |   3.107       | 0.002     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.KP KAUFFMAN COMPANY INC]                     |  0.44  | 0.03  |  14.595       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.KT RESOURCES LLC]                            | -0.561 | 0.287 |  -1.954       | 0.051     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.LARAMIE ENERGY LLC]                          |  0.041 | 0.272 |   0.152       | 0.879     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.LASSO OIL & GAS LLC]                         |  1.69  | 0.287 |   5.891       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.LINN OPERATING INC]                          |  0.066 | 0.275 |   0.241       | 0.809     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.LINN OPERATING LLC]                          | -0.493 | 0.275 |  -1.795       | 0.073     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.LONGS PEAK RESOURCES LLC]                    |  0.007 | 0.045 |   0.147       | 0.883     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.MACHII-ROSS PETROLEUM CO]                    |  1.914 | 0.104 |  18.461       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.MAGPIE OPERATING INC]                        |  4.765 | 0.125 |  38.034       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.MARALEX RESOURCES, INC]                      | -0.493 | 0.275 |  -1.795       | 0.073     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.MARATHON OIL COMPANY]                        | -0.088 | 0.275 |  -0.319       | 0.750     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.MERRION OIL & GAS CORP]                      |  1.087 | 0.295 |   3.686       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.MONAHAN GAS & OIL INC]                       |  2.022 | 0.048 |  41.858       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.MUSTANG RESOURCES LLC]                       | -0.288 | 0.287 |  -1.004       | 0.316     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.NGL WATER SOLUTIONS DJ LLC]                  |  0.588 | 0.051 |  11.487       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.NICKEL ROAD OPERATING LLC]                   |  0.073 | 0.007 |  10.008       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.NOBLE ENERGY INC]                            |  0.088 | 0.085 |   1.029       | 0.304     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.NOBLE MIDSTREAM SERVICES LLC]                |  0.363 | 0.029 |  12.503       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.NORTHSTAR GAS COMPANY INC]                   |  0.635 | 0.295 |   2.153       | 0.031     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.OXY USA INC]                                 |  0.423 | 0.275 |   1.54        | 0.123     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.OXY USA WTP LP]                              | -0.29  | 0.275 |  -1.057       | 0.290     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.PAINTED PEGASUS PETROLEUM LLC]               |  1.673 | 0.136 |  12.303       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.PDC ENERGY INC]                              |  0.245 | 0.066 |   3.736       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.PETERSON ENERGY OPERATING INC]               |  1.25  | 0.108 |  11.622       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.PETRO MEX RESOURCES]                         |  1.132 | 0.269 |   4.201       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.PETRO OPERATING COMPANY LLC]                 |  2.697 | 0.075 |  36.111       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.PETROSHARE CORPORATION]                      |  0.528 | 0.104 |   5.093       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.PLUG NICKEL OIL COMPANY INC]                 | -0.212 | 0.295 |  -0.721       | 0.471     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.PRAIRIE OPERATING CO LLC]                    |  0.439 | 0     |   3.50358e+12 | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.PROVIDENCE OPERATING LLC DBA POCO OPERATING] |  0     | 0     |   0.208       | 0.835     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.RED HAWK PETROLEUM LLC]                      |  0.942 | 0.05  |  18.776       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.RED ROCK GATHERING COMPANY LLC]              | -0.267 | 0.285 |  -0.938       | 0.348     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.REP PROCESSING LLC]                          |  0.715 | 0.041 |  17.241       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.RIO MESA RESOURCES INC]                      |  0.825 | 0.287 |   2.877       | 0.004     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.ROBERT L BAYLESS PRODUCER LLC]               |  0.132 | 0.287 |   0.461       | 0.645     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.ROCKY MOUNTAIN MIDSTREAM LLC]                |  0.403 | 0.024 |  16.693       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.ROCKY MOUNTAIN NATURAL GAS LLC]              |  1.328 | 0.295 |   4.504       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.RWL ENTERPRISES]                             |  1.469 | 0.104 |  14.17        | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.SAMSON RESOURCES COMPANY]                    |  0.373 | 0.298 |   1.252       | 0.210     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.SCHNEIDER ENERGY SERVICES INC]               | -0.288 | 0.125 |  -2.3         | 0.021     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.SCOUT ENERGY MANAGEMENT LLC]                 | -0.365 | 0.287 |  -1.271       | 0.204     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.SMITH ENERGY CORP]                           |  0.778 | 0.122 |   6.387       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.SMITH OIL PROPERTIES INC]                    |  2.725 | 0.104 |  26.281       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.SRC ENERGY INC]                              |  0.368 | 0.071 |   5.203       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.SUMMIT DJ-S LLC]                             |  5.009 | 0.041 | 120.736       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.SUMMIT MIDSTREAM NIOBRARA LLC]               | -0.035 | 0.067 |  -0.522       | 0.601     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.SUMMIT MIDSTREAM PARTNERS LLC]               |  0.128 | 0.274 |   0.467       | 0.640     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.SYNERGY RESOURCES CORPORATION]               |  0.382 | 0.084 |   4.551       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.TALLGRASS WATER WESTERN LLC]                 |  0.022 | 0.041 |   0.534       | 0.593     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.TAPROOT ROCKIES MIDSTREAM LLC]               |  0.103 | 0.041 |   2.489       | 0.013     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.TEP ROCKY MOUNTAIN LLC]                      | -0.225 | 0.274 |  -0.819       | 0.413     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.TEXAS TEA OF COLORADO LLC DBA TEXAS TEA LLC] | -0.31  | 0.115 |  -2.703       | 0.007     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.TINDALL OPERATING COMPANY]                   | -0.288 | 0.125 |  -2.3         | 0.021     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.TOP OPERATING COMPANY]                       |  0.165 | 0.115 |   1.432       | 0.152     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.UPLAND EXPLORATION LLC]                      |  2.587 | 0.041 |  62.357       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.URSA OPERATING COMPANY LLC]                  | -0.116 | 0.277 |  -0.421       | 0.674     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.UTAH GAS OP LTD DBA UTAH GAS CORP]           |  1.334 | 0.288 |   4.629       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.VANGUARD OPERATING LLC]                      | -0.116 | 0.279 |  -0.416       | 0.678     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.VERDAD OIL & GAS CORPORATION]                | -0.057 | 0.048 |  -1.182       | 0.237     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.VERDAD RESOURCES LLC]                        |  0.186 | 0.032 |   5.769       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.VISION ENERGY LLC]                           |  0.976 | 0.276 |   3.536       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.WARD PETROLEUM CORPORATION]                  |  0.371 | 0.067 |   5.538       | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.WEXPRO COMPANY]                              |  0.884 | 0.298 |   2.968       | 0.003     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.WHITING OIL & GAS CORPORATION]               |  0.114 | 0.068 |   1.685       | 0.092     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.WINDSOR ENERGY GROUP LLC]                    |  2.659 | 0.295 |   9.02        | <0.001    |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.WOODARD* SANDRA K]                           | -0.618 | 0.295 |  -2.096       | 0.036     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.WPX ENERGY ROCKY MOUNTAIN LLC]               | -0.528 | 0.275 |  -1.923       | 0.055     |
| H2_OLS_log1p_delay_gt0_cluster_operator | C(operator)[T.XTO ENERGY INC]                              | -0.301 | 0.293 |  -1.03        | 0.303     |
| H2_OLS_log1p_delay_gt0_cluster_operator | post                                                       | -0.057 | 0.048 |  -1.182       | 0.237     |
| H2_OLS_log1p_delay_gt0_cluster_operator | historical                                                 |  0.108 | 0.08  |   1.35        | 0.177     |
| H2_OLS_log1p_delay_gt0_cluster_operator | post:historical                                            |  0.202 | 0.068 |   2.968       | 0.003     |

Mechanism decomposition table (marginal standardized):

| spill_type   | period    |   P_any_delay |   E_delay_if_pos |
|:-------------|:----------|--------------:|-----------------:|
| Recent       | pre_2020  |      0.745056 |            2.03  |
| Recent       | post_2020 |      0.572983 |            1.862 |
| Historical   | pre_2020  |      0.702362 |            2.376 |
| Historical   | post_2020 |      0.449043 |            2.904 |

### C) Threshold models

late30 formula used: `late30 ~ post + historical + post:historical + C(rurality_3) + C(county_top3)`

| model           | term                         |   log_odds |    se |   odds_ratio |   or_ci95_lo |   or_ci95_hi | p_value   |
|:----------------|:-----------------------------|-----------:|------:|-------------:|-------------:|-------------:|:----------|
| H2_logit_late30 | Intercept                    |     -6.077 | 0.58  |        0.002 |        0.001 |        0.007 | <0.001    |
| H2_logit_late30 | C(rurality_3)[T.Suburban]    |      0.093 | 0.551 |        1.097 |        0.373 |        3.232 | 0.866     |
| H2_logit_late30 | C(rurality_3)[T.Urban]       |     -0.228 | 0.324 |        0.796 |        0.422 |        1.502 | 0.482     |
| H2_logit_late30 | C(county_top3)[T.RIO BLANCO] |      2.081 | 0.508 |        8.014 |        2.959 |       21.704 | <0.001    |
| H2_logit_late30 | C(county_top3)[T.WELD]       |      0.215 | 0.709 |        1.24  |        0.309 |        4.974 | 0.762     |
| H2_logit_late30 | post                         |      0.733 | 0.471 |        2.082 |        0.827 |        5.242 | 0.120     |
| H2_logit_late30 | historical                   |      2.011 | 0.587 |        7.471 |        2.364 |       23.605 | <0.001    |
| H2_logit_late30 | post:historical              |     -0.256 | 0.528 |        0.774 |        0.275 |        2.179 | 0.628     |

late90 formula used: `late90 ~ post + historical + post:historical + C(rurality_3) + C(county_top3)`

| model           | term                         |   log_odds |    se |   odds_ratio |   or_ci95_lo |   or_ci95_hi | p_value   |
|:----------------|:-----------------------------|-----------:|------:|-------------:|-------------:|-------------:|:----------|
| H2_logit_late90 | Intercept                    |     -9.137 | 1.334 |        0     |        0     |        0.001 | <0.001    |
| H2_logit_late90 | C(rurality_3)[T.Suburban]    |      0.161 | 0.579 |        1.175 |        0.377 |        3.658 | 0.781     |
| H2_logit_late90 | C(rurality_3)[T.Urban]       |     -0.436 | 0.307 |        0.647 |        0.354 |        1.181 | 0.156     |
| H2_logit_late90 | C(county_top3)[T.RIO BLANCO] |      2.082 | 0.922 |        8.023 |        1.317 |       48.871 | 0.024     |
| H2_logit_late90 | C(county_top3)[T.WELD]       |      0.875 | 0.914 |        2.4   |        0.4   |       14.4   | 0.338     |
| H2_logit_late90 | post                         |      2.712 | 1.134 |       15.055 |        1.631 |      139     | 0.017     |
| H2_logit_late90 | historical                   |      3.626 | 1.24  |       37.544 |        3.303 |      426.734 | 0.003     |
| H2_logit_late90 | post:historical              |     -1.788 | 1.198 |        0.167 |        0.016 |        1.751 | 0.136     |

Predicted P(late30) and P(late90) pre vs post (marginal standardized):

| spill_type   | period    |   P_late30 |   P_late90 |
|:-------------|:----------|-----------:|-----------:|
| Recent       | pre_2020  |   0.00365  |   0.000239 |
| Recent       | post_2020 |   0.007531 |   0.003581 |
| Historical   | pre_2020  |   0.025917 |   0.008854 |
| Historical   | post_2020 |   0.040456 |   0.021834 |



## H3: Rural lag and heterogeneous improvements

### Interaction models

any_delay model formula used: `any_delay ~ post + historical + post:historical + C(rurality_3) + post:C(rurality_3) + C(county_norm)`

| model                              | term                           |   log_odds |    se |   odds_ratio |   or_ci95_lo |   or_ci95_hi | p_value   |
|:-----------------------------------|:-------------------------------|-----------:|------:|-------------:|-------------:|-------------:|:----------|
| H3_logit_any_delay_post_x_rurality | Intercept                      |      0.971 | 0.169 |        2.642 |        1.896 |        3.681 | <0.001    |
| H3_logit_any_delay_post_x_rurality | C(rurality_3)[T.Suburban]      |     -0.113 | 0.333 |        0.893 |        0.465 |        1.714 | 0.734     |
| H3_logit_any_delay_post_x_rurality | C(rurality_3)[T.Urban]         |     -0.12  | 0.184 |        0.887 |        0.619 |        1.272 | 0.515     |
| H3_logit_any_delay_post_x_rurality | C(county_norm)[T.RIO BLANCO]   |      0.385 | 0.211 |        1.47  |        0.972 |        2.224 | 0.068     |
| H3_logit_any_delay_post_x_rurality | C(county_norm)[T.WELD]         |      0.17  | 0.222 |        1.186 |        0.767 |        1.833 | 0.443     |
| H3_logit_any_delay_post_x_rurality | post                           |     -0.541 | 0.255 |        0.582 |        0.353 |        0.96  | 0.034     |
| H3_logit_any_delay_post_x_rurality | post:C(rurality_3)[T.Suburban] |     -0.213 | 0.417 |        0.808 |        0.357 |        1.83  | 0.610     |
| H3_logit_any_delay_post_x_rurality | post:C(rurality_3)[T.Urban]    |     -0.335 | 0.26  |        0.715 |        0.429 |        1.191 | 0.198     |
| H3_logit_any_delay_post_x_rurality | historical                     |     -0.21  | 0.204 |        0.81  |        0.543 |        1.21  | 0.303     |
| H3_logit_any_delay_post_x_rurality | post:historical                |     -0.354 | 0.215 |        0.702 |        0.461 |        1.069 | 0.099     |
Joint test post×rurality (χ²): chi2=1.667, df=2, p=0.434483; terms=['post:C(rurality_3)[T.Suburban]', 'post:C(rurality_3)[T.Urban]']

log1p_delay model formula: `log1p_delay ~ post + historical + post:historical + C(rurality_3) + post:C(rurality_3) + C(county_norm) + C(operator)`

| model                                         | term                                                       |   coef |    se |             t | p_value   |
|:----------------------------------------------|:-----------------------------------------------------------|-------:|------:|--------------:|:----------|
| H3_OLS_log1p_post_x_rurality_cluster_operator | Intercept                                                  |  1.594 | 0.355 |   4.497       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(rurality_3)[T.Suburban]                                  |  0.055 | 0.089 |   0.615       | 0.539     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(rurality_3)[T.Urban]                                     |  0.002 | 0.032 |   0.065       | 0.948     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(county_norm)[T.RIO BLANCO]                               |  0.02  | 0.037 |   0.533       | 0.594     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(county_norm)[T.WELD]                                     | -0.617 | 0.358 |  -1.724       | 0.085     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.31 OPERATING]                                |  0.736 | 0.369 |   1.994       | 0.046     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.4-H OPERATING CORPORATION]                   |  0.947 | 0.115 |   8.215       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.8 NORTH LLC]                                 | -0.542 | 0.09  |  -6.033       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.AKA ENERGY GROUP LLC]                        | -0.009 | 0.048 |  -0.192       | 0.848     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.ANADARKO DJ GAS PROCESSING LLC]              |  0.405 | 0     |   6.21559e+12 | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.ANADARKO WATTENBERG OIL COMPLEX LLC]         | -0.093 | 0.045 |  -2.081       | 0.037     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.ANSCHUTZ EXPLORATION CORP]                   | -0.586 | 0.369 |  -1.59        | 0.112     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.BARGATH LLC]                                 | -1.048 | 0.356 |  -2.942       | 0.003     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.BARRETT CORPORATION* BILL]                   |  0.039 | 0.072 |   0.545       | 0.586     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.BARRETT RESOURCES CORP]                      |  0     | 0     |   0.339       | 0.735     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.BAYLESS PRODUCER, LLC* ROBERT L]             | -0.921 | 0.37  |  -2.49        | 0.013     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.BAYSWATER EXPLORATION & PRODUCTION LLC]      |  0.233 | 0.04  |   5.818       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.BAYSWATER EXPLORATION AND PRODUCTION LLC]    | -0.235 | 0.072 |  -3.273       | 0.001     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.BERRY PETROLEUM COMPANY LLC]                 | -0.481 | 0.354 |  -1.36        | 0.174     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.BISON IV OPERATING LLC]                      |  0.274 | 0.04  |   6.914       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.BISON OIL & GAS II LLC]                      | -0.024 | 0.041 |  -0.576       | 0.565     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.BLACK HILLS PLATEAU PRODUCTION LLC]          | -1.594 | 0.355 |  -4.497       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.BLUE CHIP OIL INC]                           |  1.577 | 0.103 |  15.3         | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.BNN WESTERN LLC]                             | -0.164 | 0.058 |  -2.806       | 0.005     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.BONANZA CREEK ENERGY OPERATING COMPANY LLC]  | -0.398 | 0.05  |  -8.032       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.CAERUS PICEANCE LLC]                         | -0.911 | 0.357 |  -2.548       | 0.011     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.CAPTIVA ENERGY PARTNERS LLC]                 |  0.409 | 0.062 |   6.615       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.CARRIZO NIOBRARA LLC]                        |  0.338 | 0.062 |   5.459       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.CCRP OPERATING INC]                          | -0.284 | 0.062 |  -4.59        | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.CHACO ENERGY COMPANY]                        |  3.868 | 0.159 |  24.392       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.CHEVRON PIPELINE COMPANY]                    | -0.228 | 0.37  |  -0.616       | 0.538     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.CHEVRON PRODUCTION COMPANY]                  | -1.199 | 0.37  |  -3.242       | 0.001     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.CHEVRON USA INC]                             | -0.574 | 0.369 |  -1.556       | 0.120     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.CIVITAS NORTH LLC]                           | -0.072 | 0.06  |  -1.206       | 0.228     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.COACHMAN ENERGY OPERATING COMPANY LLC]       |  0.622 | 0.37  |   1.68        | 0.093     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.COLORADO OIL & GAS CONSERVATION COMMISSION]  | -0.64  | 0.196 |  -3.26        | 0.001     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.COMPLETE ENERGY SERVICES INC]                |  0.119 | 0.069 |   1.729       | 0.084     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.CONFLUENCE DJ LLC]                           | -0.286 | 0.069 |  -4.14        | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.CRESTONE PEAK RESOURCES OPERATING LLC]       | -0.245 | 0.073 |  -3.334       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.CUB CREEK ENERGY]                            | -0.396 | 0.034 | -11.616       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.CUB CREEK ENERGY LLC]                        |  0.115 | 0.032 |   3.633       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.DAN A HUGHES COMPANY LP]                     |  0.122 | 0.062 |   1.964       | 0.049     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.DCP MIDSTREAM LP]                            | -0.131 | 0.072 |  -1.812       | 0.070     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.DCP OPERATING COMPANY LP]                    | -0.063 | 0.042 |  -1.509       | 0.131     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.DIAMOND OPERATING INC]                       |  0.275 | 0.04  |   6.935       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.EDGE ENERGY II LLC]                          |  0.782 | 0.05  |  15.624       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.ENCANA OIL & GAS (USA) INC]                  | -0.711 | 0.294 |  -2.413       | 0.016     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.ENERPLUS RESOURCES (USA) CORPORATION]        | -0.114 | 0.06  |  -1.909       | 0.056     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.EOG RESOURCES INC]                           | -0.259 | 0.059 |  -4.369       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.EWS 13 DJ BASIN LLC]                         | -0.071 | 0.138 |  -0.511       | 0.609     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.EWS 4 DJ BASIN LLC]                          |  1.218 | 0.069 |  17.629       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.EXPEDITION WATER SOLUTIONS COLORADO LLC]     | -0.979 | 0.069 | -14.172       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.EXTRACTION OIL & GAS INC]                    | -0.253 | 0.05  |  -5.082       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.EXTRACTION OIL & GAS LLC]                    | -0.187 | 0.082 |  -2.29        | 0.022     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.FIFTH CREEK ENERGY OPERATING COMPANY LLC]    | -0.083 | 0.062 |  -1.348       | 0.178     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.FOUNDATION ENERGY MANAGEMENT LLC]            |  0.04  | 0.081 |   0.497       | 0.619     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.FRITZLER RESOURCES INC]                      |  3.381 | 0.04  |  85.341       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.FUNDARE RESOURCES OPERATING COMPANY LLC]     | -0.098 | 0.045 |  -2.158       | 0.031     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.GADECO LLC]                                  |  0.711 | 0.111 |   6.408       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.GENESIS GAS & OIL COLORADO LLC]              |  1.279 | 0.369 |   3.465       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.GRAND RIVER GATHERING LLC]                   | -0.77  | 0.358 |  -2.148       | 0.032     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.GREAT WESTERN OPERATING COMPANY LLC]         | -0.011 | 0.063 |  -0.172       | 0.864     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.GRIZZLY OPERATING LLC]                       | -0.394 | 0.359 |  -1.096       | 0.273     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.GRYNBERG* JACK DBA GRYNBERG PETROLEUM CO]    |  0.348 | 0.111 |   3.141       | 0.002     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.HIGHPOINT ENERGY LLC]                        | -0.979 | 0.069 | -14.172       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.HIGHPOINT OPERATING CORPORATION]             | -0.389 | 0.044 |  -8.846       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.HRM RESOURCES II LLC]                        | -0.979 | 0.069 | -14.172       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.HUNTER RIDGE ENERGY SERVICES LLC]            | -0.198 | 0.357 |  -0.554       | 0.579     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.HYNDREX RESOURCES]                           |  0.119 | 0.069 |   1.729       | 0.084     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.INDUSTRIAL GAS SERVICES INC]                 |  0.715 | 0.159 |   4.509       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.K P KAUFFMAN COMPANY INC]                    | -0.332 | 0.082 |  -4.054       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.KERR MCGEE GATHERING LLC]                    | -0.144 | 0.046 |  -3.164       | 0.002     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.KERR MCGEE OIL & GAS ONSHORE LP]             | -0.477 | 0.094 |  -5.063       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.KOCH EXPLORATION COMPANY LLC]                |  1.31  | 0.379 |   3.461       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.KOCH EXPLORATION COMPANY, LLC]               |  0.653 | 0.372 |   1.756       | 0.079     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.KP KAUFFMAN COMPANY INC]                     |  0.187 | 0.03  |   6.263       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.KT RESOURCES LLC]                            | -0.768 | 0.369 |  -2.079       | 0.038     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.LARAMIE ENERGY LLC]                          | -0.548 | 0.355 |  -1.545       | 0.122     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.LASSO OIL & GAS LLC]                         |  1.484 | 0.369 |   4.018       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.LINN OPERATING INC]                          | -0.521 | 0.355 |  -1.469       | 0.142     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.LINN OPERATING LLC]                          | -1.248 | 0.355 |  -3.52        | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.LONGS PEAK RESOURCES LLC]                    | -0.273 | 0.039 |  -7.004       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.MACHII-ROSS PETROLEUM CO]                    |  1.773 | 0.115 |  15.389       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.MAGPIE OPERATING INC]                        |  4.852 | 0.159 |  30.598       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.MARALEX RESOURCES, INC]                      | -0.901 | 0.355 |  -2.542       | 0.011     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.MARATHON OIL COMPANY]                        | -1.045 | 0.355 |  -2.948       | 0.003     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.MARKUS PRODUCTION, INC]                      | -0.894 | 0.159 |  -5.641       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.MDS ENERGY DEVELOPMENT LLC]                  | -0.824 | 0.04  | -20.796       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.MERRION OIL & GAS CORP]                      |  0.784 | 0.37  |   2.119       | 0.034     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.MONAHAN GAS & OIL INC]                       |  1.793 | 0.069 |  25.956       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.MUSTANG RESOURCES LLC]                       | -1.187 | 0.372 |  -3.194       | 0.001     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.NGL WATER SOLUTIONS DJ LLC]                  | -0.253 | 0.044 |  -5.801       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.NICKEL ROAD OPERATING LLC]                   | -0.057 | 0.009 |  -6.347       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.NOBLE ENERGY INC]                            | -0.269 | 0.107 |  -2.511       | 0.012     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.NOBLE MIDSTREAM SERVICES LLC]                |  0.072 | 0.029 |   2.493       | 0.013     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.NORTHSTAR GAS COMPANY INC]                   |  0.332 | 0.37  |   0.897       | 0.370     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.O'BRIEN ENERGY RESOURCES CORP]               | -0.979 | 0.069 | -14.172       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.OXY USA INC]                                 |  0.015 | 0.355 |   0.042       | 0.966     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.OXY USA WTP LP]                              | -0.898 | 0.355 |  -2.532       | 0.011     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.PAINTED PEGASUS PETROLEUM LLC]               |  1.953 | 0.142 |  13.74        | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.PDC ENERGY INC]                              | -0.119 | 0.088 |  -1.349       | 0.177     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.PETERSON ENERGY OPERATING INC]               |  0.34  | 0.122 |   2.786       | 0.005     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.PETRO MEX RESOURCES]                         |  0.889 | 0.358 |   2.485       | 0.013     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.PETRO OPERATING COMPANY LLC]                 |  0.828 | 0.067 |  12.422       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.PETROSHARE CORPORATION]                      |  0.387 | 0.115 |   3.359       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.PLUG NICKEL OIL COMPANY INC]                 | -0.515 | 0.37  |  -1.394       | 0.163     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.PRAIRIE OPERATING CO LLC]                    |  0.439 | 0     |   6.18579e+12 | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.PROVIDENCE OPERATING LLC DBA POCO OPERATING] | -0.173 | 0     |  -2.47706e+12 | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.RED HAWK PETROLEUM LLC]                      |  0.164 | 0.04  |   4.129       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.RED ROCK GATHERING COMPANY LLC]              | -0.778 | 0.364 |  -2.14        | 0.032     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.REP PROCESSING LLC]                          |  0.562 | 0.04  |  14.197       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.RIO MESA RESOURCES INC]                      |  0.619 | 0.369 |   1.675       | 0.094     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.ROBERT L BAYLESS PRODUCER LLC]               | -0.075 | 0.369 |  -0.202       | 0.840     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.ROCKY MOUNTAIN MIDSTREAM LLC]                |  0.289 | 0.035 |   8.359       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.ROCKY MOUNTAIN NATURAL GAS LLC]              |  1.025 | 0.37  |   2.771       | 0.006     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.RWL ENTERPRISES]                             |  1.328 | 0.115 |  11.528       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.SAMSON RESOURCES COMPANY]                    |  0.158 | 0.379 |   0.416       | 0.677     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.SCHNEIDER ENERGY SERVICES INC]               | -0.548 | 0.159 |  -3.456       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.SCOUT ENERGY MANAGEMENT LLC]                 | -0.759 | 0.369 |  -2.059       | 0.039     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.SMITH ENERGY CORP]                           |  0.596 | 0.15  |   3.97        | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.SMITH OIL PROPERTIES INC]                    |  2.584 | 0.115 |  22.426       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.SRC ENERGY INC]                              | -0.22  | 0.086 |  -2.568       | 0.010     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.SUMMIT DJ-S LLC]                             |  4.856 | 0.04  | 122.586       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.SUMMIT MIDSTREAM NIOBRARA LLC]               | -0.284 | 0.062 |  -4.59        | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.SUMMIT MIDSTREAM PARTNERS LLC]               | -0.651 | 0.358 |  -1.816       | 0.069     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.SYNERGY RESOURCES CORPORATION]               |  0.162 | 0.095 |   1.707       | 0.088     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.TALLGRASS WATER WESTERN LLC]                 | -0.279 | 0.04  |  -7.049       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.TAPROOT ROCKIES MIDSTREAM LLC]               | -0.377 | 0.04  |  -9.521       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.TEP ROCKY MOUNTAIN LLC]                      | -0.781 | 0.359 |  -2.175       | 0.030     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.TEXAS TEA OF COLORADO LLC DBA TEXAS TEA LLC] | -0.071 | 0.138 |  -0.511       | 0.609     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.TINDALL OPERATING COMPANY]                   | -0.201 | 0.159 |  -1.27        | 0.204     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.TOP OPERATING COMPANY]                       |  0.284 | 0.141 |   2.011       | 0.044     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.UPLAND EXPLORATION LLC]                      |  2.434 | 0.04  |  61.446       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.URSA OPERATING COMPANY LLC]                  | -0.629 | 0.363 |  -1.734       | 0.083     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.UTAH GAS OP LTD DBA UTAH GAS CORP]           |  0.207 | 0.371 |   0.56        | 0.576     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.VANGUARD OPERATING LLC]                      | -0.527 | 0.339 |  -1.558       | 0.119     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.VERDAD OIL & GAS CORPORATION]                | -0.286 | 0.069 |  -4.14        | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.VERDAD RESOURCES LLC]                        | -0.325 | 0.04  |  -8.071       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.VISION ENERGY LLC]                           |  0.858 | 0.361 |   2.377       | 0.017     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.WARD PETROLEUM CORPORATION]                  | -0.429 | 0.064 |  -6.745       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.WEXPRO COMPANY]                              |  0.668 | 0.379 |   1.766       | 0.077     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.WHITING OIL & GAS CORPORATION]               | -0.424 | 0.059 |  -7.156       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.WINDSOR ENERGY GROUP LLC]                    |  2.356 | 0.37  |   6.371       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.WOODARD* SANDRA K]                           | -0.921 | 0.37  |  -2.49        | 0.013     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.WPX ENERGY ROCKY MOUNTAIN LLC]               | -1.364 | 0.358 |  -3.808       | <0.001    |
| H3_OLS_log1p_post_x_rurality_cluster_operator | C(operator)[T.XTO ENERGY INC]                              | -0.735 | 0.369 |  -1.991       | 0.047     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | post                                                       | -0.153 | 0.057 |  -2.694       | 0.007     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | post:C(rurality_3)[T.Suburban]                             | -0.156 | 0.105 |  -1.488       | 0.137     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | post:C(rurality_3)[T.Urban]                                | -0.133 | 0.057 |  -2.338       | 0.019     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | historical                                                 |  0.02  | 0.085 |   0.234       | 0.815     |
| H3_OLS_log1p_post_x_rurality_cluster_operator | post:historical                                            |  0.051 | 0.085 |   0.592       | 0.554     |
Joint test post×rurality (F): F=3.278, df=(2, 141), p=0.0405981; terms=['post:C(rurality_3)[T.Suburban]', 'post:C(rurality_3)[T.Urban]']

late90 model formula used: `late90 ~ post + historical + post:historical + C(rurality_3) + post:C(rurality_3) + C(county_top3)`

| model                           | term                           |   log_odds |    se |   odds_ratio |   or_ci95_lo |   or_ci95_hi | p_value   |
|:--------------------------------|:-------------------------------|-----------:|------:|-------------:|-------------:|-------------:|:----------|
| H3_logit_late90_post_x_rurality | Intercept                      |     -9.389 | 1.257 |        0     |        0     |        0.001 | <0.001    |
| H3_logit_late90_post_x_rurality | C(rurality_3)[T.Suburban]      |      0.527 | 1.256 |        1.693 |        0.144 |       19.856 | 0.675     |
| H3_logit_late90_post_x_rurality | C(rurality_3)[T.Urban]         |      0.209 | 0.866 |        1.232 |        0.226 |        6.73  | 0.810     |
| H3_logit_late90_post_x_rurality | C(county_top3)[T.RIO BLANCO]   |      2.092 | 0.936 |        8.098 |        1.293 |       50.711 | 0.025     |
| H3_logit_late90_post_x_rurality | C(county_top3)[T.WELD]         |      0.889 | 0.932 |        2.432 |        0.392 |       15.103 | 0.340     |
| H3_logit_late90_post_x_rurality | post                           |      2.993 | 1.088 |       19.94  |        2.366 |      168.077 | 0.006     |
| H3_logit_late90_post_x_rurality | post:C(rurality_3)[T.Suburban] |     -0.442 | 1.039 |        0.643 |        0.084 |        4.92  | 0.670     |
| H3_logit_late90_post_x_rurality | post:C(rurality_3)[T.Urban]    |     -0.767 | 0.937 |        0.465 |        0.074 |        2.914 | 0.413     |
| H3_logit_late90_post_x_rurality | historical                     |      3.4   | 1.466 |       29.951 |        1.694 |      529.644 | 0.020     |
| H3_logit_late90_post_x_rurality | post:historical                |     -1.522 | 1.456 |        0.218 |        0.013 |        3.783 | 0.296     |
Joint test post×rurality (χ²): chi2=0.685, df=2, p=0.709937; terms=['post:C(rurality_3)[T.Suburban]', 'post:C(rurality_3)[T.Urban]']

### Rurality gradient (Recent spills only; model-implied median delay = exp(lp)-1)

| rurality_3   | period    |   P_any_delay |   median_delay_implied |   P_late30 |   P_late90 |
|:-------------|:----------|--------------:|-----------------------:|-----------:|-----------:|
| Rural        | pre_2020  |      0.757073 |                  1.47  |   0.005869 |   0.000344 |
| Rural        | post_2020 |      0.645204 |                  1.119 |   0.012055 |   0.005139 |
| Suburban     | pre_2020  |      0.71421  |                  1.544 |   0.002721 |   0.000188 |
| Suburban     | post_2020 |      0.540791 |                  0.867 |   0.005649 |   0.002819 |
| Urban        | pre_2020  |      0.735393 |                  1.216 |   0.002262 |   0.000167 |
| Urban        | post_2020 |      0.536487 |                  0.664 |   0.004697 |   0.002508 |



## Extreme tail (>=99 days): rare-events strategy

Used ridge (L2) logistic regression with CV on C, class_weight='balanced'.

|   chosen_C |   event_rate |     n |
|-----------:|-------------:|------:|
|  0.0123285 |   0.00712769 | 26376 |

Stable predicted probabilities (marginal standardized) and pre/post risk ratios:

| spill_type   |    p_pre |   p_post |   risk_ratio |   risk_diff |
|:-------------|---------:|---------:|-------------:|------------:|
| Recent       | 0.095476 | 0.302575 |      3.16912 |    0.207099 |
| Historical   | 0.374337 | 0.706926 |      1.88848 |    0.332589 |



## Operator + geography variation (Aim 3 deliverables)

### Operators (min n>=50): adjusted predicted probabilities

Top/bottom 15 for late30 and any_delay saved as CSVs under `step2_model_outputs/operator_adjusted/`.

### Counties (min n>=50): adjusted predicted P(late30) and P(late90)

| county_norm   |   n_total |   p_late30_adj |   p_late90_adj |
|:--------------|----------:|---------------:|---------------:|
| RIO BLANCO    |      2024 |          4.349 |          1.284 |
| WELD          |     20874 |          1.456 |          0.805 |
| GARFIELD      |      3478 |          0.575 |          0.171 |

Choropleth map skipped (no county geometry join detected in this notebook).



## Robustness set (must include)

### Continuous model (cluster by operator): compare key terms

| variant           |   post |   post_se |   post:historical |   int_se |
|:------------------|-------:|----------:|------------------:|---------:|
| baseline          | -0.22  |     0.06  |             0.008 |    0.081 |
| cap180            | -0.22  |     0.06  |             0.006 |    0.08  |
| exclude_extreme99 | -0.232 |     0.062 |            -0.037 |    0.075 |

### Key logit (late30): compare key terms

| variant                                              |   post |   post_se |   post:historical |   int_se |
|:-----------------------------------------------------|-------:|----------:|------------------:|---------:|
| baseline                                             |  0.733 |     0.471 |            -0.256 |    0.528 |
| cap180 (affects DV only via delay; late30 unchanged) |  0.733 |     0.471 |            -0.256 |    0.528 |
| exclude_extreme99                                    |  0.147 |     0.633 |            -0.153 |    0.767 |



## Outputs

- Report: `/home/dadams/Repos/colorado_redux/step2_final_models.md`

- Plots/tables: `/home/dadams/Repos/colorado_redux/analysis_postgis/step2_model_outputs`
