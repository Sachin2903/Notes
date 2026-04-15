# 🗄️ Complete SQL Notes (Basic → Advanced)

---

# 📘 1. What is SQL?

Structured Query Language (SQL) is used to:

* Store data
* Retrieve data
* Update/Delete data
* Manage databases

---

# 🧱 2. Database Basics

## Create Database

```sql
CREATE DATABASE mydb;
```

## Use Database

```sql
USE mydb;
```

## Show Databases

```sql
SHOW DATABASES;
```

---

# 📊 3. Table Operations

## Create Table

```sql
CREATE TABLE category (
  id BIGINT PRIMARY KEY AUTO_INCREMENT,
  name VARCHAR(255)
);
```

## Show Tables

```sql
SHOW TABLES;
```

## Describe Table

```sql
DESCRIBE category;
```

## Drop Table

```sql
DROP TABLE category;
```

---

# ✍️ 4. CRUD Operations

## Insert

```sql
INSERT INTO category (name) VALUES ('Food');
```

## Select

```sql
SELECT * FROM category;
SELECT name FROM category;
```

## Update

```sql
UPDATE category SET name='Tech' WHERE id=1;
```

## Delete

```sql
DELETE FROM category WHERE id=1;
```

---

# 🔍 5. Filtering & Conditions

```sql
SELECT * FROM category WHERE name='Food';
SELECT * FROM category WHERE id > 2;
SELECT * FROM category WHERE name LIKE '%oo%';
```

---

# 🔢 6. Sorting & Limiting

```sql
SELECT * FROM category ORDER BY name ASC;
SELECT * FROM category LIMIT 5;
```

---

# 🔗 7. Relationships (Joins)

## Inner Join

```sql
SELECT * FROM product p
JOIN category c ON p.category_id = c.id;
```

## Left Join

```sql
SELECT * FROM product p
LEFT JOIN category c ON p.category_id = c.id;
```

---

# 📊 8. Aggregation

```sql
SELECT COUNT(*) FROM category;
SELECT AVG(price) FROM product;
SELECT MAX(price), MIN(price) FROM product;
```

---

# 🧠 9. Group By

```sql
SELECT category_id, COUNT(*)
FROM product
GROUP BY category_id;
```

---

# 🔒 10. Constraints

* PRIMARY KEY
* FOREIGN KEY
* NOT NULL
* UNIQUE

---

# ⚙️ 11. Indexes

```sql
CREATE INDEX idx_name ON category(name);
```

---

# 🔐 12. USER MANAGEMENT (IMPORTANT 🚀)

## Create User

```sql
CREATE USER 'springuser'@'localhost' IDENTIFIED BY 'password123';
```

## Grant Permissions

```sql
GRANT ALL PRIVILEGES ON mydb.* TO 'springuser'@'localhost';
```

## Limited Permissions

```sql
GRANT SELECT, INSERT ON mydb.* TO 'springuser'@'localhost';
```

## Apply Changes

```sql
FLUSH PRIVILEGES;
```

## Show Users

```sql
SELECT user, host FROM mysql.user;
```

## Show Grants

```sql
SHOW GRANTS FOR 'springuser'@'localhost';
```

## Change Password

```sql
ALTER USER 'springuser'@'localhost' IDENTIFIED BY 'newpassword';
```

## Change Auth Method

```sql
ALTER USER 'springuser'@'localhost'
IDENTIFIED WITH mysql_native_password BY 'password123';
```

## Revoke Permissions

```sql
REVOKE ALL PRIVILEGES ON mydb.* FROM 'springuser'@'localhost';
```

## Delete User

```sql
DROP USER 'springuser'@'localhost';
```

## Rename User

```sql
RENAME USER 'olduser'@'localhost' TO 'newuser'@'localhost';
```

## Lock / Unlock User

```sql
ALTER USER 'springuser'@'localhost' ACCOUNT LOCK;
ALTER USER 'springuser'@'localhost' ACCOUNT UNLOCK;
```

## Password Expiry

```sql
ALTER USER 'springuser'@'localhost' PASSWORD EXPIRE;
```

---

# 🌐 13. Host Types

| Host         | Meaning      |
| ------------ | ------------ |
| localhost    | same machine |
| %            | any machine  |
| 192.168.1.10 | specific IP  |
| 192.168.1.%  | IP range     |

---

# 🚀 14. Transactions

