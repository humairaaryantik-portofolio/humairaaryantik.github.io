![image alt]()
<h1 align="center" = > UDEMY PROJECT HOMEWORK </h1>

I recently completed a SQL homework project from a Udemy course, which consisted of 2 comprehensive problems. These tasks were designed to strengthen my understanding of SQL fundamentals, including data querying, grouping, joins, and aggregation functions.

Below are the problems completed as part of this SQL project:
1. Created all required tables for the homework and populated them with test data.
2. Completed six SQL tasks to analyze.
      - Select distinct emails of users who made at least one purchase
      - Select Product Names and purchase ID for each Purchase
      - Select credit card, and product name
      - Select last name of user, and total amount of purchases made by this user
      - Select last name of user, and total amount of purchases made by this user, only for users who made two or more purchases
      - Select user last name, and total amount of money user spent in online shop

### **1. Created Tables Required** 
They are : 
- product
- purchase
- purchase_product
- role
- user
      
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
Or See SQL Syntax problem 1 [in Here](PROJECT_UDEMY/TABLE-TABLE.sql)

#### Output
*product table*
| id | product_name | price|
|----|--------------|------|
| 1 |Hp Laptop | 1500.56 |
| 2 | Apple iPhone | 2000.99 |
| 3 | Samsung Galaxy | 1100.10 |
| 4 | Asuss Zenbook | 1857.28 |
| 5 | Brick | 100.00 |
| 6 | TV | 2519.78 |
| 7 | Keyboard | 23.00 |

*purchase table*
| id | fk_purchase_user | purchase timestamp |
|----|--------------|------|
| 12 |	1 | 2021-11-02 22:14:28|
|13	|3 |	2021-11-02 22:14:28|
|14	|11	|2021-11-02 22:14:28|
|15	|1	|2021-11-02 22:14:28|
|16	|11	|2021-11-02 22:14:28|
|17	|12	|2021-11-02 22:14:28|
|18	|12	|2021-11-02 22:14:28|
|19	|12	|2021-11-02 22:14:28|
|20	|17	|2021-11-02 22:14:28|
|21	|1	|2021-11-02 22:14:28|
|22	|18	|2021-11-02 22:14:28|
|23	|11	|2021-11-02 22:14:28|
|24	|18	|2021-11-02 22:49:46|
		

*purchase_product table*
| purchase_id | product_id |
|----|--------------|
|12	|1|
|12	|2|
|12	|3|
|13	|1|
|13	|4|
|14	|5|
|15	|1|
|15	|6|
|15	|7|
|16	|2|
|17	|2|
|18	|1|
|19	|5|
|20	|6|
|21	|4|
|22	|3|
|23	|3|
|24	|7|

*role table*
| id | role_name |
|----|--------------|
|3|	CONTENT_MANAGER|
|4	|EMPLOYEE|
|5	|MEDIA_EDITOR|
|6	|CONTRIBUTOR|

*user table*
| id | first_name | last_name | email | fk_user_role | money | credit_card |
|----|--------------|-----|----|--------------|-----|-----|
|1|	Sergey|	Ivanov|	s.ivanov@email.com|	NULL|	400.60|	1234567890123456|
|3|	Petr|Skomorohov	|p.skomorohov@email.com	|3	|100.25	|4444444444444444|
|11|	Andrey	|Pavlenko|	a.pavlenko@email.com	| NULL |	754.28	|5555555555555555|
|12|	John|	Smith	|john.smith@email.com	|4|	1000.75	|6666666666666666|
|17|	Yegor|	Hromov|	y.hromov@email.com	|4	|0.00|	7777777777777777|
|18|	Vasyl|	Leonenko|	v.leonenko@email.com|	6|	0.00|	8888888888888888|


