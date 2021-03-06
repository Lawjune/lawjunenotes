# 1. Getting Started

## 1.1  What is SQL?

A **DATABASE** 
is a collection of data stored in a format
that can easily be accessed.

**DBMS**: Database Management System

**RELATIONAL DATABASE**
[customers] - [Orders] - [Products] 

**RDBMS**
- MySQL
- SQL Server
- Oracle

**NoSQL** systems don't understand SQL

## 1.2 Creating Database

## 1.3 What You'll Learn

- Retrieving Data
- Inserting Data
- Updating Data
- Deleting Data

- Summarizing Data
- Writing Complex Queries
- Built-in Functions
- Views
- Stored Procedures

- Triggers
- Events
- Transactions
- Concurrency

- Desiging Databases
- Indexing for High Performance
- Securing Databases


# 2 Retrieving Data From a Single Table 

## 2.1 The SELECT Statement

```sql
USE sql_store;

SELECT *
FROM customers
-- WHERE customer_id = 1
-- ORDER BY first_name
```

## 2.2 The SELECT Clause

```sql
SELECT 
	last_name, 
    first_name, 
    points, 
    (points + 10) * 100 AS 'dicount_factor'
FROM customers
```

```sql
SELECT name, unit_price, unit_price*1.1 AS 'new_price' FROM sql_store.products;
```

## 2.3 The WHERE Clause

```sql
SELECT *
FROM customers
WHERE points > 3000
```

```sql
SELECT *
FROM customers
-- WHERE state != 'VA'
-- WHERE state <> 'VA'
WHERE birth_date > '1990-01-01'
```

**Exercise:**
*Get the orders placed this year (2019)*
```sql
SELECT *
FROM orders
WHERE order_date > '2019-01-01'
```

## 2.4 The AND, OR and NOT Operators

## 2.5 The IN Operator

```sql
SELECT *
FROM customers
WHERE state NOT IN ('VA', 'GA', 'FL')
```

## 2.6 The BETWEEN Operator

```sql
SELECT *
FROM customers
WHERE points BETWEEN 1000 AND 3000
```

## 2.7 The LIKE Operator

```sql
SELECT *
FROM customers
-- WHERE last_name LIKE 'b%'
-- WHERE last_name LIKE '%b%'
WHERE last_name LIKE 'b____y'
```

% any number of characters
_ single character


**Exercise:**
*Get the customres whose*
    *addresses contain TRAIL or AVENUE*
    *phone numbers end with 9*
```sql
SELECT *
FROM customers
WHERE (address LIKE '%trail%' OR address LIKE 'AVENUE')
    AND phone LIKE '%9'
```

## 2.8 The REGEXP Operator

```sql
SELECT *
FROM customers
-- WHERE last_name LIKE '%field%'
-- WHERE last_name REGEXP '^field|mac|rose'
WHERE last_name REGEXP 'field$|mac|rose'
```

```sql
WHERE last_name REGEXP '[gim]e'
-- ge
-- ie
-- me
```

```regexp
^ beginning
$ end
| logical or
[abcd]
[a-f]
```

**Exercise:**
*Get the customres whose*
    *first names are ELKA or AMBUR*
    *last names end with EY or ON*
    *last names start with MY or contains SE*
    *last names contain B followed by R or U*
```sql
WHERE first_name REGEXP 'ELKA|AMBUR'
WHERE last_name REGEXP 'EY$|ON$'
WHERE last_name REGEXP '^MY|SE'
WHERE last_name REGEXP 'B[RU]'
```

## 2.9 The IS NULL Operator

```sql
SELECT *
FROM customers
WHERE phone IS NOT NULL
```

## 2.10 The ORDER BY Clause

```sql
SELECT first_name, last_name, 10 AS points
FROM customers
ORDER BY state DESC, birth_date DESC
```

## The 2.11 LIMIT Clause

```sql
SELECT *
FROM customers
LIMIT 6, 3 -- skip 6 records and pick 3 records
-- page 1: 1 - 3
-- page 2: 4 - 6
-- page 3: 7 - 9
```

