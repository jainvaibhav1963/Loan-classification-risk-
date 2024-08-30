# Loan Classification Risk

## Introduction
This project focuses on developing and evaluating a loan prediction model to assess an applicant's creditworthiness. Using machine learning techniques, we analyze various features extracted from applicant data to predict whether a loan will default or be repaid on time.

## Problem Statement
Our client, a lending company, provided a dataset containing details of all previous loans disbursed. This data includes application details and a marker indicating whether the loan defaulted or was repaid on time. The goal is to build a model that predicts the loan outcome (good or bad) based on the data available at the time of application.

## Data Provided
The data folder includes both train and test sets. Each set contains accounts data and enquiry data in JSON format, and a flag dataset in CSV format. Here’s a quick overview:

1. **Train Data**: Details of loans disbursed by the client.
2. **Accounts Data**: Information about previous loans taken by the borrower, collected when they applied for a loan.
3. **Enquiry Data**: Details of previous loan applications made by the borrower, which might or might not have been successful.

## Data Preparation and Exploration
The dataset consists of three main parts:

- **Flag Data**: Includes applicant details, loan type, and outcome.
- **Accounts Data**: Shows details of prior loans taken by the borrower.
- **Enquiry Data**: Contains information about previous loan applications.

### Key Findings:
- **Class Imbalance**: The dataset is imbalanced, with a high proportion of good loans compared to bad loans.
- **Enquiry Patterns**: On average, applicants make 7.3 enquiries before deciding, suggesting frequent exploration of loan options.
- **Loan Types**: Consumer credit is the most common loan type, with credit cards being the next most common.
- **Missing Data**: Many entries in the accounts data lack `closed_date`, indicating that some loans are still ongoing.

## Feature Engineering
To boost model performance, we engineered several features from the existing data:

- **Enquiry-related Features**: Number of enquiries, average enquiry amount, most recent enquiry date, days since the last enquiry, and days since the first enquiry.
- **Account-related Features**: Total and average loan amounts, total and proportion of overdue amounts, ongoing and closed loan amounts, loan duration, loan type diversity, payment history statistics, and credit type counts.

## Model Development and Evaluation
We trained a machine learning model using the engineered features to predict loan outcomes. Here’s a summary of the process:

- **Data Split**: We divided the dataset into training and validation sets.
- **Model Selection**: XGBoost was chosen for its ability to handle complex relationships and its strong performance in classification tasks.
- **Hyperparameter Tuning**: Optimized using GridSearchCV, with the following best settings:
  - `gamma`: 0.2
  - `learning_rate`: 0.1
  - `max_depth`: 10
  - `n_estimators`: 150
  - `reg_alpha`: 2
  - `reg_lambda`: 2
  - `scale_pos_weight`: 1
- **Model Training and Evaluation**: The XGBoost model, trained with these parameters, achieved an ROC AUC score of 0.6410 on the validation set.

### Feature Importance
Key features influencing predictions include:
- `enquiry_year`
- `enquiry_count_10`
- `enquiry_count_30`
- `loan_type_diversity`
- `ongoing_loan_count`

### Addressing Class Imbalance
We used the SMOTE algorithm to balance the classes, which slightly improved the ROC AUC score to 0.6206.

## Results
The final model achieved an ROC AUC score of 0.6410, showing good predictive performance.

## Conclusion
This project demonstrates how data exploration, feature engineering, and machine learning techniques can effectively predict loan outcomes. The model is useful for assessing loan default risk and guiding lending decisions.

## Future Work
- **Additional Features**: Adding features like macroeconomic indicators or applicant demographics might improve the model.
- **Ensemble Methods**: Combining multiple models could enhance accuracy.
- **Time-Series Analysis**: Analyzing loan behavior over time, if applicable, could offer more insights.
- **Explainability**: Exploring ways to explain the model’s predictions could build trust in the results.
