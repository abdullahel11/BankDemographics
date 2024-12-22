# Banking Demographics Data Analysis Project

## Project Overview
This project involves analyzing banking data to extract key insights about customer demographics, account balances, investments, and other banking-related features. The analysis is based on a synthetic dataset containing customer information, financial history, account activity, and loan details. The project uses SQL, Excel, and Tableau to clean, process, and visualize the data.

## Tools Used
- **SQL**: Used for database creation, data queries, and analysis.
- **Excel**: Used for data cleaning, initial data manipulation, and working with raw datasets.
- **Tableau**: Used for creating interactive visualizations and dashboards to represent the findings.

## Dataset
The dataset consists of various attributes for each customer, such as:
- **Customer Demographics**: Age, occupation, marital status, income level, etc.
- **Account Information**: Account balance, deposits, withdrawals, international transfers, etc.
- **Investment Data**: Amount invested through accounts, risk tolerance, and investment goals.
- **Loan Information**: Loan amount, loan term, interest rate, loan status, etc.

The datasets used in this project contain synthetic customer banking data, which includes various customer attributes such as demographics, account activity, investments, and loan information.

- **Initial Dataset (`Initial.csv`)**: This is the raw dataset that was imported from Excel. It contains the original customer data before any cleaning or processing.
  
- **Final Dataset (`Final.csv`)**: After performing data cleaning and transformation, this is the cleaned version of the dataset, ready for analysis.

## Data Cleaning

The dataset was cleaned in Excel before importing into SQL to simplify the cust_id column for easier reference and analysis. The primary data cleaning step involved changing the original, long customer IDs to a simpler numeric format.

- **Original cust_id Format:** The original dataset contained long and complex customer IDs.
- **Modified cust_id Format:** The cust_id was simplified to a numeric sequence starting from "0001", "0002", ..., up to "1000". This format was used to make the dataset more manageable and to maintain consistency across the analysis.
- **Duplicates and Inconsistencies:** Removed any duplicate rows or inconsistencies in the dataset.

This cleaned dataset was then used to investigate key business questions and generate actionable insights.

## Key Business Questions



####  1. Customer Distribution: 
 - How is our customer base distributed across the newly defined income groups (Low, Middle, High Income)?
####  2. Banking Behaviour by Income Group:
 - What are the average account balances and investment contributions for each income group?
####  3. Loan Application trends by region:
 - What are the approval and rejection rates for loan applications across different continents?
####  4. Loan Size and Interest Analysis
 - What are the average loan sizes and interest rates for approved, rejected, and pending loan applications
####  5. Unemployment vs Loan Approval
 - To what extent does unemployment affect the chances of loan approval?
####  6. Risk Tolerance and Investments
 - How does the average investment vary across different risk tolerance groups (e.g., low, medium, high)?

## SQL and Tableau Analysis
This section documents the process of creating the database, organising the data into tables, and performing SQL analysis to derive insights. Each part includes the SQL queries used, a description of the analysis, visualisations, and the business questions answered in each section.

#### Database creation and Initial setup

To begin, the database was created in SQL using the cleaned dataset. The first step involved creating the raw data table, which served as the foundation for further analysis.

SQL Query performed:

```sql
CREATE DATABASE bank_project; -- Creating and Using the database
USE bank_project;
```
``` sql
CREATE TABLE Raw_Data ( -- Create the inital raw data table
    cust_id VARCHAR(255) PRIMARY KEY,
    age INT,
    occupation VARCHAR(100),
    risk_tolerance VARCHAR(10),
    investment_goals VARCHAR(255),
    education VARCHAR(100),
    marital_status VARCHAR(20),
    dependents INT,
    region VARCHAR(100),
    financial_history VARCHAR(50),
    sector VARCHAR(100),
    income_level DECIMAL(65,30),
    account_balance DECIMAL(65,30),
    account_deposits DECIMAL(65,30),
    account_withdrawals DECIMAL(65,30),
    account_transfers DECIMAL(65,30),
    international_transfers DECIMAL(65,30),
    account_investments DECIMAL(65,30),
    account_type VARCHAR(50),
    loan_amount DECIMAL(65,30),
    loan_purpose VARCHAR(255),
    employment_status VARCHAR(50),
    loan_term INT,
    interest_rate DECIMAL(65,15),
    loan_status VARCHAR(50)
);
```

- The Raw_Data table contains all the columns from the cleaned dataset imported directly from Excel.
- This table was used as a source for creating specialized tables focusing on specific aspects of the dataset, such as demographics, account activity, and loan details.**
- 
#### Overview of table creation
The database was structured into three main tables, each focusing on a specific aspect of customer data
1. ```customer_demographics``` **This table contains information about customer profiles, such as age, marital status, occupation, income level, and region.**
2. ```account_activity``` **This table focuses on financial activity, including account balances, deposits, withdrawals, and investments**
3. ```loan_details``` **This table contains all loan-related information, such as loan amounts, terms, interest rates, and statuses**

### Section-specific analysis

#### Customer Demographics 
This section focuses on segmenting customers based on the newly modified  income levels and analysing their account balances and investments. Customers were categorised into three income groups: Low Income, Middle Income, and High Income. The analysis highlights the distribution of customers across these groups, their average and total account balances, and their investment contributions.

**SQL Query performed**:

```sql
SELECT -- Customer Segmentation Analysis
    CASE 
        WHEN cd.income_level < 30000 THEN 'Low Income'
        WHEN cd.income_level BETWEEN 30000 AND 70000 THEN 'Middle Income'
        ELSE 'High Income'
    END AS income_group,
    COUNT(cd.cust_id) AS customer_count,
    ROUND(COUNT(cd.cust_id) * 100.0 / (SELECT COUNT(*) FROM Customer_Demographics), 2) AS customer_percentage,
    ROUND(AVG(aa.account_balance), 2) AS avg_balance, 
    ROUND(SUM(aa.account_balance), 2) AS total_balance,
    ROUND(SUM(aa.account_balance) * 100.0 / (SELECT SUM(account_balance) FROM Account_Activity), 2) AS balance_contribution_percentage,
    ROUND(AVG(aa.account_investments), 2) AS avg_investments, 
    ROUND(SUM(aa.account_investments), 2) AS total_investments,
    ROUND(SUM(aa.account_investments) * 100.0 / (SELECT SUM(account_investments) FROM Account_Activity), 2) AS investment_contribution_percentage
FROM Customer_Demographics AS cd
JOIN Account_Activity AS aa ON cd.cust_id = aa.cust_id
GROUP BY income_group;
```

**Results and Insights:**

This query produced the following results:

- Customer count per income group
- Average account balance and investment balance for customers in each income group
- Total amount of funds in balance and investment accounts for each income group
- Contribution of each income group to the total balance and investments 

### Tableau Visualisation for Customer Demographics.











