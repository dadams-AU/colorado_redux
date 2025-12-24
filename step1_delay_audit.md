# Step 1 measurement audit for reporting delay (Colorado spills)

This report diagnoses whether `delay_days` values (especially 99+) look like true delays vs. top-coding/placeholder/heaping, and where they concentrate.
**No filtering/capping/winsorizing is performed in this step.**

## Inputs & denominators
- Rows total: 26,376
- Non-missing delay_days: 26,376
- Non-integer delay_days (not exactly whole-day): 0
- Spill type column: `Spill Type`
- Operator column: `Operator`
- County column: `county`
- RUCA/rurality source column: `rurality`

## A) Heaping / spikes at key values
### A1) Exact-value frequency (key values)
```
 n_all_rows  n_nonmissing_delay  delay_days_value  n_exact  pct_of_all_rows  pct_of_nonmissing_delay
      26376               26376                 0    10562          40.0440                  40.0440
      26376               26376                 1     9300          35.2593                  35.2593
      26376               26376                 2     2896          10.9797                  10.9797
      26376               26376                 3     1894           7.1808                   7.1808
      26376               26376                 4      354           1.3421                   1.3421
      26376               26376                 5      190           0.7204                   0.7204
      26376               26376                 6      110           0.4170                   0.4170
      26376               26376                 7      128           0.4853                   0.4853
      26376               26376                14       32           0.1213                   0.1213
      26376               26376                21       22           0.0834                   0.0834
      26376               26376                30        6           0.0227                   0.0227
      26376               26376                60        0           0.0000                   0.0000
      26376               26376                90        0           0.0000                   0.0000
      26376               26376                98        2           0.0076                   0.0076
      26376               26376                99       10           0.0379                   0.0379
      26376               26376               100        2           0.0076                   0.0076
      26376               26376               180        2           0.0076                   0.0076
      26376               26376               365        8           0.0303                   0.0303
```

### A2) Neighborhood around 99 (90–110)
```
 delay_days_int  n_exact  pct_of_nonmissing_delay  pct_of_all_rows
             90        0                   0.0000           0.0000
             91        0                   0.0000           0.0000
             92        6                   0.0227           0.0227
             93        0                   0.0000           0.0000
             94        0                   0.0000           0.0000
             95        2                   0.0076           0.0076
             96        2                   0.0076           0.0076
             97        0                   0.0000           0.0000
             98        2                   0.0076           0.0076
             99       10                   0.0379           0.0379
            100        2                   0.0076           0.0076
            101        2                   0.0076           0.0076
            102        2                   0.0076           0.0076
            103        2                   0.0076           0.0076
            104        0                   0.0000           0.0000
            105        2                   0.0076           0.0076
            106        0                   0.0000           0.0000
            107        0                   0.0000           0.0000
            108        0                   0.0000           0.0000
            109        2                   0.0076           0.0076
            110        0                   0.0000           0.0000
```

Plot saved: `/home/dadams/Repos/colorado_redux/analysis_postgis/step1_delay_audit_outputs/delay_days_neighborhood_90_110.png`

### A3) Top 20 most frequent delay_days values (integer-only; includes <NA> bucket if many non-integers)
```
 delay_days_int     n  pct_of_all_rows
              0 10562           40.044
              1  9300          35.2593
              2  2896          10.9797
              3  1894           7.1808
              4   354           1.3421
              5   190           0.7204
              7   128           0.4853
              6   110            0.417
              8    80           0.3033
              9    52           0.1971
             10    44           0.1668
             12    42           0.1592
             15    38           0.1441
             14    32           0.1213
             11    30           0.1137
             17    26           0.0986
             18    24            0.091
             13    24            0.091
             21    22           0.0834
             33    18           0.0682
```

Plot saved: `/home/dadams/Repos/colorado_redux/analysis_postgis/step1_delay_audit_outputs/delay_days_top20.png`

## B) Where the 99+ values live (concentration)
### B4) Indicators
- `is_99 = (delay_days_int == 99)`
- `ge_99 = (delay_days >= 99)`
- `ge_90 = (delay_days >= 90)`
- `ge_30 = (delay_days >= 30)`

### B5) Cross-tabs (n, % within-group, % of total rows)
#### is_99 by period
```
   period  n_total  n_true  pct_true_within_group  pct_true_of_total_rows
post_2020    15704      10                 0.0637                  0.0379
 pre_2020    10672       0                 0.0000                  0.0000
```

#### ge_99 by period
```
   period  n_total  n_true  pct_true_within_group  pct_true_of_total_rows
post_2020    15704     166                 1.0571                  0.6294
 pre_2020    10672      22                 0.2061                  0.0834
```

#### is_99 by spill type
```
spill_type  n_total  n_true  pct_true_within_group  pct_true_of_total_rows
Historical    11294       4                 0.0354                  0.0152
    Recent    15082       6                 0.0398                  0.0227
```

#### ge_99 by spill type
```
spill_type  n_total  n_true  pct_true_within_group  pct_true_of_total_rows
Historical    11294     158                 1.3990                  0.5990
    Recent    15082      30                 0.1989                  0.1137
```

