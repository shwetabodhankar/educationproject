# Predicting School ACT Scores: Does the Model Work Equally Well Across States?

**Team member:** Shweta Bodhankar  
**Arrangement:** Solo project, with instructor approval.
**Status:** Proposal draft for review.

## Problem statement

I want to find out whether we can predict a school's average ACT score using information like household income, unemployment, adult education, family structure, and free or reduced-price lunch eligibility. I'm also interested in whether the model works better in some states than others. A model could look good overall but still make larger errors for schools in a particular state, so I don't want to stop at one overall accuracy number.

This matters because the project looks at educational opportunity and how it relates to a school's socioeconomic context. I'll be working with school averages, not individual students' scores. I also won't be claiming that poverty or lunch eligibility causes a particular score.

## Data sources and access

I'll use the EdGap spreadsheet from our DATA 5100 course, which the course describes as 2016 data [1]. It has the school-average scores and the five socioeconomic variables I need. Some of the scores were converted from SAT averages to ACT equivalents, so that's something to keep in mind when comparing schools. I'll add the state and school level from the 2016-2017 NCES file [2], along with Census Bureau region information for geographic context [3].

All three files are already downloaded, and the data-preparation notebook runs. The left join kept all 7,986 EdGap records. After keeping identified high schools and removing schools with missing ACT scores, there are 7,227 schools across 20 states. Of those, 7,207 have both ACT scores and lunch-eligibility values. That gives me enough data to get started, but it doesn't cover the whole country.

One issue came up with the NCES download linked on the assignment page: its school IDs were rounded, which would make the matches unreliable. The alternative file on the Data Collection page has intact IDs, so that's the version used in the notebook. The cleaning also checks for duplicate IDs, flags impossible values, and records which rows were left out.

For modeling, I'll start with the cleaned file that still has missing predictor values. I'll fill those gaps using only the training data in each split or cross-validation fold. I won't fill in missing ACT scores, since those are the outcomes I'm trying to predict.

## Analytical approach

Each row will be one school. The model will use the five socioeconomic variables to predict that school's average ACT-equivalent score. I'll first try a simple baseline that predicts the training-set average for every school. Then I'll try multiple linear regression, since it's a useful starting point and its coefficients are easier to interpret. If the predictors overlap enough to make the estimates unstable, I may also compare ridge regression.

I'll split the schools into training and test sets, making sure each available state is represented in both. The test set will stay separate while I choose the model and fit the preprocessing steps. I'll also try leaving out one state at a time to see how the model does on schools from a state it hasn't seen during training.

I'll report mean absolute error and root mean squared error, both overall and for each state, along with the number of test schools. States with fewer schools will need more cautious interpretation. Any relationships I find will be treated as associations, not proof of cause and effect.

## Solution technologies

I'll use Python with pandas and NumPy to work with the data, scikit-learn for the models, and Matplotlib and Seaborn for the charts. I'll keep the steps and explanations together in a Jupyter notebook. A scikit-learn pipeline will help make sure that filling missing values, scaling, and model fitting happen using the training data only [4].

The files fit on my computer, so I don't expect to need cloud computing or a distributed system. I'll use GitHub to keep track of the code, documentation, and data files that can be shared.

## Main challenge and risks

The hardest part will be figuring out what differences in prediction errors across states actually mean. A larger error might reflect a weaker model, but it could also come from differences in which schools or students took the tests and how scores were reported. There are also missing states, converted SAT scores, and missing values that may not be spread evenly across schools.

Another limitation is that census-tract information may not line up exactly with a school's attendance area. Some predictors may also be closely related to each other. These issues make the project more than just fitting a regression: I'll need to check the data carefully, compare against the baseline, and be clear about what the results can and can't tell us.

## Related work and citations

The Education exercise in DATA 5100 is my starting point for the question and data preparation. My next step is to build the prediction models and compare their errors across states. I'll use the sources below for data and background, and I won't copy another project's code or notebook.

1. [EdGap course spreadsheet](https://github.com/brian-fischer/DATA-5100/blob/main/EdGap_data.xlsx) and [EdGap background](https://www.edgap.org/).
2. [Course-linked NCES CSV](https://www.dropbox.com/s/lkl5nvcdmwyoban/ccd_sch_029_1617_w_1a_11212017.csv?dl=1); [NCES school universe documentation](https://nces.ed.gov/ccd/pubschuniv.asp).
3. [Census Bureau regions and divisions](https://www2.census.gov/geo/docs/maps-data/maps/reg_div.txt).
4. [Scikit-learn imputation documentation](https://scikit-learn.org/stable/modules/impute.html).

## Solo collaboration and work plan

I'm doing this project on my own with instructor approval, so I'll handle the cleaning, modeling, charts, and write-up. I plan to use Canvas messages or university email for instructor updates so the communication is easy to share and refer back to, rather than relying on texts or WhatsApp. I'll share the code and documentation through GitHub, along with data that I'm allowed to redistribute.

My proposed plan is to set aside one focused work session each week and send a short progress update to the instructor. I still need to confirm the day and time. I'll first review the question and cleaning results, then build the baseline and regression models, compare the overall and state-level errors, and finish the notebook and report. Since I'm working alone, all of these next steps are mine. At the end of each session, I'll note what I finished, what got stuck, and what I need to do next.

**Acknowledgement:** I used AI assistance to develop this draft. I'll review the plan and wording to make sure they reflect my understanding and follow any course disclosure requirements.
