# README

## Project Title
**Student Depression Analysis and Modeling**

## Abstract
This project investigates the factors contributing to depression among students in India. Utilizing a dataset comprising responses from 27,901 students across various regions, the study aims to identify and predict depression in its early stages using statistical modeling and machine learning techniques. By shedding light on mental health issues, the project seeks to improve awareness and proactive mental health management among Indian youth.

---

## Dataset Overview

### Source
The dataset, referred to as the **Student Depression Dataset**, includes data points to analyze, understand, and predict depression among students.

### Features
The dataset comprises the following features:
- **Demographic Data**: Age, Gender, City
- **Academic Data**: CGPA, Degree, Academic Pressure, Study Satisfaction
- **Lifestyle Data**: Sleep Duration, Dietary Habits, Study Hours
- **Mental Health Data**: Family History of Mental Illness, Suicidal Thoughts
- **Responses to Standardized Depression Scales**

### Statistics
- **Total Observations**: 27,901
- **Variables**: 18
- **Unique Identifier**: Each student is identified by a unique ID.

### Notable Regions
Cities with higher reported cases include:
- Hyderabad
- Srinagar (Jammu and Kashmir)
- Kalyan (Maharashtra)
- Lucknow (Uttar Pradesh)
- Ludhiana (Punjab)
- Surat (Gujarat)
- Thane (Maharashtra)
- Vasai-Virar (Maharashtra)

### Limitations
- Underrepresentation of East India in the dataset.
- Some observations with low counts (≤ 10) were excluded.

---

## Methodology

### Preprocessing
The preprocessing steps involved:
1. **Handling Missing Data**: Three missing values in the `Financial.Pressure` column were removed.
2. **Encoding Categorical Variables**:
   - Gender: Male = 0, Female = 1
   - Sleep Duration: Less than 5 hours = 1, 5-6 hours = 2, 7-8 hours = 3, More than 8 hours = 4
   - Suicidal Thoughts: Yes = 1, No = 0
   - Family History of Mental Illness: Yes = 1, No = 0
   - Dietary Habits: Healthy = 1, Unhealthy = 2, Moderate = 3
   - Degree: Graduated = 1, Post Graduate = 2, Higher Secondary = 3
3. **Exclusion Criteria**:
   - Categories with low counts (≤ 10), such as “Others” in `Dietary Habits`.
   - Age groups under 30 due to limited representation.
   - Variables with singular values (`Work.Pressure`, `Profession`).
4. **New Features**:
   - **State**: Derived from the `City` column for state-level analysis.

### Modeling
#### Logistic Regression
The logistic regression model is employed to predict depression, focusing on binary outcomes. The logit link function ensures probabilities remain between 0 and 1.

**Model Formula**:
\[
\log \left( \frac{\mu}{1-\mu} \right) = \beta_0 + \beta_1 X_1 + \beta_2 X_2 + \ldots + \beta_p X_p
\]
- \( \mu \): Probability of success (binary outcome = 1)
- \( \beta_0, \beta_1, \ldots \beta_p \): Coefficients to be estimated
- \( X_1, X_2, \ldots, X_p \): Predictor variables

#### Pooling Approaches
1. **Complete Pooling**:
   - Assumes homogeneity across all groups.
   - General logistic regression formula applies.
2. **No Pooling**:
   - Estimates separate coefficients for each group.
   - May overfit when observations per group are low.
3. **Partial Pooling**:
   - Implements hierarchical models (using `glmer()` from the `lme4` package).
   - Balances between complete and no pooling by sharing information across groups while allowing group-specific variations.

#### Quasi-binomial Regression
In cases of overdispersion, the model (used will be) adjusts with a dispersion parameter (ϕ):
\[
Var(Y) = \mu(1 - \mu) \cdot \phi
\]
Where:
- \( \phi > 1 \): Overdispersion
- \( \phi = 1 \): Standard binomial variance

---

## Evaluation Metrics
- **Akaike Information Criterion (AIC)**: Balances model fit and complexity.
- **Confusion Matrix**: Compares accuracy across models.
- **Alternative Models**: Considered if overdispersion or lack of fit is detected (e.g., quasi-binomial).

---

## Files
1. **Dataset**: `SDD.csv`
2. **Processed Dataset**: It is included in Rmd file while running the code.
3. **Scripts**:
   - `Code.rmd`: Data cleaning and preprocessing, Exploratory data analysis, Logistic regression and hierarchical modeling.
4. **Results**:
   - `678_Final_Report.pdf`: Summary of model performance metrics, Visualizations (e.g., distribution of cases, regional analysis).
---

## Usage

### Prerequisites
- **R**: Version 4.2+
- **R Packages**:
  - `dplyr`
  - `ggplot2`
  - `lme4`
  - `caret`

### Instructions
1. **Data Preparation**:
   - Load the dataset: `read.csv("Student_Depression_Dataset.csv")`
   - Preprocess the data using `Code.rmd`.
2. **Exploratory Analysis**:
   - Run `Code.rmd` for insights and visualizations.
3. **Modeling**:
   - Use `Code.rmd` to apply logistic regression and evaluate models.

### Outputs
- Visualizations and model evaluation metrics will be saved in the `results/` directory.

---

## Future Work
- Inclusion of more comprehensive data from East India.
- Analysis of temporal trends in depression rates.
- Implementation of machine learning models for enhanced prediction accuracy.

---

## Contributors
- **[Vajinder Kaur]**: MS Statistical Practice, Boston University, MA, USA



