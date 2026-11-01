# Verified Week 3 results

## Data preparation

- Original EdGap records: **7,986**.
- NCES school records: **102,181**, with unique, intact school IDs.
- Left join: **7,986** records retained; **88** had no NCES match.
- Identified high schools: **7,230**.
- High schools with observed ACT and state: **7,227**, across **20 states**.
- Schools with both observed ACT and lunch eligibility: **7,207**.

The assignment-page Dropbox file contained rounded identifiers. The alternate NCES file linked on the course Data Collection page had intact identifiers and was used instead. The notebook checks this before joining.

## State comparison

All 20 represented states show a negative within-state Pearson correlation between lunch eligibility and ACT-equivalent averages. The correlations range from approximately **-0.878 to -0.634**. Paired sample sizes range from **24 schools in Delaware** to **913 in Texas**.

This pattern is consistent with an association between socioeconomic disadvantage and school-average test performance in this sample. It does not show that lunch eligibility causes lower scores. A school's average score also reflects factors such as student composition, test participation, and reporting practices.

Do not rank states by these correlations without accounting for sampling variability and differences in the available schools. The sample covers only 20 states, and school-level results cannot be used to infer individual students' performance.

## Missing data

After outcome and school-level exclusions, missing predictor counts are:

| Predictor | Missing values |
|---|---:|
| Unemployment rate | 12 |
| College-degree share | 11 |
| Married-family share | 20 |
| Median household income | 16 |
| Lunch eligibility share | 20 |

Missingness counts include originally missing values and values identified as invalid during cleaning. The notebook exports both the observed and imputed versions and a state-level sensitivity table.

## Validation

All seven code cells executed successfully and the executed notebook was saved. Checks confirmed valid score/share ranges, unique school IDs, unchanged observed predictors and outcomes, missingness indicators, and three nonempty plot files. Four synthetic tests cover insufficient pairs, constant values, a known negative correlation, and missing lunch observations.

For a future predictive project, use the non-imputed cleaned export and fit preprocessing on training folds only. Do not evaluate a model using the full-data imputed EDA export.
