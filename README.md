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

### Flag Data Analysis:
- The dataset contains 261,383 rows and 3 columns.
- There are no missing values.
- Class imbalance is observed with 91.94% of loans being good and 8.06% being bad.
- The majority of loans are Cash loans (90.49%), followed by Revolving loans (9.51%).

### Enquiry Data Analysis:
- The dataset contains 1,909,926 rows and 4 columns.
- There are no missing values.
- The most common enquiry types are Cash loans, Revolving loans, and Mobile operator loans.
- The average number of enquiries per applicant is 7.3, with a maximum of 69.

### Accounts Data Analysis:
- The dataset contains 1,245,310 rows and 7 columns.
- There are missing values in the `closed_date` column (46,3035 rows).
- The majority of loans are Consumer credit (72.97%), followed by Credit card (23.48%).
- The average loan duration is 1006 days.

### Data Merging:
- The flag data is merged with the aggregated enquiry and account data based on the applicant ID (`uid`).
- A new feature `missing_account_data` is created to indicate if account data is missing.

## Key Findings
- **Class Imbalance**: The dataset exhibits a significant class imbalance, with a higher proportion of good loans compared to bad loans.
- **Enquiry Data**: The average number of enquiries per applicant is 7.3, suggesting that applicants frequently explore different loan options before making a final decision.
- **Accounts Data**: The majority of loans are Consumer credit, indicating that this type of loan is more common among applicants. The average loan duration is 1006 days, which can be used to analyze the repayment behavior of borrowers.
- **Missing Data**: A significant number of rows in the accounts data are missing the `closed_date`, indicating that these loans are still ongoing.

## Next Steps
1. **Feature Engineering**: Create additional features based on the existing data to improve model performance.
2. **Model Selection and Training**: Experiment with different machine learning algorithms to find the best model for predicting loan outcomes.
3. **Model Evaluation**: Evaluate the performance of the selected model using appropriate metrics, such as ROC AUC score.
4. **Hyperparameter Tuning**: Fine-tune the model's hyperparameters to optimize its performance.
