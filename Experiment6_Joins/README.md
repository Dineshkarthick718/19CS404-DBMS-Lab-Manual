# Experiment 6: Joins

## AIM
To study and implement different types of joins.

## THEORY

SQL Joins are used to combine records from two or more tables based on a related column.

### 1. INNER JOIN
Returns records with matching values in both tables.

**Syntax:**
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

### 2. LEFT JOIN
Returns all records from the left table, and matched records from the right.

**Syntax:**

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```
### 3. RIGHT JOIN
Returns all records from the right table, and matched records from the left.

**Syntax:**

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```
### 4. FULL OUTER JOIN
Returns all records when there is a match in either left or right table.

**Syntax:**

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;
```

**Question 1**
--
Write the SQL query that accomplishes the selection of all columns from the "patients" table and the first name of doctors from the "doctors" table, with an inner join on the "doctor_id" column.

```sql

SELECT o.patient_id,
        o.first_name,
        o.last_name,
        o.date_of_birth,
        o.admission_date,
        o.discharge_date,
        s.doctor_id,
        s.first_name AS 'doctor_name'
FROM PATIENTS o
INNER JOIN DOCTORS s
         ON o.doctor_id=s.doctor_id;
```

**Output:**

<img width="1303" height="495" alt="640849717-df776507-376b-4d6c-9c79-9dee6760712c" src="https://github.com/user-attachments/assets/4ca7290f-b23a-4b20-a751-cde629910008" />


**Question 2**
---

From the following tables write a SQL query to find the salesperson(s) and the customer(s) he represents. Return Customer Name, city, Salesman, commission

```sql
SELECT
    c.cust_name AS "Customer Name",
    c.city,
    s.name AS Salesman,
    s.commission
FROM customer c
JOIN salesman s
ON c.salesman_id = s.salesman_id;
```

**Output:**

<img width="1247" height="611" alt="640850158-96533ef0-81db-4167-9ce0-4ad03b14e5a3" src="https://github.com/user-attachments/assets/1be70212-04a7-490b-98cd-4af94a2eca63" />


**Question 3**
---
From the following tables write a SQL query to find those orders where the order amount exists between 500 and 2000. Return ord_no, purch_amt, cust_name, city.

```sql

SELECT
    o.ord_no,
    o.purch_amt,
    c.cust_name,
    c.city
FROM orders o
JOIN customer c
ON o.customer_id = c.customer_id
WHERE o.purch_amt BETWEEN 500 AND 2000;
```

**Output:**

<img width="1248" height="407" alt="640850601-c37922a0-dd5a-4a27-a0af-b14c32209d21" src="https://github.com/user-attachments/assets/868dc168-54e7-4da0-a06d-cb080ec6af54" />


**Question 4**
---
Write the SQL query that achieves the selection of the date of birth from the "patients" table (aliased as "p") and all columns from the "appointments" table (aliased as "a"), with an inner join on the "patient_id" column and a condition filtering for patients with the first name 'Alice'.

```sql
SELECT
    p.date_of_birth,
    a.*
FROM patients AS p
INNER JOIN appointments AS a
ON p.patient_id = a.patient_id
WHERE p.first_name = 'Alice';
```

**Output:**

<img width="1293" height="455" alt="640850984-20811207-e190-4f93-b26d-ae2fa561651b" src="https://github.com/user-attachments/assets/3e23289a-224e-4411-86d1-e8601ee94acc" />


**Question 5**

Write the SQL query that achieves the selection of all columns from the "patients" table (aliased as "p"), with an inner join on the "patient_id" column and conditions filtering for test results with the test names 'Blood Test' or 'Blood Pressure' and results not containing the substring 'Normal'

```sql
SELECT p.*
FROM patients p
INNER JOIN test_results t
    ON p.patient_id = t.patient_id
WHERE t.test_name = 'Blood Pressure';

