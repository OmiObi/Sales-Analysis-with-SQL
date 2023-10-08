# DATA EXPLORATION
## DATA INSIGHTS 


- The Organization is planning to reward the best-performing manager (the one who made the best sales) and wants to know the region to which the manager belongs.
```sql
Select Top 1 b.Manager, a.Region, sum(a.Sales) Total_Sales
FROM [Sales_Analysis].[dbo].[Sales_transaction] a
inner join [Sales_Analysis].[dbo].[Regional_manager] b
on a.Region = b.Region_Name
group by b.Manager, a.Region
order by Total_Sales desc;
```
![alt text](C:\Users\omowu\OneDrive\Documents\GitHub\Sales-Analysis-with-SQL\images\1.jpg)

Pat, the Manager in charge of the West Region is the Manager with the best Sales ($3,597,549.329).


- How many times was the delivery truck used as the ship mode?
```sql
select count (Ship_Mode) 'Count of Transation'
from [Sales_Analysis].[dbo].[Sales_transaction]
where Ship_mode = 'Delivery Truck';
```
![alt text](C:\Users\omowu\OneDrive\Documents\GitHub\Sales-Analysis-with-SQL\images\2.jpg)

The delivery Truck was used as a ship mode 1,146 times.


- How many orders were returned, and which product category got rejected the most?
```sql
select count(Order_Status) 'Count of Returned Order Status'
from [Sales_Analysis].[dbo].[Returned_items]
where Order_status ='Returned';
```
```sql
Select b.Product_Category, count(a.Order_status)'Count of Returned Order Status'
from [Sales_Analysis].[dbo].[Returned_items] a
inner join [Sales_Analysis].[dbo].[Sales_transaction] b
on a.Sales_id = b.Sales_id
where a.Order_status = 'Returned'
group by b.Product_category
order by 'count of Returned Order Status' desc;
```
![alt text](C:\Users\omowu\OneDrive\Documents\GitHub\Sales-Analysis-with-SQL\images\3.jpg)

872 orders were returned in total and the most rejected product category is Office supplies with a total of 461 returned orders.


- Which Year did the company incur the least shipping cost?
```sql
Select top 1 datepart (year, Ship_date) as Ship_year, sum(shipping_cost) Ship_Cost
from [Sales_Analysis].[dbo].[Sales_transaction]
Group by datepart (year, Ship_date)
order by Ship_Cost;
```
![alt text](C:\Users\omowu\OneDrive\Documents\GitHub\Sales-Analysis-with-SQL\images\5.jpg)

In company incurred the least shipping cost in 2011.


- Day of the week in which the customer segment has the most sales.
```SQL
Select 
	top 1 datename (weekday, Real_order_date) as Order_day, 
	customer_segment, 
	sum(Sales) Sales
from [Sales_Analysis].[dbo].[Sales_transaction]
Group by datename (weekday, Real_order_date), Customer_segment
order by Sales desc;
```
![alt text](C:\Users\omowu\OneDrive\Documents\GitHub\Sales-Analysis-with-SQL\images\6.jpg)

Saturday is the day of the week that corporate customer segment has the most sales.


- The company wants to determine its profitability by knowing the actual orders that were delivered.
```SQL
Select a.Order_status, sum(b.Profit) Profit
from [Sales_Analysis].[dbo].[Returned_items] a
inner join [Sales_Analysis].[dbo].[Sales_transaction] b
on a.order_id = b.order_id
where a.Order_status = 'Delivered'
group by a.Order_status;
```
![alt text](C:\Users\omowu\OneDrive\Documents\GitHub\Sales-Analysis-with-SQL\images\7.jpg)

The company got $2,560,886.130 profit from the orders that were delivered.


- The Organization is eager to know the customer names and persons born in 2011.
```SQL
Select First_Name, Last_Name, datepart (year, Birth_date) as Birth_year
from [Sales_Analysis].[dbo].[Sales_transaction]
where datepart (year, Birth_date) = 2011;
```
![alt text](C:\Users\omowu\OneDrive\Documents\GitHub\Sales-Analysis-with-SQL\images\8.jpg)

There is no customer born in the year 2011


- What are the aggregate orders made by all the customers?
```SQL
Select sum(Order_quantity) Total_order
from [Sales_Analysis].[dbo].[Sales_transaction];
```
![alt text](C:\Users\omowu\OneDrive\Documents\GitHub\Sales-Analysis-with-SQL\images\9.jpg)

A total of 214,777 orders were made by all customers.


- If the company intends to discontinue any product that brings in the least profit, what products should they consider?
```SQL
Select Top 4 Product_sub_category, sum(Profit) Profit
from [Sales_Analysis].[dbo].[Sales_transaction]
Group by Product_sub_category
Order by Profit;
```
![alt text](C:\Users\omowu\OneDrive\Documents\GitHub\Sales-Analysis-with-SQL\images\10.jpg)

Tables, Bookcases, Scissors, Rulers and Trimmers, and Rubber Bands have a negative profit total, and they should be considered for discontinuation.


- What are the top 2 best-selling items that the company should keep selling?
```SQL
Select Top 2 Product_sub_category, sum(Profit) Profit
from [Sales_Analysis].[dbo].[Sales_transaction]
Group by Product_sub_category
Order by Profit desc;
```
![alt text](C:\Users\omowu\OneDrive\Documents\GitHub\Sales-Analysis-with-SQL\images\11.jpg)

Telephones and Communication, and Office Machines are the 2 most profitable products with total profit of $316,951.620 and $307,712.930 respectively