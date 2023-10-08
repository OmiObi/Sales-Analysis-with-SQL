# DATA AND TABLE CREATION

Data set for a Super Mart store was provide. 3 CSV files (Regional_Manager, Sales_Transaction and Returned_items) were provided. I created a database (Sales_Analysis) to store the data provided. Then, I created 3 tables (Regional_Manager, Sales_Transaction and Returned_items). Data from the CSV files provided were loaded and stored in the table using the bulk insert transact.

```SQL
---Create a database

Create database Sales_Analysis;


---Create Regional_manager table for this project.
Create table Regional_manager(
Region_Name varchar (50) primary key,
Manager varchar (30));

--Load the data into the table using Bulk insert transact
BULK INSERT Regional_manager 
FROM 'C:\Program Files\Microsoft SQL Server\MSSQL16.SQLEXPRESS\MSSQL\Backup\regional_manager.csv'
   WITH (
      Format = 'CSV',
	  FIRSTROW = 2,
	  FIELDTERMINATOR = ',',
      ROWTERMINATOR = '\n'
)
GO


---Create Sales_transaction table for this project.
create table Sales_transaction(
Sales_id integer primary key,
Order_id integer,
Real_order_date date,
Order_priority Varchar (30),
Order_quantity integer,
Sales decimal (8,3),
Discount decimal (8,3),
Ship_mode varchar (30),
Profit decimal (8,3),
Unit_profit decimal (8,3),
Shipping_cost decimal (8,3),
First_name varchar (30),
Last_name varchar (30),
Region Varchar (50),
Customer_segment varchar (40),
Product_category varchar (40),
Product_sub_category varchar (30),
Product_container varchar (40),
Ship_date date,
Birth_date date,
Foreign key (Region) references Regional_manager (Region_Name));

--Load the data into the table using Bulk insert transact
BULK INSERT Sales_transaction FROM 'C:\Program Files\Microsoft SQL Server\MSSQL16.SQLEXPRESS\MSSQL\Backup\sales_transaction.csv'
   WITH (
      Format = 'CSV',
	  FIRSTROW = 2,
	  FIELDTERMINATOR = ',',
      ROWTERMINATOR = '\n'
)
GO

---Create Returned_items table for this project.
create table Returned_items(
Returned_id integer primary key,
Order_id integer,
Sales_id integer,
Order_status varchar (30)
Foreign key (Sales_id) references Sales_transaction (Sales_id));

--Load the data into the table using Bulk insert transact
BULK INSERT Returned_items 
FROM 'C:\Program Files\Microsoft SQL Server\MSSQL16.SQLEXPRESS\MSSQL\Backup\returned_item.csv'
   WITH (
      Format = 'CSV',
	  FIRSTROW = 2,
	  FIELDTERMINATOR = ',',
      ROWTERMINATOR = '\n'
)
GO
```