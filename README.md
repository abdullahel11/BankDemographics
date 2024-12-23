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

## Tableau Visualisation for Customer Demographics.
![Image 22-12-2024 at 15 36](https://github.com/user-attachments/assets/e2fbd4d7-824b-48e6-8757-90398761a7a0)

#### Business Questions Answered from this Analysis:

**1. How is our customer base distributed across the newly defined income groups (Low, Middle, High Income)?**

The visualisation clearly shows the distribution of customers across the newly defined income groups:
- **High Income**: 23 customers
- **Middle Income**: 113 customers
- **Low Income**: 864 customers

**2. What are the average account balances and investment contributions for each income group?**

The bar chart highlights the average account balances and investment amounts for each group:
- **High Income earners** have the highest average account balance and investment amounts compared to the other groups.
- Middle and Low Income groups contribute significantly less on average.

## Additional Insights:

**- High Income Group Impact:** Despite representing only **2.3%** of the total customers, high-income earners contribute a significant **13.77%** to the cumulative account balances across all customers. This means that their financial contribution is approximately **6x** their population proportion, highlighting their outsized impact on total account balances.

![Image 23-12-2024 at 11 03](https://github.com/user-attachments/assets/57694236-c3cf-418e-9c75-3baed2aa5ad2)


**- Low Income Group Contribution:** Conversely, low-income earners account for **86.4%** of the total customers but contribute only **46.4%** to the cumulative account balances. This shows that their financial contribution is approximately **0.54x** their population proportion, reflecting the relatively lower financial capacity of this group compared to their size.

![Image 23-12-2024 at 11 04](https://github.com/user-attachments/assets/444f701f-9fac-4fde-b5a8-d9b0950fc3f4)


#### Loan Performance
This section focuses on analysing loan performance, including the outcomes of loan applications , the average loan amount, and interest rates for each loan status. Additionally, the analysis breaks down loan approval and rejection rates by region, providing insights into regional disparities and if unemployment influence loan application decisions.

**SQL Query's  performed**:

```sql
SELECT 
    loan_status,
    COUNT(*) AS total_loans,
    COUNT(CASE WHEN employment_status = 'Unemployed' THEN 1 END) AS unemployed_count,
    ROUND(AVG(loan_amount), 2) AS avg_loan_amount,
    ROUND(AVG(interest_rate), 3) AS avg_interest_rate
FROM Loan_Details
JOIN Customer_Demographics ON Loan_Details.cust_id = Customer_Demographics.cust_id
GROUP BY loan_status
ORDER BY total_loans DESC;
```
**For regional analysis**
```sql
SELECT -- Rejection/Approval Rates per region (4)
    region,
    COUNT(CASE WHEN loan_status = 'rejected' THEN 1 END) AS rejected_count,
    ROUND((COUNT(CASE WHEN loan_status = 'rejected' THEN 1 END) * 100.0 / COUNT(Customer_Demographics.cust_id)), 2) AS rejected_rate,
    COUNT(CASE WHEN loan_status = 'approved' THEN 1 END) AS approved_count,
    ROUND((COUNT(CASE WHEN loan_status = 'approved' THEN 1 END) * 100.0 / COUNT(Customer_Demographics.cust_id)), 2) AS approved_rate,
    COUNT(Customer_Demographics.cust_id) AS total_customers
FROM Customer_Demographics
JOIN Loan_Details ON Customer_Demographics.cust_id = Loan_Details.cust_id
GROUP BY region
ORDER BY rejected_rate DESC;
```
**Results and Insights:**

These query's  produced the following results:

- Count of loan application outcomes (approved, rejected) for each loan status.
- The number of unemployed customers for each loan outcome (approved, rejected).
- Average loan amount and interest rate for each loan decision (approved, rejected).
- Rejection and approval rates for loan applications by region.

## Tableau Visualisation for Loan Performance
![Image 23-12-2024 at 13 08](https://github.com/user-attachments/assets/da201aa7-5086-44c9-9599-2da5a27f011d)

#### Business Questions Answered from this Analysis:

**3. What are the approval and rejection rates for loan applications across different continents?**

This question was answered and visualized using a bar chart that shows the rejection and approval rates for loan applications by region. The visualization allows for a clear comparison of loan application outcomes across different geographic regions. For example, the region with the highest approval rate is North America, with an approval rate of 48.32%, while customers from Asia had the highest rejection rate, at 32.12%.

**4. What are the average loan sizes and interest rates for approved, rejected, and pending loan applications**

This question was answered and visualized using two bar charts that display the average loan amount and average interest rates for each loan outcome (approved, rejected, and pending).The first bar chart illustrates the average loan amount corresponding to each loan outcome, while the second bar chart shows the average interest rate for each loan decision.

**Approved Applications** had an average Loan Amount of **$10,951** and an average interest rate of **6.5%**

**Pending Applications** had an average Loan Amount of **$10,987** and an average interest rate of **9.2%**

**Rejected Applications** had an average Loan Amount of **$11,286** and an average interest rate of **9.1%**


























