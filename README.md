# Spinal Tumor Disparities: SEER Analysis

## Overview
This project examines racial and ethnic differences in surgery receipt and survival status among adult and pediatric patients with spinal tumors. It relates to my work as a neurosurgery resident and my interests in oncology and disparities research.

## Dataset
- Source: SEER Research Data, 1975–2023, November 2025 Submission
- Website: https://seer.cancer.gov/data/
- Cohort: 5,831 spinal tumor records diagnosed during 2010–2023
- Original export: 25 columns
- Outcome: Survival status at the study cutoff, coded 0 = living and 1 = deceased

The patient-level CSV is excluded because SEER restricts redistribution. Reproducing the analysis requires authorized access to the corresponding SEER export. Any processing environment must meet the applicable SEER agreement requirements.

## Notebook Workflow
1. CSV upload, automated profiling, and input validation
2. Descriptive statistics and exploratory visualizations
3. Data cleaning, predictor selection, and treatment-time feature engineering
4. Stratified 80/20 training/test split
5. Training-only imputation, scaling, and categorical encoding
6. Logistic regression, decision tree, and random forest classification
7. Model evaluation and comparison
8. Unadjusted chi-square analyses
9. Adjusted logistic regression in the four most common histologies
10. Interpretation and limitations

The notebook accepts compatible SEER exports with the required column names and coding. It is not designed for arbitrary datasets. Interpretation text describes the original cohort and must be reviewed if another dataset is used.

## Model Evaluation
F1 is the primary comparison metric. Precision, recall, and ROC-AUC are also reported, with deceased status treated as the positive class. This priority was clarified after reviewing initial results, so model selection is exploratory.

| Model | Precision | Recall | F1 | ROC-AUC |
|---|---:|---:|---:|---:|
| Logistic regression | 0.753 | 0.619 | 0.679 | 0.856 |
| Decision tree | 0.805 | 0.252 | 0.384 | 0.718 |
| Random forest | 0.742 | 0.465 | 0.571 | 0.829 |

Logistic regression had the highest observed F1. Confusion matrices and precision–recall curves provide additional information about classification errors and threshold tradeoffs.

## Inferential Analyses
Unadjusted chi-square tests found overall associations between race/ethnicity and:
- Survival status: p = 0.00184
- Surgery receipt: p = 0.00321

An additional logistic regression included 3,487 records from the four most common histologies, adjusting for age band, sex, histology, and diagnosis year. None of the racial/ethnic comparisons with non-Hispanic White patients reached statistical significance.

The restricted adjusted analysis and full-cohort comparisons address different populations. The adjusted findings do not establish that disparities are absent.

## Pipeline Enhancements
- Input validation and explicit checks for unexpected codes
- Treatment-time missingness and top-coded-value indicators
- Reusable model-evaluation function
- Automated comparison and highest-F1 model selection
- Confusion matrices and precision–recall curves
- Conditional Monte Carlo inference when expected counts are small
- Software-version reporting
- Small-cell suppression in surgery-by-race displays

## Dependencies
Python packages:
- pandas
- numpy
- matplotlib
- seaborn
- scipy
- scikit-learn
- statsmodels

The notebook includes a cell reporting installed Python and package versions.

## Execution
In an environment permitted under the applicable SEER agreement:
1. Open the notebook in Google Colab.
2. Run the cells in order.
3. At the upload prompt, select the authorized CSV exported, included in the Canvas submission titled SEER_FINAL. 
4. Review validation messages, warnings, and outputs.

The upload uses file selection rather than a local Windows path. Other environments require replacing the Colab upload cell with a local CSV-reading step.

## Limitations
Survival status reflects unequal follow-up rather than survival at a fixed interval. Treatment receipt does not directly measure access. Small groups, ambiguous treatment categories, and residual confounding limit interpretation.

The adjusted model omits stage, treatment, and socioeconomic factors. Predictive models include treatment information and are exploratory classifications, not predictions made at diagnosis or tools ready for clinical use.

## Author
Jean-Paul Bryant, MD, MS, MPH