**Exercise:**
*Get the top three loyal customers*
```sql
SELECT *
FROM customers
ORDER BY points DESC
LIMIT 3
```

# 3 Retrieving Data From Multiple Tables

## 3.1 Inner Joins

```sql
SELECT order_id, o.product_id, quantity, o.unit_price, name
FROM sql_store.order_items o 
INNER JOIN sql_store.products p 
    ON o.product_id = p.product_id
    ORDER BY o.quantity DESC
```

**Exercise:**
```sql
SELECT * FROM sql_store.order_items o 
INNER JOIN sql_store.products p 
    ON o.product_id = p.product_id
    ORDER BY o.quantity DESC
```


## 3.2 Joinning Across Databases

```sql
USE sql_store;

SELECT * 
FROM order_items oi
JOIN sql_inventory.products p
	ON oi.product_id = p.product_id
```

## 3.3 Self Joins

```sql
USE sql_hr;

SELECT 
	e.employee_id,
    e.first_name,
    m.first_name AS manager
FROM employees e
JOIN employees m
	ON e.reports_to = m.employee_id
``` 


## 3.4 Joining Multiple Tables

```sql
USE sql_store;

SELECT 
	o.order_id,
    o.order_date,
    c.first_name,
    c.last_name,
    os.name AS status
FROM orders o
JOIN customers c
	ON o.customer_id = c.customer_id
JOIN order_statuses os
	ON o.status = os.order_status_id
```

**Exercise:**
```sql
USE sql_invoicing;

SELECT 
	p.date,
    p.invoice_id,
    p.amount,
    c.name,
    pm.name AS 'payment_method'
FROM payments p
JOIN clients c
	ON p.client_id = c.client_id
JOIN payment_methods pm
	ON p.payment_method = pm.payment_method_id
```

## 3.5 Compound Join Conditions

```sql
USE sql_store;

SELECT *
FROM order_items oi
JOIN order_item_notes oin
	ON oi.order_id = oin.order_id
    AND oi.product_id = oin.product_id
```

## 3.6 Implict Join Syntax

```sql
USE sql_store;

-- SELECT *
-- FROM orders o
-- JOIN customers c
-- 	ON o.customer_id = c.customer_id
    
-- Implicit Join Syntax
SELECT *
FROM orders o, customers c
WHERE o.customer_id = c.customer_id
```

## 3.7 Outer Joins

```sql
USE sql_store;

SELECT 
    c.customer_id, 
    c.first_name, 
    c.last_name,
    o.order_id
FROM customers c
LEFT JOIN orders o
    ON c.customer_id = o.customer_id
ORDER BY c.customer_id
```

## 3.8 Outer Join Between Multiple Tables

```sql
USE sql_store;

SELECT 
    c.customer_id, 
    c.first_name, 
    c.last_name,
    o.order_id,
    sh.name AS shipper
FROM customers c
LEFT JOIN orders o
    ON c.customer_id = o.customer_id
LEFT JOIN shippers sh
    ON o.shipper_id = sh.shipper_id
ORDER BY c.customer_id
```

**Exercise:**
```sql
USE sql_store;

SELECT p.product_id, p.name, oi.quantity
FROM products p
LEFT JOIN order_items oi
ON
    p.product_id = oi.product_id
```

## 3.9 Self Outer Joins

```sql
USE sql_hr;

SELECT 
    e.employee_id,
    e.first_name,
    m.first_name AS manager
FROM employees e
LEFT JOIN employees m
    ON e.reports_to = m.employee_id
```

## 3.10 The USING Clause

```sql
USE sql_store;

SELECT 
    c.customer_id, 
    c.first_name, 
    c.last_name,
    o.order_id,
    sh.shipper_id AS shipper
FROM customers c
LEFT JOIN orders o
    -- ON c.customer_id = o.customer_id
    USING (customer_id)
LEFT JOIN shippers sh
    USING (shipper_id)
```

