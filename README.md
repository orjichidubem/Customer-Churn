# Customer-Churn

### Project Overview
---
Customer churn is when customers terminates or stops using a product or services of a company, resulting in loss of revenue and potential long-term damage to the company. This project analyzes the customer churn dataset to identify key factors contributing to customer churn and gives key insights for business improvement.

### Data Sources
The analysis is based on the customer churn dataset containing informations on:
- Payment history.
- Contract details.
- Customer identifiers
- Other relevant customer attributes.

### Tools
- Excel - Data Cleaning.
- SQL Server - Data Analysis.
- Power BI - Data Visualization.

### Data Cleaning Process

Data cleaning process was carried out to ensure data quality as follows:
1. Data loading and inspection.
2. Handling of spelling Erros.
3. Assigning of data types.
4. Removal of duplicate.
5. Making use of power query to fix an error.

### Exploratoy Data Analysis

EDA involved in exploring the customer churn dataset to answer key questions and identify patterns and trends:

- How has the churn rate changed overtime.
- Average age of customers who churned and who did not.
- Gender with the highest churn count.
- Distribution of customers by age group.
- Subscription with the highest churn count.

### Data Analysis

This was analyzied with SQL Server:

```sql
--Q1. How has the churn rate changed overtime.
select contract_length,
round(count(case when churn = 1
then CustomerID end) * 100.0 / count(CustomerID), 2) as churn_rate
from customer_churn
group by contract_length
order by contact_length;
```

![trend](https://github.com/user-attachments/assets/7b5c1177-b6ae-48d7-ac79-f78174c1b936)


```sql
--Q2. Average age of customers who churned and who did not.
selwct avg(age) as AverageChurnedAge
from customer_churn
where churn = 1;
select avg(age) as AverageChurnedAge
from customer_churn
where churn = 0:
```

![churn](https://github.com/user-attachments/assets/fadc74dc-d5ff-474e-a292-76580fba0818)


```sql
--Q3. Gender with the highest churn count.
select Gender, sum(case when churn = 1 then 1 end) as churn_count
from customer_churn
group by gender
oerder by Churn_count desc;
```


```sql
--Q4. Distribution of customers by age group.
select
    case
    when age >= 18 and age <= 28
then '18-28'
    when age >= 29 and age <= 38
then '28-38'
    when age >= 39 and age <= 48
then '39-48'
    when age >= 49 and age <= 58
then '49-58'
    when age >= 59 then '68+'
    else 'UNKNOWN'
    end as Age_Group,
    count(*) as Customer_count
from Customer_churn
group by
      case
    when age >= 18 and age <= 28
then '18-28'
    when age >= 29 and age <= 38
then '28-38'
    when age >= 39 and age <= 48
then '39-48'
    when age >= 49 and age <= 58
then '49-58'
    when age >= 59 then '68+'
    else 'UNKNOWN'
    end
order by Age_Group;
```

![age grp](https://github.com/user-attachments/assets/bee23ec1-d29b-4841-986e-96ec6f209456)


```sql
--Q5.Subscription with the highest churn count.
select Subscription_type, sum(case when churn = 1 then 1 end) as TotalChurn
from customer_churn
group by subcription_type;
```

![sub typ](https://github.com/user-attachments/assets/87f5b7b0-a4a3-4efb-a76f-6badab0156d0)


### Results And Findings

The potential analysis are summarized as follows:
1. Customers with support calls and payment delay are likely to churn.
2. Payment delay imposes a huge factor to customer churn.

### Recommendations
Based on my analysis, here are some recommendations:
- Improve Payment Process: Streamline payment systems, offer flexible payment options, and send timely reminders to reduce payment delays.
- Enhance Customer Support: Provide effective support through multiple channels(e.g,phone,email,chat), and ensure issues are resloved promptly.
- Proactive Churn Prevention: Identify early warning signs of churn(e.g,payment delay,support calls) and intervene proactively.

### Limitations
1. The analysis does not account for external factors, such as economic changes or competiton activity, that may impact customer churn. 
