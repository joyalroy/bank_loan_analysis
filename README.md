### Bank Loan Analysis

## Table of Contents

- [Project Overview](#project-overview)
- [Data Sources](#data-sources)
- [Tools](#tools)
- [Data Cleaning](#data-cleaning)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data Analysis](#data-analysis)
- [Results](#results)
- [References](#references)

### Project Overview

This project analyzes bank loan data to understand various factors influencing loan approval, default rates, and repayment patterns. The analysis aims to provide insights into the data, identify trends, and build predictive models to assist in decision-making processes.

[New Bank Loan Project.pdf](https://github.com/user-attachments/files/16431375/New.Bank.Loan.Project.pdf)

### Data Sources

Bank Loan Data: The dataset contains information about bank loans including features like:

- `Loan_ID`: Unique identifier for each loan
- `Address State`: Address State indicates the borrower's location. It helps in assessing regional risk factors, compliance with state regulations, and estimating default probabilities.
- `Employee Length`: Employee Length provides insights into the borrower's employment stability. Longer employment durations may indicate greater job security.
- `Employee Title`: Employee Title specifies the borrower's occupation or job title. It helps lenders understand the source of the borrower's income.
- `Grade`: Grade represents a risk classification assigned to the loan based on creditworthiness. Higher grades signify lower risk.
- `Sub-Grade`: Sub Grade refines the risk assessment within a grade, providing additional risk differentiation.
- `Home Ownership`: Home Ownership indicates the borrower's housing status. It offers insights into financial stability.
- `Issue Date`: Issue Date marks the loan's origination date. It's crucial for loan tracking and maturity calculations.
- `Last Credit Pull Date`: Last Credit Pull Date records when the borrower's credit report was last accessed. It helps monitor creditworthiness.
- `Last Payment Date`: Last Payment Date marks the most recent loan payment received. It tracks the borrower's payment history.
- `Loan Status`: Loan Status indicates the current state of the loan (e.g., fully paid, current, default). It tracks loan performance.
- `Next Payment Date`: Next Payment Date estimates the date of the next loan payment. It assists in cash flow forecasting.
- `Purpose`: Purpose specifies the reason for the loan (e.g., debt consolidation, education). It helps understand borrower intentions.
- `Term`: Term defines the duration of the loan in months. It sets the repayment period.
- `Verification Status`: Verification Status indicates whether the borrower's financial information has been verified. It assesses data accuracy.
- `Annual Income`: Annual Income reflects the borrower's total yearly earnings. It assesses repayment capacity.
- `DTI(Debt-to-Income-Ratio)`: DTI measures the borrower's debt burden relative to income. It gauges the borrower's capacity to take on additional debt.
- `Installment`: Installment is the fixed monthly payment amount for loan repayment, including principal and interest.
- `Interest Rate`: Interest Rate represents the annual cost of borrowing expressed as a percentage. It determines the loan's cost.
- `Loan Amount`: Loan Amount is the total borrowed sum. It defines the principal amount.

Dataset Source: [financial_loan.csv](https://github.com/user-attachments/files/16432114/financial_loan.csv)


File Format: CSV
 
### Tools

- Microsoft Power BI :- Data Cleaning, Data Analysis & Data Visualization.

### Data Cleaning

In the initial data preparation phase, the following tasks were performed.

1. Data loading & inspection.
2. Handling missing values/null values.
3. Data cleaning & formatting.

### Exploratory Data Analysis

EDA involved exploring the HR data to answer KPI's, such as;

- What is the total number of employees in the organization?
- Find the overall attrition and attrition rate.
- Evaluate the average age of personnel in the organization.
- Calculate the average salary of personnel in the organization.
- Figure out the average employment period.

### Data Analysis

include some interesting code/features worked with

```power bi

#Conditional Column

Column Name:AttritionCount, Operator:Equals, Value:Yes, Output:1, Else:0

#New Measure

AttritionRate = SUM(HR_Analytics[AttritionCount])/SUM(HR_Analytics[EmployeeCount])

```

### Results

1. The total Head count is (1,470).
2. Total Attrition count (237) & Attrition rate (16.1%).
3. Average age (37yrs).
4. Average salary (6.5k).
5. Average years spent (7.0yrs).

### References

- Google
- Youtube
- Credits:Rishabh Mishra

