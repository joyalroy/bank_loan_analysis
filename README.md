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

- Microsoft Sql Server :- Data Cleaning & Data Processing.
 
- Microsoft Power BI :- Data Analysis & Data Visualization.

### Data Cleaning

In the initial data preparation phase, the following tasks were performed.

1. Data loading & inspection.
2. Handling missing values/null values.
3. Data cleaning & formatting.

### Exploratory Data Analysis

EDA involved exploring the Bank Loan data to answer KPI's, such as;

- Calculate the total loan applications received during a specific period.
- Monitor the Month-to-Date (MTD) loan applications and track changes Month-over-Month (MoM).
- Find the overall funded amount disbursed as loan.
- Evaluate the Month-to-Date (MTD) total funded amount & analyse the Month-over-Month (MoM) changes in this metric.
- Track the total amount received from debtors for assessing the bank's cash flow & loan repayment.
- Analyse the Month-to-Date (MTD) total amount received & observe Month-over-Month (MoM) changes.
- Compute the average interest rate across all loans, Month-to-Date (MTD) & keep tabs on Month-over-Month (MoM) variations in interest rates to provide insights into lending portfolio's overall cost.
- Evaluate the average DTI for debtors to assist them in their financial health.
- Compute the average DTI for all loans, Month-to-Date (MTD) & keep track on Month-over-Month (MoM) fluctuations.

### Data Analysis

include some interesting code/features worked with

