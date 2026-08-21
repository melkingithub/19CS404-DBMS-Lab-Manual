# Experiment 2: DDL Commands

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
--
Create a new table named item with the following specifications and constraints:

item_id as TEXT and as primary key.
item_desc as TEXT.
rate as INTEGER.
icom_id as TEXT with a length of 4.
icom_id is a foreign key referencing com_id in the company table.
The foreign key should set NULL on updates and deletes.
item_desc and rate should not accept NULL.

```sql
CREATE TABLE item (
item_id TEXT PRIMARY KEY,
item_desc TEXT NOT NULL,
rate INTEGER NOT NULL,
icom_id TEXT CHECK (LENGTH(icom_id) >=4),
FOREIGN KEY (icom_id) REFERENCES company(com_id)
    ON UPDATE SET NULL
    ON DELETE SET NULL
);
```

**Output:**

<img width="1157" height="246" alt="image" src="https://github.com/user-attachments/assets/41dfe64f-4ac0-43c8-9dbf-10f0b42dc853" />



**Question 2**
---
Write an SQL query to add a new column salary of type INTEGER to the Employees table, with a CHECK constraint that ensures the value in this column is greater than 0.

 

```sql
ALTER TABLE Employees
ADD COLUMN salary INTEGER
```

**Output:**

<img width="1194" height="221" alt="image" src="https://github.com/user-attachments/assets/9a28c209-857f-4740-b472-3c49b7fecc44" />



**Question 3**
---
Create a new table named products with the following specifications:
product_id as INTEGER and primary key.
product_name as TEXT and not NULL.
list_price as DECIMAL (10, 2) and not NULL.
discount as DECIMAL (10, 2) with a default value of 0 and not NULL.
A CHECK constraint at the table level to ensure:
list_price is greater than or equal to discount
discount is greater than or equal to 0
list_price is greater than or equal to 0

```sql
CREATE TABLE products (
product_id INTEGER PRIMARY KEY,
product_name TEXT NOT NULL,
list_price DECIMAL(10,2) NOT NULL,
discount DECIMAL(10,2) NOT NULL DEFAULT 0,
CHECK(
    list_price >=discount
    AND discount >= 0
    AND list_price >= 0

)
);
```

**Output:**

<img width="1186" height="215" alt="image" src="https://github.com/user-attachments/assets/b4cb214b-4d8a-469f-9cf1-fa4e65b454f4" />



**Question 4**
---
Create a table named Tasks with the following columns:

TaskID as INTEGER
TaskName as TEXT
DueDate as DATE

```sql
CREATE TABLE Tasks (
TaskID INTEGER,
TaskName TEXT,
DueDate DATE

);
```

**Output:**
<img width="1183" height="305" alt="image" src="https://github.com/user-attachments/assets/bda0f80b-e7b2-438f-b548-11f12cb17fe0" />



**Question 5**
---
Create a table named Invoices with the following constraints:
InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
Amount as REAL should be greater than 0.
DueDate as DATE should be greater than the InvoiceDate.
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).

```sql
CREATE TABLE Invoices (
InvoiceID INTEGER PRIMARY KEY,
InvoiceDate DATE,
Amount REAL CHECK (Amount > 0),
DueDate DATE CHECK (Duedate > InvoiceDate),
OrderID INTEGER,
FOREIGN KEY (OrderId) REFERENCES Orders(OrderID)
);
```

**Output:**

<img width="1176" height="190" alt="image" src="https://github.com/user-attachments/assets/c06305c1-2c27-400b-9c70-bb624fe30b81" />



**Question 6**
---
In the Books table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

ISBN             Title                      Author           Publisher   Year
---------------  -------------------------  ---------------  ----------  ----------
978-1234567890   Introduction to AI         John Doe
978-9876543210   Deep Learning              Jane Doe         TechPress   2022
978-1122334455   Cybersecurity Essentials   Alice Smith                  2021

```sql
INSERT INTO Books (ISBN,Title,Author,Publisher,Year)
VALUES
('978-1234567890','Introduction to AI', 'John Doe', NULL,NULL),
('978-9876543210','Deep Learning', 'Jane Doe','TechPress','2022'),
('978-1122334455','Cybersecurity Essentials','Alice Smith',NULL,'2021');
```

**Output:**

<img width="1188" height="207" alt="image" src="https://github.com/user-attachments/assets/aa3bd338-a178-4e67-abc1-2d1d1f60259f" />



**Question 7**
---
Insert all customers from Old_customers into Customers

Table attributes are CustomerID, Name, Address, Email
```sql
INSERT INTO Customers (CustomerID, Name, Address, Email)
SELECT CustomerID,Name,Address,Email
FROM Old_customers; 
```

**Output:**

<img width="1182" height="196" alt="image" src="https://github.com/user-attachments/assets/db3de9e5-87ad-4b51-b08e-89c9e458e173" />



**Question 8**
---
Create a table named Reviews with the following columns:

ReviewID as INTEGER
ProductID as INTEGER
Rating as REAL
ReviewText as TEXT

```sql
CREATE TABLE Reviews (
ReviewID INTEGER,
ProductID INTEGER,
Rating REAL,
ReviewText TEXT
);
```

**Output:**

<img width="1198" height="328" alt="image" src="https://github.com/user-attachments/assets/b4ce5f4d-c3c2-4376-be5d-904744fdd350" />



**Question 9**
---
In the Student_details table, insert a student record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

RollNo      Name            Gender      Subject      MARKS
----------  ------------    ----------  ----------   ----------
205         Olivia Green    F
207         Liam Smith      M           Mathematics  85
208         Sophia Johnson  F           Science

```sql
INSERT INTO Student_details (RollNo,Name,Gender,Subject,MARKS)
VALUES
(205,'Olivia Green','F',NULL,NULL),
(207,'Liam Smith','M','Mathematic',85),
(208,'Sophia Johns','F','Science',NULL);
```

**Output:**

<img width="1212" height="224" alt="image" src="https://github.com/user-attachments/assets/da509c86-1f30-419a-aef5-1e63e70fdd15" />


**Question 10**
---
Write a SQL Query  to add attribute Date_of_joining as Date and rename the attribute job_title as Designation in the table 'Employees'

For example:

Test	Result
pragma table_info('Employees');
cid         name         type        notnull     dflt_value  pk
----------  -----------  ----------  ----------  ----------  ----------
0           employee_id  INT         0                       1
1           first_name   VARCHAR(50  0                       0
2           last_name    VARCHAR(50  0                       0
3           Designation  VARCHAR(10  0                       0
4           Date_of_joi  Date        0                       0


```sql
ALTER TABLE Employees
ADD COLUMN Date_of_joining Date;

ALTER TABLE Employees
RENAME COLUMN job_title TO Designation;
```

**Output:**

<img width="1197" height="268" alt="image" src="https://github.com/user-attachments/assets/64030e8f-b5d0-4251-9415-4ea21f07f1a7" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
