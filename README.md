# PowerBI_Portfolio

# 1. Pizza Sales Report

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
- Connect SQL Server to Power BI and import the Pizza sales data
- Verify data for any missing values and anomalies, and sort out the same.
- Make sure data is consistent and clean with respect to data type, data format and values used.
- DAX calculations, Dashboard lay outing, Charts Development and Formatting using interactive features like slicers, buttons, bookmarks etc.
- Dashboard/ Report Development
- Run SQL queries for all the requirements and KPIs so that dashboard output can be validated.
- Insights generation

## Dashboard</br>
-HomePage</br>
![PizzaSQL_Home](https://github.com/user-attachments/assets/33b5ab3c-cbb1-4229-9022-5b91537a3636) </br>

-Best/Worst Sellers Page</br>
![BestWorstSellers](https://github.com/user-attachments/assets/316fae8a-8475-4e8d-909d-64a2cf871393) </br>


## SQL Queries used to Validate Dashboard Data

A. KPI’s
1. Total Revenue:</br>
SELECT SUM(total_price) AS Total_Revenue FROM pizza_sales;</br>
![total revenue](https://github.com/user-attachments/assets/4f1842a7-d8f5-43c1-a3b8-dca9e748a89b)

2. Average Order Value</br>
SELECT (SUM(total_price) / COUNT(DISTINCT order_id)) AS Avg_order_Value FROM pizza_sales;</br>
 ![AverageOrderValue](https://github.com/user-attachments/assets/5721be19-e68a-46c5-8f08-5c8770884038)

3. Total Pizzas Sold</br>
SELECT SUM(quantity) AS Total_pizza_sold FROM pizza_sales;</br>
 ![Tot Pizza sold](https://github.com/user-attachments/assets/7416d15e-4f8a-43f6-9581-5fadb1736203)

4. Total Orders</br>
SELECT COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sales;</br>
 ![Total Oders](https://github.com/user-attachments/assets/5b005f33-edfc-451e-a7e0-f287abb3d08e)

5. Average Pizzas Per Order</br>
SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10,2)) / 
CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS DECIMAL(10,2))
AS Avg_Pizzas_per_order
FROM pizza_sales</br>
Output:</br>
![Avg pizza perr order](https://github.com/user-attachments/assets/5f246c66-9c0a-4b23-b206-0b6d81f7d4c7)

 
B. Daily Trend for Total Orders</br>
SELECT DATENAME(DW, order_date) AS order_day, COUNT(DISTINCT order_id) AS total_orders 
FROM pizza_sales
GROUP BY DATENAME(DW, order_date);</br>
Output:</br>
![Daily Trend](https://github.com/user-attachments/assets/7e9f3d15-9c7b-4bd5-b80d-1e9d46a5e8ca)

C. Monthly Trend for Orders</br>
select DATENAME(MONTH, order_date) as Month_Name, COUNT(DISTINCT order_id) as Total_Orders
from pizza_sales
GROUP BY DATENAME(MONTH, order_date);</br>
Output:</br>
![Monthly Trend](https://github.com/user-attachments/assets/5745d9c8-364c-4340-969f-3762bc0197b8)

D. % of Sales by Pizza Category</br>
SELECT pizza_category, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_category;</br>
Output:</br>
 ![sales by cat](https://github.com/user-attachments/assets/74e3d6fe-bebd-4ca1-af4f-1a4b1bf4ef80)

E. % of Sales by Pizza Size</br>
SELECT pizza_size, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_size
ORDER BY pizza_size;</br>
Output:</br>
![sales by size](https://github.com/user-attachments/assets/cc92f6c3-3204-481c-a2ea-76858680dfda)

F. Total Pizzas Sold by Pizza Category</br>
SELECT pizza_category, SUM(quantity) as Total_Quantity_Sold
FROM pizza_sales
WHERE MONTH(order_date) = 2
GROUP BY pizza_category
ORDER BY Total_Quantity_Sold DESC;</br>
Output:</br>
![pizzas sold by cat](https://github.com/user-attachments/assets/41a6523e-e7fa-49f5-b21c-30bb5de4fcc0)

 
G. Top 5 Pizzas by Revenue</br>
SELECT Top 5 pizza_name, SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue DESC;</br>
![top 5](https://github.com/user-attachments/assets/9624666e-b95d-4c18-b66c-5eb839efca0a)

 
H. Bottom 5 Pizzas by Revenue</br>
SELECT Top 5 pizza_name, SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue ASC;</br>
![bottom 5](https://github.com/user-attachments/assets/89bd5d12-06e4-4432-8f77-1d47de31d967)

I. Top 5 Pizzas by Quantity</br>
SELECT Top 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold DESC;</br>
Output</br>
![topQty](https://github.com/user-attachments/assets/43facca3-f02e-4e79-9b15-c5b7f26aff04)

J. Bottom 5 Pizzas by Quantity</br>
SELECT TOP 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold ASC;</br>
Output</br>
![bottomQuantity](https://github.com/user-attachments/assets/edf0758b-e61b-4b46-8576-94754131754f)

K. Top 5 Pizzas by Total Orders</br>
SELECT Top 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders DESC;</br>
![topOrders](https://github.com/user-attachments/assets/d500f497-876a-4bb3-a051-ed68e52670d9)
 
L. Borrom 5 Pizzas by Total Orders</br>
SELECT Top 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders ASC;</br>

![botOrders](https://github.com/user-attachments/assets/a653fc55-45a3-4795-bf28-715a3dd4022a)

## Project Insight
- Orders are highest on Weekends.(FRI, SAT, SUN)
- There are maximum orders from the month of July and January
- Classic Category contributes maximum sales(~27%) and Max Orders (14888)
- Large Size Pizza contributes to  maximum sales (~46%) and X-Large/XX-Large Pizzas have lowest sales.
- Best Seller by Revenue is "The Thai Chicken Pizza" and the Best Seller by Quantity Sold, Total Orders is "The Classic Deluxe Pizza".
- Worst Seller in all three parameters is "The Brie Carre Pizza"

## Final Conclusion:
To improve the Pizza sales, a strategic marketing plan for the weekends sales should be implemented. Customers make maximum purchases on weekends so more lucrative offers can be rolled out to improve sales. X-Large/XX-Large Pizzas as well as The Brie Carre Pizza have lowest sales so feedback must be taken from customers on the products and if sales don't improve further even after rolling offers, reducing price and implementing customer's feedback, they can be discontinued.</br>


# 2. Spotify Report

## Project Objective
In today’s digital music era, understanding listening patterns is crucial for both users and streaming platforms. This analysis focuses on Spotify Data, providing insights into user engagement with albums/artists/Tracks over time.

## Dataset used
- <a href="https://github.com/sukanyaChoudhury/PowerBI_Portfolio/blob/main/Spotify%20Dashboard%20Files/spotify_history.csv">Dataset</a>

## Questions (KPIs)
🎵 Total Albums Played Over Time – Track how album listening trends change over months and years.📅 Number of Albums Listened by Year – Identify annual listening habits and volume (Find the Min and Max Albums in the view).</br>
💥Albums Played on Weekday & Weekend – Identify the Pattern of music listening on weekdays and weekends.🏆 Top 5 Albums – Identify the most played albums based on listening frequency.</br>
📊 Latest Year vs Previous Year Analysis – Compare album consumption between the latest and previous years, including:</br>
LY (Latest Year) vs PY (Previous Year) Trends</br>
YoY (Year-over-Year) Growth Analysis</br>