#### is_99 by period × spill type
```
   period spill_type  n_total  n_true  pct_true_within_group  pct_true_of_total_rows
post_2020 Historical     7518       4                 0.0532                  0.0152
post_2020     Recent     8186       6                 0.0733                  0.0227
 pre_2020 Historical     3776       0                 0.0000                  0.0000
 pre_2020     Recent     6896       0                 0.0000                  0.0000
```

#### ge_99 by period × spill type
```
   period spill_type  n_total  n_true  pct_true_within_group  pct_true_of_total_rows
post_2020 Historical     7518     136                 1.8090                  0.5156
post_2020     Recent     8186      30                 0.3665                  0.1137
 pre_2020 Historical     3776      22                 0.5826                  0.0834
 pre_2020     Recent     6896       0                 0.0000                  0.0000
```

### B6) By operator
#### Top 25 operators by total spills
```
                                  operator  n_total  pct_ge_99  pct_is_99  median_delay  p95_delay  p99_delay
                          NOBLE ENERGY INC   5430.0     1.1786     0.0000           1.0       3.00     114.00
           KERR MCGEE OIL & GAS ONSHORE LP   4714.0     0.4243     0.0424           0.0       3.00      17.61
                            PDC ENERGY INC   2454.0     0.3260     0.0000           1.0       3.00      27.00
                       CAERUS PICEANCE LLC   2194.0     0.1823     0.0912           1.0       3.00      18.28
BONANZA CREEK ENERGY OPERATING COMPANY LLC   1130.0     0.0000     0.0000           1.0       4.00       9.00
                   KP KAUFFMAN COMPANY INC    940.0     2.3404     0.6383           1.0      31.00     435.87
                           CHEVRON USA INC    872.0     1.6055     0.0000           2.0       7.00     202.00
           HIGHPOINT OPERATING CORPORATION    856.0     0.0000     0.0000           1.0       3.00       5.00
     CRESTONE PEAK RESOURCES OPERATING LLC    694.0     0.2882     0.0000           1.0       3.00      17.00
                    TEP ROCKY MOUNTAIN LLC    592.0     0.0000     0.0000           1.0       3.00       4.00
                  EXTRACTION OIL & GAS INC    494.0     1.6194     0.0000           1.0       3.00     113.00
             WHITING OIL & GAS CORPORATION    446.0     0.0000     0.0000           1.0       4.00      35.00
                  DCP OPERATING COMPANY LP    400.0     0.0000     0.0000           1.0      13.05      27.00
                        LARAMIE ENERGY LLC    286.0     0.0000     0.0000           1.0      17.00      65.00
                  KERR MCGEE GATHERING LLC    250.0     0.0000     0.0000           1.0       7.00      36.00
                          DCP MIDSTREAM LP    208.0     0.0000     0.0000           1.0       9.00      26.00
       GREAT WESTERN OPERATING COMPANY LLC    206.0     1.9417     0.0000           1.0       6.00     103.00
   FUNDARE RESOURCES OPERATING COMPANY LLC    196.0     1.0204     0.0000           1.0       5.00      20.20
                            XTO ENERGY INC    184.0     0.0000     0.0000           1.0       3.00      10.99
             WPX ENERGY ROCKY MOUNTAIN LLC    164.0     0.0000     0.0000           0.0       1.00       1.00
          FOUNDATION ENERGY MANAGEMENT LLC    160.0     2.5000     0.0000           2.0       7.00     176.00
                            SRC ENERGY INC    158.0     2.5316     0.0000           1.0       6.90     303.00
                      VERDAD RESOURCES LLC    144.0     0.0000     0.0000           1.0       3.00       5.00
                 BARRETT CORPORATION* BILL    140.0     0.0000     0.0000           1.0      29.00      42.00
                 GRAND RIVER GATHERING LLC    138.0     0.0000     0.0000           1.0       5.00      25.00
```

#### Top 15 operators by pct_ge_99 (min n >= 50)
```
                               operator  n_total  pct_ge_99  pct_is_99  median_delay  p95_delay  p99_delay
      UTAH GAS OP LTD DBA UTAH GAS CORP    122.0     6.5574     0.0000           1.0      130.0     167.37
                 BISON IV OPERATING LLC     70.0     5.7143     0.0000           2.0      105.2     188.00
                         SRC ENERGY INC    158.0     2.5316     0.0000           1.0        6.9     303.00
       FOUNDATION ENERGY MANAGEMENT LLC    160.0     2.5000     0.0000           2.0        7.0     176.00
                KP KAUFFMAN COMPANY INC    940.0     2.3404     0.6383           1.0       31.0     435.87
    GREAT WESTERN OPERATING COMPANY LLC    206.0     1.9417     0.0000           1.0        6.0     103.00
 BAYSWATER EXPLORATION & PRODUCTION LLC    116.0     1.7241     0.0000           2.0       13.0      90.10
               EXTRACTION OIL & GAS INC    494.0     1.6194     0.0000           1.0        3.0     113.00
                        CHEVRON USA INC    872.0     1.6055     0.0000           2.0        7.0     202.00
                       NOBLE ENERGY INC   5430.0     1.1786     0.0000           1.0        3.0     114.00
FUNDARE RESOURCES OPERATING COMPANY LLC    196.0     1.0204     0.0000           1.0        5.0      20.20
        KERR MCGEE OIL & GAS ONSHORE LP   4714.0     0.4243     0.0424           0.0        3.0      17.61
                         PDC ENERGY INC   2454.0     0.3260     0.0000           1.0        3.0      27.00
  CRESTONE PEAK RESOURCES OPERATING LLC    694.0     0.2882     0.0000           1.0        3.0      17.00
                    CAERUS PICEANCE LLC   2194.0     0.1823     0.0912           1.0        3.0      18.28
```

