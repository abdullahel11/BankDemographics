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



