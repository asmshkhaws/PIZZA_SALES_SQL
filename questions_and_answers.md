PIZZA SALES SQL QUERIES
A. KPI’s

1. Total Revenue:
   
        SELECT SUM(total_price) AS Total_Revenue FROM pizza_sales;
   Output:
      |total_revenue|
      |:----|
      |817860.05083847|

 
2. Average Order Value
   
        SELECT (SUM(total_price) / COUNT(DISTINCT order_id)) AS Avg_order_Value FROM pizza_sales
   Output:
      |avg_order_Value|
      |:----|
      |38.3072623343546|

 
3. Total Pizzas Sold
    
        SELECT SUM(quantity) AS Total_pizza_sold FROM pizza_sales
   Output:
      |total_pizza_sold|
      |:----|
      |49574|

 
4. Total Orders
   
        SELECT COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sales
   Output:
   
   |Total_orders|
   |:----|
   |21350|


5. Average Pizzas Per Order
   
        SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10,2)) / 
        CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS DECIMAL(10,2))
        AS Avg_Pizzas_per_order
        FROM pizza_sales
   Output:
   |avg_pizza_per_order|
   |:----|
   |2.32|


B. Daily Trend for Total Orders

        SELECT DATENAME(DW, order_date) AS order_day, COUNT(DISTINCT order_id) AS total_orders 
        FROM pizza_sales
        GROUP BY DATENAME(DW, order_date)
        
   Output:
   |order_day|total_order|
   |:----|:----|
   |Saturday|3158|
   |Wednesday|3024|
   |Monday|2794|
   |Sunday|2624|
   |Friday|3538|
   |Thursday|3239|
   |Tuesday|2973|

C. Hourly Trend for Orders

        SELECT DATEPART(HOUR, order_time) as order_hours, COUNT(DISTINCT order_id) as total_orders
        from pizza_sales
        group by DATEPART(HOUR, order_time)
        order by DATEPART(HOUR, order_time)
   Output:
   |order_hour|total_order|
   |:----|:----|
   |9|1|
   |10|8|
   |11|1231|
   |12|2520|
   |13|2455|
   |14|1472|
   |15|1468|
   |16|1920|
   |17|2336|
   |18|2399|
   |19|2009|
   |20|1642|
   |21|1198|
   |22|663|
   |23|28|


         
D. % of Sales by Pizza Category

        SELECT pizza_category, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
        CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
        FROM pizza_sales
        GROUP BY pizza_category
   Output:
   |pizza_category|total_revenue|pct_of_sale_per_category|
   |:----|:----|:----|
   |Classic|18619.40|26.68|
   |Chicken|16188.75|23.20|
   |Veggie|17055.40|24.44|
   |Supreme|17929.75|25.69|


 
E. % of Sales by Pizza Size

        SELECT pizza_size, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
        CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
        FROM pizza_sales
        GROUP BY pizza_size
        ORDER BY pizza_size
        
   Output:
   |pizza_size|total_revenue|pct_sales_by_pizza_size|
   |:----|:----|:----|
   |L|375318.70|45.89|
   |XXL|1006.60|0.12|
   |M|249382.25|30.49|
   |XL|14076.00|1.72|
   |S|178076.50|21.77|

F. Total Pizzas Sold by Pizza Category

        SELECT pizza_category, SUM(quantity) as Total_Quantity_Sold
        FROM pizza_sales
        WHERE MONTH(order_date) = 2
        GROUP BY pizza_category
        ORDER BY Total_Quantity_Sold DESC
        
   Output:
   |pizza_category|total_quantity|
   |:----|:----|
   |Classic|14888|
   |Supreme|11987|
   |Veggie|11649|
   |Chicken|11050|

 
G. Top 5 Best Sellers by Total Pizzas Sold

      SELECT Top 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
      FROM pizza_sales
      GROUP BY pizza_name
      ORDER BY Total_Pizza_Sold DESC
      
   Output:
   |pizza_name|total_sold|
   |:----|:----|
   |The Classic Deluxe Pizza|2453|
   |The Barbecue Chicken Pizza|2432|
   |The Hawaiian Pizza|2422|
   |The Pepperoni Pizza|2418|
   |The Thai Chicken Pizza|2371|



H. Bottom 5 Best Sellers by Total Pizzas Sold

      SELECT TOP 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
      FROM pizza_sales
      GROUP BY pizza_name
      ORDER BY Total_Pizza_Sold ASC
      
   Output:
   |pizza_name	|total_sold|
   |:----|:----|
   |The Classic Deluxe Pizza	|2453|
   |The Barbecue Chicken Pizza	|2432|
   |The Hawaiian Pizza	|2422|
   |The Pepperoni Pizza	|2418|
   |The Thai Chicken Pizza	|2371|




 