```sql
USE sql_store;

SELECT *
FROM order_items oi
JOIN order_item_notes oin
    USING (order_id, product_id)
```

**Exercise:**
```sql
USE sql_invoicing;

SELECT 
    p.date,
    c.name AS client,
    p.amount,
    pm.name AS payment_method

FROM payments p
JOIN clients c USING (client_id)
JOIN payment_methods pm
    ON p.payment_method = pm.payment_method_id
```

## 3.11 Natural Joins

***DISCOURAGE TO USE THEM***


## 3.12 Cross Join

```sql
USE sql_store;

SELECT 
    c.first_name AS customer,
    p.name AS product
FROM customers c
CROSS JOIN products p
ORDER BY c.first_name
```

**Excercise:**
*Do a cross join between shippers and products*
    *using the implict syntax*
    *and then using the explicit syntax*

```sql
USE sql_store;

SELECT *
FROM shippers, products
```

```sql
USE sql_store;

SELECT *
FROM shippers
CROSS JOIN products
```

## 3.13 Unions

```sql
USE sql_store;

SELECT 
    order_id,
    order_date,
    'Active' AS status
FROM orders
WHERE order_date >= '2019-01-01'
UNION
SELECT 
    order_id,
    order_date,
    'Archived' AS status
FROM orders
WHERE order_date < '2019-01-01'
```

```sql
USE sql_store;

SELECT first_name
FROM customers
UNION
SELECT name
FROM shippers
```

**Exercise:**
```sql
USE sql_store;

SELECT 
    customer_id,
    first_name,
    points,
    'Bronze' AS type
FROM customers
WHERE points < 2000
UNION
SELECT 
    customer_id,
    first_name,
    points,
    'Silver' AS type
FROM customers
WHERE points BETWEEN 2000 AND 3000
UNION
SELECT 
    customer_id,
    first_name,
    points,
    'Gold' AS type
FROM customers
WHERE points BETWEEN > 000
ORDER BY first_name
```

# 4 Inserting, Updating, and Deleting Data

## 4.1 Column Attributes

## 4.2 Inserting a Single Row

```sql
INSERT INTO customers 
VALUES (
    DEFAULT, 
    'John', 
    'Smith', 
    '1990-01-01', 
    NULL,
    'address',
    'city',
    'CA'
    DEFAULT
    )
```

```sql
INSERT INTO customers (
    first_name,
    last_name,
    birth_date,
    address,
    city,
    state
    )
VALUES (
--  DEFAULT, 
    'John', 
    'Smith', 
    '1990-01-01', 
--     NULL,
    'address',
    'city',
    'CA'
--     DEFAULT
    )
```

## 4.3 Inserting Multiple Rows

```sql
INSERT INTO shippers (name)
VALUES 
    ('Shipper1'), 
    ('Shipper2'),
    ('Shipper3')
```

**Exercise:**
*Insert three rows in the products table*

```sql
USE sql_store;

INSERT INTO products 
VALUES 
    (DEFAULT, 'product_1', 1, 1.0), 
    (DEFAULT, 'product_2', 2, 2.0),
    (DEFAULT, 'product_3', 3, 3.0)
```

## 4.4 Inserting Hierarchical Rows

*Each order in orders table has several order_items.*
*Or orders table is the parent of order_items table.*


*Use to **LAST_INSERT_ID()** function*
```sql
INSERT INTO orders (
    customer_id,
    order_date,
    status
    )
VALUES (
    1, '2019-01-02', 1
    );
SELECT LAST_INSERT_ID()
```


```sql
INSERT INTO orders (
    customer_id,
    order_date,
    status
    )
VALUES (
    1, '2019-01-02', 1
    );
    
INSERT INTO order_items 
VALUES 
    (LAST_INSERT_ID(), 1, 1, 2.95),
    (LAST_INSERT_ID(), 2, 1, 3.95)
```

## 4.5 Creating a Copy of A Table

```sql
CREATE TABLE orders_archived  AS
SELECT * 
FROM orders
WHERE order_date < '2019-01-01'
```
***We don't have the `Primary Key` on orders_archived table!***