```

**Output:**

<img width="1202" height="362" alt="640851355-a915e03a-b11f-428d-910f-fcc86c4363a1" src="https://github.com/user-attachments/assets/9b7beb5d-bec2-42dd-aa11-aca9a36e7699" />


**Question 6**
---
From the following tables write a SQL query to locate those salespeople who do not live in the same city where their customers live and have received a commission of more than 12% from the company. Return Customer Name, customer city, Salesman, salesman city, commission.

```sql
SELECT
    c.cust_name AS "Customer Name",
    c.city AS "city",
    s.name AS 'Salesman',
    s.city AS "city",
    s.commission
FROM customer c
JOIN salesman s
ON c.salesman_id = s.salesman_id
WHERE c.city <> s.city
  AND s.commission > 0.12;
```

**Output:**

<img width="1275" height="621" alt="640851741-a0c14890-d89a-4dd4-8b04-bd2365be298f" src="https://github.com/user-attachments/assets/4c5922f3-dfa4-4cf3-b76a-dbc510e0921c" />


**Question 7**
---
Write the SQL query that achieves the selection of all columns from the "customer" table (aliased as "c"), with a left join on the "salesman_id" column and a condition filtering for salesman with the name 'Mc Lyon'.

Customer Table: (customer_id, cust_name, city, grade, salesman_id)

Salesman Table: (salesman_id, name, city, commission)


```sql
SELECT c.*
FROM customer AS c
LEFT JOIN salesman AS s
ON c.salesman_id = s.salesman_id
WHERE s.name = 'Mc Lyon';
```

**Output:**

<img width="1250" height="421" alt="640852254-a436ef81-2ca9-4de6-aca9-37262e24a3af" src="https://github.com/user-attachments/assets/194ec215-5e29-4072-b548-5873b6397eb6" />


**Question 8**
---
Write a SQL statement to make a report with customer name, city, order number, order date, and order amount in ascending order according to the order date to determine whether any of the existing customers have placed an order or not.

```sql
SELECT
    c.cust_name,
    c.city,
    o.ord_no,
    o.ord_date,
    o.purch_amt AS "Order Amount"
FROM customer c
LEFT JOIN orders o
ON c.customer_id = o.customer_id
ORDER BY o.ord_date ASC;
```

**Output:**

<img width="1255" height="761" alt="640852815-690c5dca-94d6-4023-86c0-f349f487a20b" src="https://github.com/user-attachments/assets/82a1b5e0-bdc9-4d39-98e0-fe40809945f3" />


**Question 9**
---
From the following tables write a SQL query to find those customers with a grade less than 300. Return cust_name, customer city, grade, Salesman, salesmancity. The result should be ordered by ascending customer_id.

```sql
SELECT
    c.cust_name,
    c.city,
    c.grade,
    s.name AS Salesman,
    s.city
FROM customer c
JOIN salesman s
ON c.salesman_id = s.salesman_id
WHERE c.grade < 300
ORDER BY c.customer_id ASC;
```

**Output:**
<img width="1281" height="686" alt="640853172-dfe8f4c7-9e6a-4826-803e-4935ab2e88dd" src="https://github.com/user-attachments/assets/4cb9f026-3b60-434e-8988-6aea2ae06f35" />


**Question 10**
---
Write the SQL query that achieves the selection of all columns from the "salesman" table (aliased as "s"), with a left join on the "salesman_id" column and a condition filtering for customers with the name 'Fabian Johns'.

Customer Table: (customer_id, cust_name, city, grade, salesman_id)

Salesman Table: (salesman_id, name, city, commission)

```sql
SELECT s.*
FROM salesman AS s
LEFT JOIN customer AS c
ON s.salesman_id = c.salesman_id
WHERE c.cust_name = 'Fabian Johns';
```

**Output:**
<img width="1267" height="420" alt="640853535-978c0706-88aa-4ce8-b24d-bee34c55e9ed" src="https://github.com/user-attachments/assets/a570cae7-bec7-4c74-bfdc-c03cafeb4af5" />

## Result:
Thus, the SQL queries to implement different types of joins have been executed successfully.
![Output10](output.png)


## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
