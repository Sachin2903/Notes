# 🔹 1. SQL Basics

* **SQL (Structured Query Language)** → used to interact with databases
* Performs **CRUD operations**:

| Operation | Description     |
| --------- | --------------- |
| CREATE    | Insert new data |
| READ      | Fetch data      |
| UPDATE    | Modify data     |
| DELETE    | Remove data     |

👉 SQL is **not a database**, it's a **query language**

---

# 🔹 2. RDBMS

* **RDBMS** = software to manage relational databases
* Examples: MySQL, Oracle, SQL Server
* Data stored in **tables (relations)**

👉 **MySQL** = open-source RDBMS using SQL

---

# 🔹 3. SQL vs MySQL

| SQL            | MySQL                 |
| -------------- | --------------------- |
| Query language | Database software     |
| Used for CRUD  | Stores & manages data |

---

# 🔹 4. Data Types

* Numeric → INT, BIGINT
* String → CHAR, VARCHAR
* Date → DATE, TIME

👉 Order of size:
`TINY < SMALL < MEDIUM < INT < BIGINT`

👉 Prefer `VARCHAR` (dynamic size)

---

# 🔹 5. Types of SQL Commands

## ✅ DDL (Structure)

* CREATE, ALTER, DROP, TRUNCATE, RENAME

## ✅ DML (Data)

* INSERT, UPDATE, DELETE

## ✅ DQL/DRL (Query)

* SELECT

## ✅ DCL (Permissions)

* GRANT, REVOKE

## ✅ TCL (Transactions)

* COMMIT, ROLLBACK, SAVEPOINT

---

# 🔹 6. Database Operations

```sql
CREATE DATABASE db;
USE db;
DROP DATABASE db;
SHOW DATABASES;
SHOW TABLES;
```

---

# 🔹 7. SELECT & Filtering

```sql
SELECT * FROM table;
```

## Conditions

```sql
WHERE age > 18
BETWEEN 1 AND 10
IN ('A','B')
IS NULL
```

## Operators

```sql
AND, OR, NOT
```

## Pattern Matching

```sql
LIKE '%abc%'   -- any
LIKE 'a_'      -- single char
```

---

# 🔹 8. Sorting & Grouping

```sql
ORDER BY col ASC/DESC
GROUP BY col
```

## Aggregates

* COUNT(), SUM(), AVG(), MIN(), MAX()

---

# 🔹 9. HAVING vs WHERE

| WHERE           | HAVING         |
| --------------- | -------------- |
| Before grouping | After grouping |
| Filters rows    | Filters groups |

---

# 🔹 10. DISTINCT

```sql
SELECT DISTINCT col FROM table;
```

---

# 🔹 11. Constraints

| Type        | Description             |
| ----------- | ----------------------- |
| PRIMARY KEY | Unique + not null       |
| FOREIGN KEY | Reference another table |
| UNIQUE      | Unique values           |
| CHECK       | Condition               |
| DEFAULT     | Default value           |

---

# 🔹 12. ALTER Table

```sql
ADD column
MODIFY column
DROP column
RENAME table
```

---

# 🔹 13. DML Operations

```sql
INSERT INTO table VALUES (...)
UPDATE table SET col=val WHERE cond
DELETE FROM table WHERE cond
```

---

# 🔹 14. CASCADE

* `ON DELETE CASCADE` → delete child rows
* `ON UPDATE CASCADE` → update child rows

---

# 🔹 15. Joins

## INNER JOIN

* Matching data only

## LEFT JOIN

* All left + matched right

## RIGHT JOIN

* All right + matched left

## FULL JOIN

* All records (use UNION in MySQL)

## CROSS JOIN

* Cartesian product

## SELF JOIN

* Table joins itself

---

# 🔹 16. Set Operations

```sql
UNION        -- combine (distinct)
UNION ALL    -- allow duplicates
```

---

# 🔹 17. Subqueries

* Query inside query

```sql
SELECT * FROM table WHERE id IN (SELECT id FROM table2);
```

## Types

* WHERE clause
* FROM clause
* SELECT clause
* Correlated subquery

---

# 🔹 18. Views

* Virtual table (no data stored)

```sql
CREATE VIEW v AS SELECT * FROM table;
```

👉 Updates in base table reflect in view

---

# 🔹 19. Key Concepts

* SQL works **right → left execution**
* `GROUP BY` without aggregation ≈ DISTINCT
* Views are **virtual tables**
* Joins = combine tables
* Subqueries = nested logic

---

# 🔑 Final Takeaway

* SQL = language
* MySQL = database
* Tables = data storage
* Joins + Subqueries = data relationships
* Constraints = data rules

---


1. SELECT * FROM CUSTOMER;

2. SELECT COUNTRY, CITY FROM CUSTOMER;

3. SELECT DISTINCT COUNTRY, CITY FROM CUSTOMER;
DISTINCT applies to the entire row combination
It returns unique pairs of (Country, City)

4. SELECT * FROM CUSTOMERS
WHERE CITY = 'DELHI';
WHERE PRICE > 40;
WHERE PRICE < 40;
WHERE PRICE != or <> 40;
WHERE PRICE = 40;
WHERE PRICE BETWEEN 40 AND 100;
WHERE CITY LIKE 'S%'  '%S' '%S'
WHERE CITY IN ('DELHI','GOA');

5. SELECT * FROM CUSTOMER
ORDER BY CITY ASC, COUNTRY DESC;

6. PRIOPITY CHAIN
()       → comparison operators (=, >, <, LIKE, BETWEEN, IN, etc.)      → NOT      → AND      → OR

7. INSERT INTO CUSTOMER (COUNTRY,CITY)
VALUES ('INDIA','DELHI')

8. SELECT * FROM CUSTOMER 
WHERE COUNTRY IS NOT NULL;
     ---  or ---
WHERE COUNTRY IS NULL;

9. UPDATE CUSOMTER
SET COUNTRY = 'DELHI'
WHERE COUNTRY ='UP';

10. DELETE FROM CUSTOMERS
WHERE CITY ="DELHI"

11. DROP TABLE CUSTOMERS;

12. SELECT TOP 3 * FROM CUSTOMER;
SELECT TOP 3 PERCENT * FROM CUSTOMER;

MYSQL -> 
SELECT * FROM CUSTOMER
LIMIT 3;

13. An aggregate function is a function that performs a calculation on a set of values, and returns a single value.




