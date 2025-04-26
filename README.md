# Gravity Bookstore Data Warehouse Project

## Project Overview

This project models and develops the **Gravity Bookstore** data warehouse.  
It transforms a transactional database into a normalized dimensional warehouse using a Snowflake Schema.

## Features

- Designed and built a Snowflake Schema data warehouse  
- Created tables, keys, and constraints  
- Developed a Date Dimension table  
- Prepared the foundation for ETL, OLAP, and BI solutions  

## Technologies

- Microsoft SQL Server  
- SQL Server Management Studio (SSMS)  

## Data Warehouse Design

### Approach

**Snowflake Schema**

### Why Snowflake Schema

- Reduces data redundancy  
- Improves data integrity  
- Saves storage space  
- Suits complex analytical queries  

### Main Tables

- **Fact Table**  
  - Sales Fact (combines `cust_order` and `order_line`)  

- **Dimension Tables**  
  - Book (linked to Publisher and Language)  
  - Author  
  - Customer (linked to Address → Country, Address Status)  
  - Shipping Method  
  - Order Status  
  - Date  

### ERD

- Available in the `/ERD` directory  
- Built based on normalized relationships  

### Integrity Constraints

- Enforced through Foreign Key relationships  
- SQL scripts created for consistency checks  

Example check:
```sql
SELECT *
FROM fact_sales
WHERE customer_id NOT IN (SELECT customer_id FROM dim_customer);
