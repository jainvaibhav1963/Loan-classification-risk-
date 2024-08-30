## Introduction
This report presents the development and evaluation of a loan prediction model designed to assess an applicant's creditworthiness. The model leverages machine learning techniques to analyze various features extracted from applicant data and predict the likelihood of loan default.

## Problem Statement
This dataset has been provided by a lending company. It includes application details of all previous loans disbursed by the company, with data collected at the time of application and a marker indicating whether the loan was defaulted or paid on time. The task is to prepare a model that predicts the loan outcome (good/bad) at the time of application.

## Data Provided
The data folder contains data for both the train and test sets. Both sets include accounts data and enquiry data in JSON format, and a flag dataset in CSV format. Brief descriptions are as follows:

1. **Train Data**: Contains details of loans provided by the client.
2. **Accounts Data**: Details of loans taken by the borrower before applying for a loan from the client, collected when the borrower applied for a loan from the client.
3. **Enquiry Data**: Details of previous loan applications made by the applicant, which may or may not have been successful.

## Data Preparation and Exploration
The dataset utilized for this analysis comprises three primary components:

- **Flag Data**: Contains applicant information, loan type, and loan outcome.
- **Accounts Data**: Details of previous loans taken by the applicant.
- **Enquiry Data**: Information about previous loan applications made by the applicant.

Upon exploration, several key findings emerged:

- **Class Imbalance**: The dataset exhibits a significant class imbalance, with a higher proportion of good loans compared to bad loans.
- **Enquiry Patterns**: Applicants frequently explore different loan options before making a final decision, as evidenced by the average of 7.3 enquiries per applicant.
- **Loan Types**: Consumer credit is the most common loan type, followed by credit cards.
- **Missing Data**: A significant portion of the accounts data lacks `closed_date` information, suggesting that these loans are still ongoing.

## Data Exploration and Analysis

### Key Findings:
- **Class Imbalance**: The dataset exhibits a significant class imbalance, with a higher proportion of good loans compared to bad loans.
- **Enquiry Data**: The average number of enquiries per applicant is 7.3, suggesting that applicants frequently explore different loan options before making a final decision.
- **Accounts Data**: The majority of loans are Consumer credit, indicating that this type of loan is more common among applicants. The average loan duration is 1006 days, which can be used to analyze the repayment behavior of borrowers.
- **Missing Data**: A significant number of rows in the accounts data are missing the `closed_date`, indicating that these loans are still ongoing.

## Feature Engineering

To enhance model performance, various features were engineered from the existing data. These features include:

- **Enquiry-related features**: Number of enquiries, average enquiry amount, most recent enquiry date, days since the last enquiry, and days since the first enquiry.
- **Account-related features**: Total loan amount, average loan amount, total amount overdue, proportion of overdue loans, ongoing loan amount, closed loan amount, loan duration, loan type diversity, payment history statistics, and credit type counts.

## Model Development and Evaluation

A machine learning model was trained using the engineered features to predict loan outcomes. The following steps were involved:

- **Data Split**: The dataset was divided into training and validation sets to evaluate model performance.
- **Model Selection**: XGBoost was selected as the modeling algorithm due to its ability to handle complex relationships and its performance in classification tasks.
- **Hyperparameter Tuning**: GridSearchCV was employed to optimize the model's hyperparameters, resulting in the following optimal configuration:
  - `gamma`: 0.2
  - `learning_rate`: 0.1
  - `max_depth`: 10
  - `n_estimators`: 150
  - `reg_alpha`: 2
  - `reg_lambda`: 2
  - `scale_pos_weight`: 1
- **Model Training and Evaluation**: The XGBoost model was trained on the training set using the optimized hyperparameters. The model's performance was evaluated on the validation set using the ROC AUC score, achieving a score of 0.6410.

### Feature Importance
The relative importance of features in predicting loan outcomes was assessed using XGBoost's feature importance analysis. Key features identified as influential in the model's predictions include:
- `enquiry_year`
- `enquiry_count_10`
- `enquiry_count_30`
- `loan_type_diversity`
- `ongoing_loan_count`

### Addressing Class Imbalance
To mitigate the impact of class imbalance, the SMOTE algorithm was employed to oversample the minority class (defaulters). This resulted in a slight improvement in the ROC AUC score, reaching 0.6206.

## Results
The final model achieved an ROC AUC score of 0.6410 on the validation set, indicating strong predictive performance.

## Conclusion
This analysis demonstrates the effectiveness of data exploration, feature engineering, and machine learning techniques in predicting loan outcomes. The developed model can be used to assess the risk of loan defaults and inform decision-making in the lending process.

## Future Work
- **Additional Features**: Exploring incorporating additional features, such as macroeconomic indicators or applicant demographics, could further enhance model performance.
- **Ensemble Methods**: Combining multiple models through techniques like stacking or bagging might improve predictive accuracy.
- **Time-Series Analysis**: If the data includes a temporal dimension, analyzing loan behavior over time could provide valuable insights.
- **Explainability**: Investigating techniques to explain the model's predictions can enhance transparency and build trust in the decision-making process.