*Use `Truncate Table` to delete all of the data on rders_archived table*
```sql
INSERT INTO orders_archived
SELECT * 
FROM orders
WHERE order_date < '2019-01-01'
```

**Exercise:**
```sql
USE sql_invoicing;

CREATE TABLE invoices_archived AS
SELECT *
FROM invoices i
JOIN clients c USING (client_id)
WHERE payment_date IS NOT NULL
```

## 4.6 Updating a Single Row

```sql
UPDATE invoices
SET 
    payment_total = 10, 
    payment_date = '2019-03-01'
WHERE invoice_id = 1
```

```sql
USE sql_invoicing;

UPDATE invoices
SET 
    payment_total = DEFAULT, 
    payment_date = DEFAULT
WHERE invoice_id = 1
```

```sql
UPDATE invoices
SET 
    payment_total = invoice_total * 0.5, 
    payment_date = due_date
WHERE invoice_id = 3
```


## 4.7 Updating Multiple Rows

*Disable the SQL-Workbench `Safe Updates` function in Edit->Preferences->SQL Editor.*
```sql
UPDATE invoices
SET 
    payment_total = invoice_total * 0.5, 
    payment_date = due_date
WHERE invoice_id IN (3, 4)
```

*Write a SQL statement to*
    *give any customers born before 1990*
    *50 extra points*
```sql
USE sql_store;

UPDATE customers
SET points = points + 50
WHERE birth_date < '1990-01-01'
```

## 4.8 Using Subqueries in Updates

```sql
use sql_invoicing;

UPDATE invoices
SET 
    payment_total = invoice_total * 0.5, 
    payment_date = due_date
WHERE client_id = 
        (SELECT client_id 
        FROM clients
        WHERE name = "Myworks")
```

```sql
use sql_invoicing;

UPDATE invoices
SET 
    payment_total = invoice_total * 0.5, 
    payment_date = due_date
WHERE client_id IN
        (SELECT client_id 
        FROM clients
        WHERE state IN ('CA', 'NY'))
```

**Exercise:**
```sql
USE sql_store;

UPDATE orders
SET comments = 'Gold customer'
WHERE customer_id IN 
    (SELECT customer_id
    FROM customers
    WHERE points > 3000)
```

## 4.9 Deleting Rows

```sql
USE sql_invoicing;

DELETE FROM invoices
WHERE client_id = 
    (SELECT *
    FROM cilents
    WHERE name = 'Myworks')
```

## 4.10 Restoring the Databases


# 5 Summarizing Data

## 5.1 Aggregate Functions

```sql
MAX()
MIN()
AVG()
SUM()
COUNT()
```

```sql
USE sql_invoicing;

SELECT 
    MAX(invoice_total) AS highest,
    MIN(invoice_total) AS lowest,
    AVG(invoice_total) AS average,
    SUM(invoice_total) AS total,
    COUNT(invoice_total * 1.1) AS number_of_invoices,
    COUNT(payment_date) AS count_of_payments,
    COUNT(DISTINCT client_id) AS total_clients,
    COUNT(*) AS total_records
FROM invoices
WHERE invoice_date > '2019-07-01'
```

**Exercise:**
```sql
USE sql_invoicing;

SELECT 
    'First half of 2019' AS date_range,
    SUM(invoice_total) AS total_sales,
    SUM(payment_total) AS total_payments,
    SUM(invoice_total - payment_total) AS what_we_expect
FROM invoices
WHERE invoice_date
    BETWEEN '2019-01-01' AND '2019-06-30'
UNION
SELECT 
    'Second half of 2019' AS date_range,
    SUM(invoice_total) AS total_sales,
    SUM(payment_total) AS total_payments,
    SUM(invoice_total - payment_total) AS what_we_expect
FROM invoices
WHERE invoice_date
    BETWEEN '2019-07-01' AND '2019-12-31'
UNION
SELECT 
    'Total' AS date_range,
    SUM(invoice_total) AS total_sales,
    SUM(payment_total) AS total_payments,
    SUM(invoice_total - payment_total) AS what_we_expect
FROM invoices
WHERE invoice_date
    BETWEEN '2019-01-01' AND '2019-12-31'
```

