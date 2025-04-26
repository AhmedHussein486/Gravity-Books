# Gravity Bookstore Data Warehouse Project

## Project Overview

This project models and develops the **Gravity Bookstore** data warehouse.  
It transforms a transactional database into a normalized dimensional warehouse using a Snowflake Schema.  
It includes data modeling, OLAP cube design, and is ready for BI reporting.

## Features

- Designed and built a Snowflake Schema data warehouse  
- Created tables, surrogate keys, and integrity constraints  
- Developed a Date Dimension table  
- Built a Tabular OLAP Cube using SSAS  
- Prepared the foundation for ETL using SSIS  
- Ready for Power BI or Excel analysis  

## Technologies

- Microsoft SQL Server  
- SQL Server Management Studio (SSMS)  
- SQL Server Integration Services (SSIS)  
- SQL Server Analysis Services (SSAS Tabular)  

## Data Sources

- SQL script files from the Gravity Bookstore dataset  
- Source:  
  [`sample_db_gravity`](https://github.com/bbrumm/databasestar/tree/main/sample_databases/sample_db_gravity/gravity_sqlserver)  
- Used to populate the transactional database `gravity_books`

## OLTP Tables

The original transactional database `gravity_books` contains:

- `address`  
- `address_status`  
- `author`  
- `book`  
- `book_author`  
- `book_language`  
- `country`  
- `cust_order`  
- `customer`  
- `customer_address`  
- `order_history`  
- `order_line`  
- `order_status`  
- `publisher`  
- `shipping_method`  

These tables follow a normalized OLTP design and were used as raw input for the warehouse model.

## Data Warehouse Tables

The dimensional warehouse `gravity_books_SnowFlake_DWH` contains:

- `Authors_Dim`  
- `Book_Author_Dim`  
- `Book_Dim`  
- `Cust_Dim`  
- `DimDate`  
- `Shipping_Dim`  
- `fact_Dim`  

The schema uses surrogate keys, and dimensions are modeled with historical tracking fields for SCD (e.g., `start_date`, `end_date`, `is_current`).

## Data Warehouse Design

### Approach

**Snowflake Schema**

### Why Snowflake Schema

- Reduces redundancy  
- Enforces data consistency  
- Suitable for historical tracking  
- Well-aligned with business reporting needs  

### Data Warehouse Model

The warehouse follows a normalized snowflake schema with surrogate keys and SCD fields.

Key facts:
- All dimensions link to the `fact_Dim` via surrogate keys  
- SCD Type 2 handled with `start_date`, `end_date`, `is_current`  
- Book and Author linked through a bridge (`Book_Author_Dim`)  

![DWH Schema](./ERD/dwh_model.png)

### Integrity Constraints

- All foreign key relationships are explicitly enforced  
- Scripts for data integrity checks are included  

Example:
```sql
SELECT *
FROM fact_Dim
WHERE book_sk NOT IN (SELECT book_sk FROM Book_Dim);