```sql

#Total Loan Application

SELECT COUNT(id) as Total_Applications FROM bank_loan_data

#MTD Loan Applications

SELECT COUNT(id) AS MTD_Total_Applications FROM bank_loan_data
WHERE MONTH(issue_date) = 12

#PMTD Loan Applications

SELECT COUNT(id) AS PMTD_Total_Applications FROM bank_loan_data
WHERE MONTH(issue_date) = 11

#Total Funded Amount

SELECT SUM(loan_amount) AS Total_Funded_Amount FROM bank_loan_data

#MTD Total Funded Amount

SELECT SUM(loan_amount) AS Total_Funded_Amount FROM bank_loan_data
WHERE MONTH(issue_date) = 12

#PMTD Total Funded Amount

SELECT SUM(loan_amount) AS Total_Funded_Amount FROM bank_loan_data
WHERE MONTH(issue_date) = 11

#Total Amount Received

SELECT SUM(total_payment) AS Total_Amount_Collected FROM bank_loan_data

#MTD Total Amount Received

SELECT SUM(total_payment) AS Total_Amount_Collected FROM bank_loan_data
WHERE MONTH(issue_date) = 12

#PMTD Total Amount Received

SELECT SUM(total_payment) AS Total_Amount_Collected FROM bank_loan_data
WHERE MONTH(issue_date) = 11

#Average Interest Rate

SELECT AVG(int_rate)*100 AS Avg_Int_Rate FROM bank_loan_data

#MTD Average Interest

SELECT AVG(int_rate)*100 AS MTD_Avg_Int_Rate FROM bank_loan_data
WHERE MONTH(issue_date) = 12

#PMTD Average Interest

SELECT AVG(int_rate)*100 AS PMTD_Avg_Int_Rate FROM bank_loan_data
WHERE MONTH(issue_date) = 11

#Avg DTI

SELECT AVG(dti)*100 AS Avg_DTI FROM bank_loan_data

#MTD Avg DTI

SELECT AVG(dti)*100 AS MTD_Avg_DTI FROM bank_loan_data
WHERE MONTH(issue_date) = 12

#PMTD Avg DTI

SELECT AVG(dti)*100 AS PMTD_Avg_DTI FROM bank_loan_data
WHERE MONTH(issue_date) = 11

#Good Loan Percentage

SELECT
    (COUNT(CASE WHEN loan_status = 'Fully Paid' OR loan_status = 'Current' THEN id END) * 100.0) / 
	COUNT(id) AS Good_Loan_Percentage
FROM bank_loan_data

#Good Loan Applications

SELECT COUNT(id) AS Good_Loan_Applications FROM bank_loan_data
WHERE loan_status = 'Fully Paid' OR loan_status = 'Current'

#Good Loan Funded Amount

SELECT SUM(loan_amount) AS Good_Loan_Funded_amount FROM bank_loan_data
WHERE loan_status = 'Fully Paid' OR loan_status = 'Current'

#Good Loan Amount Received

SELECT SUM(total_payment) AS Good_Loan_amount_received FROM bank_loan_data
WHERE loan_status = 'Fully Paid' OR loan_status = 'Current'

#Bad Loan Percentage

SELECT
    (COUNT(CASE WHEN loan_status = 'Charged Off' THEN id END) * 100.0) / 
	COUNT(id) AS Bad_Loan_Percentage
FROM bank_loan_data

#Bad Loan Applications

SELECT COUNT(id) AS Bad_Loan_Applications FROM bank_loan_data
WHERE loan_status = 'Charged Off'

#Bad Loan Funded Amount

SELECT SUM(loan_amount) AS Bad_Loan_Funded_amount FROM bank_loan_data
WHERE loan_status = 'Charged Off'

#Bad Loan Amount Received

SELECT SUM(total_payment) AS Bad_Loan_amount_received FROM bank_loan_data
WHERE loan_status = 'Charged Off'

#LOAN STATUS
	SELECT
        loan_status,
        COUNT(id) AS LoanCount,
        SUM(total_payment) AS Total_Amount_Received,
        SUM(loan_amount) AS Total_Funded_Amount,
        AVG(int_rate * 100) AS Interest_Rate,
        AVG(dti * 100) AS DTI
    FROM bank_loan_data
    GROUP BY loan_status

SELECT 
	loan_status, 
	SUM(total_payment) AS MTD_Total_Amount_Received, 
	SUM(loan_amount) AS MTD_Total_Funded_Amount 
FROM bank_loan_data
WHERE MONTH(issue_date) = 12 
GROUP BY loan_status

#MONTH

SELECT 
	MONTH(issue_date) AS Month_Number, 
	DATENAME(MONTH, issue_date) AS Month_name, 
	COUNT(id) AS Total_Loan_Applications,
	SUM(loan_amount) AS Total_Funded_Amount,
	SUM(total_payment) AS Total_Amount_Received
FROM bank_loan_data
GROUP BY MONTH(issue_date), DATENAME(MONTH, issue_date)
ORDER BY MONTH(issue_date)

#STATE

SELECT 
	address_state AS State, 
	COUNT(id) AS Total_Loan_Applications,
	SUM(loan_amount) AS Total_Funded_Amount,
	SUM(total_payment) AS Total_Amount_Received
FROM bank_loan_data
GROUP BY address_state
ORDER BY address_state

#TERM

SELECT 
	term AS Term, 
	COUNT(id) AS Total_Loan_Applications,
	SUM(loan_amount) AS Total_Funded_Amount,
	SUM(total_payment) AS Total_Amount_Received
FROM bank_loan_data
GROUP BY term
ORDER BY term

#EMPLOYEE LENGTH

SELECT 
	emp_length AS Employee_Length, 
	COUNT(id) AS Total_Loan_Applications,
	SUM(loan_amount) AS Total_Funded_Amount,
	SUM(total_payment) AS Total_Amount_Received
FROM bank_loan_data
GROUP BY emp_length
ORDER BY emp_length

#PURPOSE

SELECT 
	purpose AS PURPOSE, 
	COUNT(id) AS Total_Loan_Applications,
	SUM(loan_amount) AS Total_Funded_Amount,
	SUM(total_payment) AS Total_Amount_Received
FROM bank_loan_data
GROUP BY purpose
ORDER BY purpose

#HOME OWNERSHIP

SELECT 
	home_ownership AS Home_Ownership, 
	COUNT(id) AS Total_Loan_Applications,
	SUM(loan_amount) AS Total_Funded_Amount,
	SUM(total_payment) AS Total_Amount_Received
FROM bank_loan_data
GROUP BY home_ownership
ORDER BY home_ownership

#Grade

SELECT 
	purpose AS PURPOSE, 
	COUNT(id) AS Total_Loan_Applications,
	SUM(loan_amount) AS Total_Funded_Amount,
	SUM(total_payment) AS Total_Amount_Received
FROM bank_loan_data
WHERE grade = 'A'
GROUP BY purpose
ORDER BY purpose
```

### Results

#Total Loan Applications