## 5.2 The GROUP BY Clause

```sql
SELECT
    client_id,
    SUM(invoice_total) AS total_sales
FROM invoices
WHERE invoice_date >= '2019-07-01'
GROUP BY client_id
ORDER BY total_sales DESC
```

```sql
SELECT
    state,
    city,
    SUM(invoice_total) AS total_sales
FROM invoices i
JOIN clients USING (client_id)
GROUP BY state, city
ORDER BY total_sales DESC
```

**Exercise:**
```sql
SELECT 
    date,
    pm.name AS payment_method,
    SUM(amount) AS total_payments
FROM payments p
JOIN payment_methods pm
    ON p.payment_method = pm.payment_method_id
GROUP BY date, payment_method
ORDER BY date
```

## 5.3 The HAVING Clause

```sql
SELECT
    client_id,
    SUM(invoice_total) AS total_sales,
    COUNT(*) AS number_of_invoices
FROM invoices
GROUP BY client_id
HAVING 
    total_sales > 500 AND 
    number_of_invoices > 5
```

**Exercise:**
*-- Get the customers*
*--     located in Virginia*
*--     who have spent more than $100*

```sql
USE sql_store;

SELECT 
    c.customer_id,
    c.first_name,
    c.last_name,
    SUM(oi.quantity * oi.unit_price) AS total_sales
FROM customers c
JOIN orders o USING (customer_id)
JOIN order_items oi USING (order_id)
WHERE state = 'VA'
GROUP BY 
    c.customer_id,
    c.first_name,
    c.last_name
HAVING total_sales > 100
```

## 5.4 The ROLLUP Operator

```sql
use sql_invoicing;

SELECT
    state,
    city,
    SUM(invoice_total) AS total_sales
FROM invoices i 
JOIN clients c USING (client_id)
GROUP BY state, city WITH ROLLUP
```

**Exercise:**
```sql
use sql_invoicing;

SELECT 
    pm.name AS payment_method,
    SUM(amount) AS total
FROM payments p
JOIN payment_methods pm
    ON p.payment_method = pm.payment_method_id
-- GROUP BY payment_method WITH ROLLUP
GROUP BY pm.name WITH ROLLUP
```


# 6 Writing Complex Query 


## Subqueries

Find products that are more expensive than Lettuce (id=3)
```sql
SELECT *
FROM products
WHERE unit_price > (
    SELECT unit_price
    from products
    WHERE product_id = 3
)
```

In sql_hr db, find employees whose earn more than average
```sql
USE sql_hr;

SELECT 
    employee_id,
    first_name,
    last_name,
    salary
FROM employees
WHERE salary > (
SELECT AVG(salary)
FROM employees
)
ORDER BY salary DESC
```

## The IN Operator

Find the products that never been order
```sql
USE sql_store;

SELECT *
FROM products
WHERE product_id NOT IN (
SELECT DISTINCT product_id
from order_items
)
```

Find clients without invoices
```sql
USE sql_invoicing;

SELECT *
FROM clients
WHERE client_id NOT IN (
SELECT DISTINCT client_id
FROM invoices
)
```

## Subqueries vs Joins

```sql
USE sql_invoicing;

SELECT *
FROM clients
LEFT JOIN invoices USING (client_id)
WHERE invoice_id IS NULL
```

Find customers who have ordered lettuce ( id = 3 ) 
Select customer_id, first_name, last_name
```sql
USE sql_store;

SELECT DISTINCT
    customer_id,
    first_name,
    last_name
FROM customers c
LEFT JOIN orders USING (customer_id)
LEFT JOIN order_items USING (order_id)
LEFT JOIN products USING (product_id)
WHERE product_id = 3
```

## The ALL Keyword

