# A Guide to SQL and Sequelize

This document provides an overview of SQL (Structured Query Language), common commands for working with relational databases like MySQL, and notes on using the Sequelize ORM in a Node.js application.

## 1. Introduction to SQL and Relational Databases

-   **SQL**: A standard language for managing and manipulating data in relational databases.
-   **RDBMS (Relational Database Management System)**: A program that allows you to create, update, and administer a relational database. Examples include MySQL, PostgreSQL, MS SQL Server, and Oracle.
-   **Database GUI**: A graphical user interface for interacting with your database (e.g., MySQL Workbench, DBeaver).

### 1.1. Core Concepts

-   **Table**: The primary data structure, organized into rows and columns (e.g., a `users` table).
-   **Row** (or Record/Tuple): A single entry in a table, representing one item (e.g., a specific user).
-   **Column** (or Field/Attribute): A specific piece of information for each row (e.g., `firstName`).
-   **Primary Key**: A column (or set of columns) that uniquely identifies each row in a table. Values must be unique and cannot be `NULL`.
-   **Foreign Key**: A key used to link two tables together. It's a field in one table that refers to the Primary Key in another table.
-   **Index**: A data structure that improves the speed of data retrieval operations on a database table at the cost of additional writes and storage space.

## 2. Working with MySQL

### 2.1. Installation and Setup

1.  **Download and Install**: Get the MySQL Community Server for your OS from the official website. During installation, you will set a password for the `root` user.
2.  **Verify Installation**: After installing, you can connect to the server via the command line.
    ```bash
    # Login as the root user; you will be prompted for your password
    mysql -u root -p
    ```
3.  **Create a Non-Root User**: It's best practice to create a dedicated user for your application instead of using `root`.

### 2.2. Common MySQL Commands

Once you are in the `mysql>` shell:
-   `SHOW DATABASES;`: List all databases on the server.
-   `CREATE DATABASE my_new_db;`: Create a new database.
-   `DROP DATABASE my_new_db;`: Delete a database.
-   `USE my_new_db;`: Select a database to work with.
-   `SELECT database();`: Show the currently selected database.
-   `SHOW TABLES;`: List all tables in the current database.
-   `DESCRIBE my_table;`: Show the column structure of a table.

## 3. Basic SQL Commands

### 3.1. DDL (Data Definition Language)

Used for defining and managing database structure.

**`CREATE TABLE`**: Defines a new table and its columns.
```sql
CREATE TABLE products (
    id INT NOT NULL AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    price DECIMAL(10, 2),
    submission_date DATE,
    PRIMARY KEY (id)
);
```
- **Column Properties**: `NOT NULL`, `AUTO_INCREMENT`, `UNIQUE`.

**`ALTER TABLE`**: Modifies an existing table.
```sql
-- Add a column
ALTER TABLE products ADD COLUMN in_stock BOOLEAN;

-- Drop a column
ALTER TABLE products DROP COLUMN in_stock;
```

**`DROP TABLE`**: Deletes a table.
```sql
DROP TABLE products;
```

### 3.2. DML (Data Manipulation Language)

Used for adding, retrieving, modifying, and deleting data.

**`INSERT INTO`**: Adds a new row to a table.
```sql
INSERT INTO products (name, price) VALUES ('Laptop', 999.99);
```

**`SELECT`**: Retrieves data from a table.
```sql
-- Select all columns from all rows
SELECT * FROM products;

-- Select specific columns
SELECT name, price FROM products;

-- Filter rows with a WHERE clause
SELECT * FROM products WHERE price > 500;

-- Select unique values
SELECT DISTINCT category FROM products;
```

**`UPDATE`**: Modifies existing rows.
```sql
-- WARNING: Always use a WHERE clause with UPDATE, or you will update ALL rows!
UPDATE products
SET price = 1099.99
WHERE name = 'Laptop';
```
- **Note on Safe Updates**: MySQL's "Safe Update Mode" may prevent `UPDATE` or `DELETE` statements without a `WHERE` clause that uses a key column. You can disable this for the session with `SET SQL_SAFE_UPDATES = 0;`.

**`DELETE FROM`**: Deletes rows.
```sql
-- WARNING: Always use a WHERE clause with DELETE!
DELETE FROM products WHERE id = 1;
```

## 4. Advanced Queries: JOINs

A `JOIN` clause is used to combine rows from two or more tables based on a related column between them.

**Example**: Imagine a `salespeople` table and a `customers` table, linked by a `city` column. To find which salespeople are in the same city as their customers:
```sql
SELECT
  s.name,    -- Select the salesperson's name
  c.cust_name  -- Select the customer's name
FROM
  salespeople AS s  -- From the salespeople table, aliased as 's'
JOIN
  customers AS c     -- Join with the customers table, aliased as 'c'
ON
  s.city = c.city;   -- The condition for joining the tables
```
- **Aliases (`AS`)**: Using aliases for table names (like `salespeople AS s`) makes queries shorter and more readable.

## 5. Using an ORM: Sequelize in Node.js

An **ORM (Object-Relational Mapper)** is a library that creates a "bridge" between object-oriented programming (like JavaScript) and a relational database (like MySQL). It lets you interact with your database using JavaScript objects and methods instead of writing raw SQL.

### 5.1. Example Project Structure

A typical Node.js project using Express and Sequelize is structured as follows:
-   **`server.js`**: The main entry point. Initializes the Express app and connects to the database.
-   **`/config`**: Contains database connection details (host, user, password).
-   **`/routes`**: Defines the API endpoints (e.g., `/api/products`). Maps endpoints to controller functions.
-   **`/controllers`**: Contains the application logic. Uses Sequelize models to perform CRUD operations.
-   **`/models`**:
    -   **`index.js`**: Sets up the Sequelize connection and collects all the models.
    -   **`product.model.js`**: Defines a Sequelize model, which corresponds to a table in the database.

### 5.2. Setting Up the Project

1.  **Install Dependencies**:
    ```bash
    npm install express sequelize mysql2 cors --save
    ```
    -   `express`: Web framework.
    -   `sequelize`: The ORM library.
    -   `mysql2`: The database driver for MySQL. Sequelize requires a separate driver for the specific database you are using.
    -   `cors`: Middleware to enable Cross-Origin Resource Sharing.

2.  **Define a Model (`/models/product.model.js`)**:
    ```javascript
    module.exports = (sequelize, DataTypes) => {
      const Product = sequelize.define("product", {
        title: {
          type: DataTypes.STRING
        },
        description: {
          type: DataTypes.STRING
        }
      });

      return Product;
    };
    ```

3.  **Implement a Controller (`/controllers/product.controller.js`)**:
    ```javascript
    const db = require("../models");
    const Product = db.products;

    // Create a new Product
    exports.create = (req, res) => {
      // ... logic to create a product using Product.create()
    };

    // Retrieve all Products
    exports.findAll = (req, res) => {
      // ... logic to find products using Product.findAll()
    };
    ```
This structure separates concerns, making the application easier to manage and scale.
