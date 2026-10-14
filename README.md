# Spinal Tumor Disparities: SEER Analysis

## Project Overview
This project examines racial and ethnic differences in surgery receipt and survival status among adult and pediatric patients with spinal tumors. I selected this topic because it relates to my work as a neurosurgery resident and my interest in oncology and disparities research.

The notebook includes exploratory analysis, preprocessing, two inferential statistical analyses, and three supervised classification models.

## Dataset
- Source: SEER Research Data, 1975–2023 (November 2025 Submission)
- Website: https://seer.cancer.gov/data/
- Selected cohort: 5,831 spinal tumor records diagnosed between 2010 and 2023
- Original export: 25 columns
- Outcome: Survival status at the study cutoff (0 = living, 1 = deceased)

SEER requires approved access. The patient-level CSV is not included in this repository. Saved notebook outputs can be viewed without the dataset, but rerunning the analysis requires the corresponding authorized export.

## Running the Notebook
1. Open the `.ipynb` notebook in Google Colab.
2. Select **Runtime → Run all**.
3. When prompted, upload `SEER_FINAL.csv`.
4. Allow the remaining cells to execute.

The CSV must match the cohort and column names used in the notebook. A local Windows file path will not load the data into Colab.

Required Python libraries: pandas, matplotlib, seaborn, scipy, and scikit-learn.

## Analytical Workflow
- Data import, structure review, and validation
- Descriptive statistics and exploratory visualizations
- Review of coded missing and unavailable information
- Predictor selection and treatment-time feature engineering
- Stratified 80/20 training/test split
- Training-only imputation, encoding, and scaling within model pipelines
- Logistic regression, decision tree, and random forest classification
- Evaluation using precision, recall, F1, and ROC-AUC
- Chi-square tests of race/ethnicity versus survival status and surgery receipt
- Interpretation and limitations

## Initial Results
Logistic regression had the highest test-set F1 score (0.679) and ROC-AUC (0.856). Its precision was 0.753 and recall was 0.619.

Unadjusted chi-square tests found overall associations between race/ethnicity and survival status (p = 0.00184) and surgery receipt (p = 0.00321).

## Pipeline Enhancements
The notebook documents five enhancements since the last submitted notebook (the updates):
1. Additional validation and error handling
2. Treatment-time missingness and top-coded-value indicators
3. A reusable model-evaluation function
4. An automated model-comparison table
5. Confusion matrices and precision–recall curves

## Limitations
The disparities analyses are unadjusted and do not establish causation or unequal access to care. Survival status reflects unequal follow-up periods. Small racial/ethnic groups and ambiguous treatment categories require cautious interpretation. This is essentially a surrogate for access but there are so many confounders that I will take into account in my next analysis. The models include treatment information and are exploratory classifications, not predictions made at diagnosis or tools ready for clinical use. The adjusted models which take the confounders into account will definitely be more generalizable.

## Author
Jean-Paul Bryant, MD, MS, MPH