Select invoices larger than all invoices of client 3 
```sql
USE sql_invoicing;

SELECT *
FROM invoices
WHERE invoice_total > (
    SELECT MAX(invoice_total)
    FROM invoices
    WHERE client_id = 3
)
```

```sql
USE sql_invoicing;

SELECT *
FROM invoices
WHERE invoice_total > ALL (
    SELECT invoice_total
    FROM invoices
    WHERE client_id = 3
)
```

## The ANY Keyword

Select client with at least two invoices
```sql
USE sql_invoicing;

SELECT *
FROM clients
WHERE client_id IN (
    SELECT client_id
    FROM invoices
    GROUP BY client_id
    HAVING COUNT(*) >= 2
)
```

```sql
USE sql_invoicing;

SELECT *
FROM clients
WHERE client_id = ANY (
    SELECT client_id
    FROM invoices
    GROUP BY client_id
    HAVING COUNT(*) >= 2
)
```

## The Correlated Subqueries 

Select employees whose salary is above the average in their office

```pseudo
for each employee
    calculate the avg salary for employee.office
    return the employee if salary > avg
```

```sql
USE sql_hr;

SELECT *
FROM employees e
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
    WHERE office_id = e.office_id
)
```

Get invoices that are larger than the client's average invoice amount
```sql
USE sql_invoicing;

SELECT *
FROM invoices i
WHERE invoice_total > (
    SELECT AVG(invoice_total)
    FROM invoices
    WHERE client_id = i.client_id
)
```

## The EXISTS Operator

Select clients that have an invoice
```sql
USE sql_invoicing;

SELECT *
FROM clients
WHERE client_id IN (
    SELECT DISTINCT client_id
    FROM invoices
)
```

```sql
USE sql_invoicing;

SELECT *
FROM clients c
-- return True
WHERE EXISTS ( 
    SELECT client_id
    FROM invoices
    WHERE client_id = c.client_id
)
```

Find the products that have never been ordered
```sql
USE sql_store;

SELECT *
FROM products p
WHERE EXISTS (
    SELECT product_id
    FROM order_items
    WHERE product_id = p.product_id
)
```

## Subqueries in the SELECT Clause

```sql
USE sql_invoicing;

SELECT 
    invoice_id,
    invoice_total,
    (SELECT AVG(invoice_total)
        FROM invoices) AS invoice_average,
    invoice_total - (SELECT invoice_average) AS difference
FROM invoices
```

```sql
USE sql_invoicing;

SELECT 
    client_id,
    name,
    (SELECT SUM(invoice_total) 
        FROM invoices
        WHERE client_id = c.client_id) AS total_sales,
    (SELECT AVG(invoice_total) FROM invoices) AS average,
    (SELECT total_sales) - (SELECT average) AS differences
FROM clients c
```

## Subqueries in the FROM Clause

```sql
USE sql_invoicing;

SELECT *
FROM (
    SELECT 
        client_id,
        name,
        (SELECT SUM(invoice_total) 
            FROM invoices
            WHERE client_id = c.client_id) AS total_sales,
        (SELECT AVG(invoice_total) FROM invoices) AS average,
        (SELECT total_sales) - (SELECT average) AS differences
    FROM clients c
) AS sales_summary
WHERE total_sales IS NOT NULL
```


# 7 Essential MySQL Functions

## Numeric Functions

```sql
SELECT ROUND(5.7345, 2) -- 5.73
SELECT TRUNCATE(5.7345, 2) -- 5.73
SELECT CEILING(5.2) -- 6
SELECT FLOOR(5.2) -- 5
SELECT ABS(-5.2) -- 5.2
SELECT RAND() -- random(0, 1)
```

Google "mysql numeric functions"

## String Functions

