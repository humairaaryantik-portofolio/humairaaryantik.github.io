# Udemy Project Homework <h1>

I recently completed a SQL homework project from a Udemy course, which consisted of 2 comprehensive tasks. These tasks were designed to strengthen my understanding of SQL fundamentals, including data querying, grouping, joins, and aggregation functions.

Below are the 2 tasks that were completed as part of this SQL project:
1. Created all tables required for the homework and populated them with the test data
2. Proceed with the hometasks
      - Select distinct emails of users who made at least one purchase
      - Select Product Names and purchase ID for each Purchase
      - Select credit card, and product name
      - Select last name of user, and total amount of purchases made by this user
      - Select last name of user, and total amount of purchases made by this user, only for users who made two or more purchases
      - Select user last name, and total amount of money user spent in online shop

### **1. Created Tables Required** 
They are : 
- user
- product
- purchase
- role
- purchase_product
      
#### SQL Syntax 
````
CREATE DATABASE project_udemy;
SHOW DATABASES;
USE project_udemy;

-- product table
CREATE TABLE product (
	id INT AUTO_INCREMENT PRIMARY KEY,
	product_name VARCHAR(45) COLLATE utf8mb4_unicode_ci DEFAULT NULL, 
	price DECIMAL(15,2) DEFAULT NULL
) ENGINE=InnoDB AUTO_INCREMENT=8 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;
DESC product;

LOCK TABLES product WRITE;
INSERT INTO product
VALUES
	(1,'HP Laptop',1500.56),
    (2,'Apple iPhone',2000.99),
    (3,'Samsung Galaxy',1100.10),
    (4,'Asus Zenbook',1857.28),
    (5,'Bricks',100.00),
    (6,'TV',2519.78),
    (7,'Keybord',23.00);
UNLOCK TABLES;
SELECT * FROM product;

-- purchase table
DROP TABLE IF EXISTS purchase;
CREATE TABLE purchase(
  id int NOT NULL AUTO_INCREMENT PRIMARY KEY,
  fk_purchase_user INT DEFAULT NULL,
  pruchase_timestamp TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP 
) ENGINE=InnoDB AUTO_INCREMENT=25 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

LOCK TABLES purchase WRITE;
INSERT INTO purchase
VALUES 
	(12,1,'2021-11-02 22:14:28'),
    (13,3,'2021-11-02 22:14:28'),
    (14,11,'2021-11-02 22:14:28'),
    (15,1,'2021-11-02 22:14:28'),
    (16,11,'2021-11-02 22:14:28'),
    (17,12,'2021-11-02 22:14:28'),
    (18,12,'2021-11-02 22:14:28'),
    (19,12,'2021-11-02 22:14:28'),
    (20,17,'2021-11-02 22:14:28'),
    (21,1,'2021-11-02 22:14:28'),
    (22,18,'2021-11-02 22:14:28'),
    (23,11,'2021-11-02 22:14:28'),
    (24,18,'2021-11-02 22:49:46');
UNLOCK TABLES;
SELECT * FROM purchase;

-- purchase_product table
DROP TABLE IF EXISTS purchase_product;
CREATE TABLE purchase_product(
  purchase_id INT NOT NULL,
  product_id INT NOT NULL,
  PRIMARY KEY (purchase_id, product_id)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

LOCK TABLES purchase_product WRITE;
INSERT INTO purchase_product 
VALUES (12,1),(12,2),(12,3),(13,1),(13,4),(14,5),(15,1),(15,6),(15,7),(16,2),(17,2),(18,1),(19,5),(20,6),(21,4),(22,3),(23,3),(24,7);
UNLOCK TABLES;
SELECT * FROM purchase_product;

-- role table
DROP TABLE IF EXISTS role;
CREATE TABLE role (
  id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
  role_name varchar(45) COLLATE utf8mb4_unicode_ci DEFAULT NULL
) ENGINE=InnoDB AUTO_INCREMENT=101 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

LOCK TABLES role WRITE;
INSERT INTO role 
VALUES 
	(3,'CONTENT_MANAGER'),
    (4,'EMPLOYEE'),
    (5,'MEDIA_EDITOR'),
    (6,'CONTRIBUTOR');
UNLOCK TABLES;
SELECT * FROM role;

-- user table
DROP TABLE IF EXISTS user;
CREATE TABLE user (
  id INT UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY, 
  first_name VARCHAR(45) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
  last_name VARCHAR(45) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
  email VARCHAR(50) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
  fk_user_role INT DEFAULT NULL,
  money DECIMAL(15,2) DEFAULT '0.00',
  credit_card VARCHAR(16) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
  UNIQUE KEY email_UNIQUE (email),
  KEY role_id_idx (fk_user_role),
  CONSTRAINT fk_user_role FOREIGN KEY (fk_user_role) REFERENCES role (id) 
  ON DELETE SET NULL 
  ON UPDATE SET NULL
) ENGINE=InnoDB AUTO_INCREMENT=20 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

LOCK TABLES user WRITE;
INSERT INTO user 
VALUES 
	(1,'Sergey','Ivanov','s.ivanov@email.com',NULL,400.60,'1234567890123456'),
    (3,'Petr','Skomorohov','p.skomorohov@email.com',3,100.25,'4444444444444444'),
    (11,'Andrey','Pavlenko','a.pavlenko@email.com',NULL,754.28,'5555555555555555'),
    (12,'John','Smith','john.smith@email.com',4,1000.75,'6666666666666666'),
    (17,'Yegor','Hromov','y.hromov@email.com',4,0.00,'7777777777777777'),
    (18,'Vasyl','Leonenko','v.leonenko@email.com',6,0.00,'8888888888888888');
UNLOCK TABLES;
SELECT * FROM user;
SHOW TABLES;
````
Or See Task 1 [in Here](PROJECT_UDEMY/TABLE-TABLE.sql)

#### Output

### **2. Proceed with the hometasks** 
1️⃣ Select distinct emails of users who made at least one purchase

  
