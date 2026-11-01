# Education: lunch eligibility and ACT scores

This project explores how the association between free/reduced-price lunch eligibility and school-average ACT-equivalent scores varies across states represented in the EdGap data.

## Project Overview

- **Objective:** Compare school-level associations within states, rather than treating the available schools as a representative national sample.
- **Domain:** Educational opportunity.
- **Techniques:** Data validation, left joins, missing-data assessment, iterative imputation, descriptive statistics, scatter plots, and correlations.
- **Scope:** Week 3 data preparation and exploratory analysis. Predictive modeling is not included.

## Project Structure

```text
education/
  data/                 Raw datasets and generated clean datasets
  code/                 Education.ipynb
  reports/              Generated tables, plots, and discussion drafts
  requirements.txt
  README.md
```

## Data

1. [EdGap course data](https://github.com/brian-fischer/DATA-5100/blob/main/EdGap_data.xlsx), sourced from [EdGap](https://www.edgap.org/). The course describes this as 2016 data. It includes school-average ACT scores (including converted SAT scores), census-tract socioeconomic measures, and school lunch eligibility.
2. [NCES school information CSV linked on the course Data Collection page](https://www.dropbox.com/s/lkl5nvcdmwyoban/ccd_sch_029_1617_w_1a_11212017.csv?dl=1), for 2016-2017, saved as `nces_school_information.csv`. [NCES background](https://nces.ed.gov/ccd/pubschuniv.asp). The alternate Dropbox link on the setup assignment contained rounded scientific-notation identifiers and many duplicate keys. This module-linked version preserves all 102,181 unique school IDs; do not substitute the rounded-ID version.
3. [Census Bureau regions, divisions, and state FIPS codes](https://www2.census.gov/geo/docs/maps-data/maps/reg_div.txt). This additional reference supplies geographic context; it does not add school outcomes or expand EdGap coverage.

The original files remain unchanged. The notebook exports cleaned data separately. Dataset redistribution permissions should be checked before publishing; no new license is asserted for these sources.

## Analysis

The notebook:

1. Checks file availability, schemas, school IDs, and duplicate join keys.
2. Left-joins NCES metadata onto EdGap without increasing the row count.
3. Adds Census region information by full state name.
4. Replaces impossible numerical values with missing values and audits exclusions.
5. Restricts the analysis to identified high schools with observed ACT outcomes.
6. Produces a cleaned, non-imputed version and a separate imputed version with missingness indicators.
7. Uses observed lunch eligibility for the main state comparisons and compares those results with imputed-data summaries.

An iterative imputer is fitted on the full cleaned dataset **only for descriptive EDA**. For later predictive evaluation, split the data first and fit the imputer on training data only.

## Results and Limitations

The notebook was executed successfully. The 7,986 EdGap rows were preserved by the left join; 88 did not match NCES. Restricting to identified high schools left 7,230 rows, and removing missing ACT outcomes left 7,227 schools across 20 states. The observed ACT/lunch comparison includes 7,207 paired schools.

Within-state Pearson correlations are negative in all 20 represented states, ranging from approximately -0.878 to -0.634. This describes the available sample, not a causal effect or a statistically established ranking of states. State paired sample sizes range from 24 to 913.

The state summary, cleaning audit, missingness table, and three plots are saved in `reports`. Correlations with fewer than three paired observations or a constant variable are explicitly unavailable. Observed predictors and ACT outcomes were verified to remain unchanged in the imputed export; correlation handling was checked on four synthetic edge cases.

These are school-level associations, not estimates of the causal effect of lunch eligibility, poverty, or any policy. Census-tract measures do not describe individual students. Missing states, test participation, ACT/SAT conversions, and differences in reporting may limit comparability. Do not interpret absence from this dataset as absence of schools in a state.

