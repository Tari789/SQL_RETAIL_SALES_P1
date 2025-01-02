# Retail Sales Analysis SQL Project

## Project Overview

**Project Title**: Retail Sales Analysis  
**Level**: Beginner  
**Database**: `sql_project_1`

This project is designed to demonstrate SQL skills and techniques typically used by data analysts to explore, clean, and analyze retail sales data. The project involves setting up a retail sales database, performing exploratory data analysis (EDA), and answering specific business questions through SQL queries.

## Objectives

1. **Set up a retail sales database**: Create and populate a retail sales database with the provided sales data.
2. **Data Cleaning**: Identify and remove any records with missing or null values.
3. **Exploratory Data Analysis (EDA)**: Perform basic exploratory data analysis to understand the dataset.
4. **Business Analysis**: Use SQL to answer specific business questions and derive insights from the sales data.

## Project Structure

### 1. Database Setup


```sql
CREATE DATABASE sql_project_1;

Create TABLE retail_sales 
( 
       transactions_id INT PRIMaRY KEY,
       sale_date DATE,
       sale_time TIME,
       customer_id INT ,
       gender VARCHAR (15),
       age INT,
       category VARCHAR (15),
       quantiy INT,
       price_per_unit FLOAT,
       cogs	 Float,
       total_sale FLOAT 
   ) ;
```

### 2. Data Exploration & Cleaning

- **Record Count**: Determine the total number of records in the dataset.

- **Null Value Check**: Check for any null values in the dataset and delete records with missing data.


```sql
Select * from retail_sales Limit 10 
SELECT COUNT(DISTINCT customer_id) FROM retail_sales;
SELECT DISTINCT category FROM retail_sales;

 Select * from retail_sales
 WHERE 
     transactions_id Is NUll 
     or 
     sale_date IS NULL 
     OR 
     sale_time Is Null 
     or 
     customer_id is null 
     or 
     gender is null 
     or 
     age  is null 
     or
     category is null
     or 
     quantiy is null 
     or 
     price_per_unit is null 
     or 
     cogs is null 
     or 
     total_sale is null 

 DELETE from retail_sales
  WHERE 
     transactions_id Is NUll 
     or 
     sale_date IS NULL 
     OR 
     sale_time Is Null 
     or 
     customer_id is null 
     or 
     gender is null 
     or 
     age  is null 
     or
     category is null
     or 
     quantiy is null 
     or 
     price_per_unit is null 
     or 
     cogs is null 
     or 
     total_sale is null

```

### 3. Data Analysis & Findings

The following SQL queries were developed to answer specific business questions:

1. **Write a SQL query to retrieve all columns for sales made on '2022-11-05**:
```sql
SELECT * from retail_sales 
where sale_date = '2022-11-05';
```

2. **Write a SQL query to retrieve all transactions where the category is 'Clothing' and the quantity sold is more than 4 in the month of Nov-2022**:
```sql
Select * 
from retail_sales 
where category = 'Clothing'
and 
quantiy = '4'
and sale_date BETWEEN '2022-11-01' and '2022-11-30'
```

3. **Write a SQL query to calculate the total sales (total_sale) for each category.**:
```sql
Select category, Sum(total_sale), count( * ) from retail_sales 
group by category
```

4. **Write a SQL query to find the average age of customers who purchased items from the 'Beauty' category.**:
```sql
Select Round(Avg(age),2) , category from retail_sales 
where category = 'Beauty'
```

5. **Write a SQL query to find all transactions where the total_sale is greater than 1000.**:
```sql
Select * from retail_sales 
where total_sale > 1000 
```

6. **Write a SQL query to find the total number of transactions (transaction_id) made by each gender in each category.**:
```sql
Select  category , gender,  count(*)   
from retail_sales 
group by 1 , 2 
order by 1 
```

7. **Write a SQL query to calculate the average sale for each month. Find out best selling month in each year**:
```sql
WITH cte_rank AS (
    SELECT
        EXTRACT(YEAR FROM sale_date) AS "year", 
        EXTRACT(MONTH FROM sale_date) AS "month",
        AVG(total_sale) AS avg_sales,
        RANK() OVER (
            PARTITION BY EXTRACT(YEAR FROM sale_date)
            ORDER BY AVG(total_sale) DESC
        ) AS rank
    FROM retail_sales
    GROUP BY 1, 2
    ORDER BY 1, 3 DESC
)
SELECT *
FROM cte_rank
WHERE rank = '1'
```

8. **Write a SQL query to find the top 5 customers based on the highest total sales **:
   
```sql
 Select 
  customer_id, SUM(total_sale)  as total_sales
  from retail_sales
   group by 1 
   order by total_sales DESC 
   limit 5 
```

9. **Write a SQL query to find the number of unique customers who purchased items from each category.**:
    
```sql
Select category , COUNT(DISTINCT customer_id)
from retail_sales
Group by category 
```

10. **Write a SQL query to create each shift and number of orders (Example Morning <12, Afternoon Between 12 & 17, Evening >17)**:
    
```sql

with hourly_sale
 as  
 (
Select * , 
 Case 
   when EXTRACT (Hour from sale_time)< 12 Then 'Morning'
   WheN EXTRACT (Hour from sale_time) BETWEEN 12 and 17 Then 'Afternoon'
   Else  'Evening'
End as shift 
From retail_sales 
) 


Select count(transactions_id as total_orders , shift 
from hourly_sale
```

## Findings

- **Customer Demographics**: The dataset includes customers from various age groups, with sales distributed across different categories such as Clothing and Beauty.
- **High-Value Transactions**: Several transactions had a total sale amount greater than 1000, indicating premium purchases.
- **Sales Trends**: Monthly analysis shows variations in sales, helping identify peak seasons.
- **Customer Insights**: The analysis identifies the top-spending customers and the most popular product categories.

## Reports

- **Sales Summary**: A detailed report summarizing total sales, customer demographics, and category performance.
- **Trend Analysis**: Insights into sales trends across different months and shifts.
- **Customer Insights**: Reports on top customers and unique customer counts per category.

## Conclusion

This project serves as a comprehensive introduction to SQL for data analysts, covering database setup, data cleaning, exploratory data analysis, and business-driven SQL queries. The findings from this project can help drive business decisions by understanding sales patterns, customer behavior, and product performance.


