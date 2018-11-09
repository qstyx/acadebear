###Begin

Create Database:
Code Syntax: 
CREATE SCHEMA (databasename) ;

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
