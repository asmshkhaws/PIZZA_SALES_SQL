Select *
From pizza_sales


--A. KPI’s
--1. Total Revenue:

    Select Sum(total_price) as total_revenue
    From pizza_sales

--------------------------------------------------------------------------------------------------------------------
--2. Average Order Value


    Select Sum(total_price)/Count(Distinct order_id) as avg_order_Value	
    From pizza_sales

--------------------------------------------------------------------------------------------------------------------
--3. Total Pizzas Sold
Select Sum(quantity) as total_pizza_sold
From pizza_sales

--------------------------------------------------------------------------------------------------------------------
--4. Total Orders

Select Count(Distinct order_id) as Total_orders
From pizza_sales

--------------------------------------------------------------------------------------------------------------------
--5. Average Pizzas Per Order

--Select Sum(quantity)/Count(Distinct order_id) as Avg_pizza_per_order
--From pizza_sales

--In Decimal
    Select Cast(Cast(Sum(quantity) as decimal(10,2))/
    Cast(Count(Distinct order_id)as Decimal(10,2)) as Decimal(10,2)) 
    as avg_pizza_per_order
    From pizza_sales

--------------------------------------------------------------------------------------------------------------------
--B. Daily Trend for Total Orders
--DATENAME = Return a specified part of a date:
--DW = Weekday

    Select DATENAME(DW, order_date) as order_day, Count(Distinct order_id) as total_order
    From pizza_sales
    Group by DATENAME(DW, order_date)

--------------------------------------------------------------------------------------------------------------------
--C. Hourly Trend for Orders

    Select DATEPART(HOUR, order_time) as order_hour, Count(Distinct order_id) as total_order
    From pizza_sales
    Group by DATEPART(HOUR, order_time)
    order by DATEPART(HOUR, order_time)

--------------------------------------------------------------------------------------------------------------------
--D. % of Sales by Pizza Category for January Month

--Total Sum of price irrespective of category := "Select Sum(total_price) From pizza_sales"
--January Month := Where Month(order_date) = 1, This clause is imp in Above formula as well other wise there will be error in result (54:00)


    Select pizza_category,CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue, 
    Cast(Sum(total_price)*100/(Select Sum(total_price) from pizza_sales Where Month(order_date) = 1) as decimal(10,2)) 
    as pct_of_sale_per_category
    From pizza_sales
    Where Month(order_date) = 1
    Group by pizza_category

--------------------------------------------------------------------------------------------------------------------
--E. % of Sales by Pizza Size

    Select pizza_size,CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue, 
    Cast(Sum(total_price)*100/(Select Sum(total_price) from pizza_sales) as Decimal(10,2)) 
    as pct_sales_by_pizza_size
    From pizza_sales
    Group by pizza_size

--------------------------------------------------------------------------------------------------------------------
--F. Total Pizzas Sold by Pizza Category
Select pizza_category, Sum(quantity) as total_quantity
From pizza_sales
Group by pizza_category
Order by total_quantity desc

--------------------------------------------------------------------------------------------------------------------
--G. Top 5 Best Sellers by Total Pizzas Sold

    Select Top 5 pizza_name, Sum(quantity) as total_sold
    From pizza_sales
    Group by pizza_name
    Order by total_sold Desc

--------------------------------------------------------------------------------------------------------------------
--H. Bottom 5 Best Sellers by Total Pizzas Sold

    Select Top 5 pizza_name, Sum(quantity) as total_sold
    From pizza_sales
    Group by pizza_name
    Order by total_sold asc

---------------------------------------------------------------------------------------------------------------------
