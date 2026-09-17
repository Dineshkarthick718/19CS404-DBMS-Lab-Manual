<img width="1227" height="332" alt="438282891-386479f3-72d3-4a8e-815e-53540d143b21" src="https://github.com/user-attachments/assets/0e0b29ad-e7fe-4d3d-a507-c340fdf289b5" /># Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
**Syntax (Single Row):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);
```
**Syntax (Multiple Rows):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES
(value_1, value_2, ...),
(value_3, value_4, ...);
```
**Syntax (Insert from another table):**
```sql
INSERT INTO table_name SELECT * FROM other_table WHERE condition;
```
### 2. UPDATE
Used to modify records in a relation.
Syntax:
```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
### 3. DELETE
Used to delete records from a relation.
**Syntax (All rows):**
```sql
DELETE FROM table_name;
```
**Syntax (Specific condition):**
```sql
DELETE FROM table_name WHERE condition;
```
### 4. SELECT
Used to retrieve records from a table.
**Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```
**Question 1**
Increase the reorder level by 30% for products from 'Food' category having quantity in stock less than 50% of existing reorder level in the products table
```
name               type
--------------  ----------
product_id         INT
product_name       VARCHAR(10)
category           VARCHAR(50)
cost_price         DECIMAL(10)
sell_price         DECIMAL(10)
reorder_lvl        INT
quantity              INT
supplier_id           INT
```

```
UPDATE products
set reorder_lvl = reorder_lvl * 1.30
where category  = 'Food' and quantity < 50;
```

**Output:**
<img width="1222" height="443" alt="438273166-e0d61fb2-958e-4bc0-bbde-7709c2b1cdbc" src="https://github.com/user-attachments/assets/70531a8d-07bb-4605-8b19-e67625574715" />


**Question 2**
Write a SQL statement to Increase the selling price per unit by 5% for product ID 15 who's sale is on '2023-01-31'. sales(sale_id,sale_date,product_id,quantity,sell_price,total_sell_price)
```
update sales
set sell_price=sell_price*1.05
where product_id=15 and sale_date='2023-01-31';
```

**Output:**
<img width="1222" height="492" alt="438274970-95f653bd-03b1-4112-95b1-cf7b96db66d0" src="https://github.com/user-attachments/assets/b839e7b2-40da-43e9-852a-741aa09f23d0" />


**Question 3**
Write a SQL statement to update the product_name as 'Grapefruit' whose product_id is 4 in the products table.
```
products table

---------------
product_id
product_name
category_id
availability
```
```
update products
set product_name = 'Grapefruit'
where product_id=4;
```

**Output:**

<img width="1220" height="282" alt="438275698-de83bbc9-4bf1-471e-8f7d-a55540d1e765" src="https://github.com/user-attachments/assets/9fb8d311-a5cd-4b4e-968e-ccd4285b31ec" />


**Question 4**
Write a SQL query to delete a doctor from Doctors table whose Specialization is 'Pediatrics' and First name is 'Michael'. Sample table: Doctors attributes : doctor_id, first_name, last_name, specialization
```
delete from Doctors
where specialization = 'Pediatrics' and first_name = 'Michael';
```

**Output:**
<img width="1215" height="422" alt="438276622-e43aeb1e-3688-4ebc-b6a5-62b72d47ba59" src="https://github.com/user-attachments/assets/5891cd8d-9861-412d-9515-f6ab703968e4" />


**Question 5**
Write a SQL query to Delete customers from 'customer' table where 'GRADE' is exactly 2.


 ```
Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSB
```

```
delete from customer
where GRADE = 2;
```

**Output:**

<img width="1230" height="623" alt="438277326-211be447-7695-4ab2-9ab4-69017098bbab" src="https://github.com/user-attachments/assets/70141986-c40f-4379-bfe7-832efd092801" />


**Question 6**
Write a SQL query to delete a specific doctor from Doctors table whose ID is 1. Sample table: Doctors attributes : doctor_id, first_name, last_name, specialization
```
DELETE FROM Doctors
where Doctor_id=1;
```
**Output:**
<img width="1212" height="301" alt="438278920-449f6fd4-f9c7-494b-8496-6ae2e60f24ae" src="https://github.com/user-attachments/assets/15d35996-6274-48d9-9722-c795516d1d73" />


**Question 7**
Write a SQL query to Delete All Doctors with a NULL Specialization Sample table: Doctors attributes : doctor_id, first_name, last_name, specialization
```
DELETE FROM Doctors
WHERE specialization IS NULL;
```

**Output:**
<img width="1221" height="813" alt="438280373-f46f563c-33c6-49ff-81a6-d4a4f2c2b581" src="https://github.com/user-attachments/assets/c29fb2bb-dc9b-453c-8e3b-4c73e865891d" />


**Question 8**
Write a SQL query to determine the age group of value1 in the Calculations table as 'Child' if it is less than 13, 'Teen' if it is between 13 and 19, and 'Adult' if it is 20 or older.

```
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          INTEGER     0                       1
1           value1      REAL        0                       0
2           value2      REAL        0                       0
3           base        INTEGER     0                       0
4           exponent    INTEGER     0                       0
5           number      REAL        0                       0
6           decimal     REAL        0                       0
```
```
select id,value1,
case
when value1<13 then 'Child'
when value1 between 13 and 19 then 'Teen' else 'Adult'
end as age_group
from Calculations;
```

**Output:**

<img width="1007" height="397" alt="438281247-04d3d2ee-c978-4c75-81f0-3946fe357b94" src="https://github.com/user-attachments/assets/02ef59f4-5c7d-4afe-991d-12a5e069155b" />


**Question 9**
Write a SQL query to calculate the absolute value of the value1 column from the Calculations table.

```
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          INTEGER     0                       1
1           value1      REAL        0                       0
2           value2      REAL        0                       0
3           base        INTEGER     0                       0
4           exponent    INTEGER     0                       0
5           number      REAL        0                       0
6           decimal     REAL        0                       0
```

```
select id,value1,abs(value1) as absolute_value
from Calculations;
```

**Output:**

<img width="1227" height="332" alt="438282891-386479f3-72d3-4a8e-815e-53540d143b21" src="https://github.com/user-attachments/assets/a9c2ac28-18a3-490d-b3fb-e7f588210191" />

**Question 10**
 Write a SQL statement to Update the grade of all customers in Chennai city as 5. Customer table (customer_id,cust_name,city,grade,salesman_id)
```
update Customer
set grade = 5
where city = 'Chennai';
```

**Output:**

<img width="1215" height="517" alt="438284812-e6f7369e-8a77-430e-b6b6-46816bbcdaf2" src="https://github.com/user-attachments/assets/382cc0e0-8078-44e9-9531-a4413d02b7cb" />



## Result:
Thus, the SQL queries to implement DML commands have been executed successfully.

## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
