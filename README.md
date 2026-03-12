# NHIS Cancer Demographic Analysis

This project analyzes demographic disparities in cancer diagnoses using the **2024 National Health Interview Survey (NHIS) Adult dataset**. The analysis explores how cancer prevalence varies across demographic groups such as race, education, and sex, and applies **survey-weighted statistical methods** to estimate population-representative patterns.

The analysis is implemented in a Jupyter notebook (`analysis.ipynb`) using Python.

---

# Dataset

The dataset used is:

```
adult24.csv
```

This file is part of the **NHIS Adult Survey**, a nationally representative survey conducted by the National Center for Health Statistics (NCHS).

NHIS uses **complex survey sampling**, so analyses incorporate the **person-level survey weight (`WTFA_A`)** to produce estimates representative of the U.S. adult population.

---

# Variables Used

The analysis focuses on cancer history and demographic characteristics.

| Variable | Description |
|--------|-------------|
| `CANEV_A` | Whether the respondent has ever been diagnosed with cancer |
| `SEX_A` | Respondent sex |
| `RACEALLP_A` | Respondent race category |
| `EDUCP_A` | Highest level of education completed |
| `WTFA_A` | NHIS person-level survey weight |

These variables were extracted from the full dataset to create a smaller dataset used for analysis.

---

# Analysis Workflow

The notebook follows a structured workflow.

---

## 1. Data Loading

The NHIS dataset is loaded using pandas.

```python
import pandas as pd

df = pd.read_csv("adult24.csv")
```

A subset of relevant variables is then extracted for analysis.

---

## 2. Data Cleaning

Responses such as:

- Refused  
- Don't know  
- Not ascertained  

are excluded from the analysis to focus on valid survey responses.

A cleaned dataset (`clean_df`) is created containing respondents with valid cancer and demographic responses.

---

## 3. Mapping Survey Codes

NHIS variables are encoded numerically, so dictionaries are used to convert codes into readable labels.

Example mappings:

**Sex**

```
1 → Male  
2 → Female
```

**Cancer diagnosis**

```
1 → Yes  
2 → No
```

Race and education variables are mapped similarly.

New labeled variables are created:

```
SEX_label
RACE_label
EDUC_label
CANEV_label
```

These labeled variables are used in visualizations and statistical models.

---

## 4. Exploratory Data Analysis

The notebook includes exploratory analysis to examine how cancer diagnoses vary across demographic groups.

Visualizations include:

- Overall cancer prevalence  
- Cancer prevalence by sex  
- Cancer prevalence by race  
- Cancer prevalence by education level  
- Race × education heatmaps  

These exploratory plots help identify demographic patterns in the data.

---

## 5. Survey-Weighted Analysis

Because NHIS uses complex sampling, analyses incorporate the survey weight:

```
WTFA_A
```

Weighted prevalence is calculated using a weighted mean:

```
weighted prevalence = sum(weight × outcome) / sum(weight)
```

This produces estimates that better represent the **U.S. adult population** rather than just the survey sample.

Weighted analyses include:

- overall cancer prevalence  
- cancer prevalence by race  
- cancer prevalence by race and education  

---

## 6. Weighted Logistic Regression

To evaluate demographic associations with cancer diagnosis, a **weighted logistic regression model** is estimated using `statsmodels`.

The model predicts the probability of reporting a cancer diagnosis.

Model specification:

```
Cancer ~ race + education + sex
```

Survey weights are applied using the `freq_weights` argument.

The model outputs:

- regression coefficients  
- odds ratios  
- confidence intervals  
- statistical significance tests  

Odds ratios allow interpretation of how demographic groups differ in the odds of reporting a cancer diagnosis.

---

# Visualization Outputs

The notebook generates several figures, including:

- cancer prevalence by demographic group  
- race × education heatmaps  
- weighted prevalence comparisons  
- regression-based effect estimates  

These visualizations help identify potential demographic disparities in cancer diagnoses.

---

# Summary

This project demonstrates a workflow for analyzing cancer prevalence using nationally representative survey data. By applying survey weights and regression modeling, the analysis provides insights into how cancer diagnoses vary across demographic groups in the United States.
