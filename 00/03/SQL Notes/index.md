# SQL Notes

## Create Database:  
Code Syntax: 
*CREATE SCHEMA databasename;

Sample Code: 
CREATE SCHEMA `fidelis` ;

Explanation: 
Creates database fidelis


View All Records

-- 1. To view all records
-- Syntax
-- SELECT [columns] FROM [table_name]employees
-- SELECT * FROM employees;




------- Creates Table

CREATE TABLE `lazada`.`products` (
)
ENGINE = InnoDB
COMMENT = 'Stores datasets for e-commerce'
PACK_KEYS = 1;

----------------------

-------Creates database tables

CREATE TABLE `lazada`.`products` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `name` VARCHAR(45) NULL,
  `description` TEXT NULL,
  `price` DECIMAL NULL,
  `seller` VARCHAR(100) NULL,
  `location` VARCHAR(100) NULL,
  `date_posted` DATETIME NULL DEFAULT NOW(),
  `productscol` VARCHAR(45) NULL,
  PRIMARY KEY (`id`))
ENGINE = InnoDB
COMMENT = 'Stores datasets for e-commerce'
PACK_KEYS = 1;

------------------

Activates database

USE `lazada`;



---Views all records:

SELECT * FROM products;

SELECT id, name FROM products;

-- ---
USE `lazada`;

-- Sets COLUMNS
INSERT INTO products
	(`name`,`description`,`price`,`seller`,`location`)
VALUES
	('iPhone XI','The best iPhone in the future', 88000.00, 'CDR-King', 'Cebu');
    
INSERT INTO products
	(`name`,`description`,`price`,`seller`,`location`)
VALUES
	('Mariod','The best smartphone in town', 50000.00, 'Masrstore', 'Baguio');
    
INSERT INTO products
	(`name`,`description`,`price`,`seller`,`location`)
VALUES
	('Samsung X','Korea NumbaWan', 800000.00, 'Samsung Store', 'Makati');

INSERT INTO products
	(`name`,`description`,`price`,`seller`,`location`)
VALUES
	('iPhone X','The best iPhone in the X', 80000.00, 'Octagon', 'Quezon');
    
INSERT INTO products
	(`name`,`description`,`price`,`seller`,`location`)
VALUES
	('Machintosh','The best lappy in town', 180000.00, 'Davao Store', 'Davao');
    
INSERT INTO products
	(`name`,`description`,`price`,`seller`,`location`)
VALUES
	('iPhone X Mac','The best iPhone in town', 80000.00, 'Kimstore', 'Manila');
    
INSERT INTO products
	(`name`,`description`,`price`,`seller`,`location`)
VALUES
	('Nokia','The number one in Asia', 84000.00, 'Nokia Store', 'Makati'),
	('Lex','Ohh My', 80000.00, 'Lex Store', 'Isabela'),
	('Lex II','Ohh yea', 80000.00, 'Lex Store', 'Dalawabela'),
	('iPhone X Mac','The best iPhone in town', 80000.00, 'Kimstore', 'Cebu'),
	('iPhone X Mac','The best iPhone in town', 80000.00, 'Kimstore', 'Manila');
	

-- Delete record(s)
-- Deadly code
-- DELETE FROM products; 

-- DELETE FROM products(specific); 
DELETE FROM products WHERE id=2; 

-- DELETE FROM products(multiple); 
DELETE FROM products WHERE id in (6,7); 

-- ---------------------------
-- Updates single products
-- UPDATE products 
-- SET price =70000, 
-- WHERE id=1;

-- Updates multiple records

-- UPDATE products
-- SET price =10000,date_posted=NOW();
-- WHERE id in (6,7); 

-- View All records
SELECT * FROM products;
-- SELECT * FROM products WHERE RANGE ;

-- Finds MAX price from products
SELECT id, name, MAX(price) from products;

-- Finds MIN price from products
SELECT id, name, MIN(price) from products;


-- Finds unique value and shows the records
SELECT DISTINCT(seller) from products;


SELECT * FROM products WHERE description LIKE '%<Value>%'; 

-- Sorting
-- Loads table
SELECT * FROM products ORDER BY price;
-- And or
SELECT * FROM products ORDER BY price ASC;

