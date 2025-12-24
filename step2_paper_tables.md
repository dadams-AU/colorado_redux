# Paper Tables (journal-ready markdown)

Source folder (CSVs): `/home/dadams/Repos/colorado_redux/analysis_postgis/step2_model_outputs`
Generated: `/home/dadams/Repos/colorado_redux/step2_paper_tables.md`

Notes: p-values and 95% confidence intervals shown; no significance stars.

## Table D1: Traditional descriptives

(Delay is in days; cells report mean (SD) and median [IQR]. Percentages are percent of spills in group.)

### Table D1-A: Delay descriptives by period

| period | n | pct_historical | mean (SD) | median [IQR] | pct_delay_0 | pct_delay_le1 | pct_any_delay | pct_late30 | pct_late90 | pct_ge99 | n_operators | n_counties | n_rurality |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| post_2020 | 15704 | 47.87 | 3.93 (30.82) | 1 [0, 1] | 48.92 | 81.58 | 51.08 | 1.92 | 1.08 | 1.06 | 86 | 3 | 3 |
| pre_2020 | 10672 | 35.38 | 2.50 (12.39) | 1 [0, 2] | 26.99 | 66.06 | 73.01 | 1.03 | 0.28 | 0.21 | 102 | 3 | 3 |

### Table D1-B: Delay descriptives by spill type × period

| spill_type | period | n | mean (SD) | median [IQR] | pct_delay_0 | pct_delay_le1 | pct_any_delay | pct_late30 | pct_late90 | pct_ge99 | n_operators | n_counties | n_rurality |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Historical | post_2020 | 7518 | 5.56 (35.23) | 0 [0, 1] | 57.99 | 85.50 | 42.01 | 3.17 | 1.86 | 1.81 | 46 | 3 | 3 |
| Historical | pre_2020 | 3776 | 3.59 (19.93) | 1 [0, 2] | 30.30 | 69.39 | 69.70 | 2.01 | 0.74 | 0.58 | 46 | 3 | 3 |
| Recent | post_2020 | 8186 | 2.42 (26.05) | 1 [0, 1] | 40.58 | 77.99 | 59.42 | 0.78 | 0.37 | 0.37 | 71 | 3 | 3 |
| Recent | pre_2020 | 6896 | 1.90 (4.40) | 1 [0, 2] | 25.17 | 64.24 | 74.83 | 0.49 | 0.03 | 0.00 | 90 | 3 | 3 |

## Claim 1: Post-2020 shifts spill composition toward inspection-identified (Historical) spills

### Table H1-A: Descriptive mix by period

| period | n_total | pct_historical |
| --- | --- | --- |
| post_2020 | 15704 | 47.9 |
| pre_2020 | 10672 | 35.4 |

### Table H1-B: Spill-level logit (full model terms) + predicted pct_historical

**Panel 1: Logit ORs (full model)**

| Term | OR [95% CI] | p |
| --- | --- | --- |
| Intercept | 0.061 [0.053, 0.070] | <0.001 |
| C[county_norm](T.RIO BLANCO) | 2.024 [1.688, 2.428] | <0.001 |
| C[county_norm](T.WELD) | 4.733 [4.148, 5.400] | <0.001 |
| C[rurality_3](T.Suburban) | 2.077 [1.840, 2.345] | <0.001 |
| C[rurality_3](T.Urban) | 4.138 [3.878, 4.414] | <0.001 |
| Post | 1.647 [1.557, 1.743] | <0.001 |

Fit stats:

| Model | N | AIC | BIC | LogLik | Pseudo R2 |
| --- | --- | --- | --- | --- | --- |
| H1 logit | 26376 | 30443.305 | 30492.387 | -15215.653 | 0.155 |

**Panel 2: Model-implied pct_historical (marginal)**

| period | pred_pct_historical |
| --- | --- |
| pre_2020 | 36.8 |
| post_2020 | 46.8 |

### Table H1-C (Appendix): Operator FE LPM (full model terms)

