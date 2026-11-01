# Education: lunch eligibility and ACT scores

This project explores how the association between free/reduced-price lunch eligibility and school-average ACT-equivalent scores varies across states represented in the EdGap data.

For this project, I’m looking at how free or reduced-price lunch eligibility relates to a school’s average ACT score, and whether that relationship looks different across states. I wanted to compare schools within each state rather than put everything together and assume the pattern would be the same everywhere.

I’m using the EdGap data provided in DATA 5100, along with NCES school information to identify each school’s state and level. I also added a Census Bureau reference that groups states into regions. The scores in EdGap are ACT averages or SAT averages converted to ACT equivalents.

One issue came up while joining the files: the NCES download linked on the setup assignment had rounded school IDs, so the schools wouldn’t match reliably. The alternate file on the course’s Data Collection page had the full IDs, and that’s the version used here. I used a left join to keep all the EdGap records while adding the school details.

After checking the values, keeping identified high schools, and removing schools with missing ACT scores, the cleaned data has 7,227 schools across 20 states. Of those, 7,207 have both reported ACT scores and lunch-eligibility values. I kept two versions of the cleaned data—one with missing predictors left as they were, and another with those gaps filled using an iterative imputer. The main state comparisons use reported lunch values, so they don’t depend on those estimates.

In all 20 states represented, higher lunch eligibility is associated with lower average ACT-equivalent scores. The strength of that relationship varies, with correlations ranging from about -0.63 to -0.88. That’s a pattern in this sample, though—not evidence that lunch eligibility causes lower scores. Differences in test participation, reporting, and which schools are included could also affect the results. Since the data only covers 20 states, I wouldn’t treat it as a picture of the whole country.

The analysis is in code\Education.ipynb. The data folder holds the source files and cleaned exports, and reports contains the charts, summary tables, and cleaning checks. To run it, install the packages in requirements.txt, open the notebook, and run the cells in order. All cells have been run successfully, and the checks confirm that imputation didn’t change the reported ACT scores or the predictor values that were already available.

For the next stage, I’m planning to try predicting school-average scores from the socioeconomic variables and checking whether prediction errors differ across states. That modeling work isn’t included yet. When I get to it, I’ll fit the imputer on training data only rather than use the full-data imputed file from this exploratory analysis.

Data sources: EdGap course spreadsheet, NCES school information, and Census Bureau regions.
