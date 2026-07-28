# 🏦 Bank Customer Churn Analysis using SQL

### End-to-End SQL Data Analysis Project | Exploratory Data Analysis | Business Intelligence | Customer Retention Analytics

![SQL](https://img.shields.io/badge/SQL-Microsoft%20SQL%20Server-blue?style=for-the-badge)
![Status](https://img.shields.io/badge/Project-Completed-success?style=for-the-badge)
![Level](https://img.shields.io/badge/Level-Intermediate%20to%20Advanced-orange?style=for-the-badge)
![Focus](https://img.shields.io/badge/Domain-Banking-red?style=for-the-badge)

</div>

---

# 📖 Project Overview

Customer churn is one of the biggest challenges faced by financial institutions. Losing existing customers directly impacts revenue, profitability, and long-term business growth.

In this project, I performed an end-to-end **Exploratory Data Analysis (EDA)** and solved **10 real-world business problems** using SQL on a Bank Customer Churn dataset.

The objective was not only to write SQL queries but also to think like a Data Analyst by converting raw customer data into actionable business insights and recommendations.

---

# 🎯 Project Objectives

- Perform Exploratory Data Analysis (EDA)
- Analyze customer churn behavior
- Identify high-risk customer segments
- Measure customer engagement
- Evaluate customer loyalty
- Build business KPIs using SQL
- Provide data-driven business recommendations
- Practice real-world SQL interview scenarios


# Bank-Customer-Churn-Analysis-using-SQL
**This project performs an end-to-end Exploratory Data Analysis (EDA) and Business Intelligence Analysis on a Bank Customer Churn dataset using Microsoft SQL Server.**

**Project Overview**
**This project performs an end-to-end Exploratory Data Analysis (EDA) and Business Intelligence Analysis on a Bank Customer Churn dataset using Microsoft SQL Server.**

**The objective is to analyze customer behavior, identify factors contributing to customer churn, and generate actionable business insights through SQL queries. The project demonstrates practical SQL techniques including aggregations, conditional logic, Common Table Expressions (CTEs), ranking functions, window functions, and business reporting.**

**This repository is designed to showcase SQL skills required for Data Analyst, Business Analyst, and Business Intelligence Analyst roles.**

🎯**Project Objective**

The objective of this project is to:

Perform Exploratory Data Analysis (EDA)
Analyze customer churn patterns
Identify high-risk customer segments
Measure customer engagement
Evaluate customer retention factors
Generate business recommendations using SQL
Build analytical thinking through real-world business scenarios

📌 **Key Business Insights**

Some important findings from the analysis include:

Overall customer churn rate is 20.37%.
Germany has the highest customer churn rate among all countries.
Middle-aged customers exhibit the highest churn behavior.
Customers with 3–4 banking products show significantly higher churn rates.
Inactive customers are almost twice as likely to churn compared to active customers.
Customers with higher account balances have greater churn risk.
Customers with poor credit scores are more likely to leave the bank.
Senior customers with high balances and inactive accounts represent the highest-risk customer segment.

💡 **Business Recommendations**

Based on the analysis:

Develop targeted retention campaigns for inactive customers.
Improve loyalty programs for long-tenured customers.
Provide exclusive benefits for high-value customers.
Strengthen customer engagement in Germany and France.
Monitor customers with poor credit scores more proactively.
Create personalized offers for customers owning multiple banking products.
Build early-warning dashboards for high-risk customer segments.


**Solving Business Problems**

**1. Customer Churn Rate Analysis**
Business Problem:
The bank's leadership wants to know the overall customer churn rate to understand how serious the retention problem is.
Question:
**Q)What percentage of customers have exited the bank?**
```sql 
SELECT 
     CONCAT(CAST(SUM(CASE WHEN Exited = 1 THEN 1 ELSE 0 END) * 100.0 / COUNT(*) AS DECIMAL (10,2)), '%') AS Percentage_Exited
FROM Bank_churn;
```
**2. Geography Performance Analysis (Beginner)**
Business Problem:
The marketing team believes certain countries are losing significantly more customers than others.
**Q. Which geographical region has the highest churn rate, and how many customers were lost from each region?**
```sql
SELECT 
Country,
SUM(CASE WHEN Exited = 1 THEN 1 ELSE 0 END) AS Customers_Exited,
CONCAT(SUM(CASE WHEN Exited = 1 THEN 1 ELSE 0 END)  * 100 /COUNT(*), '%') AS Churn_rate 
FROM Bank_churn
GROUP BY Country
```
**3. Customer Age Risk Analysis (Intermediate)**
Business Problem:
Management suspects older customers are leaving more frequently than younger customers.
**Q.Divide customers into age groups and identify which age group has the highest churn rate.?**
```sql 
SELECT 
CASE 
    WHEN Age BETWEEN 18 AND 25 THEN 'Young Adults'
    WHEN Age BETWEEN 26 AND 40 THEN 'Early Adulthood'
    WHEN Age BETWEEN 41 AND 60 THEN 'Middle Adulthood'
    ELSE 'Older Adulthood'
END AS Age_group,
CONCAT(CAST(SUM(CASE WHEN Exited = 1 THEN 1 ELSE 0 END)  * 100.0 / COUNT(*) AS DECIMAL(10,2)),'%') AS Exited_customer
FROM Bank_churn
GROUP BY CASE 
    WHEN Age BETWEEN 18 AND 25 THEN 'Young Adults'
    WHEN Age BETWEEN 26 AND 40 THEN 'Early Adulthood'
    WHEN Age BETWEEN 41 AND 60 THEN 'Middle Adulthood'
    ELSE 'Older Adulthood'
END 
```
**4. Product Retention Analysis (Intermediate)**
Business Problem:
The product team wants to know whether owning multiple bank products improves customer retention.
**Q.How does churn vary based on the number of products a customer owns?**
```sql
SELECT *,
CAST(Customer_exited * 100.0 / Total_Customer AS DECIMAL(10,2))AS Churn_rates
FROM( 
    SELECT 
    DISTINCT Num_of_Products,
    COUNT(*) AS Total_Customer,
    SUM(CASE WHEN Exited = 1 THEN 1 ELSE 0 END) AS Customer_exited
    FROM dbo.Bank_churn
    GROUP BY Num_of_Products
)t
```
**5. Active Customer Behavior (Intermediate)**
Business Problem:
The customer success team believes inactive members are more likely to leave the bank.
**Q.Compare churn rates between active and inactive members.**
```sql
SELECT *,
CONCAT(CAST(Customer_exited * 100.0 / Total_customer AS DECIMAL (18,2)),'%')AS Churn_rate
FROM (
    SELECT 
       CASE WHEN  Active_member = 1 THEN 'Active'
       ELSE 'Inactive'
    END AS Member,
    COUNT(*) AS Total_customer,
    SUM(CASE WHEN Exited = 1 THEN 1 ELSE 0 END) AS Customer_exited
    FROM Bank_churn 
    GROUP BY CASE WHEN  Active_member = 1 THEN 'Active'
       ELSE 'Inactive'
    END 
)t
```
**6. High-Value Customer Risk Analysis (Intermediate)**
Business Problem:
Losing customers with large account balances hurts the bank's profitability.
**Q.Identify the balance ranges with the highest customer churn and determine whether high-balance customers are at greater risk.**
```sql
SELECT 
RANK() OVER( ORDER BY Customer_exited * 100.0 /Total_Customer DESC) AS RANK_,
Balance_info,
CONCAT(CAST(Customer_exited * 100.0 /Total_Customer AS DECIMAL(10,2)), '%') AS Churn_rate
FROM(
    SELECT
    CASE 
         WHEN Balance BETWEEN 1 AND 50000 THEN '1-50K'
         WHEN Balance BETWEEN 50001 AND 100000 THEN '50K - 100K'
         WHEN Balance BETWEEN 100001 AND 200000 THEN '100K - 200K'
         WHEN Balance > 200001 THEN '200K +'
         ELSE 'No Balance'
    END AS Balance_info, 
    SUM(CASE WHEN Exited = 1 THEN 1 ELSE 0 END) AS Customer_exited,
    COUNT(*) AS Total_Customer
    FROM Bank_churn
    GROUP BY     
    CASE 
         WHEN Balance BETWEEN 1 AND 50000 THEN '1-50K'
         WHEN Balance BETWEEN 50001 AND 100000 THEN '50K - 100K'
         WHEN Balance BETWEEN 100001 AND 200000 THEN '100K - 200K'
         WHEN Balance > 200001 THEN '200K +'
         ELSE 'No Balance'
    END
)t
```
**7. Customer Loyalty vs Churn (Intermediate)**
Business Problem:
The retention department wants to know whether longer customer relationships reduce churn.
**Q.Analyze customer churn across different tenure groups and determine whether customer loyalty reduces the likelihood of leaving.**
```sql
WITH Base_query AS(
SELECT 
CASE WHEN Tenure BETWEEN 0 AND 2 THEN '0-2'
     WHEN Tenure BETWEEN 3 AND 5 THEN '3-5'
     WHEN Tenure BETWEEN 6 AND 8 THEN '6-8'
     ELSE '9-10'
END AS Customer_tenure,
SUM(CASE WHEN Exited = 1 THEN 1 ELSE 0 END) AS Customer_exited,
SUM(CASE WHEN Exited = 0 THEN 1 ELSE 0 END) AS Customer_retention,
COUNT(*) AS Total_customer 
FROM Bank_churn
GROUP BY CASE WHEN Tenure BETWEEN 0 AND 2 THEN '0-2'
     WHEN Tenure BETWEEN 3 AND 5 THEN '3-5'
     WHEN Tenure BETWEEN 6 AND 8 THEN '6-8'
     ELSE '9-10'
END)
SELECT *,
CONCAT(CAST(Customer_exited * 100.0 / Total_customer AS DECIMAL(10,2)),'%') AS Churn_rate
FROM Base_query
```
**8. Credit Score Impact on Churn (Advanced)**
Business Problem:
The risk department wants to understand whether customers with different credit score ranges behave differently.
**Q. Group customers into credit score categories and determine which category experiences the highest churn.**
```sql
WITH Basequery_1 AS
(
SELECT 
CASE WHEN CreditScore BETWEEN 350 AND 579 THEN 'Very poor'
     WHEN CreditScore BETWEEN 580 AND 669 THEN 'Fair'
     WHEN CreditScore BETWEEN 670 AND 739 THEN 'Good'
     WHEN CreditScore BETWEEN 740 AND 799 THEN 'Very Good'
     ELSE 'Exceptional'
END AS Creditscore_range,
SUM(CASE WHEN Exited = 1 THEN 1 ELSE 0 END) AS Customer_exited, 
COUNT(*) AS Total_customers
FROM Bank_churn
GROUP BY  CASE WHEN CreditScore BETWEEN 350 AND 579 THEN 'Very poor'
     WHEN CreditScore BETWEEN 580 AND 669 THEN 'Fair'
     WHEN CreditScore BETWEEN 670 AND 739 THEN 'Good'
     WHEN CreditScore BETWEEN 740 AND 799 THEN 'Very Good'
     ELSE 'Exceptional'
END )
SELECT *,
CAST( Customer_exited * 100.0 / Total_customers AS DECIMAL(10,2)) AS Churn_rates
FROM Basequery_1
ORDER BY Churn_rates DESC
```
**9. High-Risk Customer Profile (Advanced)**
Business Problem:
The executive team wants to identify the profile of customers most likely to leave so retention campaigns can be targeted effectively.
**Q. Identify the combination of customer characteristics (Age, Geography, Gender, Credit Score, Products, Active Status, Balance, Tenure) that produces the highest churn rate.**
```sql
WITH base_query AS
(
SELECT  
CASE WHEN CreditScore BETWEEN 350 AND 579 THEN 'Very poor'
     WHEN CreditScore BETWEEN 580 AND 669 THEN 'Fair'
     WHEN CreditScore BETWEEN 670 AND 739 THEN 'Good'
     WHEN CreditScore BETWEEN 740 AND 799 THEN 'Very Good'
     ELSE 'Exceptional'
END AS Creditscore_range,
Country,
Gender,
CASE WHEN Age BETWEEN 18 AND 30 THEN 'Young'
     WHEN Age BETWEEN 31 AND 45 THEN 'Middle'
     WHEN Age BETWEEN 46 AND 60 THEN 'Senior'
     ELSE 'Elder'
END AS Age_group,
CASE WHEN Tenure BETWEEN 0 AND 2 THEN 'New'
     WHEN Tenure BETWEEN 3 AND 5 THEN 'Regular'
     WHEN Tenure BETWEEN 6 AND 8 THEN 'Loyal'
     ELSE 'Very Loyal'
END AS Customer_tenure,
    CASE 
         WHEN Balance = 0 THEN 'Zero'
         WHEN Balance BETWEEN 1 AND 50000 THEN 'Low'
         WHEN Balance BETWEEN 50001 AND 100000 THEN 'Medium'
         WHEN Balance BETWEEN 100001 AND 200000 THEN 'High'
         ELSE 'Very High'  
    END AS Balance_info, 
Num_of_Products,
CASE WHEN Active_member = 1 THEN 'Yes'
     ELSE 'No'
END AS active_members,
Exited
FROM Bank_churn
)
SELECT 
Gender,
Country,
Age_group,
Creditscore_range,
Customer_tenure,
Balance_info,
Num_of_Products,
active_members,
COUNT(*) AS Total_customers,
SUM(CASE WHEN Exited = 1 THEN 1 ELSE 0 END) AS Customer_exited,
CAST(SUM(CASE WHEN Exited = 1 THEN 1 ELSE 0 END) * 100.0 / COUNT(*)AS DECIMAL (10,2)) AS Churn_rate 
FROM base_query
GROUP BY
Gender,
Age_group,
Country,
Creditscore_range,
Customer_tenure,
Balance_info,
Num_of_Products,
active_members
HAVING COUNT(*) > 10
ORDER BY Churn_rate DESC
```
**10. Executive Retention (Expert)**
Business Problem:
The CEO wants a dashboard highlighting where the bank is losing customers and where retention efforts should be focused.

**Q.Create a ranked report showing the top customer segments with the highest churn rates based on multiple business dimensions such as Geography, Age Group, Product Count, Active Status, Credit Score Range, and Balance Range.**
```sql
WITH base_query_2 AS 
(SELECT 
Gender,
Country,
CASE WHEN Age BETWEEN 18 AND 30 THEN 'Young'
     WHEN Age BETWEEN 31 AND 45 THEN 'Middle'
     WHEN Age BETWEEN 46 AND 60 THEN 'Senior'
     ELSE 'Elder'
END AS Age_group,
CASE WHEN CreditScore BETWEEN 350 AND 579 THEN 'Very poor'
     WHEN CreditScore BETWEEN 580 AND 669 THEN 'Fair'
     WHEN CreditScore BETWEEN 670 AND 739 THEN 'Good'
     WHEN CreditScore BETWEEN 740 AND 799 THEN 'Very Good'
     ELSE 'Exceptional'
END AS Creditscore_range,
    CASE 
         WHEN Balance = 0 THEN 'Zero'
         WHEN Balance BETWEEN 1 AND 50000 THEN 'Low'
         WHEN Balance BETWEEN 50001 AND 100000 THEN 'Medium'
         WHEN Balance BETWEEN 100001 AND 200000 THEN 'High'
         ELSE 'Very High'  
    END AS Balance_info,
Exited,
Num_of_Products,
    CASE WHEN Active_member = 1 THEN 'Yes'
     ELSE 'No'
     END AS active_member
FROM Bank_churn),

base_query_3 AS
(
    SELECT 
    Gender,
    Country,
    Age_group,
    Creditscore_range,
    Balance_info,
    Num_of_Products,
    active_member,
    COUNT(*) AS Total_customers,
    SUM(CASE WHEN Exited = 1 THEN 1 ELSE 0 END) AS Customer_exited,
    CAST(SUM(CASE WHEN Exited = 1 THEN 1 ELSE 0 END) * 100.0 / COUNT(*)AS DECIMAL (10,2)) AS Churn_rate 
    FROM base_query_2
    GROUP BY
    Gender,
    Age_group,
    Country,
    Creditscore_range,
    Balance_info,
    Num_of_Products,
    active_member
    HAVING COUNT(*) >= 10
)
SELECT *,
RANK () OVER(ORDER BY Churn_rate DESC) AS Rank_
FROM base_query_3
```




