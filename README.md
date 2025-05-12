# Apple Retail Sales SQL Project Analyzing Millions of Sales Rerords

![apple store](https://github.com/user-attachments/assets/d1bb9dcd-7789-4a74-822a-26ec61ff1433)

# 👋Introduction
  Welcome to my SQL-powered data analytics project focused on Apple Retail Sales and Warranty Insights.
  In this project, I explored a large-scale dataset comprising over 1 million records from Apple’s global retail operations. The goal was to solve business-critical questions using structured and optimized SQL 
  queries.

# 📊 What This Project Covers
  This project offers a comprehensive hands-on experience with SQL in a real-world retail context. Key areas of focus include :
  
  ✅ Practical application of advanced SQL concepts (JOINs, aggregations, window functions, subqueries)
  
  💼 Solving realistic business scenarios involving sales trends, product performance, and warranty behavior
  
  🧠 Structured query writing, optimization, and performance analysis using EXPLAIN ANALYZE

# 🚀 Project Overview
  This project demonstrates advanced SQL querying techniques by analyzing a comprehensive dataset of over 1 million records from Apple’s global retail operations. The dataset includes information on products, 
  stores, sales transactions, and warranty claims across multiple countries.
  By solving a wide range of business questions—from foundational queries to complex analytical tasks—this project highlights the ability to write structured, optimized SQL queries that uncover meaningful 
  insights from large-scale data.
  The project is ideal for data analysts looking to enhance their SQL skills by working with a large-scale dataset and solving real-world business questions.


# 🧩 Entity Relationship Diagram (ERD)

![schema](https://github.com/user-attachments/assets/9e98efae-5512-4da5-8b05-72d82bfb0d2e)


# 📊 Database Schema

This project is based on a retail analytics dataset consisting of five relational tables. Each table stores a specific component of the Apple retail ecosystem, including stores, products, sales transactions, and warranty claims.


### 1. 🏬 stores 
Contains information about Apple retail store locations.

 | Column Name | Description                        |
| ----------- | ---------------------------------- |
| store\_id   | Unique identifier for each store   |
| store\_name | Name of the store                  |
| city        | City where the store is located    |
| country     | Country where the store is located |


### 2. 🗂 category 
Holds information about product categories.
  | Column Name    | Description                         |
| -------------- | ----------------------------------- |
| category\_id   | Unique identifier for each category |
| category\_name | Name of the product category        |


### 3. 📱 products 
Stores details of Apple products available for sale.

  | Column Name   | Description                                    |
| ------------- | ---------------------------------------------- |
| product\_id   | Unique identifier for each product             |
| product\_name | Name of the product                            |
| category\_id  | Foreign key referencing category(category\_id) |
| launch\_date  | Date the product was launched                  |
| price         | Price of the product                           |

  
### 4. 💳 sales
Captures all product sales transactions.

  | Column Name | Description                                   |
| ----------- | --------------------------------------------- |
| sale\_id    | Unique identifier for each sale               |
| sale\_date  | Date of the sale                              |
| store\_id   | Foreign key referencing stores(store\_id)     |
| product\_id | Foreign key referencing products(product\_id) |
| quantity    | Number of units sold                          |


### 5. 🛠 warranty
| Column Name    | Description                                                       |
| -------------- | ----------------------------------------------------------------- |
| claim\_id      | Unique identifier for each warranty claim                         |
| claim\_date    | Date the warranty claim was filed                                 |
| sale\_id       | Foreign key referencing sales(sale\_id)                           |
| repair\_status | Status of the warranty claim (e.g., Paid Repaired, Warranty Void) |

# 🛠️ Database Setup
   The following SQL script creates the core database schema for the Apple Retail Sales & Warranty Analysis project. It includes table definitions, primary key constraints, and foreign key relationships.

-- DROP TABLE commands (to reset schema if re-run)
```sql 
   DROP TABLE IF EXISTS warranty;
   DROP TABLE IF EXISTS sales;
   DROP TABLE IF EXISTS products;
   DROP TABLE IF EXISTS category;
   DROP TABLE IF EXISTS stores;

-- CREATE TABLE: stores
CREATE TABLE stores (
    store_id VARCHAR(5) PRIMARY KEY,
    store_name VARCHAR(30),
    city VARCHAR(25),
    country VARCHAR(25)
);

-- CREATE TABLE: category
CREATE TABLE category (
    category_id VARCHAR(10) PRIMARY KEY,
    category_name VARCHAR(20)
);

-- CREATE TABLE: products
CREATE TABLE products (
    product_id VARCHAR(10) PRIMARY KEY,
    product_name VARCHAR(35),
    category_id VARCHAR(10),
    launch_date DATE,
    price FLOAT,
    CONSTRAINT fk_category FOREIGN KEY (category_id) REFERENCES category (category_id)
);

-- CREATE TABLE: sales
CREATE TABLE sales (
    sale_id VARCHAR(15) PRIMARY KEY,
    sale_date DATE,
    store_id VARCHAR(10),
    product_id VARCHAR(10),
    quantity INT,
    CONSTRAINT fk_store FOREIGN KEY (store_id) REFERENCES stores (store_id),
    CONSTRAINT fk_product FOREIGN KEY (product_id) REFERENCES products (product_id)
);

-- CREATE TABLE: warranty
CREATE TABLE warranty (
    claim_id VARCHAR(10) PRIMARY KEY,
    claim_date DATE,
    sale_id VARCHAR(15),
    repair_status VARCHAR(15),
    CONSTRAINT fk_sale FOREIGN KEY (sale_id) REFERENCES sales (sale_id)
);

-- Success Message
SELECT 'Schema Created Successful' AS Success_Message;