SELECT * FROM products ORDER BY price DESC; 

-- Loads view except


SELECT * FROM products WHERE location <> 'Manila' ORDER BY price DESC LIMIT 5; 

SELECT * FROM products WHERE location <> 'Manila' ORDER BY price DESC LIMIT 5 OFFSET 2; 

SELECT * FROM products WHERE date_posted >= '2018,-11-03 14:58.52'; 


-- Calculates price 
SELECT SUM(price) FROM products;

-- Calculates then updates the table name

SELECT AVG(price) / SUM(price)as 'Mean Score' FROM products;

SELECT AVG(price) as 'Total Average' FROM products;

-- SELECT * FROM products WHERE location 'Manila' LIMIT 2;

SELECT * FROM products;


# Quick SQL Cheatsheet

A quick reminder of all relevent SQL queries and examples on how to use them. 

# Table of Contents 
1. [ Finding Data Queries. ](#find)
2. [ Data Modification Queries. ](#modify)
3. [ Reporting Queries. ](#report)
4. [ Join Queries. ](#joins)

<a name="find"></a>
# 1. Finding Data Queries

### **SELECT**: used to select data from a database
* `SELECT` * `FROM` table_name;

### **DISTINCT**: filters away duplicate values and returns rows of specified column
* `SELECT DISTINCT` column_name;

### **WHERE**: used to filter records/rows
* `SELECT` column1, column2 `FROM` table_name `WHERE` condition;
* `SELECT` * `FROM` table_name `WHERE` condition1 `AND` condition2;
* `SELECT` * `FROM` table_name `WHERE` condition1 `OR` condition2;
* `SELECT` * `FROM` table_name `WHERE NOT` condition;
* `SELECT` * `FROM` table_name `WHERE` condition1 `AND` (condition2 `OR` condition3);

### **ORDER BY**: used to sort the result-set in ascending or descending order
* `SELECT` * `FROM` table_name `ORDER BY` column;
* `SELECT` * `FROM` table_name `ORDER BY` column `DESC`;
* `SELECT` * `FROM` table_name `ORDER BY` column1 `ASC`, column2 `DESC`;

### **SELECT TOP**: used to specify the number of records to return from top of table
* `SELECT TOP` number columns_names `FROM` table_name `WHERE` condition;
* `SELECT TOP` percent columns_names `FROM` table_name `WHERE` condition;
* Not all database systems support `SELECT TOP`. The MySQL equivalent is the `LIMIT` clause
* `SELECT` column_names `FROM` table_name `LIMIT` offset, count;

### **LIKE**: operator used in a WHERE clause to search for a specific pattern in a column
* % (percent sign) is a wildcard character that represents zero, one, or multiple characters
* _ (underscore) is a wildcard character that represents a single character
* `SELECT` column_names `FROM` table_name `WHERE` column_name `LIKE` pattern;
* `LIKE` ‘a%’ (find any values that starts with “a”)
* `LIKE` ‘%a’ (find any values that ends with “a”)
* `LIKE` ‘%or%’ (find any values that have “or” in any position)
* `LIKE` ‘_r%’ (find any values that have “r” in the second position)
* `LIKE` ‘a_%_%’ (find any values that start with “a” and are at least 3 characters in length)
* `LIKE` ‘[a-c]%’ (find any values starting with “a”, “b”, or “c”

### **IN**: operator that allows you to specify multiple values in a WHERE clause
* essentially the IN operator is shorthand for multiple OR conditions
* `SELECT` column_names `FROM` table_name `WHERE` column_name `IN` (value1, value2, …);
* `SELECT` column_names `FROM` table_name `WHERE` column_name `IN` (`SELECT STATEMENT`);

### **BETWEEN**: operator selects values within a given range inclusive
* `SELECT` column_names `FROM` table_name `WHERE` column_name `BETWEEN` value1 `AND` value2;
* `SELECT` * `FROM` Products `WHERE` (column_name `BETWEEN` value1 `AND` value2) `AND NOT` column_name2 `IN` (value3, value4);
* `SELECT` * `FROM` Products `WHERE` column_name `BETWEEN` #01/07/1999# AND #03/12/1999#;

### **NULL**: values in a field with no value
* `SELECT` * `FROM` table_name `WHERE` column_name `IS NULL`;
* `SELECT` * `FROM` table_name `WHERE` column_name `IS NOT NULL`;

### **AS**: aliases are used to assign a temporary name to a table or column
* `SELECT` column_name `AS` alias_name `FROM` table_name;
* `SELECT` column_name `FROM` table_name `AS` alias_name;
* `SELECT` column_name `AS` alias_name1, column_name2 `AS` alias_name2;
* `SELECT` column_name1, column_name2 + ‘, ‘ + column_name3 `AS` alias_name;

### **UNION**: operator used to combine the result-set of two or more SELECT statements
* Each SELECT statement winthin UNION must have the same number of columns
* The columns must have similar data types
* The columns in each SELECT statement must also be in the same order
* `SELECT` columns_names `FROM` table1 `UNION SELECT` column_name `FROM` table2;
* `UNION` operator only selects distinct values, `UNION ALL` will allow duplicates

### **GROUP BY**: statement often used with aggregate functions (COUNT, MAX, MIN, SUM, AVG) to group the result-set by one or more columns
* `SELECT` column_name1, COUNT(column_name2) `FROM` table_name `WHERE` condition `GROUP BY` column_name1 `ORDER BY` COUNT(column_name2) DESC;

### **HAVING**: this clause was added to SQL because the WHERE keyword could not be used with aggregated functions
* `SELECT` `COUNT`(column_name1), column_name2 `FROM` table `GROUP BY` column_name2 `HAVING` `COUNT(`column_name1`)` > 5;


<a name="modify"></a>
# 2. Data Modification Queries

### **INSERT INTO**: used to insert new records/rows in a table
* `INSERT INTO` table_name (column1, column2) `VALUES` (value1, value2);
* `INSERT INTO` table_name `VALUES` (value1, value2 …);

### **UPDATE**: used to modify the existing records in a table
* `UPDATE` table_name `SET` column1 = value1, column2 = value2 `WHERE` condition;
* `UPDATE` table_name `SET` column_name = value;

### **DELETE**: used to delete existing records/rows in a table
* `DELETE FROM` table_name `WHERE` condition;
* `DELETE` * `FROM` table_name;

<a name="report"></a>
# 3. Reporting Queries

### **COUNT**: returns the # of occurrences
* `SELECT COUNT (DISTINCT` column_name`)`;

### **MIN() AND MAX()**: returns the smallest/largest value of the selected column
* `SELECT MIN (`column_names`) FROM` table_name `WHERE` condition;
* `SELECT MAX (`column_names`) FROM` table_name `WHERE` condition;

### **AVG()**: returns the average value of a numeric column
* `SELECT AVG (`column_name`) FROM` table_name `WHERE` condition;

### **SUM()**: returns the total sum of a numeric column
* `SELECT SUM (`column_name`) FROM` table_name `WHERE` condition;

<a name="joins"></a>
# 4. Join Queries

###  **INNER JOIN**: returns records that have matching value in both tables
* `SELECT` column_names `FROM` table1 `INNER JOIN` table2 `ON` table1.column_name=table2.column_name;
* `SELECT` table1.column_name1, table2.column_name2, table3.column_name3 `FROM` ((table1 `INNER JOIN` table2 `ON` relationship) `INNER JOIN` table3 `ON` relationship);

### **LEFT (OUTER) JOIN**: returns all records from the left table (table1), and the matched records from the right table (table2)
* `SELECT` column_names `FROM` table1 `LEFT JOIN` table2 `ON` table1.column_name=table2.column_name;

### **RIGHT (OUTER) JOIN**: returns all records from the right table (table2), and the matched records from the left table (table1)
* `SELECT` column_names `FROM` table1 `RIGHT JOIN` table2 `ON` table1.column_name=table2.column_name;

### **FULL (OUTER) JOIN**: returns all records when there is a match in either left or right table
* `SELECT` column_names `FROM` table1 ``FULL OUTER JOIN`` table2 `ON` table1.column_name=table2.column_name;

### **Self JOIN**: a regular join, but the table is joined with itself
* `SELECT` column_names `FROM` table1 T1, table1 T2 `WHERE` condition;

