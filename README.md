# Bank Loan Data Analysis MySQL Project

**Project Overview**

This project demonstrates an analysis of bank loan data using MySQL. We explore key financial metrics such as total loan amounts, loan statuses, and payment details by joining two datasets (finance_1 and finance_2). The analysis is performed using SQL queries, which provide insights into loan distribution, borrower creditworthiness, and payment performance.

**Datasets**

**finance_1:** Contains core loan details like issue date, loan amount, loan status, and more.

**finance_2:** Contains additional financial data such as revolving balance, total payment, and last credit pull date.
These tables are related by the id column, which acts as the primary key for both datasets.

**Project Structure**

The project is divided into multiple SQL queries that cover a variety of analytical tasks on the dataset. Each query is structured to answer specific questions related to loan distribution, borrower behavior, and financial status.

**Analysis Queries**

**1) Year-wise Loan Amount**

This query calculates the total loan amount issued in each year.

     SELECT YEAR(issue_d) as Year_of_issue_d, SUM(loan_amnt) as Total_loan_amount
     FROM finance_1
     GROUP BY Year_of_issue_d
     ORDER BY Year_of_issue_d;

* **Objective:** Understand how loan amounts vary over the years.
  
* **Output:** Total loan amount for each year of issuance.

**2) Grade and Sub-grade wise Revolving Balance**

This query shows the revolving balance categorized by loan grade and sub-grade.

     SELECT grade, sub_grade, SUM(revol_bal) As Total_revol_bal
     FROM finance_1
     INNER JOIN finance_2 ON finance_1.id = finance_2.id
     GROUP BY grade, sub_grade
     ORDER BY grade, sub_grade;

* **Objective:** Analyze borrower creditworthiness by loan grades and revolving balances.
  
* **Output:** Total revolving balance for each grade and sub-grade.
  
**3) Verified vs Non-Verified Status: Total Payments**

This query compares the total payments made by borrowers with verified and non-verified loan statuses.

     SELECT verification_status, 
     CONCAT("$",FORMAT(ROUND(SUM(total_pymnt)/1000000,2),2),"M") As Total_payment
     FROM finance_1
     INNER JOIN finance_2 ON finance_1.id = finance_2.id
     GROUP BY verification_status;

* **Objective:** Compare financial performance between verified and non-verified borrowers.
  
* **Output:** Total payments for each verification status.
  
**4) State-wise Loan Status by Last Credit Pull Date**

This query retrieves loan status based on the state and last credit pull date.

     SELECT addr_statE, last_credit_pull_d, loan_status
     FROM finance_1
     INNER JOIN finance_2 ON finance_1.id = finance_2.id
     GROUP BY addr_statE, last_credit_pull_d, loan_status
     ORDER BY last_credit_pull_d;

* **Objective:** Examine loan status across states and last credit pull date.
  
* **Output:** Loan status for each state and credit pull date combination.
  
**5) Home Ownership vs Last Payment Date Status**

This query shows the relationship between home ownership and the last payment date.

     SELECT home_ownership, last_pymnt_d, 
     CONCAT("$",FORMAT(ROUND(SUM(last_pymnt_amnt)/10000,2),2),"k") As Total_amount
     FROM finance_1
     INNER JOIN finance_2 ON finance_1.id = finance_2.id
     GROUP BY home_ownership, last_pymnt_d
     ORDER BY last_pymnt_d DESC, home_ownership DESC;
     
* **Objective:** Analyze how home ownership impacts payment behavior.
  
* **Output:** Total last payment amounts based on home ownership and payment date.

**Conclusion**

This project highlights the power of SQL in data analysis, focusing on key financial indicators in the context of bank loans. By running these queries, you can gain insights into loan distribution across years, grades, and borrower verification statuses, providing a deeper understanding of bank lending practices.









