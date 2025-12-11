#  Identifying Risk Factors for Major Depressive Disorder (MDD)
### Predictive Modeling & Data Analysis Using the 2023 MH-CLD Dataset  

This project analyzes over **7 million client records** from the **2023 Mental Health Client-Level Data (MH-CLD)** dataset to identify the key demographic, socioeconomic, and clinical predictors of **Major Depressive Disorder (MDD)**. Using statistical modeling and machine-learning techniques, we evaluate risk factors and build predictive models for early detection of the disorder.  

---

## Data Preprocessing

A full preprocessing pipeline was created to prepare the dataset for statistical and machine-learning analysis:

- Replaced SAMHSA-specific missing codes with `NaN`  
- Converted coded variables (age, sex, education, region, etc.) into human-readable labels  
- Constructed binary indicators such as:  
  - MDD diagnosis  
  - Substance-use flags  
  - Homelessness  
  - Veteran status  
  - Marital status  
- One-hot encoded all categorical variables  
- Mode/median imputation for missing data  
- Output two final datasets:  
  - `clean_df` for EDA + visualization  
  - `model_df` for regression + ML modeling  

---

## Exploratory Data Analysis (EDA)

Key observations from **7,035,641 cleaned records**:

- **27%** of clients had an MDD diagnosis  
- **76%** had at least one co-occurring mental-health condition  
- Significant missingness in socioeconomic variables (education, employment, veteran status)  
- MDD prevalence patterns:  
  - Higher in **females** (32% vs. 21%)  
  - Elevated in ages **18–24** and **50–64**  
- Strong associations with:  
  - Anxiety disorders  
  - Personality disorders  
  - Substance-use problems  
- Strongest effect sizes (Cramer's V): **age**, **sex**, **education**

---

## Regression

Both **logistic** and **probit** regression models were used to quantify the influence of predictors on MDD:

### Strongest *positive* predictors
- Anxiety disorders (OR ≈ 2.6)  
- Personality disorders  
- Substance-abuse problems  

### Predictors associated with *lower* MDD odds
- Bipolar disorder  
- Schizophrenia  

### Additional socioeconomic effects
- Homelessness ↑  
- Employment ↓  

**AUC ≈ 0.77** for both logistic and probit models, indicating good discriminative performance.

---

## Machine Learning Models

We evaluated four machine-learning models using the processed dataset:

| Model | Accuracy | Recall | AUC | Notes |
|-------|----------|--------|-----|-------|
| **Random Forest** | 0.735 | **0.810** | 0.836 | Best clinical recall; balanced + interpretable |
| **SGD Classifier** | 0.755 | 0.352 | 0.776 | Underfits nonlinear patterns |
| **LightGBM** | 0.803 | 0.503 | **0.850** | Highest accuracy; low recall; well-calibrated |
| **CatBoost** | 0.801 | 0.502 | 0.848 | Similar to LightGBM; strong calibration |

### Final Model Selection: **Random Forest**
Chosen because:
- It achieves the **highest recall**, minimizing false negatives  
- Provides interpretable feature importance  
- More stable for clinical risk-screening applications  

---

## Feature Importance (Random Forest)

Most influential predictors for MDD classification:

- Presence of other mental-health diagnoses (anxiety, personality disorders, etc.)  
- **Age**  
- **Region**  
- **Employment status**  

These results show strong interactions between clinical and socioeconomic factors in shaping mental-health outcomes.

---

## Conclusion

This project demonstrates that combining **statistical modeling** with **ensemble machine-learning methods** can:

- Identify robust predictors of Major Depressive Disorder  
- Provide reliable tools for early clinical detection

  ---

 ## Repository Contents

### `AMS 595 Group Project.ipynb`
A Jupyter Notebook containing the full workflow for the project.  
This notebook includes:

- Data loading and preprocessing  
- Exploratory data analysis (EDA)  
- Modeling steps (logistic regression, random forest, SGD, LightGBM, CatBoost, etc.)  
- Visualizations of distributions, correlations, and model performance  
- Interpretation of results and final conclusions  

This is the primary document where all analysis is conducted.

---

### `mh-cld-2023-ds0001-info-codebook_v1_0.pdf`  
The official **codebook** for the *Mental Health Client-Level Data (MH-CLD), 2023* dataset.  
This document provides:

- Detailed variable definitions (demographics, diagnoses, socioeconomic indicators, service-use variables, etc.)  
- Value labels and frequencies (pages 9–47) describing category distributions  
- Notes on confidentiality, derived variables, and dataset structure  
- Appendices containing recoding rules and technical documentation  

This file is essential for interpreting the dataset and understanding how variables are encoded and used throughout the analysis.

- Support mental-health professionals and policy makers  
- Handle large-scale, complex, imbalanced datasets effectively  