| Term | Estimate [95% CI] | p |
| --- | --- | --- |
| Intercept | -0.055 [-0.408, 0.298] | 0.759 |
| C[county_norm](T.RIO BLANCO) | 0.088 [0.023, 0.153] | 0.007 |
| C[county_norm](T.WELD) | -0.184 [-0.519, 0.151] | 0.281 |
| C[rurality_3](T.Suburban) | 0.125 [0.058, 0.192] | <0.001 |
| C[rurality_3](T.Urban) | 0.133 [0.072, 0.194] | <0.001 |
| C[operator](T.31 OPERATING) | -0.140 [-0.493, 0.213] | 0.437 |
| C[operator](T.4-H OPERATING CORPORATION) | 1.107 [1.044, 1.170] | <0.001 |
| C[operator](T.8 NORTH LLC) | 0.620 [0.544, 0.696] | <0.001 |
| C[operator](T.AKA ENERGY GROUP LLC) | 0.075 [0.032, 0.118] | <0.001 |
| C[operator](T.ANADARKO DJ GAS PROCESSING LLC) | -0.000 [-0.000, 0.000] | 0.992 |
| C[operator](T.ANADARKO WATTENBERG OIL COMPLEX LLC) | 0.094 [0.045, 0.143] | <0.001 |
| C[operator](T.ANSCHUTZ EXPLORATION CORP) | -0.040 [-0.393, 0.313] | 0.825 |
| C[operator](T.BARGATH LLC) | 0.220 [-0.121, 0.561] | 0.205 |
| C[operator](T.BARRETT CORPORATION* BILL) | 0.559 [0.463, 0.655] | <0.001 |
| C[operator](T.BARRETT RESOURCES CORP) | -0.000 [-0.000, 0.000] | 0.966 |
| C[operator](T.BAYLESS PRODUCER, LLC* ROBERT L) | -0.033 [-0.398, 0.332] | 0.859 |
| C[operator](T.BAYSWATER EXPLORATION & PRODUCTION LLC) | 0.229 [0.202, 0.256] | <0.001 |
| C[operator](T.BAYSWATER EXPLORATION AND PRODUCTION LLC) | 0.489 [0.403, 0.575] | <0.001 |
| C[operator](T.BERRY PETROLEUM COMPANY LLC) | 0.012 [-0.333, 0.357] | 0.947 |
| C[operator](T.BISON IV OPERATING LLC) | 0.133 [0.072, 0.194] | <0.001 |
| C[operator](T.BISON OIL & GAS II LLC) | 0.174 [0.096, 0.252] | <0.001 |
| C[operator](T.BLACK HILLS PLATEAU PRODUCTION LLC) | 0.055 [-0.298, 0.408] | 0.759 |
| C[operator](T.BLUE CHIP OIL INC) | 1.005 [0.940, 1.070] | <0.001 |
| C[operator](T.BNN WESTERN LLC) | 0.231 [0.123, 0.339] | <0.001 |
| C[operator](T.BONANZA CREEK ENERGY OPERATING COMPANY LLC) | 0.289 [0.216, 0.362] | <0.001 |
| C[operator](T.CAERUS PICEANCE LLC) | 0.062 [-0.277, 0.401] | 0.722 |
| C[operator](T.CAPTIVA ENERGY PARTNERS LLC) | 0.240 [0.128, 0.352] | <0.001 |
| C[operator](T.CARRIZO NIOBRARA LLC) | 0.240 [0.128, 0.352] | <0.001 |
| C[operator](T.CCRP OPERATING INC) | 0.240 [0.128, 0.352] | <0.001 |
| C[operator](T.CHACO ENERGY COMPANY) | 1.133 [1.072, 1.194] | <0.001 |
| C[operator](T.CHEVRON PIPELINE COMPANY) | -0.033 [-0.398, 0.332] | 0.859 |
| C[operator](T.CHEVRON PRODUCTION COMPANY) | -0.033 [-0.398, 0.332] | 0.859 |
| C[operator](T.CHEVRON USA INC) | 0.028 [-0.333, 0.389] | 0.880 |
| C[operator](T.CIVITAS NORTH LLC) | 0.360 [0.299, 0.421] | <0.001 |
| C[operator](T.COACHMAN ENERGY OPERATING COMPANY LLC) | -0.070 [-0.411, 0.271] | 0.686 |
| C[operator](T.COLORADO OIL & GAS CONSERVATION COMMISSION) | 0.483 [0.301, 0.665] | <0.001 |
| C[operator](T.COMPLETE ENERGY SERVICES INC) | 0.107 [0.044, 0.170] | <0.001 |
| C[operator](T.CONFLUENCE DJ LLC) | 0.107 [0.044, 0.170] | <0.001 |
| C[operator](T.CRESTONE PEAK RESOURCES OPERATING LLC) | 0.525 [0.503, 0.547] | <0.001 |
| C[operator](T.CUB CREEK ENERGY) | 0.086 [0.047, 0.125] | <0.001 |
| C[operator](T.CUB CREEK ENERGY LLC) | 0.106 [0.059, 0.153] | <0.001 |
| C[operator](T.DAN A HUGHES COMPANY LP) | 0.240 [0.128, 0.352] | <0.001 |
| C[operator](T.DCP MIDSTREAM LP) | 0.291 [0.222, 0.360] | <0.001 |
| C[operator](T.DCP OPERATING COMPANY LP) | 0.281 [0.254, 0.308] | <0.001 |
| C[operator](T.DIAMOND OPERATING INC) | 0.133 [0.072, 0.194] | <0.001 |
| C[operator](T.EDGE ENERGY II LLC) | 0.333 [0.296, 0.370] | <0.001 |
| C[operator](T.ENCANA OIL & GAS (USA) INC) | 0.109 [-0.177, 0.395] | 0.457 |
| C[operator](T.ENERPLUS RESOURCES (USA) CORPORATION) | 0.092 [0.037, 0.147] | <0.001 |
| C[operator](T.EOG RESOURCES INC) | 0.233 [0.125, 0.341] | <0.001 |
| C[operator](T.EWS 13 DJ BASIN LLC) | 1.000 [1.000, 1.000] | <0.001 |
| C[operator](T.EWS 4 DJ BASIN LLC) | 0.107 [0.044, 0.170] | <0.001 |
| C[operator](T.EXPEDITION WATER SOLUTIONS COLORADO LLC) | 0.107 [0.044, 0.170] | <0.001 |
| C[operator](T.EXTRACTION OIL & GAS INC) | 0.392 [0.365, 0.419] | <0.001 |
| C[operator](T.EXTRACTION OIL & GAS LLC) | 0.441 [0.374, 0.508] | <0.001 |
| C[operator](T.FIFTH CREEK ENERGY OPERATING COMPANY LLC) | 0.240 [0.128, 0.352] | <0.001 |
| C[operator](T.FOUNDATION ENERGY MANAGEMENT LLC) | 0.274 [0.164, 0.384] | <0.001 |
| C[operator](T.FRITZLER RESOURCES INC) | 0.133 [0.072, 0.194] | <0.001 |
| C[operator](T.FUNDARE RESOURCES OPERATING COMPANY LLC) | 0.215 [0.154, 0.276] | <0.001 |
| C[operator](T.GADECO LLC) | 1.240 [1.128, 1.352] | <0.001 |
| C[operator](T.GENESIS GAS & OIL COLORADO LLC) | -0.140 [-0.493, 0.213] | 0.437 |
| C[operator](T.GRAND RIVER GATHERING LLC) | -0.140 [-0.475, 0.195] | 0.413 |
| C[operator](T.GREAT WESTERN OPERATING COMPANY LLC) | 0.401 [0.356, 0.446] | <0.001 |
| C[operator](T.GRIZZLY OPERATING LLC) | -0.162 [-0.497, 0.173] | 0.344 |
| C[operator](T.GRYNBERG* JACK DBA GRYNBERG PETROLEUM CO) | 1.240 [1.128, 1.352] | <0.001 |
| C[operator](T.HIGHPOINT ENERGY LLC) | 0.107 [0.044, 0.170] | <0.001 |
| C[operator](T.HIGHPOINT OPERATING CORPORATION) | 0.243 [0.178, 0.308] | <0.001 |
| C[operator](T.HRM RESOURCES II LLC) | 0.107 [0.044, 0.170] | <0.001 |
| C[operator](T.HUNTER RIDGE ENERGY SERVICES LLC) | -0.007 [-0.356, 0.342] | 0.969 |
| C[operator](T.HYNDREX RESOURCES) | 0.107 [0.044, 0.170] | <0.001 |
| C[operator](T.INDUSTRIAL GAS SERVICES INC) | 1.133 [1.072, 1.194] | <0.001 |
| C[operator](T.K P KAUFFMAN COMPANY INC) | 0.447 [0.373, 0.521] | <0.001 |
| C[operator](T.KERR MCGEE GATHERING LLC) | 0.290 [0.255, 0.325] | <0.001 |
| C[operator](T.KERR MCGEE OIL & GAS ONSHORE LP) | 0.722 [0.697, 0.747] | <0.001 |
| C[operator](T.KOCH EXPLORATION COMPANY LLC) | 0.967 [0.602, 1.332] | <0.001 |
| C[operator](T.KOCH EXPLORATION COMPANY, LLC) | 0.467 [0.102, 0.832] | 0.012 |
| C[operator](T.KP KAUFFMAN COMPANY INC) | 0.179 [0.154, 0.204] | <0.001 |
| C[operator](T.KT RESOURCES LLC) | -0.140 [-0.493, 0.213] | 0.437 |
| C[operator](T.LARAMIE ENERGY LLC) | 0.056 [-0.289, 0.401] | 0.749 |
| C[operator](T.LASSO OIL & GAS LLC) | -0.140 [-0.493, 0.213] | 0.437 |
| C[operator](T.LINN OPERATING INC) | 0.055 [-0.298, 0.408] | 0.759 |
| C[operator](T.LINN OPERATING LLC) | 0.055 [-0.298, 0.408] | 0.759 |
| C[operator](T.LONGS PEAK RESOURCES LLC) | 0.158 [0.087, 0.229] | <0.001 |
| C[operator](T.MACHII-ROSS PETROLEUM CO) | 1.107 [1.044, 1.170] | <0.001 |
| C[operator](T.MAGPIE OPERATING INC) | 1.133 [1.072, 1.194] | <0.001 |
| C[operator](T.MARALEX RESOURCES, INC) | 0.055 [-0.298, 0.408] | 0.759 |
| C[operator](T.MARATHON OIL COMPANY) | 0.055 [-0.298, 0.408] | 0.759 |
| C[operator](T.MARKUS PRODUCTION, INC) | 1.133 [1.072, 1.194] | <0.001 |
| C[operator](T.MDS ENERGY DEVELOPMENT LLC) | 0.133 [0.072, 0.194] | <0.001 |
| C[operator](T.MERRION OIL & GAS CORP) | -0.033 [-0.398, 0.332] | 0.859 |
| C[operator](T.MONAHAN GAS & OIL INC) | 0.107 [0.044, 0.170] | <0.001 |
| C[operator](T.MUSTANG RESOURCES LLC) | 0.358 [0.017, 0.699] | 0.039 |
| C[operator](T.NGL WATER SOLUTIONS DJ LLC) | 0.147 [0.078, 0.216] | <0.001 |
| C[operator](T.NICKEL ROAD OPERATING LLC) | 0.014 [0.006, 0.022] | <0.001 |
| C[operator](T.NOBLE ENERGY INC) | 0.851 [0.818, 0.884] | <0.001 |
| C[operator](T.NOBLE MIDSTREAM SERVICES LLC) | 0.099 [0.054, 0.144] | <0.001 |
| C[operator](T.NORTHSTAR GAS COMPANY INC) | -0.033 [-0.398, 0.332] | 0.859 |
| C[operator](T.O'BRIEN ENERGY RESOURCES CORP) | 0.107 [0.044, 0.170] | <0.001 |
| C[operator](T.OXY USA INC) | 0.055 [-0.298, 0.408] | 0.759 |
| C[operator](T.OXY USA WTP LP) | 0.055 [-0.298, 0.408] | 0.759 |
| C[operator](T.PAINTED PEGASUS PETROLEUM LLC) | 1.007 [0.942, 1.072] | <0.001 |
| C[operator](T.PDC ENERGY INC) | 0.680 [0.649, 0.711] | <0.001 |
| C[operator](T.PETERSON ENERGY OPERATING INC) | 1.076 [1.033, 1.119] | <0.001 |
| C[operator](T.PETRO MEX RESOURCES) | 0.234 [-0.105, 0.573] | 0.175 |
| C[operator](T.PETRO OPERATING COMPANY LLC) | 0.481 [0.465, 0.497] | <0.001 |
| C[operator](T.PETROSHARE CORPORATION) | 1.107 [1.044, 1.170] | <0.001 |
| C[operator](T.PLUG NICKEL OIL COMPANY INC) | -0.033 [-0.398, 0.332] | 0.859 |
| C[operator](T.PRAIRIE OPERATING CO LLC) | -0.000 [-0.000, 0.000] | 0.922 |
| C[operator](T.PROVIDENCE OPERATING LLC DBA POCO OPERATING) | -0.000 [-0.000, 0.000] | 0.947 |
| C[operator](T.RED HAWK PETROLEUM LLC) | 0.167 [0.093, 0.241] | <0.001 |
| C[operator](T.RED ROCK GATHERING COMPANY LLC) | 0.202 [-0.157, 0.561] | 0.270 |
| C[operator](T.REP PROCESSING LLC) | 0.133 [0.072, 0.194] | <0.001 |
| C[operator](T.RIO MESA RESOURCES INC) | -0.140 [-0.493, 0.213] | 0.437 |
| C[operator](T.ROBERT L BAYLESS PRODUCER LLC) | -0.140 [-0.493, 0.213] | 0.437 |
| C[operator](T.ROCKY MOUNTAIN MIDSTREAM LLC) | 0.053 [0.022, 0.084] | <0.001 |
| C[operator](T.ROCKY MOUNTAIN NATURAL GAS LLC) | -0.033 [-0.398, 0.332] | 0.859 |
| C[operator](T.RWL ENTERPRISES) | 1.107 [1.044, 1.170] | <0.001 |
| C[operator](T.SAMSON RESOURCES COMPANY) | 0.967 [0.602, 1.332] | <0.001 |
| C[operator](T.SCHNEIDER ENERGY SERVICES INC) | 1.133 [1.072, 1.194] | <0.001 |
| C[operator](T.SCOUT ENERGY MANAGEMENT LLC) | -0.090 [-0.443, 0.263] | 0.618 |
| C[operator](T.SMITH ENERGY CORP) | 1.085 [1.048, 1.122] | <0.001 |
| C[operator](T.SMITH OIL PROPERTIES INC) | 1.107 [1.044, 1.170] | <0.001 |
| C[operator](T.SRC ENERGY INC) | 0.691 [0.620, 0.762] | <0.001 |
| C[operator](T.SUMMIT DJ-S LLC) | 0.133 [0.072, 0.194] | <0.001 |
| C[operator](T.SUMMIT MIDSTREAM NIOBRARA LLC) | 0.240 [0.128, 0.352] | <0.001 |
| C[operator](T.SUMMIT MIDSTREAM PARTNERS LLC) | -0.126 [-0.461, 0.209] | 0.463 |
| C[operator](T.SYNERGY RESOURCES CORPORATION) | 0.831 [0.760, 0.902] | <0.001 |
| C[operator](T.TALLGRASS WATER WESTERN LLC) | 0.133 [0.072, 0.194] | <0.001 |
| C[operator](T.TAPROOT ROCKIES MIDSTREAM LLC) | 0.133 [0.072, 0.194] | <0.001 |
| C[operator](T.TEP ROCKY MOUNTAIN LLC) | 0.003 [-0.342, 0.348] | 0.988 |
| C[operator](T.TEXAS TEA OF COLORADO LLC DBA TEXAS TEA LLC) | 1.000 [1.000, 1.000] | <0.001 |
| C[operator](T.TINDALL OPERATING COMPANY) | 1.133 [1.072, 1.194] | <0.001 |
| C[operator](T.TOP OPERATING COMPANY) | 1.022 [1.012, 1.032] | <0.001 |
| C[operator](T.UPLAND EXPLORATION LLC) | 0.133 [0.072, 0.194] | <0.001 |
| C[operator](T.URSA OPERATING COMPANY LLC) | 0.196 [-0.155, 0.547] | 0.272 |
| C[operator](T.UTAH GAS OP LTD DBA UTAH GAS CORP) | 0.445 [0.092, 0.798] | 0.014 |
| C[operator](T.VANGUARD OPERATING LLC) | -0.014 [-0.326, 0.298] | 0.932 |
| C[operator](T.VERDAD OIL & GAS CORPORATION) | 0.107 [0.044, 0.170] | <0.001 |
| C[operator](T.VERDAD RESOURCES LLC) | 0.210 [0.159, 0.261] | <0.001 |
| C[operator](T.VISION ENERGY LLC) | -0.177 [-0.512, 0.158] | 0.301 |
| C[operator](T.WARD PETROLEUM CORPORATION) | 0.173 [0.087, 0.259] | <0.001 |
| C[operator](T.WEXPRO COMPANY) | 0.967 [0.602, 1.332] | <0.001 |
| C[operator](T.WHITING OIL & GAS CORPORATION) | 0.313 [0.209, 0.417] | <0.001 |
| C[operator](T.WINDSOR ENERGY GROUP LLC) | -0.033 [-0.398, 0.332] | 0.859 |
| C[operator](T.WOODARD* SANDRA K) | -0.033 [-0.398, 0.332] | 0.859 |
| C[operator](T.WPX ENERGY ROCKY MOUNTAIN LLC) | 0.180 [-0.167, 0.527] | 0.309 |
| C[operator](T.XTO ENERGY INC) | 0.000 [-0.363, 0.363] | 0.998 |
| Post | 0.107 [0.044, 0.170] | <0.001 |

Fit stats:

| Model | N | AIC | BIC | LogLik | R2 | Adj R2 |
| --- | --- | --- | --- | --- | --- | --- |
| H1 LPM | 26376 | 25247.181 | 26449.672 | -12476.590 | 0.384 | 0.381 |

Note: Standard errors are clustered by operator.

## Claim 2: Typical reporting timeliness improves post-2020

### Table H2-A: OLS on log(1+delay) (full model terms)

| Term | Estimate [95% CI] | p |
| --- | --- | --- |
| Intercept | 1.590 [0.880, 2.300] | <0.001 |
| C[county_norm](T.RIO BLANCO) | 0.024 [-0.049, 0.097] | 0.510 |
| C[county_norm](T.WELD) | -0.600 [-1.317, 0.117] | 0.102 |
| C[rurality_3](T.Suburban) | -0.039 [-0.104, 0.026] | 0.230 |
| C[rurality_3](T.Urban) | -0.077 [-0.124, -0.030] | 0.001 |
| C[operator](T.31 OPERATING) | 0.803 [0.062, 1.544] | 0.033 |
| C[operator](T.4-H OPERATING CORPORATION) | 0.990 [0.790, 1.190] | <0.001 |
| C[operator](T.8 NORTH LLC) | -0.503 [-0.660, -0.346] | <0.001 |
| C[operator](T.AKA ENERGY GROUP LLC) | 0.037 [-0.045, 0.119] | 0.380 |
| C[operator](T.ANADARKO DJ GAS PROCESSING LLC) | 0.405 [0.405, 0.405] | <0.001 |
| C[operator](T.ANADARKO WATTENBERG OIL COMPLEX LLC) | -0.052 [-0.126, 0.022] | 0.179 |
| C[operator](T.ANSCHUTZ EXPLORATION CORP) | -0.517 [-1.256, 0.222] | 0.170 |
| C[operator](T.BARGATH LLC) | -1.021 [-1.731, -0.311] | 0.005 |
| C[operator](T.BARRETT CORPORATION* BILL) | 0.041 [-0.098, 0.180] | 0.564 |
| C[operator](T.BARRETT RESOURCES CORP) | 0.000 [0.000, 0.000] | 0.960 |
| C[operator](T.BAYLESS PRODUCER, LLC* ROBERT L) | -0.921 [-1.666, -0.176] | 0.015 |
| C[operator](T.BAYSWATER EXPLORATION & PRODUCTION LLC) | 0.259 [0.192, 0.326] | <0.001 |
| C[operator](T.BAYSWATER EXPLORATION AND PRODUCTION LLC) | -0.216 [-0.347, -0.085] | 0.001 |
| C[operator](T.BERRY PETROLEUM COMPANY LLC) | -0.450 [-1.160, 0.260] | 0.214 |
| C[operator](T.BISON IV OPERATING LLC) | 0.328 [0.281, 0.375] | <0.001 |
| C[operator](T.BISON OIL & GAS II LLC) | 0.004 [-0.065, 0.073] | 0.898 |
| C[operator](T.BLACK HILLS PLATEAU PRODUCTION LLC) | -1.590 [-2.300, -0.880] | <0.001 |
| C[operator](T.BLUE CHIP OIL INC) | 1.599 [1.413, 1.785] | <0.001 |
| C[operator](T.BNN WESTERN LLC) | -0.171 [-0.294, -0.048] | 0.006 |
| C[operator](T.BONANZA CREEK ENERGY OPERATING COMPANY LLC) | -0.370 [-0.454, -0.286] | <0.001 |
| C[operator](T.CAERUS PICEANCE LLC) | -0.856 [-1.569, -0.143] | 0.019 |
| C[operator](T.CAPTIVA ENERGY PARTNERS LLC) | 0.396 [0.265, 0.527] | <0.001 |
| C[operator](T.CARRIZO NIOBRARA LLC) | 0.325 [0.194, 0.456] | <0.001 |
| C[operator](T.CCRP OPERATING INC) | -0.297 [-0.428, -0.166] | <0.001 |
| C[operator](T.CHACO ENERGY COMPANY) | 3.941 [3.659, 4.223] | <0.001 |
| C[operator](T.CHEVRON PIPELINE COMPANY) | -0.228 [-0.973, 0.517] | 0.549 |
| C[operator](T.CHEVRON PRODUCTION COMPANY) | -1.199 [-1.944, -0.454] | 0.002 |
| C[operator](T.CHEVRON USA INC) | -0.555 [-1.296, 0.186] | 0.141 |
| C[operator](T.CIVITAS NORTH LLC) | -0.014 [-0.100, 0.072] | 0.752 |
| C[operator](T.COACHMAN ENERGY OPERATING COMPANY LLC) | 0.721 [0.002, 1.440] | 0.049 |
| C[operator](T.COLORADO OIL & GAS CONSERVATION COMMISSION) | -0.630 [-1.020, -0.240] | 0.002 |
| C[operator](T.COMPLETE ENERGY SERVICES INC) | 0.186 [0.068, 0.304] | 0.002 |
| C[operator](T.CONFLUENCE DJ LLC) | -0.220 [-0.338, -0.102] | <0.001 |
| C[operator](T.CRESTONE PEAK RESOURCES OPERATING LLC) | -0.222 [-0.353, -0.091] | <0.001 |
| C[operator](T.CUB CREEK ENERGY) | -0.354 [-0.401, -0.307] | <0.001 |
| C[operator](T.CUB CREEK ENERGY LLC) | 0.158 [0.121, 0.195] | <0.001 |
| C[operator](T.DAN A HUGHES COMPANY LP) | 0.109 [-0.022, 0.240] | 0.106 |
| C[operator](T.DCP MIDSTREAM LP) | -0.080 [-0.202, 0.042] | 0.200 |
| C[operator](T.DCP OPERATING COMPANY LP) | -0.039 [-0.108, 0.030] | 0.270 |
| C[operator](T.DIAMOND OPERATING INC) | 0.328 [0.281, 0.375] | <0.001 |
| C[operator](T.EDGE ENERGY II LLC) | 0.821 [0.741, 0.901] | <0.001 |
| C[operator](T.ENCANA OIL & GAS (USA) INC) | -0.673 [-1.257, -0.089] | 0.024 |
| C[operator](T.ENERPLUS RESOURCES (USA) CORPORATION) | -0.057 [-0.159, 0.045] | 0.275 |
| C[operator](T.EOG RESOURCES INC) | -0.268 [-0.393, -0.143] | <0.001 |
| C[operator](T.EWS 13 DJ BASIN LLC) | -0.051 [-0.314, 0.212] | 0.704 |
| C[operator](T.EWS 4 DJ BASIN LLC) | 1.284 [1.166, 1.402] | <0.001 |
| C[operator](T.EXPEDITION WATER SOLUTIONS COLORADO LLC) | -0.913 [-1.031, -0.795] | <0.001 |
| C[operator](T.EXTRACTION OIL & GAS INC) | -0.231 [-0.315, -0.147] | <0.001 |
| C[operator](T.EXTRACTION OIL & GAS LLC) | -0.134 [-0.265, -0.003] | 0.046 |
| C[operator](T.FIFTH CREEK ENERGY OPERATING COMPANY LLC) | -0.096 [-0.227, 0.035] | 0.151 |
| C[operator](T.FOUNDATION ENERGY MANAGEMENT LLC) | 0.052 [-0.107, 0.211] | 0.520 |
| C[operator](T.FRITZLER RESOURCES INC) | 3.435 [3.388, 3.482] | <0.001 |
| C[operator](T.FUNDARE RESOURCES OPERATING COMPANY LLC) | -0.043 [-0.100, 0.014] | 0.146 |
| C[operator](T.GADECO LLC) | 0.675 [0.454, 0.896] | <0.001 |
| C[operator](T.GENESIS GAS & OIL COLORADO LLC) | 1.346 [0.605, 2.087] | <0.001 |
| C[operator](T.GRAND RIVER GATHERING LLC) | -0.748 [-1.461, -0.035] | 0.040 |
| C[operator](T.GREAT WESTERN OPERATING COMPANY LLC) | 0.026 [-0.080, 0.132] | 0.623 |
| C[operator](T.GRIZZLY OPERATING LLC) | -0.372 [-1.087, 0.343] | 0.308 |
| C[operator](T.GRYNBERG* JACK DBA GRYNBERG PETROLEUM CO) | 0.312 [0.091, 0.533] | 0.006 |
| C[operator](T.HIGHPOINT ENERGY LLC) | -0.913 [-1.031, -0.795] | <0.001 |
| C[operator](T.HIGHPOINT OPERATING CORPORATION) | -0.357 [-0.428, -0.286] | <0.001 |
| C[operator](T.HRM RESOURCES II LLC) | -0.913 [-1.031, -0.795] | <0.001 |
| C[operator](T.HUNTER RIDGE ENERGY SERVICES LLC) | -0.170 [-0.885, 0.545] | 0.642 |
| C[operator](T.HYNDREX RESOURCES) | 0.186 [0.068, 0.304] | 0.002 |
| C[operator](T.INDUSTRIAL GAS SERVICES INC) | 0.788 [0.506, 1.070] | <0.001 |
| C[operator](T.K P KAUFFMAN COMPANY INC) | -0.289 [-0.424, -0.154] | <0.001 |
| C[operator](T.KERR MCGEE GATHERING LLC) | -0.119 [-0.195, -0.043] | 0.002 |
| C[operator](T.KERR MCGEE OIL & GAS ONSHORE LP) | -0.449 [-0.620, -0.278] | <0.001 |
| C[operator](T.KOCH EXPLORATION COMPANY LLC) | 1.287 [0.528, 2.046] | <0.001 |
| C[operator](T.KOCH EXPLORATION COMPANY, LLC) | 0.641 [-0.104, 1.386] | 0.092 |
| C[operator](T.KP KAUFFMAN COMPANY INC) | 0.199 [0.150, 0.248] | <0.001 |
| C[operator](T.KT RESOURCES LLC) | -0.701 [-1.442, 0.040] | 0.063 |
| C[operator](T.LARAMIE ENERGY LLC) | -0.508 [-1.218, 0.202] | 0.161 |
| C[operator](T.LASSO OIL & GAS LLC) | 1.550 [0.809, 2.291] | <0.001 |
| C[operator](T.LINN OPERATING INC) | -0.516 [-1.226, 0.194] | 0.154 |
| C[operator](T.LINN OPERATING LLC) | -1.243 [-1.953, -0.533] | <0.001 |
| C[operator](T.LONGS PEAK RESOURCES LLC) | -0.234 [-0.291, -0.177] | <0.001 |
| C[operator](T.MACHII-ROSS PETROLEUM CO) | 1.816 [1.616, 2.016] | <0.001 |
| C[operator](T.MAGPIE OPERATING INC) | 4.925 [4.643, 5.207] | <0.001 |
| C[operator](T.MARALEX RESOURCES, INC) | -0.897 [-1.607, -0.187] | 0.013 |
| C[operator](T.MARATHON OIL COMPANY) | -1.041 [-1.751, -0.331] | 0.004 |
| C[operator](T.MARKUS PRODUCTION, INC) | -0.821 [-1.103, -0.539] | <0.001 |
| C[operator](T.MDS ENERGY DEVELOPMENT LLC) | -0.770 [-0.817, -0.723] | <0.001 |
| C[operator](T.MERRION OIL & GAS CORP) | 0.784 [0.039, 1.529] | 0.039 |
| C[operator](T.MONAHAN GAS & OIL INC) | 1.860 [1.742, 1.978] | <0.001 |
| C[operator](T.MUSTANG RESOURCES LLC) | -1.098 [-1.819, -0.377] | 0.003 |
| C[operator](T.NGL WATER SOLUTIONS DJ LLC) | -0.235 [-0.317, -0.153] | <0.001 |
| C[operator](T.NICKEL ROAD OPERATING LLC) | -0.049 [-0.065, -0.033] | <0.001 |
| C[operator](T.NOBLE ENERGY INC) | -0.237 [-0.431, -0.043] | 0.016 |
| C[operator](T.NOBLE MIDSTREAM SERVICES LLC) | 0.091 [0.040, 0.142] | <0.001 |
| C[operator](T.NORTHSTAR GAS COMPANY INC) | 0.332 [-0.413, 1.077] | 0.382 |
| C[operator](T.O'BRIEN ENERGY RESOURCES CORP) | -0.913 [-1.031, -0.795] | <0.001 |
| C[operator](T.OXY USA INC) | 0.020 [-0.690, 0.730] | 0.957 |
| C[operator](T.OXY USA WTP LP) | -0.893 [-1.603, -0.183] | 0.014 |
| C[operator](T.PAINTED PEGASUS PETROLEUM LLC) | 1.964 [1.701, 2.227] | <0.001 |
| C[operator](T.PDC ENERGY INC) | -0.092 [-0.251, 0.067] | 0.259 |
| C[operator](T.PETERSON ENERGY OPERATING INC) | 0.379 [0.163, 0.595] | <0.001 |
| C[operator](T.PETRO MEX RESOURCES) | 0.965 [0.254, 1.676] | 0.008 |
| C[operator](T.PETRO OPERATING COMPANY LLC) | 0.852 [0.730, 0.974] | <0.001 |
| C[operator](T.PETROSHARE CORPORATION) | 0.430 [0.230, 0.630] | <0.001 |
| C[operator](T.PLUG NICKEL OIL COMPANY INC) | -0.515 [-1.260, 0.230] | 0.174 |
| C[operator](T.PRAIRIE OPERATING CO LLC) | 0.439 [0.439, 0.439] | <0.001 |
| C[operator](T.PROVIDENCE OPERATING LLC DBA POCO OPERATING) | -0.173 [-0.173, -0.173] | <0.001 |
| C[operator](T.RED HAWK PETROLEUM LLC) | 0.197 [0.134, 0.260] | <0.001 |
| C[operator](T.RED ROCK GATHERING COMPANY LLC) | -0.781 [-1.510, -0.052] | 0.036 |
| C[operator](T.REP PROCESSING LLC) | 0.616 [0.569, 0.663] | <0.001 |
| C[operator](T.RIO MESA RESOURCES INC) | 0.685 [-0.056, 1.426] | 0.069 |
| C[operator](T.ROBERT L BAYLESS PRODUCER LLC) | -0.008 [-0.749, 0.733] | 0.983 |
| C[operator](T.ROCKY MOUNTAIN MIDSTREAM LLC) | 0.322 [0.263, 0.381] | <0.001 |
| C[operator](T.ROCKY MOUNTAIN NATURAL GAS LLC) | 1.025 [0.280, 1.770] | 0.007 |
| C[operator](T.RWL ENTERPRISES) | 1.371 [1.171, 1.571] | <0.001 |
| C[operator](T.SAMSON RESOURCES COMPANY) | 0.135 [-0.624, 0.894] | 0.728 |
| C[operator](T.SCHNEIDER ENERGY SERVICES INC) | -0.475 [-0.757, -0.193] | <0.001 |
| C[operator](T.SCOUT ENERGY MANAGEMENT LLC) | -0.699 [-1.438, 0.040] | 0.064 |
| C[operator](T.SMITH ENERGY CORP) | 0.650 [0.376, 0.924] | <0.001 |
| C[operator](T.SMITH OIL PROPERTIES INC) | 2.627 [2.427, 2.827] | <0.001 |
| C[operator](T.SRC ENERGY INC) | -0.185 [-0.332, -0.038] | 0.014 |
| C[operator](T.SUMMIT DJ-S LLC) | 4.910 [4.863, 4.957] | <0.001 |
| C[operator](T.SUMMIT MIDSTREAM NIOBRARA LLC) | -0.297 [-0.428, -0.166] | <0.001 |
| C[operator](T.SUMMIT MIDSTREAM PARTNERS LLC) | -0.616 [-1.329, 0.097] | 0.090 |
| C[operator](T.SYNERGY RESOURCES CORPORATION) | 0.198 [0.033, 0.363] | 0.018 |
| C[operator](T.TALLGRASS WATER WESTERN LLC) | -0.226 [-0.273, -0.179] | <0.001 |
| C[operator](T.TAPROOT ROCKIES MIDSTREAM LLC) | -0.324 [-0.371, -0.277] | <0.001 |
| C[operator](T.TEP ROCKY MOUNTAIN LLC) | -0.740 [-1.457, -0.023] | 0.043 |
| C[operator](T.TEXAS TEA OF COLORADO LLC DBA TEXAS TEA LLC) | -0.051 [-0.314, 0.212] | 0.704 |
| C[operator](T.TINDALL OPERATING COMPANY) | -0.128 [-0.410, 0.154] | 0.372 |
| C[operator](T.TOP OPERATING COMPANY) | 0.312 [0.045, 0.579] | 0.021 |
| C[operator](T.UPLAND EXPLORATION LLC) | 2.488 [2.441, 2.535] | <0.001 |
| C[operator](T.URSA OPERATING COMPANY LLC) | -0.594 [-1.317, 0.129] | 0.107 |
| C[operator](T.UTAH GAS OP LTD DBA UTAH GAS CORP) | 0.260 [-0.479, 0.999] | 0.490 |
| C[operator](T.VANGUARD OPERATING LLC) | -0.439 [-1.096, 0.218] | 0.190 |
| C[operator](T.VERDAD OIL & GAS CORPORATION) | -0.220 [-0.338, -0.102] | <0.001 |
| C[operator](T.VERDAD RESOURCES LLC) | -0.283 [-0.338, -0.228] | <0.001 |
| C[operator](T.VISION ENERGY LLC) | 0.867 [0.152, 1.582] | 0.018 |
| C[operator](T.WARD PETROLEUM CORPORATION) | -0.402 [-0.525, -0.279] | <0.001 |
| C[operator](T.WEXPRO COMPANY) | 0.645 [-0.114, 1.404] | 0.095 |
| C[operator](T.WHITING OIL & GAS CORPORATION) | -0.426 [-0.546, -0.306] | <0.001 |
| C[operator](T.WINDSOR ENERGY GROUP LLC) | 2.356 [1.611, 3.101] | <0.001 |
| C[operator](T.WOODARD* SANDRA K) | -0.921 [-1.666, -0.176] | 0.015 |
| C[operator](T.WPX ENERGY ROCKY MOUNTAIN LLC) | -1.329 [-2.042, -0.616] | <0.001 |
| C[operator](T.XTO ENERGY INC) | -0.722 [-1.463, 0.019] | 0.056 |
| Post | -0.220 [-0.338, -0.102] | <0.001 |
| Historical | 0.043 [-0.135, 0.221] | 0.636 |
| Post × Historical | 0.008 [-0.151, 0.167] | 0.923 |

Fit stats:

| Model | N | AIC | BIC | LogLik | R2 | Adj R2 |
| --- | --- | --- | --- | --- | --- | --- |
| H2 OLS (cluster op) | 26376 | 57562.551 | 58781.402 | -28632.275 | 0.147 | 0.142 |

Note: Standard errors are clustered by operator; model includes operator fixed effects and county/rurality controls.

### Table H2-A′ (Appendix): Same model clustered by county

| Term | Estimate [95% CI] | p |
| --- | --- | --- |
| Intercept | 1.590 [1.361, 1.819] | <0.001 |
| C[county_norm](T.RIO BLANCO) | 0.024 [-0.052, 0.100] | 0.538 |
| C[county_norm](T.WELD) | -0.600 [-0.827, -0.373] | <0.001 |
| C[rurality_3](T.Suburban) | -0.039 [-0.080, 0.002] | 0.059 |
| C[rurality_3](T.Urban) | -0.077 [-0.102, -0.052] | <0.001 |
| C[operator](T.31 OPERATING) | 0.803 [0.570, 1.036] | <0.001 |
| C[operator](T.4-H OPERATING CORPORATION) | 0.990 [0.957, 1.023] | <0.001 |
| C[operator](T.8 NORTH LLC) | -0.503 [-0.625, -0.381] | <0.001 |
| C[operator](T.AKA ENERGY GROUP LLC) | 0.037 [-0.416, 0.490] | 0.873 |
| C[operator](T.ANADARKO DJ GAS PROCESSING LLC) | 0.405 [0.405, 0.405] | <0.001 |
| C[operator](T.ANADARKO WATTENBERG OIL COMPLEX LLC) | -0.052 [-0.338, 0.234] | 0.722 |
| C[operator](T.ANSCHUTZ EXPLORATION CORP) | -0.517 [-0.882, -0.152] | 0.006 |
| C[operator](T.BARGATH LLC) | -1.021 [-1.366, -0.676] | <0.001 |
| C[operator](T.BARRETT CORPORATION* BILL) | 0.041 [-0.100, 0.182] | 0.572 |
| C[operator](T.BARRETT RESOURCES CORP) | 0.000 [0.000, 0.000] | 0.449 |
| C[operator](T.BAYLESS PRODUCER, LLC* ROBERT L) | -0.921 [-1.154, -0.688] | <0.001 |
| C[operator](T.BAYSWATER EXPLORATION & PRODUCTION LLC) | 0.259 [0.110, 0.408] | <0.001 |
| C[operator](T.BAYSWATER EXPLORATION AND PRODUCTION LLC) | -0.216 [-0.322, -0.110] | <0.001 |
| C[operator](T.BERRY PETROLEUM COMPANY LLC) | -0.450 [-0.736, -0.164] | 0.002 |
| C[operator](T.BISON IV OPERATING LLC) | 0.328 [0.054, 0.602] | 0.019 |
| C[operator](T.BISON OIL & GAS II LLC) | 0.004 [-0.119, 0.127] | 0.943 |
| C[operator](T.BLACK HILLS PLATEAU PRODUCTION LLC) | -1.590 [-1.819, -1.361] | <0.001 |
| C[operator](T.BLUE CHIP OIL INC) | 1.599 [1.266, 1.932] | <0.001 |
| C[operator](T.BNN WESTERN LLC) | -0.171 [-0.294, -0.048] | 0.006 |
| C[operator](T.BONANZA CREEK ENERGY OPERATING COMPANY LLC) | -0.370 [-0.409, -0.331] | <0.001 |
| C[operator](T.CAERUS PICEANCE LLC) | -0.856 [-1.085, -0.627] | <0.001 |
| C[operator](T.CAPTIVA ENERGY PARTNERS LLC) | 0.396 [0.359, 0.433] | <0.001 |
| C[operator](T.CARRIZO NIOBRARA LLC) | 0.325 [0.007, 0.643] | 0.045 |
| C[operator](T.CCRP OPERATING INC) | -0.297 [-0.334, -0.260] | <0.001 |
| C[operator](T.CHACO ENERGY COMPANY) | 3.941 [3.896, 3.986] | <0.001 |
| C[operator](T.CHEVRON PIPELINE COMPANY) | -0.228 [-0.461, 0.005] | 0.056 |
| C[operator](T.CHEVRON PRODUCTION COMPANY) | -1.199 [-1.471, -0.927] | <0.001 |
| C[operator](T.CHEVRON USA INC) | -0.555 [-0.796, -0.314] | <0.001 |
| C[operator](T.CIVITAS NORTH LLC) | -0.014 [-0.157, 0.129] | 0.848 |
| C[operator](T.COACHMAN ENERGY OPERATING COMPANY LLC) | 0.721 [-0.400, 1.842] | 0.207 |
| C[operator](T.COLORADO OIL & GAS CONSERVATION COMMISSION) | -0.630 [-1.604, 0.344] | 0.205 |
| C[operator](T.COMPLETE ENERGY SERVICES INC) | 0.186 [0.161, 0.211] | <0.001 |
| C[operator](T.CONFLUENCE DJ LLC) | -0.220 [-0.245, -0.195] | <0.001 |
| C[operator](T.CRESTONE PEAK RESOURCES OPERATING LLC) | -0.222 [-0.271, -0.173] | <0.001 |
| C[operator](T.CUB CREEK ENERGY) | -0.354 [-0.577, -0.131] | 0.002 |
| C[operator](T.CUB CREEK ENERGY LLC) | 0.158 [-0.222, 0.538] | 0.414 |
| C[operator](T.DAN A HUGHES COMPANY LP) | 0.109 [0.072, 0.146] | <0.001 |
| C[operator](T.DCP MIDSTREAM LP) | -0.080 [-0.182, 0.022] | 0.128 |
| C[operator](T.DCP OPERATING COMPANY LP) | -0.039 [-0.112, 0.034] | 0.292 |
| C[operator](T.DIAMOND OPERATING INC) | 0.328 [0.303, 0.353] | <0.001 |
| C[operator](T.EDGE ENERGY II LLC) | 0.821 [0.039, 1.603] | 0.040 |
| C[operator](T.ENCANA OIL & GAS (USA) INC) | -0.673 [-0.896, -0.450] | <0.001 |
| C[operator](T.ENERPLUS RESOURCES (USA) CORPORATION) | -0.057 [-0.251, 0.137] | 0.566 |
| C[operator](T.EOG RESOURCES INC) | -0.268 [-0.366, -0.170] | <0.001 |
| C[operator](T.EWS 13 DJ BASIN LLC) | -0.051 [-0.084, -0.018] | 0.003 |
| C[operator](T.EWS 4 DJ BASIN LLC) | 1.284 [1.259, 1.309] | <0.001 |
| C[operator](T.EXPEDITION WATER SOLUTIONS COLORADO LLC) | -0.913 [-0.938, -0.888] | <0.001 |
| C[operator](T.EXTRACTION OIL & GAS INC) | -0.231 [-0.304, -0.158] | <0.001 |
| C[operator](T.EXTRACTION OIL & GAS LLC) | -0.134 [-0.273, 0.005] | 0.057 |
| C[operator](T.FIFTH CREEK ENERGY OPERATING COMPANY LLC) | -0.096 [-0.304, 0.112] | 0.364 |
| C[operator](T.FOUNDATION ENERGY MANAGEMENT LLC) | 0.052 [-0.117, 0.221] | 0.546 |
| C[operator](T.FRITZLER RESOURCES INC) | 3.435 [3.410, 3.460] | <0.001 |
| C[operator](T.FUNDARE RESOURCES OPERATING COMPANY LLC) | -0.043 [-0.133, 0.047] | 0.357 |
| C[operator](T.GADECO LLC) | 0.675 [0.009, 1.341] | 0.047 |
| C[operator](T.GENESIS GAS & OIL COLORADO LLC) | 1.346 [1.111, 1.581] | <0.001 |
| C[operator](T.GRAND RIVER GATHERING LLC) | -0.748 [-1.001, -0.495] | <0.001 |
| C[operator](T.GREAT WESTERN OPERATING COMPANY LLC) | 0.026 [-0.082, 0.134] | 0.634 |
| C[operator](T.GRIZZLY OPERATING LLC) | -0.372 [-0.674, -0.070] | 0.016 |
| C[operator](T.GRYNBERG* JACK DBA GRYNBERG PETROLEUM CO) | 0.312 [-0.154, 0.778] | 0.189 |
| C[operator](T.HIGHPOINT ENERGY LLC) | -0.913 [-0.938, -0.888] | <0.001 |
| C[operator](T.HIGHPOINT OPERATING CORPORATION) | -0.357 [-0.400, -0.314] | <0.001 |
| C[operator](T.HRM RESOURCES II LLC) | -0.913 [-0.938, -0.888] | <0.001 |
| C[operator](T.HUNTER RIDGE ENERGY SERVICES LLC) | -0.170 [-0.464, 0.124] | 0.259 |
| C[operator](T.HYNDREX RESOURCES) | 0.186 [0.161, 0.211] | <0.001 |
| C[operator](T.INDUSTRIAL GAS SERVICES INC) | 0.788 [0.743, 0.833] | <0.001 |
| C[operator](T.K P KAUFFMAN COMPANY INC) | -0.289 [-0.487, -0.091] | 0.004 |
| C[operator](T.KERR MCGEE GATHERING LLC) | -0.119 [-0.221, -0.017] | 0.022 |
| C[operator](T.KERR MCGEE OIL & GAS ONSHORE LP) | -0.449 [-0.480, -0.418] | <0.001 |
| C[operator](T.KOCH EXPLORATION COMPANY LLC) | 1.287 [1.050, 1.524] | <0.001 |
| C[operator](T.KOCH EXPLORATION COMPANY, LLC) | 0.641 [0.135, 1.147] | 0.013 |
| C[operator](T.KP KAUFFMAN COMPANY INC) | 0.199 [0.128, 0.270] | <0.001 |
| C[operator](T.KT RESOURCES LLC) | -0.701 [-0.934, -0.468] | <0.001 |
| C[operator](T.LARAMIE ENERGY LLC) | -0.508 [-0.757, -0.259] | <0.001 |
| C[operator](T.LASSO OIL & GAS LLC) | 1.550 [1.317, 1.783] | <0.001 |
| C[operator](T.LINN OPERATING INC) | -0.516 [-0.998, -0.034] | 0.036 |
| C[operator](T.LINN OPERATING LLC) | -1.243 [-1.576, -0.910] | <0.001 |
| C[operator](T.LONGS PEAK RESOURCES LLC) | -0.234 [-0.332, -0.136] | <0.001 |
| C[operator](T.MACHII-ROSS PETROLEUM CO) | 1.816 [1.783, 1.849] | <0.001 |
| C[operator](T.MAGPIE OPERATING INC) | 4.925 [4.880, 4.970] | <0.001 |
| C[operator](T.MARALEX RESOURCES, INC) | -0.897 [-1.126, -0.668] | <0.001 |
| C[operator](T.MARATHON OIL COMPANY) | -1.041 [-1.486, -0.596] | <0.001 |
| C[operator](T.MARKUS PRODUCTION, INC) | -0.821 [-0.866, -0.776] | <0.001 |
| C[operator](T.MDS ENERGY DEVELOPMENT LLC) | -0.770 [-0.795, -0.745] | <0.001 |
| C[operator](T.MERRION OIL & GAS CORP) | 0.784 [0.551, 1.017] | <0.001 |
| C[operator](T.MONAHAN GAS & OIL INC) | 1.860 [1.835, 1.885] | <0.001 |
| C[operator](T.MUSTANG RESOURCES LLC) | -1.098 [-1.457, -0.739] | <0.001 |
| C[operator](T.NGL WATER SOLUTIONS DJ LLC) | -0.235 [-0.355, -0.115] | <0.001 |
| C[operator](T.NICKEL ROAD OPERATING LLC) | -0.049 [-0.139, 0.041] | 0.287 |
| C[operator](T.NOBLE ENERGY INC) | -0.237 [-0.268, -0.206] | <0.001 |
| C[operator](T.NOBLE MIDSTREAM SERVICES LLC) | 0.091 [-0.046, 0.228] | 0.194 |
| C[operator](T.NORTHSTAR GAS COMPANY INC) | 0.332 [0.099, 0.565] | 0.005 |
| C[operator](T.O'BRIEN ENERGY RESOURCES CORP) | -0.913 [-0.938, -0.888] | <0.001 |
| C[operator](T.OXY USA INC) | 0.020 [-0.209, 0.249] | 0.867 |
| C[operator](T.OXY USA WTP LP) | -0.893 [-1.160, -0.626] | <0.001 |
| C[operator](T.PAINTED PEGASUS PETROLEUM LLC) | 1.964 [1.302, 2.626] | <0.001 |
| C[operator](T.PDC ENERGY INC) | -0.092 [-0.129, -0.055] | <0.001 |
| C[operator](T.PETERSON ENERGY OPERATING INC) | 0.379 [-0.178, 0.936] | 0.183 |
| C[operator](T.PETRO MEX RESOURCES) | 0.965 [0.712, 1.218] | <0.001 |
| C[operator](T.PETRO OPERATING COMPANY LLC) | 0.852 [0.088, 1.616] | 0.029 |
| C[operator](T.PETROSHARE CORPORATION) | 0.430 [0.397, 0.463] | <0.001 |
| C[operator](T.PLUG NICKEL OIL COMPANY INC) | -0.515 [-0.748, -0.282] | <0.001 |
| C[operator](T.PRAIRIE OPERATING CO LLC) | 0.439 [0.280, 0.598] | <0.001 |
| C[operator](T.PROVIDENCE OPERATING LLC DBA POCO OPERATING) | -0.173 [-0.293, -0.053] | 0.005 |
| C[operator](T.RED HAWK PETROLEUM LLC) | 0.197 [-0.093, 0.487] | 0.185 |
| C[operator](T.RED ROCK GATHERING COMPANY LLC) | -0.781 [-1.155, -0.407] | <0.001 |
| C[operator](T.REP PROCESSING LLC) | 0.616 [0.591, 0.641] | <0.001 |
| C[operator](T.RIO MESA RESOURCES INC) | 0.685 [0.452, 0.918] | <0.001 |
| C[operator](T.ROBERT L BAYLESS PRODUCER LLC) | -0.008 [-0.241, 0.225] | 0.947 |
| C[operator](T.ROCKY MOUNTAIN MIDSTREAM LLC) | 0.322 [0.157, 0.487] | <0.001 |
| C[operator](T.ROCKY MOUNTAIN NATURAL GAS LLC) | 1.025 [0.792, 1.258] | <0.001 |
| C[operator](T.RWL ENTERPRISES) | 1.371 [0.936, 1.806] | <0.001 |
| C[operator](T.SAMSON RESOURCES COMPANY) | 0.135 [-0.102, 0.372] | 0.265 |
| C[operator](T.SCHNEIDER ENERGY SERVICES INC) | -0.475 [-0.818, -0.132] | 0.007 |
| C[operator](T.SCOUT ENERGY MANAGEMENT LLC) | -0.699 [-0.948, -0.450] | <0.001 |
| C[operator](T.SMITH ENERGY CORP) | 0.650 [0.166, 1.134] | 0.008 |
| C[operator](T.SMITH OIL PROPERTIES INC) | 2.627 [2.594, 2.660] | <0.001 |
| C[operator](T.SRC ENERGY INC) | -0.185 [-0.346, -0.024] | 0.024 |
| C[operator](T.SUMMIT DJ-S LLC) | 4.910 [4.885, 4.935] | <0.001 |
| C[operator](T.SUMMIT MIDSTREAM NIOBRARA LLC) | -0.297 [-0.334, -0.260] | <0.001 |
| C[operator](T.SUMMIT MIDSTREAM PARTNERS LLC) | -0.616 [-0.924, -0.308] | <0.001 |
| C[operator](T.SYNERGY RESOURCES CORPORATION) | 0.198 [0.006, 0.390] | 0.043 |
| C[operator](T.TALLGRASS WATER WESTERN LLC) | -0.226 [-0.304, -0.148] | <0.001 |
| C[operator](T.TAPROOT ROCKIES MIDSTREAM LLC) | -0.324 [-0.436, -0.212] | <0.001 |
| C[operator](T.TEP ROCKY MOUNTAIN LLC) | -0.740 [-0.971, -0.509] | <0.001 |
| C[operator](T.TEXAS TEA OF COLORADO LLC DBA TEXAS TEA LLC) | -0.051 [-0.084, -0.018] | 0.003 |
| C[operator](T.TINDALL OPERATING COMPANY) | -0.128 [-0.173, -0.083] | <0.001 |
| C[operator](T.TOP OPERATING COMPANY) | 0.312 [0.132, 0.492] | <0.001 |
| C[operator](T.UPLAND EXPLORATION LLC) | 2.488 [2.463, 2.513] | <0.001 |
| C[operator](T.URSA OPERATING COMPANY LLC) | -0.594 [-0.845, -0.343] | <0.001 |
| C[operator](T.UTAH GAS OP LTD DBA UTAH GAS CORP) | 0.260 [-0.134, 0.654] | 0.195 |
| C[operator](T.VANGUARD OPERATING LLC) | -0.439 [-0.706, -0.172] | 0.001 |
| C[operator](T.VERDAD OIL & GAS CORPORATION) | -0.220 [-0.245, -0.195] | <0.001 |
| C[operator](T.VERDAD RESOURCES LLC) | -0.283 [-0.373, -0.193] | <0.001 |
| C[operator](T.VISION ENERGY LLC) | 0.867 [0.638, 1.096] | <0.001 |
| C[operator](T.WARD PETROLEUM CORPORATION) | -0.402 [-0.759, -0.045] | 0.027 |
| C[operator](T.WEXPRO COMPANY) | 0.645 [0.408, 0.882] | <0.001 |
| C[operator](T.WHITING OIL & GAS CORPORATION) | -0.426 [-0.487, -0.365] | <0.001 |
| C[operator](T.WINDSOR ENERGY GROUP LLC) | 2.356 [2.123, 2.589] | <0.001 |
| C[operator](T.WOODARD* SANDRA K) | -0.921 [-1.154, -0.688] | <0.001 |
| C[operator](T.WPX ENERGY ROCKY MOUNTAIN LLC) | -1.329 [-1.562, -1.096] | <0.001 |
| C[operator](T.XTO ENERGY INC) | -0.722 [-0.967, -0.477] | <0.001 |
| Post | -0.220 [-0.245, -0.195] | <0.001 |
| Historical | 0.043 [0.010, 0.076] | 0.009 |
| Post × Historical | 0.008 [-0.031, 0.047] | 0.697 |

Fit stats:

| Model | N | AIC | BIC | LogLik | R2 | Adj R2 |
| --- | --- | --- | --- | --- | --- | --- |
| H2 OLS (cluster county) | 26376 | 57562.551 | 58781.402 | -28632.275 | 0.147 | 0.142 |

### Table R1 (Appendix): Robustness (key terms)

| variant | post | post_se | post:historical | int_se |
| --- | --- | --- | --- | --- |
| baseline | -0.220 | 0.060 | 0.008 | 0.081 |
| cap180 | -0.220 | 0.060 | 0.006 | 0.080 |
| exclude_extreme99 | -0.232 | 0.062 | -0.037 | 0.075 |

## Claim 3: Mechanism is mostly fewer any-delay cases; tail behaves differently for Historical

### Table H2-B: Two-part model (full model terms)

**Panel 1: any_delay logit (ORs)**

| Term | OR [95% CI] | p |
| --- | --- | --- |
| Intercept | 238.335 [14.135, 4018.540] | <0.001 |
| C[rurality_3](T.Suburban) | 0.677 [0.497, 0.922] | 0.013 |
| C[rurality_3](T.Urban) | 0.681 [0.604, 0.768] | <0.001 |
| C[county_norm](T.RIO BLANCO) | 0.806 [0.533, 1.219] | 0.307 |
| C[county_norm](T.WELD) | 0.239 [0.038, 1.507] | 0.128 |
| C[operator](T.31 OPERATING) | 10.663 [0.359, 316.929] | 0.171 |
| C[operator](T.4-H OPERATING CORPORATION) | 165.687 [8.984, 3055.542] | <0.001 |
| C[operator](T.8 NORTH LLC) | 0.040 [0.005, 0.336] | 0.003 |
| C[operator](T.AKA ENERGY GROUP LLC) | 0.033 [0.004, 0.277] | 0.002 |
| C[operator](T.ANADARKO DJ GAS PROCESSING LLC) | 330.528 [18.614, 5869.249] | <0.001 |
| C[operator](T.ANADARKO WATTENBERG OIL COMPLEX LLC) | 0.033 [0.004, 0.276] | 0.002 |
| C[operator](T.ANSCHUTZ EXPLORATION CORP) | 0.031 [0.002, 0.480] | 0.013 |
| C[operator](T.BARGATH LLC) | 0.005 [0.000, 0.089] | <0.001 |
| C[operator](T.BARRETT CORPORATION* BILL) | 0.234 [0.027, 2.004] | 0.185 |
| C[operator](T.BARRETT RESOURCES CORP) | 330.528 [18.614, 5869.249] | <0.001 |
| C[operator](T.BAYLESS PRODUCER, LLC* ROBERT L) | 4.290 [0.141, 130.205] | 0.403 |
| C[operator](T.BAYSWATER EXPLORATION & PRODUCTION LLC) | 0.398 [0.049, 3.250] | 0.390 |
| C[operator](T.BAYSWATER EXPLORATION AND PRODUCTION LLC) | 0.104 [0.012, 0.895] | 0.039 |
| C[operator](T.BERRY PETROLEUM COMPANY LLC) | 0.034 [0.002, 0.552] | 0.017 |
| C[operator](T.BISON IV OPERATING LLC) | 0.142 [0.017, 1.155] | 0.068 |
| C[operator](T.BISON OIL & GAS II LLC) | 0.244 [0.030, 1.998] | 0.189 |
| C[operator](T.BLACK HILLS PLATEAU PRODUCTION LLC) | 0.000 [0.000, 0.000] | <0.001 |
| C[operator](T.BLUE CHIP OIL INC) | 666.268 [36.600, 12128.623] | <0.001 |
| C[operator](T.BNN WESTERN LLC) | 0.141 [0.016, 1.208] | 0.074 |
| C[operator](T.BONANZA CREEK ENERGY OPERATING COMPANY LLC) | 0.041 [0.005, 0.341] | 0.003 |
| C[operator](T.CAERUS PICEANCE LLC) | 0.012 [0.001, 0.191] | 0.002 |
| C[operator](T.CAPTIVA ENERGY PARTNERS LLC) | 77.194 [4.113, 1448.945] | 0.004 |
| C[operator](T.CARRIZO NIOBRARA LLC) | 365.585 [19.481, 6860.477] | <0.001 |
| C[operator](T.CCRP OPERATING INC) | 107.497 [5.727, 2017.571] | 0.002 |
| C[operator](T.CHACO ENERGY COMPANY) | 276.132 [14.661, 5200.885] | <0.001 |
| C[operator](T.CHEVRON PIPELINE COMPANY) | 22.480 [0.742, 681.496] | 0.074 |
| C[operator](T.CHEVRON PRODUCTION COMPANY) | 0.003 [0.000, 0.048] | <0.001 |
| C[operator](T.CHEVRON USA INC) | 0.031 [0.002, 0.487] | 0.013 |
| C[operator](T.CIVITAS NORTH LLC) | 0.307 [0.037, 2.518] | 0.271 |
| C[operator](T.COACHMAN ENERGY OPERATING COMPANY LLC) | 30.707 [0.952, 990.453] | 0.053 |
| C[operator](T.COLORADO OIL & GAS CONSERVATION COMMISSION) | 0.025 [0.003, 0.244] | 0.001 |
| C[operator](T.COMPLETE ENERGY SERVICES INC) | 76.712 [4.104, 1433.830] | 0.004 |
| C[operator](T.CONFLUENCE DJ LLC) | 76.712 [4.104, 1433.830] | 0.004 |
| C[operator](T.CRESTONE PEAK RESOURCES OPERATING LLC) | 0.110 [0.013, 0.912] | 0.041 |
| C[operator](T.CUB CREEK ENERGY) | 0.029 [0.004, 0.241] | 0.001 |
| C[operator](T.CUB CREEK ENERGY LLC) | 0.182 [0.022, 1.480] | 0.111 |
| C[operator](T.DAN A HUGHES COMPANY LP) | 77.194 [4.113, 1448.945] | 0.004 |
| C[operator](T.DCP MIDSTREAM LP) | 0.077 [0.009, 0.662] | 0.020 |
| C[operator](T.DCP OPERATING COMPANY LP) | 0.122 [0.015, 0.994] | 0.049 |
| C[operator](T.DIAMOND OPERATING INC) | 287.950 [16.176, 5125.713] | <0.001 |
| C[operator](T.EDGE ENERGY II LLC) | 0.093 [0.011, 0.761] | 0.027 |
| C[operator](T.ENCANA OIL & GAS (USA) INC) | 0.027 [0.002, 0.330] | 0.005 |
| C[operator](T.ENERPLUS RESOURCES (USA) CORPORATION) | 0.081 [0.010, 0.690] | 0.021 |
| C[operator](T.EOG RESOURCES INC) | 0.056 [0.006, 0.484] | 0.009 |
| C[operator](T.EWS 13 DJ BASIN LLC) | 654.588 [34.883, 12283.460] | <0.001 |
| C[operator](T.EWS 4 DJ BASIN LLC) | 76.712 [4.104, 1433.830] | 0.004 |
| C[operator](T.EXPEDITION WATER SOLUTIONS COLORADO LLC) | 0.000 [0.000, 0.001] | <0.001 |
| C[operator](T.EXTRACTION OIL & GAS INC) | 0.060 [0.007, 0.491] | 0.009 |
| C[operator](T.EXTRACTION OIL & GAS LLC) | 0.081 [0.009, 0.697] | 0.022 |
| C[operator](T.FIFTH CREEK ENERGY OPERATING COMPANY LLC) | 0.253 [0.029, 2.218] | 0.215 |
| C[operator](T.FOUNDATION ENERGY MANAGEMENT LLC) | 0.080 [0.009, 0.684] | 0.021 |
| C[operator](T.FRITZLER RESOURCES INC) | 215.501 [12.106, 3836.317] | <0.001 |
| C[operator](T.FUNDARE RESOURCES OPERATING COMPANY LLC) | 0.317 [0.039, 2.581] | 0.283 |
| C[operator](T.GADECO LLC) | 345.666 [18.710, 6386.121] | <0.001 |
| C[operator](T.GENESIS GAS & OIL COLORADO LLC) | 26.384 [0.888, 783.567] | 0.059 |
| C[operator](T.GRAND RIVER GATHERING LLC) | 0.022 [0.001, 0.354] | 0.007 |
| C[operator](T.GREAT WESTERN OPERATING COMPANY LLC) | 0.128 [0.016, 1.059] | 0.057 |
| C[operator](T.GRIZZLY OPERATING LLC) | 365.514 [11.977, 11154.378] | <0.001 |
| C[operator](T.GRYNBERG* JACK DBA GRYNBERG PETROLEUM CO) | 641.971 [34.750, 11859.828] | <0.001 |
| C[operator](T.HIGHPOINT ENERGY LLC) | 0.000 [0.000, 0.001] | <0.001 |
| C[operator](T.HIGHPOINT OPERATING CORPORATION) | 0.036 [0.004, 0.294] | 0.002 |
| C[operator](T.HRM RESOURCES II LLC) | 0.000 [0.000, 0.001] | <0.001 |
| C[operator](T.HUNTER RIDGE ENERGY SERVICES LLC) | 111.446 [3.693, 3363.475] | 0.007 |
| C[operator](T.HYNDREX RESOURCES) | 76.712 [4.104, 1433.830] | 0.004 |
| C[operator](T.INDUSTRIAL GAS SERVICES INC) | 276.132 [14.661, 5200.885] | <0.001 |
| C[operator](T.K P KAUFFMAN COMPANY INC) | 0.028 [0.003, 0.246] | 0.001 |
| C[operator](T.KERR MCGEE GATHERING LLC) | 0.055 [0.007, 0.456] | 0.007 |
| C[operator](T.KERR MCGEE OIL & GAS ONSHORE LP) | 0.030 [0.004, 0.251] | 0.001 |
| C[operator](T.KOCH EXPLORATION COMPANY LLC) | 5.341 [0.178, 160.168] | 0.334 |
| C[operator](T.KOCH EXPLORATION COMPANY, LLC) | 26.268 [0.878, 786.024] | 0.059 |
| C[operator](T.KP KAUFFMAN COMPANY INC) | 0.221 [0.027, 1.802] | 0.159 |
| C[operator](T.KT RESOURCES LLC) | 121.643 [4.098, 3611.143] | 0.006 |
| C[operator](T.LARAMIE ENERGY LLC) | 0.029 [0.002, 0.465] | 0.012 |
| C[operator](T.LASSO OIL & GAS LLC) | 10.663 [0.359, 316.929] | 0.171 |
| C[operator](T.LINN OPERATING INC) | 0.026 [0.002, 0.443] | 0.012 |
| C[operator](T.LINN OPERATING LLC) | 0.004 [0.000, 0.070] | <0.001 |
| C[operator](T.LONGS PEAK RESOURCES LLC) | 0.197 [0.024, 1.607] | 0.129 |
| C[operator](T.MACHII-ROSS PETROLEUM CO) | 165.687 [8.984, 3055.542] | <0.001 |
| C[operator](T.MAGPIE OPERATING INC) | 135.889 [7.212, 2560.369] | 0.001 |
| C[operator](T.MARALEX RESOURCES, INC) | 12.305 [0.392, 385.999] | 0.153 |
| C[operator](T.MARATHON OIL COMPANY) | 0.004 [0.000, 0.070] | <0.001 |
| C[operator](T.MARKUS PRODUCTION, INC) | 0.000 [0.000, 0.001] | <0.001 |
| C[operator](T.MDS ENERGY DEVELOPMENT LLC) | 0.000 [0.000, 0.001] | <0.001 |
| C[operator](T.MERRION OIL & GAS CORP) | 15.237 [0.503, 461.984] | 0.118 |
| C[operator](T.MONAHAN GAS & OIL INC) | 122.501 [6.555, 2289.277] | 0.001 |
| C[operator](T.MUSTANG RESOURCES LLC) | 0.005 [0.000, 0.087] | <0.001 |
| C[operator](T.NGL WATER SOLUTIONS DJ LLC) | 0.027 [0.003, 0.228] | <0.001 |
| C[operator](T.NICKEL ROAD OPERATING LLC) | 0.375 [0.046, 3.047] | 0.359 |
| C[operator](T.NOBLE ENERGY INC) | 0.098 [0.012, 0.828] | 0.033 |
| C[operator](T.NOBLE MIDSTREAM SERVICES LLC) | 0.223 [0.027, 1.816] | 0.161 |
| C[operator](T.NORTHSTAR GAS COMPANY INC) | 4.290 [0.141, 130.205] | 0.403 |
| C[operator](T.O'BRIEN ENERGY RESOURCES CORP) | 0.000 [0.000, 0.001] | <0.001 |
| C[operator](T.OXY USA INC) | 3.652 [0.116, 114.678] | 0.461 |
| C[operator](T.OXY USA WTP LP) | 0.015 [0.001, 0.248] | 0.003 |
| C[operator](T.PAINTED PEGASUS PETROLEUM LLC) | 1004.887 [53.952, 18716.624] | <0.001 |
| C[operator](T.PDC ENERGY INC) | 0.123 [0.015, 1.023] | 0.053 |
| C[operator](T.PETERSON ENERGY OPERATING INC) | 0.071 [0.008, 0.607] | 0.016 |
| C[operator](T.PETRO MEX RESOURCES) | 286.878 [9.380, 8773.935] | 0.001 |
| C[operator](T.PETRO OPERATING COMPANY LLC) | 0.056 [0.007, 0.465] | 0.008 |
| C[operator](T.PETROSHARE CORPORATION) | 340.153 [18.447, 6272.136] | <0.001 |
| C[operator](T.PLUG NICKEL OIL COMPANY INC) | 15.237 [0.503, 461.984] | 0.118 |
| C[operator](T.PRAIRIE OPERATING CO LLC) | 615.321 [34.656, 10925.105] | <0.001 |
| C[operator](T.PROVIDENCE OPERATING LLC DBA POCO OPERATING) | 0.184 [0.023, 1.495] | 0.113 |
| C[operator](T.RED HAWK PETROLEUM LLC) | 0.056 [0.007, 0.460] | 0.007 |
| C[operator](T.RED ROCK GATHERING COMPANY LLC) | 0.020 [0.001, 0.322] | 0.006 |
| C[operator](T.REP PROCESSING LLC) | 215.501 [12.106, 3836.317] | <0.001 |
| C[operator](T.RIO MESA RESOURCES INC) | 48.282 [1.626, 1433.557] | 0.025 |
| C[operator](T.ROBERT L BAYLESS PRODUCER LLC) | 10.663 [0.359, 316.929] | 0.171 |
| C[operator](T.ROCKY MOUNTAIN MIDSTREAM LLC) | 759.700 [42.597, 13548.886] | <0.001 |
| C[operator](T.ROCKY MOUNTAIN NATURAL GAS LLC) | 9.172 [0.302, 278.153] | 0.203 |
| C[operator](T.RWL ENTERPRISES) | 165.687 [8.984, 3055.542] | <0.001 |
| C[operator](T.SAMSON RESOURCES COMPANY) | 11.947 [0.399, 357.976] | 0.153 |
| C[operator](T.SCHNEIDER ENERGY SERVICES INC) | 0.080 [0.009, 0.703] | 0.023 |
| C[operator](T.SCOUT ENERGY MANAGEMENT LLC) | 0.045 [0.003, 0.705] | 0.027 |
| C[operator](T.SMITH ENERGY CORP) | 0.383 [0.044, 3.354] | 0.386 |
| C[operator](T.SMITH OIL PROPERTIES INC) | 42.347 [2.295, 781.556] | 0.012 |
| C[operator](T.SRC ENERGY INC) | 0.054 [0.006, 0.461] | 0.008 |
| C[operator](T.SUMMIT DJ-S LLC) | 60.579 [3.401, 1079.145] | 0.005 |
| C[operator](T.SUMMIT MIDSTREAM NIOBRARA LLC) | 45.744 [2.437, 858.800] | 0.011 |
| C[operator](T.SUMMIT MIDSTREAM PARTNERS LLC) | 0.016 [0.001, 0.264] | 0.004 |
| C[operator](T.SYNERGY RESOURCES CORPORATION) | 0.693 [0.081, 5.910] | 0.737 |
| C[operator](T.TALLGRASS WATER WESTERN LLC) | 0.153 [0.019, 1.249] | 0.080 |
| C[operator](T.TAPROOT ROCKIES MIDSTREAM LLC) | 0.057 [0.007, 0.461] | 0.007 |
| C[operator](T.TEP ROCKY MOUNTAIN LLC) | 0.023 [0.001, 0.380] | 0.008 |
| C[operator](T.TEXAS TEA OF COLORADO LLC DBA TEXAS TEA LLC) | 427.287 [22.768, 8019.057] | <0.001 |
| C[operator](T.TINDALL OPERATING COMPANY) | 276.132 [14.661, 5200.885] | <0.001 |
| C[operator](T.TOP OPERATING COMPANY) | 1.189 [0.135, 10.434] | 0.876 |
| C[operator](T.UPLAND EXPLORATION LLC) | 215.501 [12.106, 3836.317] | <0.001 |
| C[operator](T.URSA OPERATING COMPANY LLC) | 0.032 [0.002, 0.517] | 0.015 |
| C[operator](T.UTAH GAS OP LTD DBA UTAH GAS CORP) | 0.021 [0.001, 0.326] | 0.006 |
| C[operator](T.VANGUARD OPERATING LLC) | 0.073 [0.005, 1.044] | 0.054 |
| C[operator](T.VERDAD OIL & GAS CORPORATION) | 76.712 [4.104, 1433.830] | 0.004 |
| C[operator](T.VERDAD RESOURCES LLC) | 0.056 [0.007, 0.455] | 0.007 |
| C[operator](T.VISION ENERGY LLC) | 68.392 [2.243, 2085.339] | 0.015 |
| C[operator](T.WARD PETROLEUM CORPORATION) | 0.021 [0.002, 0.187] | <0.001 |
| C[operator](T.WEXPRO COMPANY) | 11.947 [0.399, 357.976] | 0.153 |
| C[operator](T.WHITING OIL & GAS CORPORATION) | 0.034 [0.004, 0.289] | 0.002 |
| C[operator](T.WINDSOR ENERGY GROUP LLC) | 9.172 [0.302, 278.153] | 0.203 |
| C[operator](T.WOODARD* SANDRA K) | 9.172 [0.302, 278.153] | 0.203 |
| C[operator](T.WPX ENERGY ROCKY MOUNTAIN LLC) | 0.003 [0.000, 0.049] | <0.001 |
| C[operator](T.XTO ENERGY INC) | 0.037 [0.002, 0.580] | 0.019 |
| Post | 0.420 [0.244, 0.724] | 0.002 |
| Historical | 0.790 [0.520, 1.198] | 0.267 |
| Post × Historical | 0.721 [0.437, 1.190] | 0.200 |

Fit stats:

| Model | N | AIC | BIC | LogLik | Pseudo R2 |
| --- | --- | --- | --- | --- | --- |
| H2 any_delay logit | 26376 | 31128.316 | 32347.167 | -15415.158 | 0.132 |

**Panel 2: conditional delay>0 OLS (coefficients)**

| Term | Estimate [95% CI] | p |
| --- | --- | --- |
| Intercept | 1.186 [0.647, 1.725] | <0.001 |
| C[county_norm](T.RIO BLANCO) | 0.125 [-0.096, 0.346] | 0.270 |
| C[county_norm](T.WELD) | -0.458 [-0.995, 0.079] | 0.094 |
| C[rurality_3](T.Suburban) | 0.092 [0.029, 0.155] | 0.004 |
| C[rurality_3](T.Urban) | 0.022 [-0.058, 0.102] | 0.593 |
| C[operator](T.31 OPERATING) | 0.943 [0.380, 1.506] | 0.001 |
| C[operator](T.4-H OPERATING CORPORATION) | 1.088 [0.884, 1.292] | <0.001 |
| C[operator](T.8 NORTH LLC) | -0.146 [-0.334, 0.042] | 0.126 |
| C[operator](T.AKA ENERGY GROUP LLC) | 1.018 [0.924, 1.112] | <0.001 |
| C[operator](T.ANADARKO DJ GAS PROCESSING LLC) | 0.405 [0.405, 0.405] | <0.001 |
| C[operator](T.ANADARKO WATTENBERG OIL COMPLEX LLC) | 0.843 [0.745, 0.941] | <0.001 |
| C[operator](T.ANSCHUTZ EXPLORATION CORP) | -0.039 [-0.600, 0.522] | 0.892 |
| C[operator](T.BARGATH LLC) | -0.043 [-0.578, 0.492] | 0.875 |
| C[operator](T.BARRETT CORPORATION* BILL) | 0.348 [0.205, 0.491] | <0.001 |
| C[operator](T.BARRETT RESOURCES CORP) | 0.000 [0.000, 0.000] | 0.887 |
| C[operator](T.BAYLESS PRODUCER, LLC* ROBERT L) | -0.618 [-1.196, -0.040] | 0.036 |
| C[operator](T.BAYSWATER EXPLORATION & PRODUCTION LLC) | 0.432 [0.375, 0.489] | <0.001 |
| C[operator](T.BAYSWATER EXPLORATION AND PRODUCTION LLC) | 0.135 [0.002, 0.268] | 0.045 |
| C[operator](T.BERRY PETROLEUM COMPANY LLC) | 0.080 [-0.455, 0.615] | 0.769 |
| C[operator](T.BISON IV OPERATING LLC) | 0.752 [0.672, 0.832] | <0.001 |
| C[operator](T.BISON OIL & GAS II LLC) | 0.276 [0.182, 0.370] | <0.001 |
| C[operator](T.BLUE CHIP OIL INC) | 1.677 [1.493, 1.861] | <0.001 |
| C[operator](T.BNN WESTERN LLC) | 0.187 [0.062, 0.312] | 0.003 |
| C[operator](T.BONANZA CREEK ENERGY OPERATING COMPANY LLC) | 0.145 [0.047, 0.243] | 0.003 |
| C[operator](T.CAERUS PICEANCE LLC) | -0.189 [-0.720, 0.342] | 0.484 |
| C[operator](T.CAPTIVA ENERGY PARTNERS LLC) | 0.658 [0.527, 0.789] | <0.001 |
| C[operator](T.CARRIZO NIOBRARA LLC) | 0.587 [0.456, 0.718] | <0.001 |
| C[operator](T.CCRP OPERATING INC) | -0.035 [-0.166, 0.096] | 0.601 |
| C[operator](T.CHACO ENERGY COMPANY) | 3.781 [3.536, 4.026] | <0.001 |
| C[operator](T.CHEVRON PIPELINE COMPANY) | 0.075 [-0.503, 0.653] | 0.799 |
| C[operator](T.CHEVRON PRODUCTION COMPANY) | -0.162 [-0.740, 0.416] | 0.583 |
| C[operator](T.CHEVRON USA INC) | -0.079 [-0.651, 0.493] | 0.786 |
| C[operator](T.CIVITAS NORTH LLC) | 0.136 [0.032, 0.240] | 0.011 |
| C[operator](T.COACHMAN ENERGY OPERATING COMPANY LLC) | 0.993 [0.446, 1.540] | <0.001 |
| C[operator](T.COLORADO OIL & GAS CONSERVATION COMMISSION) | 0.095 [-0.130, 0.320] | 0.407 |
| C[operator](T.COMPLETE ENERGY SERVICES INC) | 0.348 [0.254, 0.442] | <0.001 |
| C[operator](T.CONFLUENCE DJ LLC) | -0.057 [-0.151, 0.037] | 0.237 |
| C[operator](T.CRESTONE PEAK RESOURCES OPERATING LLC) | 0.027 [-0.102, 0.156] | 0.685 |
| C[operator](T.CUB CREEK ENERGY) | 0.322 [0.271, 0.373] | <0.001 |
| C[operator](T.CUB CREEK ENERGY LLC) | 0.465 [0.404, 0.526] | <0.001 |
| C[operator](T.DAN A HUGHES COMPANY LP) | 0.371 [0.240, 0.502] | <0.001 |
| C[operator](T.DCP MIDSTREAM LP) | 0.370 [0.258, 0.482] | <0.001 |
| C[operator](T.DCP OPERATING COMPANY LP) | 0.293 [0.217, 0.369] | <0.001 |
| C[operator](T.DIAMOND OPERATING INC) | 0.428 [0.348, 0.508] | <0.001 |
| C[operator](T.EDGE ENERGY II LLC) | 1.724 [1.599, 1.849] | <0.001 |
| C[operator](T.ENCANA OIL & GAS (USA) INC) | -0.172 [-0.627, 0.283] | 0.460 |
| C[operator](T.ENERPLUS RESOURCES (USA) CORPORATION) | 0.377 [0.283, 0.471] | <0.001 |
| C[operator](T.EOG RESOURCES INC) | 0.222 [0.097, 0.347] | <0.001 |
| C[operator](T.EWS 13 DJ BASIN LLC) | -0.310 [-0.535, -0.085] | 0.007 |
| C[operator](T.EWS 4 DJ BASIN LLC) | 1.447 [1.353, 1.541] | <0.001 |
| C[operator](T.EXTRACTION OIL & GAS INC) | 0.286 [0.229, 0.343] | <0.001 |
| C[operator](T.EXTRACTION OIL & GAS LLC) | 0.284 [0.161, 0.407] | <0.001 |
| C[operator](T.FIFTH CREEK ENERGY OPERATING COMPANY LLC) | 0.229 [0.098, 0.360] | <0.001 |
| C[operator](T.FOUNDATION ENERGY MANAGEMENT LLC) | 0.555 [0.408, 0.702] | <0.001 |
| C[operator](T.FRITZLER RESOURCES INC) | 3.534 [3.454, 3.614] | <0.001 |
| C[operator](T.FUNDARE RESOURCES OPERATING COMPANY LLC) | 0.134 [0.048, 0.220] | 0.002 |
| C[operator](T.GADECO LLC) | 0.872 [0.645, 1.099] | <0.001 |
| C[operator](T.GENESIS GAS & OIL COLORADO LLC) | 1.486 [0.923, 2.049] | <0.001 |
| C[operator](T.GRAND RIVER GATHERING LLC) | -0.233 [-0.772, 0.306] | 0.397 |
| C[operator](T.GREAT WESTERN OPERATING COMPANY LLC) | 0.367 [0.259, 0.475] | <0.001 |
| C[operator](T.GRIZZLY OPERATING LLC) | -0.239 [-0.780, 0.302] | 0.386 |
| C[operator](T.GRYNBERG* JACK DBA GRYNBERG PETROLEUM CO) | 0.510 [0.283, 0.737] | <0.001 |
| C[operator](T.HIGHPOINT OPERATING CORPORATION) | 0.216 [0.122, 0.310] | <0.001 |
| C[operator](T.HUNTER RIDGE ENERGY SERVICES LLC) | 0.148 [-0.387, 0.683] | 0.589 |
| C[operator](T.HYNDREX RESOURCES) | 0.348 [0.254, 0.442] | <0.001 |
| C[operator](T.INDUSTRIAL GAS SERVICES INC) | 0.628 [0.383, 0.873] | <0.001 |
| C[operator](T.K P KAUFFMAN COMPANY INC) | 0.471 [0.344, 0.598] | <0.001 |
| C[operator](T.KERR MCGEE GATHERING LLC) | 0.469 [0.379, 0.559] | <0.001 |
| C[operator](T.KERR MCGEE OIL & GAS ONSHORE LP) | 0.230 [0.101, 0.359] | <0.001 |
| C[operator](T.KOCH EXPLORATION COMPANY LLC) | 1.525 [0.941, 2.109] | <0.001 |
| C[operator](T.KOCH EXPLORATION COMPANY, LLC) | 0.912 [0.336, 1.488] | 0.002 |
| C[operator](T.KP KAUFFMAN COMPANY INC) | 0.440 [0.381, 0.499] | <0.001 |
| C[operator](T.KT RESOURCES LLC) | -0.561 [-1.124, 0.002] | 0.051 |
| C[operator](T.LARAMIE ENERGY LLC) | 0.041 [-0.492, 0.574] | 0.879 |
| C[operator](T.LASSO OIL & GAS LLC) | 1.690 [1.127, 2.253] | <0.001 |
| C[operator](T.LINN OPERATING INC) | 0.066 [-0.473, 0.605] | 0.809 |
| C[operator](T.LINN OPERATING LLC) | -0.493 [-1.032, 0.046] | 0.073 |
| C[operator](T.LONGS PEAK RESOURCES LLC) | 0.007 [-0.081, 0.095] | 0.883 |
| C[operator](T.MACHII-ROSS PETROLEUM CO) | 1.914 [1.710, 2.118] | <0.001 |
| C[operator](T.MAGPIE OPERATING INC) | 4.765 [4.520, 5.010] | <0.001 |
| C[operator](T.MARALEX RESOURCES, INC) | -0.493 [-1.032, 0.046] | 0.073 |
| C[operator](T.MARATHON OIL COMPANY) | -0.088 [-0.627, 0.451] | 0.750 |
| C[operator](T.MERRION OIL & GAS CORP) | 1.087 [0.509, 1.665] | <0.001 |
| C[operator](T.MONAHAN GAS & OIL INC) | 2.022 [1.928, 2.116] | <0.001 |
| C[operator](T.MUSTANG RESOURCES LLC) | -0.288 [-0.851, 0.275] | 0.316 |
| C[operator](T.NGL WATER SOLUTIONS DJ LLC) | 0.588 [0.488, 0.688] | <0.001 |
| C[operator](T.NICKEL ROAD OPERATING LLC) | 0.073 [0.059, 0.087] | <0.001 |
| C[operator](T.NOBLE ENERGY INC) | 0.088 [-0.079, 0.255] | 0.304 |
| C[operator](T.NOBLE MIDSTREAM SERVICES LLC) | 0.363 [0.306, 0.420] | <0.001 |
| C[operator](T.NORTHSTAR GAS COMPANY INC) | 0.635 [0.057, 1.213] | 0.031 |
| C[operator](T.OXY USA INC) | 0.423 [-0.116, 0.962] | 0.123 |
| C[operator](T.OXY USA WTP LP) | -0.290 [-0.829, 0.249] | 0.290 |
| C[operator](T.PAINTED PEGASUS PETROLEUM LLC) | 1.673 [1.406, 1.940] | <0.001 |
| C[operator](T.PDC ENERGY INC) | 0.245 [0.116, 0.374] | <0.001 |
| C[operator](T.PETERSON ENERGY OPERATING INC) | 1.250 [1.038, 1.462] | <0.001 |
| C[operator](T.PETRO MEX RESOURCES) | 1.132 [0.605, 1.659] | <0.001 |
| C[operator](T.PETRO OPERATING COMPANY LLC) | 2.697 [2.550, 2.844] | <0.001 |
| C[operator](T.PETROSHARE CORPORATION) | 0.528 [0.324, 0.732] | <0.001 |
| C[operator](T.PLUG NICKEL OIL COMPANY INC) | -0.212 [-0.790, 0.366] | 0.471 |
| C[operator](T.PRAIRIE OPERATING CO LLC) | 0.439 [0.439, 0.439] | <0.001 |
| C[operator](T.PROVIDENCE OPERATING LLC DBA POCO OPERATING) | 0.000 [0.000, 0.000] | 0.835 |
| C[operator](T.RED HAWK PETROLEUM LLC) | 0.942 [0.844, 1.040] | <0.001 |
| C[operator](T.RED ROCK GATHERING COMPANY LLC) | -0.267 [-0.826, 0.292] | 0.348 |
| C[operator](T.REP PROCESSING LLC) | 0.715 [0.635, 0.795] | <0.001 |
| C[operator](T.RIO MESA RESOURCES INC) | 0.825 [0.262, 1.388] | 0.004 |
| C[operator](T.ROBERT L BAYLESS PRODUCER LLC) | 0.132 [-0.431, 0.695] | 0.645 |
| C[operator](T.ROCKY MOUNTAIN MIDSTREAM LLC) | 0.403 [0.356, 0.450] | <0.001 |
| C[operator](T.ROCKY MOUNTAIN NATURAL GAS LLC) | 1.328 [0.750, 1.906] | <0.001 |
| C[operator](T.RWL ENTERPRISES) | 1.469 [1.265, 1.673] | <0.001 |
| C[operator](T.SAMSON RESOURCES COMPANY) | 0.373 [-0.211, 0.957] | 0.210 |
| C[operator](T.SCHNEIDER ENERGY SERVICES INC) | -0.288 [-0.533, -0.043] | 0.021 |
| C[operator](T.SCOUT ENERGY MANAGEMENT LLC) | -0.365 [-0.928, 0.198] | 0.204 |
| C[operator](T.SMITH ENERGY CORP) | 0.778 [0.539, 1.017] | <0.001 |
| C[operator](T.SMITH OIL PROPERTIES INC) | 2.725 [2.521, 2.929] | <0.001 |
| C[operator](T.SRC ENERGY INC) | 0.368 [0.229, 0.507] | <0.001 |
| C[operator](T.SUMMIT DJ-S LLC) | 5.009 [4.929, 5.089] | <0.001 |
| C[operator](T.SUMMIT MIDSTREAM NIOBRARA LLC) | -0.035 [-0.166, 0.096] | 0.601 |
| C[operator](T.SUMMIT MIDSTREAM PARTNERS LLC) | 0.128 [-0.409, 0.665] | 0.640 |
| C[operator](T.SYNERGY RESOURCES CORPORATION) | 0.382 [0.217, 0.547] | <0.001 |
| C[operator](T.TALLGRASS WATER WESTERN LLC) | 0.022 [-0.058, 0.102] | 0.593 |
| C[operator](T.TAPROOT ROCKIES MIDSTREAM LLC) | 0.103 [0.023, 0.183] | 0.013 |
| C[operator](T.TEP ROCKY MOUNTAIN LLC) | -0.225 [-0.762, 0.312] | 0.413 |
| C[operator](T.TEXAS TEA OF COLORADO LLC DBA TEXAS TEA LLC) | -0.310 [-0.535, -0.085] | 0.007 |
| C[operator](T.TINDALL OPERATING COMPANY) | -0.288 [-0.533, -0.043] | 0.021 |
| C[operator](T.TOP OPERATING COMPANY) | 0.165 [-0.060, 0.390] | 0.152 |
| C[operator](T.UPLAND EXPLORATION LLC) | 2.587 [2.507, 2.667] | <0.001 |
| C[operator](T.URSA OPERATING COMPANY LLC) | -0.116 [-0.659, 0.427] | 0.674 |
| C[operator](T.UTAH GAS OP LTD DBA UTAH GAS CORP) | 1.334 [0.770, 1.898] | <0.001 |
| C[operator](T.VANGUARD OPERATING LLC) | -0.116 [-0.663, 0.431] | 0.678 |
| C[operator](T.VERDAD OIL & GAS CORPORATION) | -0.057 [-0.151, 0.037] | 0.237 |
| C[operator](T.VERDAD RESOURCES LLC) | 0.186 [0.123, 0.249] | <0.001 |
| C[operator](T.VISION ENERGY LLC) | 0.976 [0.435, 1.517] | <0.001 |
| C[operator](T.WARD PETROLEUM CORPORATION) | 0.371 [0.240, 0.502] | <0.001 |
| C[operator](T.WEXPRO COMPANY) | 0.884 [0.300, 1.468] | 0.003 |
| C[operator](T.WHITING OIL & GAS CORPORATION) | 0.114 [-0.019, 0.247] | 0.092 |
| C[operator](T.WINDSOR ENERGY GROUP LLC) | 2.659 [2.081, 3.237] | <0.001 |
| C[operator](T.WOODARD* SANDRA K) | -0.618 [-1.196, -0.040] | 0.036 |
| C[operator](T.WPX ENERGY ROCKY MOUNTAIN LLC) | -0.528 [-1.067, 0.011] | 0.055 |
| C[operator](T.XTO ENERGY INC) | -0.301 [-0.875, 0.273] | 0.303 |
| Post | -0.057 [-0.151, 0.037] | 0.237 |
| Historical | 0.108 [-0.049, 0.265] | 0.177 |
| Post × Historical | 0.202 [0.069, 0.335] | 0.003 |

Fit stats:

| Model | N | AIC | BIC | LogLik | R2 | Adj R2 |
| --- | --- | --- | --- | --- | --- | --- |
| H2 delay>0 OLS | 15814 | 32881.364 | 33970.312 | -16298.682 | 0.155 | 0.147 |

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

### Table H2-E (Appendix): late30 and late90 logits (full model terms)

**Panel 1: late30 logit (ORs)**

| Term | OR [95% CI] | p |
| --- | --- | --- |
| Intercept | 0.002 [0.001, 0.007] | <0.001 |
| C[rurality_3](T.Suburban) | 1.097 [0.373, 3.232] | 0.866 |
| C[rurality_3](T.Urban) | 0.796 [0.422, 1.502] | 0.482 |
| C[county_top3](T.RIO BLANCO) | 8.014 [2.959, 21.704] | <0.001 |
| C[county_top3](T.WELD) | 1.240 [0.309, 4.974] | 0.762 |
| Post | 2.082 [0.827, 5.242] | 0.120 |
| Historical | 7.471 [2.364, 23.605] | <0.001 |
| Post × Historical | 0.774 [0.275, 2.179] | 0.628 |

Fit stats:

| Model | N | AIC | BIC | LogLik | Pseudo R2 |
| --- | --- | --- | --- | --- | --- |
| H2 late30 logit | 26376 | 3877.807 | 3943.249 | -1930.904 | 0.090 |

**Panel 2: late90 logit (ORs)**

| Term | OR [95% CI] | p |
| --- | --- | --- |
| Intercept | 0.000 [0.000, 0.001] | <0.001 |
| C[rurality_3](T.Suburban) | 1.175 [0.377, 3.658] | 0.781 |
| C[rurality_3](T.Urban) | 0.647 [0.354, 1.181] | 0.156 |
| C[county_top3](T.RIO BLANCO) | 8.023 [1.317, 48.871] | 0.024 |
| C[county_top3](T.WELD) | 2.400 [0.400, 14.400] | 0.338 |
| Post | 15.055 [1.631, 139.000] | 0.017 |
| Historical | 37.544 [3.303, 426.734] | 0.003 |
| Post × Historical | 0.167 [0.016, 1.751] | 0.136 |

Fit stats:

| Model | N | AIC | BIC | LogLik | Pseudo R2 |
| --- | --- | --- | --- | --- | --- |
| H2 late90 logit | 26376 | 2127.648 | 2193.090 | -1055.824 | 0.102 |

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
