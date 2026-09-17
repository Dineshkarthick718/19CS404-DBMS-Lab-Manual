<img width="1160" height="375" alt="641326882-24f6f203-55e7-430b-9b68-b7258e51fea8" src="https://github.com/user-attachments/assets/d84bd804-b246-4b0e-a3da-98c0dd67953b" /># Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
Create a table named Products with the following constraints:

ProductID should be the primary key. ProductName should be NOT NULL. Price is of real datatype and should be greater than 0. Stock is of integer datatype and should be greater than or equal to 0.
```
CREATE TABLE Products (
         ProductID PRIMARY KEY,
         ProductName NOT NULL,
         Price REAL CHECK (Price>0),
         Stock INTEGER CHECK (Stock>=0)
);
```
**Output:**

<img width="1213" height="277" alt="image" src="https://github.com/user-attachments/assets/8ce3d02e-f1fb-46cb-8b55-a2c56f43f63e" />


**Question 2**
Create a table named Orders with the following columns:

OrderID as INTEGER OrderDate as TEXT CustomerID as INTEGER
```
CREATE TABLE Orders (
  OrderID INTEGER,
  OrderDate TEXT,
  CustomerID INTEGER
);
```

**Output:**

<img width="1160" height="375" alt="641326882-24f6f203-55e7-430b-9b68-b7258e51fea8" src="https://github.com/user-attachments/assets/51d31da4-78b9-4bb7-acdb-d18802f256fb" />


**Question 3**
Create a table named ProjectAssignments with the following constraints: AssignmentID as INTEGER should be the primary key. EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID). ProjectID as INTEGER should be a foreign key referencing Projects(ProjectID). AssignmentDate as DATE should be NOT NULL

```
CREATE TABLE ProjectAssignments(
           AssignmentID INTEGER PRIMARY KEY,
           EmployeeID INTEGER,
           ProjectID INTEGER,
           AssignmentDate DATE NOT NULL,
           FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID),
           FOREIGN KEY (ProjectID) REFERENCES Projects(ProjectID)
);
```

**Output:**

<img width="1203" height="292" alt="641327614-3170e964-b240-4eb6-9eef-57e0e05abc97" src="https://github.com/user-attachments/assets/4a1f4930-d262-4751-a245-1ccebaaf373c" />


**Question 4**
Write a SQL query to Add a new ParentsNumber column as number and Adhar_Number as Number in the Student_details table.
```
ALTER TABLE Student_details
ADD COLUMN ParentsNumber number;

ALTER TABLE Student_details
ADD COLUMN Adhar_Number number;
```

**Output:**

<img width="1212" height="398" alt="641327831-766fbc83-fa8c-4dbd-832e-890036ab72c0" src="https://github.com/user-attachments/assets/c16432ce-3125-49a0-a2a8-38c85cbf6f4e" />


**Question 5**
Create a new table named orders with the following specifications: ord_id as TEXT with a length of 4. item_id as TEXT. ord_date as DATE. ord_qty as INTEGER. cost as INTEGER. The primary key is a composite key consisting of item_id and ord_date. ord_id and item_id should not accept NULL

```
CREATE TABLE orders (
    ord_id TEXT NOT NULL CHECK (LENGTH(ord_id) = 4),
    item_id TEXT NOT NULL,
    ord_date DATE,
    ord_qty INTEGER,
    cost INTEGER,
    PRIMARY KEY (item_id, ord_date)
);
```

**Output:**

<img width="1187" height="322" alt="641328037-44f544d0-c5ab-4a7d-8830-090009f77a44" src="https://github.com/user-attachments/assets/b19a5878-83ad-4f67-b538-9326f52e041c" />


**Question 6**
Write a SQL query for adding a new column named "email" with the datatype VARCHAR(100) to the table "customer"
```
ALTER TABLE customer ADD email VARCHAR(100);
```
**Output:**

<img width="1172" height="362" alt="641328267-7f122e51-abad-4217-a47d-8e8ce614f5d6" src="https://github.com/user-attachments/assets/1e12f3ec-6cb9-4213-9a1d-a6bcc1cfd502" />


**Question 7**
Insert a new product with ProductID 101, Name Laptop, Category Electronics, Price 1500, and Stock 50 into the Products table.
```
INSERT INTO Customers(CustomerID,  Name, Address )
VALUES(306,         'Diana Prince',  'Themyscira');
INSERT INTO Customers(CustomerID,  Name, Address,     City,  ZipCode )
VALUES(307,         'Bruce Wayne',   'Wayne Mano',  'Gotham',  10007);
INSERT INTO Customers(CustomerID,  Name, Address,  ZipCode )
VALUES(308,        'Peter Parker',  'Queens', 11375);
```

**Output:**

<img width="1182" height="307" alt="641402758-6036d8fa-2e8a-4260-820d-2e3267fde530" src="https://github.com/user-attachments/assets/32e90944-8de3-4141-8389-5007dc20d239" />


**Question 8**
Create a table named Shipments with the following constraints: ShipmentID as INTEGER should be the primary key. ShipmentDate as DATE. SupplierID as INTEGER should be a foreign key referencing Suppliers(SupplierID). OrderID as INTEGER should be a foreign key referencing Orders(OrderID).
```
CREATE TABLE Shipments(
       ShipmentID INTEGER PRIMARY KEY,
       ShipmentDate DATE,
       SupplierID INTEGER,
       OrderID INTEGER,
       FOREIGN KEY (SupplierID) REFERENCES Suppliers(SupplierID),
       FOREIGN KEY (OrderID) REFERENCES Orders(OrderID)
);
```


**Output:**

<img width="1160" height="245" alt="641403249-3033b5af-acc0-47ea-885b-6317508ed06f" src="https://github.com/user-attachments/assets/431a9ca4-9153-4d43-a281-d5e2a4186f9c" />


**Question 9**
Create a table named Shipments with the following constraints: ShipmentID as INTEGER should be the primary key. ShipmentDate as DATE. SupplierID as INTEGER should be a foreign key referencing Suppliers(SupplierID). OrderID as INTEGER should be a foreign key referencing Orders(OrderID).
```
CREATE TABLE Shipments(
       ShipmentID INTEGER PRIMARY KEY,
       ShipmentDate DATE,
       SupplierID INTEGER,
       OrderID INTEGER,
       FOREIGN KEY (SupplierID) REFERENCES Suppliers(SupplierID),
       FOREIGN KEY (OrderID) REFERENCES Orders(OrderID)
);
```


**Output:**




**Question 10**
Insert all books from Out_of_print_books into Books

Table attributes are ISBN, Title, Author, Publisher, YearPublished
```
INSERT INTO Books (ISBN, Title, Author, Publisher, YearPublished)
SELECT ISBN, Title, Author, Publisher, YearPublished
FROM Out_of_print_books;
```


**Output:**

![Uploading 641403638-a2dc607e-31c7-4d1e-b41f-77a88306d67b.png…]()

## Result:
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.

## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