```sql
START TRANSACTION;
UPDATE category SET name='Test';
ROLLBACK;
COMMIT;
```

---

# ⚡ 15. Views

```sql
CREATE VIEW my_view AS
SELECT name FROM category;
```

---

# 📦 16. Stored Procedures

```sql
DELIMITER //
CREATE PROCEDURE getCategories()
BEGIN
  SELECT * FROM category;
END //
DELIMITER ;
```

---

# 🧩 17. Triggers

```sql
CREATE TRIGGER before_insert_category
BEFORE INSERT ON category
FOR EACH ROW
SET NEW.name = UPPER(NEW.name);
```

---

# ⚠️ Best Practices

* Use indexes for performance
* Avoid SELECT * in production
* Use proper constraints
* Use dedicated DB users (not root)

---

# 🎯 FINAL SUMMARY

* DDL → CREATE, ALTER, DROP
* DML → INSERT, UPDATE, DELETE
* DQL → SELECT
* DCL → GRANT, REVOKE
* TCL → COMMIT, ROLLBACK

---

💡 This is a complete SQL roadmap from beginner → advanced 🚀

---

# 🧠 18. Advanced Filtering

```sql
SELECT * FROM product WHERE price BETWEEN 100 AND 500;
SELECT * FROM product WHERE name IN ('A','B');
SELECT * FROM product WHERE name IS NULL;
```

---

# 🔄 19. Subqueries

```sql
SELECT * FROM product
WHERE category_id IN (SELECT id FROM category WHERE name='Food');
```

---

# 🧮 20. CASE Statement

```sql
SELECT name,
CASE
  WHEN price > 100 THEN 'Expensive'
  ELSE 'Cheap'
END
FROM product;
```

---

# 🧵 21. String Functions

```sql
SELECT UPPER(name), LOWER(name) FROM category;
SELECT LENGTH(name) FROM category;
SELECT CONCAT(name, ' category') FROM category;
```

---

# 📅 22. Date Functions

```sql
SELECT NOW();
SELECT CURDATE();
SELECT DATE_ADD(NOW(), INTERVAL 5 DAY);
```

---

# 🔢 23. Numeric Functions

```sql
SELECT ROUND(10.567, 2);
SELECT CEIL(10.2), FLOOR(10.9);
```

---

# 🪟 24. Window Functions (Advanced 🔥)

```sql
SELECT name, price,
RANK() OVER (ORDER BY price DESC) as rank
FROM product;
```

---

# 🧩 25. Normalization

* 1NF → atomic values
* 2NF → remove partial dependency
* 3NF → remove transitive dependency

---

# ⚡ 26. Denormalization

👉 Used for performance optimization

---

# 🔍 27. Execution Order of SQL

1. FROM
2. WHERE
3. GROUP BY
4. HAVING
5. SELECT
6. ORDER BY

---

# 🧱 28. HAVING vs WHERE

```sql
SELECT category_id, COUNT(*)
FROM product
GROUP BY category_id
HAVING COUNT(*) > 2;
```

---

# 🧾 29. UNION vs UNION ALL

```sql
SELECT name FROM category
UNION
SELECT name FROM product;
```

---

# 🔐 30. Transactions Deep Dive

* ACID Properties

  * Atomicity
  * Consistency
  * Isolation
  * Durability

---

# 🧠 31. Isolation Levels

* READ UNCOMMITTED
* READ COMMITTED
* REPEATABLE READ
* SERIALIZABLE

---

# ⚙️ 32. Performance Tips

* Use indexes
* Avoid full table scan
* Use LIMIT
* Use proper joins

---

# 📦 33. Backup & Restore

```bash
mysqldump -u root -p mydb > backup.sql
mysql -u root -p mydb < backup.sql
```

---

# 🔥 34. Real Interview Topics

* Difference between DELETE vs TRUNCATE vs DROP
* Index types
* Joins types
* Normalization
* Transactions
* Query optimization

---

# 🎯 FINAL MASTER SUMMARY

You now know:

✔ SQL Basics
✔ CRUD Operations
✔ Joins & Relationships
✔ Aggregation & Grouping
✔ User Management
✔ Transactions
✔ Advanced SQL (Window, Subquery)
✔ Performance & Optimization
✔ Real-world concepts

---

🚀 This is now a COMPLETE SQL roadmap (Beginner → Advanced → Interview Ready)