### **2. Six SQL tasks to analyze** 
**1️⃣ TASK 1 : Select distinct emails of users who made at least one purchase**
```
SELECT * FROM user;
SELECT * FROM purchase;
SELECT DISTINCT u.id, u.email 
FROM user u
JOIN purchase p 
ON p.fk_purchase_user = u.id
ORDER BY 1 ASC;
```
Or See SQL Syntax Task 1 [in Here](https://github.com/humairaaryantik-portofolio/humairaaryantik.github.io/blob/84746cb5971b13c4b3aee1452a8d003533be19fe/PROJECT_UDEMY/TASK%201.sql)

#### Output
| id | email |
|----|--------------|
|1|	s.ivanov@email.com|
|3|	p.skomorohov@email.com|
|11|	a.pavlenko@email.com|
|12|	john.smith@email.com|
|17|	y.hromov@email.com|
|18	|v.leonenko@email.com|


**2️⃣ TASK 2 : Select Product Names and purchase ID for each Purchase**
```
SELECT * FROM product;
SELECT * FROM purchase_product;

SELECT p.product_name, pi.purchase_id
FROM product p
JOIN purchase_product pi
ON p.id = pi.product_id;
```
Or See SQL Syntax Task 2 [in Here](https://github.com/humairaaryantik-portofolio/humairaaryantik.github.io/blob/1ebff35b2f6938049db5510b4724dc60c2e05746/PROJECT_UDEMY/TASK%202.sql)

#### Output
| profuct_name | purchase_id |
|----|--------------|
|HP Laptop |	12|
|Apple iPhone|	12|
|Samsung Galaxy	|12|
|HP Laptop	|13|
|Asus Zenbook|	13|
|Bricks|	14|
|HP Laptop|	15|
|TV|	15|
|Keybord|	15|
|Apple iPhone|	16|
|Apple iPhone|	17|
|HP Laptop|	18|
|Bricks|	19|
|TV	|20|
|Asus Zenbook|	21|
|Samsung Galaxy|	22|
|Samsung Galaxy	|23|
|Keybord	|24|


**3️⃣ TASK 3 : Select credit card, and product name**
```
SELECT u.credit_card, pro.product_name 
FROM user u 
JOIN purchase p
ON p.fk_purchase_user = u.id 

JOIN purchase_product pp
ON pp.purchase_id = p.id

JOIN product pro 
ON pro.id = pp.product_id; 
```
Or See SQL Syntax Task 3 [in Here](https://github.com/humairaaryantik-portofolio/humairaaryantik.github.io/blob/b44743032bec12155d62ba832ea6654806a40a15/PROJECT_UDEMY/TASK%203.sql)


#### Output
| credit_card | product_name |
|----|--------------|
|1234567890123456|	HP Laptop|
|1234567890123456|	Apple iPhone|
|1234567890123456|	Samsung Galaxy|
|4444444444444444|	HP Laptop|
|4444444444444444|	Asus Zenbook|
|5555555555555555|	Bricks|
|1234567890123456|	HP Laptop|
|1234567890123456|	TV|
|1234567890123456|	Keybord|
|5555555555555555|	Apple iPhone|
|6666666666666666|	Apple iPhone|
|6666666666666666|	HP Laptop|
|6666666666666666	|Bricks|
|7777777777777777|	TV|
|1234567890123456|	Asus Zenbook|
|8888888888888888|	Samsung Galaxy|
|5555555555555555|	Samsung Galaxy|
|8888888888888888|	Keybord|


4️⃣ TASK 4 : Select last name of user, and total amount of purchases made by this user
```
SELECT u.last_name, COUNT(*) AS total_purchase
FROM user u
JOIN purchase p
ON u.id = p.fk_purchase_user
GROUP BY u.last_name;
```
Or See SQL Syntax Task 4 [in Here](https://github.com/humairaaryantik-portofolio/humairaaryantik.github.io/blob/b44743032bec12155d62ba832ea6654806a40a15/PROJECT_UDEMY/TASK%204.sql)


#### Output
| last_name | total_purchase |
|----|--------------|
|Ivanov|3|
|Skomorohov|	1|
|Pavlenko|	3|
|Smith	|3|
|Hromov|	1|
|Leonenko	|2|


**5️⃣ TASK 5 : Select last name of user, and total amount of purchases made by this user, only for users who made two or more purchases**

```
SELECT u.last_name, COUNT(*) AS total_purchase
FROM user u
JOIN purchase p
ON u.id = p.fk_purchase_user
GROUP BY u.last_name
HAVING total_purchase >= 2;
```
Or See SQL Syntax Task 5 [in Here](https://github.com/humairaaryantik-portofolio/humairaaryantik.github.io/blob/5b768b4d4a1e94daca55879d2fb9eb6275354cca/PROJECT_UDEMY/TASK%205.sql)


#### Output
| last_name | total_purchase |
|----|--------------|
|Ivanov|	3|
|Pavlenko|	3|
|Smith|	3|
|Leonenko|	2|


**6️⃣ TASK 6 : Select user last name, and total amount of money user spent in online shop**

```
SELECT CONCAT(u.first_name, ' ', u.last_name) AS fullname, SUM(p.price) AS total_price
FROM user u 
JOIN purchase pur
ON pur.fk_purchase_user = u.id

JOIN purchase_product pp
ON pp.purchase_id = pur.id 

JOIN product p 
ON p.id = pp.product_id
GROUP BY fullname;
```
Or See SQL Syntax Task 6 [in Here](https://github.com/humairaaryantik-portofolio/humairaaryantik.github.io/blob/5b768b4d4a1e94daca55879d2fb9eb6275354cca/PROJECT_UDEMY/TASK%206.sql)

#### Output
| fullname | total_price |
|----|--------------|
|Sergey Ivanov|	10502.27|
|Petr Skomorohov|	3357.84|
|Andrey Pavlenko|	3201.09|
|John Smith|	3601.55|
|Yegor Hromov|	2519.78|
|Vasyl Leonenko|	1123.10|


## CREDIT 
[Humaira Aryanti K](https://github.com)
