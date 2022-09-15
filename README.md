# 
## automation import
```bat
SQLCMD -S CP -d automation -E -Q "DROP TABLE customer_hist;"
SQLCMD -S CP -d automation -E -Q "SELECT * INTO customer_hist FROM customer_temp;"
SQLCMD -S CP -d automation -E -Q "DROP TABLE order_temp;"
SQLCMD -S CP -d automation -E -Q "DROP TABLE order_new;"
SQLCMD -S CP -d automation -E -Q "DROP TABLE customer_temp;"
```

```sql
CREATE TABLE
  order_temp
  (
      row_id
          VARCHAR(50), 
      order_id
          VARCHAR(50), 
      order_date
          VARCHAR(50), 
      ship_date
          VARCHAR(50),
      ship_mode
          VARCHAR(50), 
      customer_id
          VARCHAR(50),
      country_region
          VARCHAR(50), 
      postal_code
          VARCHAR(50), 
      region
          VARCHAR(50), 
      product_id
          VARCHAR(50),
      categoty
          VARCHAR(50),
      sub_category
          VARCHAR(50),
      product_name
          VARCHAR(MAX),
      sales
          VARCHAR(50),
      quantity
          VARCHAR(50),
      discount
          VARCHAR(50),
      profit
          VARCHAR(50)
  )
  GO
  
BULK INSERT automation.dbo.order_temp FROM 'C:\...\order_temp.csv'
WITH (
    FIELDTERMINATOR = ',',
    ROWTERMINATOR = '\n',
    FIRSTROW=2
);
GO
```
#### `.bat` automation import `.csv` & `create table order new` & `create table customer hist` in sql server
```bat
--drop all table & create table customer hist
SQLCMD -S CP -d automation -E -Q "DROP TABLE customer_hist;"
SQLCMD -S CP -d automation -E -Q "SELECT * INTO customer_hist FROM customer_temp;"
SQLCMD -S CP -d automation -E -Q "DROP TABLE order_temp;"
SQLCMD -S CP -d automation -E -Q "DROP TABLE order_new;"
SQLCMD -S CP -d automation -E -Q "DROP TABLE customer_temp;"
SQLCMD -S CP -d automation -E -Q "DROP TABLE customer_new;"

SQLCMD -S CP -d automation -E -Q "CREATE TABLE order_temp (row_id VARCHAR(50), order_id VARCHAR(50), order_date VARCHAR(50), ship_date VARCHAR(50), ship_mode VARCHAR(50), customer_id VARCHAR(50), country_region VARCHAR(50), postal_code VARCHAR(50), region VARCHAR(50), product_id VARCHAR(50), category VARCHAR(50), sub_category VARCHAR(50), product_name VARCHAR(MAX), sales VARCHAR(50), quantity VARCHAR(50), discount VARCHAR(50), profit VARCHAR(50)); BULK INSERT automation.dbo.order_temp FROM 'C:\...\order_temp.csv' WITH (FIELDTERMINATOR = ',', ROWTERMINATOR = '\n', FIRSTROW = 2);"

--create table order new
SQLCMD -S CP -d automation -E -Q "SELECT * INTO order_new FROM order_temp WHERE CONVERT(DATE, order_date) = CONVERT(DATE, GETDATE());"

--
SQLCMD -S CP -d automation -E -Q "CREATE TABLE customer_temp (customer_id VARCHAR(50), customer_name VARCHAR(50), segment VARCHAR(50), city VARCHAR(50), state VARCHAR(50)); BULK INSERT automation.dbo.customer_temp FROM 'C:\...\customer_temp.csv' WITH (FIELDTERMINATOR = ',', ROWTERMINATOR = '\n', FIRSTROW = 2);"
```
## automation export

![automation](https://user-images.githubusercontent.com/108328139/190431446-7d79e111-62cd-4b60-a729-d30b557a5b07.png)
[Power BI](https://app.powerbi.com/view?r=eyJrIjoiZDg0NTIxYTYtZjdmZS00ZGU0LThjYTYtNmIzYWVkMWFlYzNiIiwidCI6ImFmZjljYzU2LTVkYzAtNGMyZS1iNTlmLTZkY2JkMzI1NzM3YiIsImMiOjEwfQ%3D%3D&pageName=ReportSection)
