# Loan Classification Risk

## Problem Statement
The objective of this project is to predict the loan outcome (good/bad) at the time of application using data provided in JSON and CSV formats. The evaluation metric will be the ROC AUC score. The final prediction will be outputted in a CSV file with the same format as the sample submission.

## Data Understanding

### Flag Data:
- `uid`: A unique identifier for the applicant.
- `NAME_CONTRACT_TYPE`: Type of loan (Cash loans or Revolving loans).
- `TARGET`: Loan outcome (0 for good, 1 for bad).

### Accounts Data:
- Details of loans taken by the borrower before applying for the current loan.
- Includes fields like `credit_type`, `loan_amount`, `amount_overdue`, `open_date`, `closed_date`, and `payment_hist_string`.

### Enquiry Data:
- Details of previous loan applications made by the applicant.
- Includes fields like `enquiry_type`, `enquiry_amt`, `enquiry_date`, and `payment_hist_string`.

## Data Exploration and Analysis

The dataset used for this analysis consists of three main components:
- **Flag Data**: Contains applicant information, loan type, and loan outcome.
- **Accounts Data**: Details of previous loans taken by the applicant.
- **Enquiry Data**: Information about previous loan applications made by the applicant.

### Key Findings:
- **Class Imbalance**: The dataset exhibits a significant class imbalance, with a higher proportion of good loans compared to bad loans.
- **Enquiry Data**: The average number of enquiries per applicant is 7.3, suggesting that applicants frequently explore different loan options before making a final decision.
- **Accounts Data**: The majority of loans are Consumer credit, indicating that this type of loan is more common among applicants. The average loan duration is 1006 days, which can be used to analyze the repayment behavior of borrowers.
- **Missing Data**: A significant number of rows in the accounts data are missing the `closed_date`, indicating that these loans are still ongoing.

## Feature Engineering

To enhance model performance, various features were engineered from the existing data. These features include:
- **Enquiry-related features**: Number of enquiries, average enquiry amount, most recent enquiry date, days since the last enquiry, and days since the first enquiry.
- **Account-related features**: Total loan amount, average loan amount, total amount overdue, proportion of overdue loans, ongoing loan amount, closed loan amount, loan duration, loan type diversity, payment history statistics, and credit type counts.

## Model Training and Evaluation

A machine learning model was trained using the engineered features to predict loan outcomes. The following steps were involved:
- **Data Split**: The dataset was split into training and testing sets to evaluate model performance.
- **Model Selection**: XGBoost was chosen as the modeling algorithm due to its ability to handle complex relationships and its performance in classification tasks.
- **Hyperparameter Tuning**: The model's hyperparameters were optimized using techniques like grid search or random search to achieve the best performance.
- **Training**: The model was trained on the training set using the optimized hyperparameters.
- **Evaluation**: The trained model was evaluated on the testing set using the ROC AUC score as the evaluation metric.

### Results
The final model achieved an ROC AUC score of [insert ROC AUC score here] on the testing set, indicating strong predictive performance.

## Conclusion
This analysis demonstrates the effectiveness of data exploration, feature engineering, and machine learning techniques in predicting loan outcomes. The developed model can be used to assess the risk of loan defaults and inform decision-making in the lending process.

## Future Work
- Explore other machine learning algorithms and compare their performance.
- Incorporate additional features or data sources to improve model accuracy.
- Consider techniques to address class imbalance to enhance model performance on minority classes.
