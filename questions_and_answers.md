PIZZA SALES SQL QUERIES
A. KPI’s

1. Total Revenue:
   
        SELECT SUM(total_price) AS Total_Revenue FROM pizza_sales;
 
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
 
C. Hourly Trend for Orders

        SELECT DATEPART(HOUR, order_time) as order_hours, COUNT(DISTINCT order_id) as total_orders
        from pizza_sales
        group by DATEPART(HOUR, order_time)
        order by DATEPART(HOUR, order_time)
        Output
         
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
 
G. Top 5 Best Sellers by Total Pizzas Sold
SELECT Top 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold DESC
Output
 




H. Bottom 5 Best Sellers by Total Pizzas Sold
SELECT TOP 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold ASC
Output
 

NOTE
If you want to apply the Month, Quarter, Week filters to the above queries you can use WHERE clause. Follow some of below examples
SELECT DATENAME(DW, order_date) AS order_day, COUNT(DISTINCT order_id) AS total_orders 
FROM pizza_sales
WHERE MONTH(order_date) = 1
GROUP BY DATENAME(DW, order_date)

*Here MONTH(order_date) = 1 indicates that the output is for the month of January. MONTH(order_date) = 4 indicates output for Month of April.

SELECT DATENAME(DW, order_date) AS order_day, COUNT(DISTINCT order_id) AS total_orders 
FROM pizza_sales
WHERE DATEPART(QUARTER, order_date) = 1
GROUP BY DATENAME(DW, order_date)

*Here DATEPART(QUARTER, order_date) = 1 indicates that the output is for the Quarter 1. MONTH(order_date) = 3 indicates output for Quarter 3.