```sql
SELECT LENGTH('sky') -- 3
SELECT UPPER('sky') -- SKY
SELECT LOWER('SKy') -- sky
SELECT LTRIM('     Sky') -- 'Sky'
SELECT RTRIM('Sky    ') -- 'Sky'
SELECT TRIM('   Sky   ') -- 'Sky'
SELECT LEFT('Kindergarten', 4) -- 'Kind'
SELECT RIGHT('Kindergarten', 6) -- 'garten'
SELECT SUBSTRING('Kindergarten', 3, 5) -- 'nderg'
SELECT LOCATE('n','Kindergarten') -- 3
SELECT LOCATE('1','Kindergarten') -- 0 //mysql
SELECT LOCATE('garten','Kindergarten') -- 7
SELECT REPLACE('Kindergarten','garten', 'garden') -- 'Kindergarden'
SELECT CONCAT('first','last') -- firstlast
``` 

```sql
USE sql_store;

SELECT 
    CONCAT(first_name, ' ', last_name) AS full_name
FROM customers
```

Google "mysql string functions"

## Date Functions in MySQL

```sql
SELECT NOW() -- 2021-07-20 07:44:11

SELECT NOW(), CURDATE(), CURTIME()

SELECT YEAR(NOW()), MONTH(NOW()), DAY(NOW)

SELECT DAYNMAE(NOW) -- Tuesday
SELECT MONTHNAME(NOW()) -- July

SELECT EXTRACT(DAY FROM NOW()) -- 20
SELECT EXTRACT(YEAR FROM NOW()) -- 2021
```

```sql
USE sql_store;

SELECT *
FROM orders
WHERE YEAR(order_date) = (YEAR(NOW()) - 4)
```

## Formatting Dates and Times

```sql
SELECT DATE_FORMAT(NOW(), '%D %M %Y') -- 20th July 2021
SELECT DATE_FORMAT(NOW(), '%M %d %Y') -- July 20 2021
```

Google "mysql date format string"

```sql
SELECT TIME_FORMAT(NOW(), '%H:%i %p') -- 08:03 AM
```

## Calculating Dates and Times
```sql
SELECT DATE_ADD(NOW(), INTERVAL 1 YEAR)

SELECT DATEDIFF('2021-07-20', '2016-01-25')

SELECT TIME_TO_SEC('09:00') - TIME_TO_SEC('09:02')
```

## The IFNULL and COALESCE Functions

```sql
USE sql_store;

SELECT 
    order_id,
    IFNULL(shipper_id, 'Not assigned') AS shipper
FROM orders
```

```sql
USE sql_store;

SELECT 
    order_id,
    IFNULL(shipper_id, '...'),
    COALESCE(shipper_id, comments, 'Not assigned') AS shipper
FROM orders
```

```sql
USE sql_store;

SELECT 
    CONCAT(first_name, ' ', last_name) AS customer,
    COALESCE(phone, 'Unknown') AS phone
FROM customers
```

## The IF Function

```sql
USE sql_store;

SELECT
    order_id,
    order_date,
    IF(YEAR(order_date) = YEAR(NOW())-2, 
        'Active', 'Archived') AS category
FROM orders
```

```sql
USE sql_store;

SELECT
    product_id,
    name,
    COUNT(*) AS orders,
    IF(COUNT(*) > 1, "Many times", "Once") AS frequency
    
FROM products 
JOIN order_items USING (product_id)
GROUP BY product_id, name
```

## The CASE Operator

```sql
USE sql_store;

SELECT
    order_id,
    CASE
        WHEN YEAR(order_date) = YEAR(NOW()) THEN 'Active'
        WHEN YEAR(order_date) = YEAR(NOW()) - 1 THEN 'Last Year'
        WHEN YEAR(order_date) < YEAR(NOW()) - 1 THEN 'Archived'
        ELSE 'Future'
    END AS category
FROM orders
```

# 8 Views

# 9 Store Precedures

## 9.1 What are Stored Procedures

**Store Precedue**
**- Store and organize SQL**
**-Faster execution**
**Data security**

## 9.2 Creating a Store Procedure

```sql

DELIMITER $$
CREATE PROCEDURE get_clients()

BEGIN
    SELECT * FROM clients;
END$$

DELIMITER ;
```
**Exercise**
*-- Create a store procedure called*
*--     get_invoices_with_balance*
*--     to return all the invoices with a balance > 0*























