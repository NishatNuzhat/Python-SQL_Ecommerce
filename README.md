# Python+SQL_Ecommerce
## Overview
Target is a globally recognized brand and a leading retailer in the united states,known for offering exceptional value,inspiration,innovation and a unique shopping experience.
This dataset focuses on Target's operations in Brazil,covering 100,000 orders placed 2016 and 2018.It includes detail information on order status,pricing,payment and shopping performance,customer locations,product attributes and customer reviews.
## The Objectives
- Loading the dataset to MySQL with the help of Python.
- Using SQL queries for analyzing the dataset.
- Using Python for data visualization.
## Dataset
The dataset for this project is sourced from kaggle.
## Business Problems and Solutions

### 1. List all unique cities where customers are located.

```sql
SELECT 
distinct customer_city 
FROM 
customers;
```
### 2. Count the number of orders placed in 2017.

```sql
SELECT 
COUNT(*) 
FROM 
orders
WHERE
YEAR(order_purchase_timestamp) = 2017;
```
### 3. Find the total sales per category.

```sql
select 
UPPER(p.product_category) as Category,
ROUND(SUM(pa.payment_value),2) as Total_Sales
FROM
products as p
left join
order_items as o
ON 
p.product_id = o.product_id
left join
payments as pa
on o.order_id = pa.order_id
GROUP BY 
Category;
```
### 4. Calculate the percentage of orders that were paid in installments.

```sql
select 
((sum(case when payment_installments >= 1 then 1 else 0 end))/count(*))*100 as Installment_Order_Percentage
from payments;
```
### 5. Count the number of customers from each state.
```sql
select 
customer_state,count(customer_id) as Total_customers
from customers
group by 1
order by 2 desc;
```
