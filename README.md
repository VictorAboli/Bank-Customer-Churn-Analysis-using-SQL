# Bank-Customer-Churn-Analysis-using-SQL
This project performs an end-to-end Exploratory Data Analysis (EDA) and Business Intelligence Analysis on a Bank Customer Churn dataset using Microsoft SQL Server.

Project Overview

This project performs an end-to-end Exploratory Data Analysis (EDA) and Business Intelligence Analysis on a Bank Customer Churn dataset using Microsoft SQL Server.

The objective is to analyze customer behavior, identify factors contributing to customer churn, and generate actionable business insights through SQL queries. The project demonstrates practical SQL techniques including aggregations, conditional logic, Common Table Expressions (CTEs), ranking functions, window functions, and business reporting.

This repository is designed to showcase SQL skills required for Data Analyst, Business Analyst, and Business Intelligence Analyst roles.

🎯 Project Objective

The objective of this project is to:

Perform Exploratory Data Analysis (EDA)
Analyze customer churn patterns
Identify high-risk customer segments
Measure customer engagement
Evaluate customer retention factors
Generate business recommendations using SQL
Build analytical thinking through real-world business scenarios

📌 Key Business Insights

Some important findings from the analysis include:

Overall customer churn rate is 20.37%.
Germany has the highest customer churn rate among all countries.
Middle-aged customers exhibit the highest churn behavior.
Customers with 3–4 banking products show significantly higher churn rates.
Inactive customers are almost twice as likely to churn compared to active customers.
Customers with higher account balances have greater churn risk.
Customers with poor credit scores are more likely to leave the bank.
Senior customers with high balances and inactive accounts represent the highest-risk customer segment.

💡 Business Recommendations

Based on the analysis:

Develop targeted retention campaigns for inactive customers.
Improve loyalty programs for long-tenured customers.
Provide exclusive benefits for high-value customers.
Strengthen customer engagement in Germany and France.
Monitor customers with poor credit scores more proactively.
Create personalized offers for customers owning multiple banking products.
Build early-warning dashboards for high-risk customer segments.


Solving Business Problems 

1. Customer Churn Rate Analysis (Beginner)
Business Problem:
The bank's leadership wants to know the overall customer churn rate to understand how serious the retention problem is.
Question:
What percentage of customers have exited the bank?
```sql 
SELECT 
     CONCAT(CAST(SUM(CASE WHEN Exited = 1 THEN 1 ELSE 0 END) * 100.0 / COUNT(*) AS DECIMAL (10,2)), '%') AS Percentage_Exited
FROM Bank_churn;
```
2. Geography Performance Analysis (Beginner)
Business Problem:
The marketing team believes certain countries are losing significantly more customers than others.
Question:
Which geographical region has the highest churn rate, and how many customers were lost from each region?




