# PowerBI_Portfolio

# Pizza Sales Report

## Project Objective
Analyze Key indicators of Pizza sales to be able to gain insights into the business performance to identify which areas need more focus to perform better.

## Dataset used
- <a href="https://github.com/sukanyaChoudhury/PowerBI_Portfolio/blob/main/Pizza%20Sales%20Dashboard/pizza_sales.csv">Dataset</a>
Above CSV raw data is imported into SQL server and then the created tables are imported in Power BI

## Questions (KPIs)
- Total Revenue: What is the Total Revenue earned?
- Average order value: How much amount is spent per order on an average?
- Total Pizzas sold: How many pizzas were sold?
- Total Orders: How many total orders were placed?
- Average Pizzas per Order: How many Pizzas were sold per Order on an average?

## Charts Requirements
- Daily Trend for Total Orders:
  Identify any pattern or fluctuations in order volumes on a daily basis.
  Create a bar chart to display the daily trend of total orders over a specific time period.
- Monthly Trend for Total Orders:
  Create a line chart to display the monthly trend of total orders over a specific time period.
- Percentage of Sales by Pizza category:
  Find popularity of various pizza categories and their contribution to overall sales. 
  Create a Pie chart to show this distribution of sales across various pizza categories.
- Percentage of Sales by Pizza size:
  Find customer preferences for Pizza sizes and their impact on the overall sales.
  Generate a Pie chart showing the percentage of sales for different pizza size.
- Total Pizzas sold by Pizza category:
  Create a funnel chart to compare the sales performance of different pizza categories.
- Top 5 Best Sellers by Revenue, Total Quantity and Total Orders:
  Create a bar chart to identify top 5 best sellers.
- Bottom 5 Best Sellers by Revenue ,Total Quantity and Total Orders:
  Create a bar chart to identify top 5 worst sellers.


## Process
- Import raw data into SQL server. 
- Verify data for any missing values and anomalies, and sort out the same.
- Run SQL queries for all the requirements and KPIs so that dashboard output can be validated.
- Connect SQL Server to Power BI and import the Pizza sales data
- Make sure data is consistent and clean with respect to data type, data format and values used.
- DAX calculations, Dashboard lay outing, Charts Development and Formatting.
- Dashboard/ Report Development
- Insights generation

## SQL Queries used to Validate Dashboard Data

A. KPI’s
1. Total Revenue:</br>
SELECT SUM(total_price) AS Total_Revenue FROM pizza_sales;</br>
![total revenue](https://github.com/user-attachments/assets/4f1842a7-d8f5-43c1-a3b8-dca9e748a89b)

 
2. Average Order Value
SELECT (SUM(total_price) / COUNT(DISTINCT order_id)) AS Avg_order_Value FROM pizza_sales
 
3. Total Pizzas Sold
SELECT SUM(quantity) AS Total_pizza_sold FROM pizza_sales
 
4. Total Orders
SELECT COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sales
 
5. Average Pizzas Per Order
SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10,2)) / 
CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS DECIMAL(10,2))
AS Avg_Pizzas_per_order
FROM pizza_sales
 
B. Daily Trend for Total Orders
SELECT DATENAME(DW, order_date) AS order_day, COUNT(DISTINCT order_id) AS total_orders 
FROM pizza_sales
GROUP BY DATENAME(DW, order_date)
Output:
 
C. Monthly Trend for Orders
select DATENAME(MONTH, order_date) as Month_Name, COUNT(DISTINCT order_id) as Total_Orders
from pizza_sales
GROUP BY DATENAME(MONTH, order_date)Output
 


D. % of Sales by Pizza Category
SELECT pizza_category, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_category
Output
 
E. % of Sales by Pizza Size
SELECT pizza_size, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_size
ORDER BY pizza_size
Output
 

F. Total Pizzas Sold by Pizza Category
SELECT pizza_category, SUM(quantity) as Total_Quantity_Sold
FROM pizza_sales
WHERE MONTH(order_date) = 2
GROUP BY pizza_category
ORDER BY Total_Quantity_Sold DESC
Output
 
G. Top 5 Pizzas by Revenue
SELECT Top 5 pizza_name, SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue DESC
 
H. Bottom 5 Pizzas by Revenue
SELECT Top 5 pizza_name, SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue ASC
 
I. Top 5 Pizzas by Quantity
SELECT Top 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold DESC
Output
 
J. Bottom 5 Pizzas by Quantity
SELECT TOP 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold ASC
Output
 



K. Top 5 Pizzas by Total Orders
SELECT Top 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders DESC
 
L. Borrom 5 Pizzas by Total Orders
SELECT Top 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders ASC
 
NOTE
If you want to apply the pizza_category or pizza_size filters to the above queries you can use WHERE clause. Follow some of below examples
SELECT Top 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
WHERE pizza_category = 'Classic'
GROUP BY pizza_name
ORDER BY Total_Orders ASC

## Dashboard



## Project Insight
- Women customers are more likely to buy products compared to men (~65%).
- The states of Maharashtra, Karnataka and Uttar Pradesh are the top 3 product buyers.
- The adult age group (30-49 yrs) is max contributing (~50%) and buys the most products.
- The maximum number of products customer orders from Amazon, Flipkart and Myntra channels.
- More than 90% of the products delivered

## Final Conclusion:
To improve the sales of Vrinda Store, a strategic marketing plan focused on women aged 30-49 years residing in Maharashtra, Karnataka, and Uttar Pradesh should be implemented. This demographic represents a key consumer segment, as they often make significant household and lifestyle purchases. The approach should include targeted digital marketing campaigns and personalized promotions to capture their attention.