![image](https://github.com/user-attachments/assets/918bf5c3-3464-49f3-b595-9988f090f2bd)

#MTD Loan Applications

![image](https://github.com/user-attachments/assets/0b64c808-1601-4f72-9a15-5df449be34dc)

#PMTD Loan Applications

![image](https://github.com/user-attachments/assets/e31a6ab9-2eda-4187-a7ce-aa0990c7220f)

#Total Funded Amount

![image](https://github.com/user-attachments/assets/6096474b-2341-46a1-b04d-112bdbd04679)

#MTD Total Funded Amount

![image](https://github.com/user-attachments/assets/a1bd48ab-e66e-4d0b-b16a-69da772daa65)

#PMTD Total Funded Amount

![image](https://github.com/user-attachments/assets/d7152ead-30f1-40db-90e5-94db4807542f)

#Total Amount Received

![image](https://github.com/user-attachments/assets/e9204844-e012-497d-9c62-08e060302d24)

#MTD Total Amount Received

![image](https://github.com/user-attachments/assets/853234b5-2e6a-4692-a988-dc2fcab327e7)

#PMTD Total Amount Received

![image](https://github.com/user-attachments/assets/a92d9f8f-2ef3-4508-8c9d-661e28f90bdd)

#Average Interest Rate

![image](https://github.com/user-attachments/assets/8cebe659-5929-4d55-918f-1566047eac7d)

#MTD Average Interest

![image](https://github.com/user-attachments/assets/61b51992-e513-4c43-b398-670d98ad8db0)

#PMTD Average Interest

![image](https://github.com/user-attachments/assets/32e0c74e-fd17-42c8-86f0-fd5794bb8238)

#Avg DTI

![image](https://github.com/user-attachments/assets/2a9dbba7-a78d-4ff7-84c7-0a21ecb14aac)

#MTD Avg DTI

![image](https://github.com/user-attachments/assets/8b885880-bb37-4e5f-857b-330471f59b0e)

#PMTD Avg DTI

![image](https://github.com/user-attachments/assets/6125c09f-2e2c-468f-b0ec-1b476bc8542a)

#Good Loan Percentage

![image](https://github.com/user-attachments/assets/e0e6294c-f85f-494d-bf07-2eb9e27b3c8c)

#Good Loan Applications

![image](https://github.com/user-attachments/assets/4ef18018-ad05-4921-903d-495b9162260b)

#Good Loan Funded Amount

![image](https://github.com/user-attachments/assets/dadb2b91-12c9-4b93-8030-04e02a05aa43)

#Good Loan Amount Received

![image](https://github.com/user-attachments/assets/871bb6fb-846d-4e8f-9128-37f91d32b32e)

#Bad Loan Percentage

![image](https://github.com/user-attachments/assets/c9bc6494-d976-4d1b-b056-74bae663b463)

#Bad Loan Applications

![image](https://github.com/user-attachments/assets/1b6b5e14-b6e7-40a5-bef7-f78d87251417)

#Bad Loan Funded Amount

![image](https://github.com/user-attachments/assets/52480420-e65f-486f-92d4-f970ea60452a)

#Bad Loan Amount Received

![image](https://github.com/user-attachments/assets/91bfe831-7408-4a1a-9a16-85edb84a8e87)

#LOAN STATUS

![image](https://github.com/user-attachments/assets/d9f8345c-a23e-416c-9ced-77ff64cdca1e)

![image](https://github.com/user-attachments/assets/0cbe88e6-3e04-472b-8340-8500beb75747)

#MONTH

![image](https://github.com/user-attachments/assets/b4cbcbd7-a041-4672-8938-a68273d2af66)

#STATE

![image](https://github.com/user-attachments/assets/9b89b88f-ee6e-47e7-9504-19034f090b39)

#TERM

![image](https://github.com/user-attachments/assets/b46eeeb3-0e1f-4fec-bc07-db4c30282a5d)

#EMPLOYEE LENGTH

![image](https://github.com/user-attachments/assets/fefeaf70-27a4-4c22-9fe6-db94417bb94e)

#PURPOSE

![image](https://github.com/user-attachments/assets/2e0e2d47-cfc1-4845-ba2a-e7d825c42eab)

#HOME OWNERSHIP

![image](https://github.com/user-attachments/assets/6aadaade-8b61-4abe-9e10-c2d566518555)

### References

- Google
- Youtube

