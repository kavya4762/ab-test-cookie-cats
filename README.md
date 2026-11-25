# A/B Test: Cookie Cats Gate Placement

**Question:** does moving the first gate from level 30 to level 40 change 7-day retention?

## Result

Moving the gate to level 40 **lowered 7-day retention by 0.82 percentage points** (19.02% → 18.20%, a 4.3% relative drop; 95% CI -1.33 to -0.31 pp; p = 0.0016). Recommendation: **keep the gate at level 30.**

| | gate_30 (control) | gate_40 (test) |
|---|---|---|
| Players | 44,699 | 45,489 |
| Retained at day 7 | 8,501 | 8,279 |
| 7-day retention | 19.02% | 18.20% |

## Data

Public "Mobile Games A/B Testing – Cookie Cats" dataset from Kaggle (90,188 players after removing one extreme outlier). The data file is not included in this repo; [download](https://www.kaggle.com/datasets/mursideyarkin/mobile-games-ab-testing-cookie-cats?resource=download
) it from Kaggle and place it next to the script. 
Link to dataset: 
## Method

1. Hypothesis, primary metric (7-day retention) and alpha (0.05) written before analysis
2. Data quality checks (duplicates, nulls, one extreme outlier removed)
3. Sample-ratio check on group sizes (p = 0.0085, a small imbalance, noted as a caveat)
4. Group metrics with SQL (SQLite)
5. Two-proportion z-test, 95% confidence interval and a simulation check of the interval
6. Chi-square test in SPSS as an independent confirmation (p = .002)
7. Secondary metric: 1-day retention (-0.59 pp, p = 0.074, not significant)
8. Exploratory segment analysis by rounds played with Bonferroni correction (clearest drop among players with 30-99 rounds; rounds played is measured after the gate, so this is not proof of cause)

## Caveats

- Revenue is not in the data; a later gate might change in-app purchases.
- One game and a single 7-day retention window.

## Files

- `a_b_testing.py`: full analysis 
- `retention7_by_version.png`, `retention7_by_segment.png`: charts
- `recommendation.pdf`: one-page recommendation
- `spss_chi_square.png`: SPSS crosstab and chi-square output

## How to run

```
pip install pandas numpy scipy matplotlib seaborn
python a_b_testing.py
```

Set `PATH` at the top of the script to where you saved `cookie_cats.csv`.
