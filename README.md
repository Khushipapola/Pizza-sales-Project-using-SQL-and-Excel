###  Pizza Sales Using SQL and Excel

## Objective

This project aims to perform a detailed analysis of pizza sales data using SQL queries and visualize key business insights using Excel dashboards. 
The goal is to understand customer behavior, product performance, and time-based trends to improve business decision-making.

## Business Requirements & Problem Statement
# The pizza restaurant wants to understand:
- How much revenue they’re generating
- What are the most and least popular pizzas
- When customers are placing orders
- Which pizza categories and sizes are performing best


## KPIs  Calculated:
1. Total Revenue: Sum of the total price of all pizza orders
2. Average Order Value: Total revenue ÷ total number of orders
3. Total Pizzas Sold: Sum of all pizza quantities
4. Total Orders: Count of unique orders placed
5. Average Pizzas Per Order: Total pizzas sold ÷ total orders


## SQL Queries Used
1.	Total revenue:
SELECT sum(total_price) as Total_Revenue from pizza_sales;
 
2.	 Average order value:
SELECT sum(total_price)/count(distinct order_id) as Avg_Order_Value from pizza_sales;
 

3.	 Total Pizzas sold:
SELECT sum(quantity) as Total_Pizza_Sold from pizza_sales;
 

4.	 Total orders placed:
SELECT count(distinct(order_id)) as Total_Orders from pizza_sales;
 

5.	 Average pizzas per order:
SELECT CAST(CAST(sum(quantity) AS DECIMAL(10,2))/CAST(count(distinct order_id) AS DECIMAL(10,2)) AS DECIMAL(10,2))  as Avg_Pizza_Sold from pizza_sales;
 

Daily trend for total orders:
SELECT DATENAME(DW, order_date) as order_day, COUNT(DISTINCT order_id) as Total_Orders from pizza_sales 
group by DATENAME(DW, order_date);
 

Hourly trend for orders:
SELECT DATEPART(hour,order_time)as order_hours, count(distinct order_id) as Total_Orders from pizza_sales
group by DATEPART(hour,order_time)
order by DATEPART(hour,order_time);
 
Percentage of sales by pizza category :
SELECT pizza_category, sum(total_price)as total_sales , sum(total_price)* 100/ (SELECT sum(total_price) from pizza_sales where MONTH(order_date)=1 )
as PCT from pizza_sales 
where MONTH(order_date)=1
GROUP BY pizza_category;
 

Percentage of sales by pizza size :
SELECT pizza_size, cast(sum(total_price)as decimal(10,2)) as total_sales , cast(sum(total_price)* 100/ (SELECT sum(total_price) from pizza_sales where DATEPART(quarter,order_date)=1 )as decimal(10,2))
as PCT from pizza_sales 
where DATEPART(quarter,order_date)=1
GROUP BY pizza_size
order by PCT desc;
 

Total no. of pizzas sold by pizza category:
SELECT pizza_category, sum(quantity)as Total_Pizza_Sold
from pizza_sales
group by pizza_category;
 

Top 5 best sellers by total pizzas sold:
SELECT top 5 pizza_name, sum(quantity) as Total_Pizzaa_Sold
from pizza_sales
group by pizza_name
order by sum(quantity) desc;
 

Bottom 5 best sellers by Total pizzas sold:
SELECT top 5 pizza_name, sum(quantity) as Total_Pizzaa_Sold
from pizza_sales
group by pizza_name
order by sum(quantity);
 




## Visualizations and Charts Created
•	Daily Order Trend: Bar chart showing total orders by day of week
•	Hourly Order Trend: Line chart showing total orders by hour
•	Sales by Pizza Category: Pie chart showing revenue contribution per category
•	Sales by Pizza Size: Pie chart showing revenue per size
•	Pizzas Sold by Category: Funnel chart for quantity sold in each category
•	Top 5 Pizzas Sold: Bar chart for best-selling pizzas
•	Bottom 5 Pizzas Sold: Bar chart for least-selling pizzas


 ![Screenshot 2025-05-13 232421](https://github.com/user-attachments/assets/85e28557-afd9-4301-926f-a852a1849f97)


## Tools & Technologies Used
•	SQL: Data cleaning and aggregation
•	Excel: Creating interactive dashboard
•	MS Word: Query documentation


## Insights and Observations

# Overall Performance Snapshot: 
•	Total Revenue: $71,403
•	Average Order Value: $38.53
•	Total Pizzas Sold: 4,328
•	Total Orders: 1,853
•	Average Pizzas Per Order: 2.34
•	Busiest Days and Times: Orders are consistently highest on Fridays and Saturdays, indicating peak demand during the weekend.

 o	The most active ordering times are between 12:00 PM - 1:00 PM and 5:00 PM - 8:00 PM, highlighting lunchtime and dinner rush periods. This information is crucial for staffing and operational planning.

# •	Sales by Category and Size:
o	The "Classic" pizza category contributes the most significantly to both sales and total orders.
o	Large-size pizzas account for the largest share of overall sales revenue, suggesting a customer preference for larger portions or potentially higher pricing for this size.

# •	Best and Worst Selling Pizzas (Based on Revenue):
o	"Classic Deluxe" and "Chicken" pizzas are the top revenue generators, indicating their popularity and potential higher price points or order frequency.
o	"The Brie Carre" is identified as the worst performer in terms of both orders and revenue, suggesting it may be unpopular or priced inappropriately.

# •	Top 5 Best Sellers by Total Pizza Sold (Quantity):
The top 5 most popular pizza choices based on the number of units sold are: 
1.	The Pepperoni Pizza 
2.	The Barbecue Chicken Pizza 
3.	The Classic Deluxe Pizza 
4.	The California Chicken Pizza 
5.	The Hawaiian Pizza 
6.	
# •	Bottom 5 Worst Sellers by Total Pizza Sold (Quantity):
o	The 5 least popular pizza choices based on the number of units sold are: 
1.	The Brie Carre Pizza 
2.	The Chicken Pesto Pizza 
3.	The Calabrese Pizza 
4.	The Chicken Alfredo Pizza 
5.	The Spinach Supreme Pizza 


## Observations:
•	There's a clear correlation between some of the best-selling pizzas by quantity and the top revenue generators (e.g., Classic Deluxe and Chicken).
•	The "Brie Carre" consistently underperforms across both revenue and quantity sold, indicating a potential need for menu review or promotional efforts.
•	Customer ordering behavior shows a strong preference for weekends and specific meal times.
•	The "Classic" pizza category and "Large" size pizzas are significant drivers of overall sales.



### Name: Khushi Papola
### MBA in AI & DS 