### B7) By geography
#### Top counties by total spills
```
county_norm  n_total  pct_ge_99  pct_is_99  median_delay  p95_delay  p99_delay
       WELD  20874.0     0.7761     0.0383           1.0        4.0       58.0
   GARFIELD   3478.0     0.1725     0.0000           1.0        6.0       21.0
 RIO BLANCO   2024.0     0.9881     0.0988           1.0       18.0       92.0
```

#### Rurality summary
```
rurality_3  n_total  pct_ge_99  pct_is_99  median_delay  p95_delay  p99_delay
     Urban  13854.0     0.8084     0.0144           1.0        4.0      64.00
     Rural  10564.0     0.5869     0.0189           1.0        6.0      50.00
  Suburban   1958.0     0.7150     0.3064           1.0        8.0      37.45
```

#### Rurality × period
```
rurality_3    period  n_total  pct_ge_99  median_delay  p95_delay
     Rural post_2020   5900.0     1.0508           1.0        5.0
     Rural  pre_2020   4664.0     0.0000           1.0        7.0
  Suburban post_2020   1230.0     0.9756           1.0        5.0
  Suburban  pre_2020    728.0     0.2747           1.0        9.0
     Urban post_2020   8574.0     1.0730           0.0        3.0
     Urban  pre_2020   5280.0     0.3788           1.0        4.0
```


## C) Sanity checks on date construction
Using discovery date column `Date of Discovery` and report date column `Initial Report Date`.

- Random-sample mismatch rate (n up to 200; tol=1e-06): 0.000%

### C8) Mismatch examples (up to 20)
```
Empty DataFrame
Columns: [period, spill_type, county_norm, operator, Date of Discovery, Initial Report Date, delay_days, delay_recomputed_days, abs_diff_days]
Index: []
```

### C8) Missingness (overall)
```
    n  n_disc_missing  n_rpt_missing  pct_disc_missing  pct_rpt_missing
26376               0              0               0.0              0.0
```

### C8) Missingness (by period × spill type)
```
   period spill_type    n  n_disc_missing  n_rpt_missing  pct_disc_missing  pct_rpt_missing
post_2020 Historical 7518               0              0               0.0              0.0
post_2020     Recent 8186               0              0               0.0              0.0
 pre_2020 Historical 3776               0              0               0.0              0.0
 pre_2020     Recent 6896               0              0               0.0              0.0
```

### C8) Missingness correlation with 99 / 99+
```
    group     n  pct_disc_missing  pct_rpt_missing
    is_99    10               0.0              0.0
not_is_99 26366               0.0              0.0
    ge_99   188               0.0              0.0
    lt_99 26188               0.0              0.0
```

## D) Conclusions (computed bullets)
- Rows total: 26,376. Non-missing delay_days: 26,376. Non-integer delay_days (not exactly whole-day): 0.
- Exact 99 count (integer-only): 10. Neighborhood 98=2, 100=2. Spike ratio vs 95–105 (excluding 99): 6.25 (higher suggests heaping at 99).
- Pre/post: pct_is_99 pre=0.000% vs post=0.064%. pct_ge_99 pre=0.206% vs post=1.057%.
- Spill Type concentration: pct_ge_99 Historical=1.399% vs Recent=0.199% (big gap suggests tail is classification-driven).
- Operator concentration: highest pct_ge_99 among operators with n>=50 is 'UTAH GAS OP LTD DBA UTAH GAS CORP' at 6.557% (n=122).
- County concentration: largest-count county is 'WELD' (n=20,874); its pct_ge_99=0.776%.
- Rurality: bucket 'Urban' has highest pct_ge_99 among n>=100 at 0.808% (n=13,854).
- Date sanity (random sample n=200): mismatch rate vs recomputed (tol 1e-06): 0.000%.

## Outputs
- Markdown report: `/home/dadams/Repos/colorado_redux/step1_delay_audit.md`
- Outputs directory: `/home/dadams/Repos/colorado_redux/analysis_postgis/step1_delay_audit_outputs`
- CSVs written for each table (see outputs directory)
- PNG: `/home/dadams/Repos/colorado_redux/analysis_postgis/step1_delay_audit_outputs/delay_days_neighborhood_90_110.png`
- PNG: `/home/dadams/Repos/colorado_redux/analysis_postgis/step1_delay_audit_outputs/delay_days_top20.png`