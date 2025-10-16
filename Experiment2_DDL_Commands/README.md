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
--Insert the below data into the Books table, allowing the Publisher and Year columns to take their default values.

ISBN             Title                 Author
---------------  --------------------  ---------------
978-6655443321   Big Data Analytics    Karen Adams

Note: The Publisher and Year columns will use their default values.
 
 
For example:

Test	Result
SELECT ISBN, Title, Author
FROM Books 


ISBN             Title                 Author
---------------  --------------------  ---------------
978-6655443321   Big Data Analytics    Karen Adams



```sql
INSERT INTO Books (ISBN, Title, Author)
VALUES ('978-6655443321', 'Big Data Analytics', 'Karen Adams');
```

**Output:**

<img width="1158" height="429" alt="image" src="https://github.com/user-attachments/assets/bb19d0fb-c8c5-4560-945d-05788714bfe5" />


**Question 2**
---
In the Student_details table, insert a student record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

RollNo      Name            Gender      Subject      MARKS
----------  ------------    ----------  ----------   ----------
205         Olivia Green    F
207         Liam Smith      M           Mathematics  85
208         Sophia Johnson  F           Science
For example:

Test	Result
select * from Student_details;
RollNo      Name          Gender      Subject     MARKS
----------  ------------  ----------  ----------  ----------
205         Olivia Green  F
207         Liam Smith    M           Mathematic  85
208         Sophia Johns  F           Science

```sql
-- 1. Insert record with some NULL values
INSERT INTO Student_details (RollNo, Name, Gender)
VALUES (205, 'Olivia Green', 'F');

-- 2. Insert record with all fields filled
INSERT INTO Student_details (RollNo, Name, Gender, Subject, Marks)
VALUES (207, 'Liam Smith', 'M', 'Mathematics', 85);

-- 3. Insert record with some filled and others NULL
INSERT INTO Student_details (RollNo, Name, Gender, Subject)
VALUES (208, 'Sophia Johnson', 'F', 'Science');
```

**Output:**

<img width="789" height="336" alt="image" src="https://github.com/user-attachments/assets/d66de856-69f6-48cd-9b64-8678ac909554" />


**Question 3**
---
Create a table named Invoices with the following constraints:

InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
DueDate as DATE should be greater than the InvoiceDate.
Amount as REAL should be greater than 0.
For example:

Test	Result
INSERT INTO Invoices (InvoiceID, InvoiceDate)
VALUES (1, '2024-08-08'),(1,'2024-09-08');
Error: UNIQUE constraint failed: Invoices.InvoiceID


```sql
CREATE TABLE Invoices (
  InvoiceID INTEGER PRIMARY KEY,
  InvoiceDate DATE,
  DueDate DATE CHECK (DueDate > InvoiceDate),
  Amount REAL CHECK (Amount > 0)
);
```

**Output:**

<img width="835" height="392" alt="image" src="https://github.com/user-attachments/assets/cd369dd8-809a-4eb3-a4b5-f25d29b1c866" />


**Question 4**
---
Create a table named Locations with the following columns:

LocationID as INTEGER
LocationName as TEXT
Address as TEXT
For example:

Test	Result
pragma table_info('Locations');
cid       name             type        notnull     dflt_value  pk
--------  ---------------  ----------  ----------  ----------  ----------
0         LocationID       INTEGER     0                       0
1         LocationName     TEXT        0                       0
2         Address          TEXT        0                       0


```sql
CREATE TABLE Locations (
    LocationID   INTEGER,
    LocationName TEXT,
    Address      TEXT
);
```

**Output:**

<img width="1159" height="487" alt="image" src="https://github.com/user-attachments/assets/2ab35612-ed34-4c65-ba10-986bcad9020a" />


**Question 5**
---
-- Write an SQL query to add two new columns, designation and net_salary, to the table Companies. The designation column should have a data type of varchar(50), and the net_salary column should have a data type of number.

 

 

For example:

Test	Result
pragma table_info('Companies');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          int         0                       0
1           name        varchar(50  0                       0
2           address     text        0                       0
3           email       varchar(50  0                       0
4           phone       varchar(10  0                       0
5           designatio  varchar(50  0                       0
6           net_salary  number      0                       0

```sql
ALTER TABLE Companies
ADD COLUMN designation varchar(50);

ALTER TABLE Companies
ADD COLUMN net_salary number;
```

**Output:**

<img width="1176" height="515" alt="image" src="https://github.com/user-attachments/assets/a7a84c93-6a88-4730-ae54-9abe9567fe64" />


**Question 6**
---
Insert all employees from Former_employees into Employee

Table attributes are EmployeeID, Name, Department, Salary

For example:

Test	Result
select * from Employee;
EmployeeID  Name        Department  Salary
----------  ----------  ----------  ----------
201         John Doe    HR          50000
202         Jane Smith  Engineerin  75000
203         Emily Davi  Marketing   60000

```sql
INSERT INTO Employee (EmployeeID, Name, Department, Salary)
SELECT EmployeeID, Name, Department, Salary
FROM Former_employees;
```

**Output:**

<img width="1151" height="394" alt="image" src="https://github.com/user-attachments/assets/8a84d89d-0b72-4d57-94fa-543deabcf022" />


**Question 7**
---
Write an SQL command can to add a column named email of type TEXT to the customers table

 

For example:

Test	Result
pragma table_info('Customers');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          integer     0                       0
1           name        text        0                       0
2           email       TEXT        0                       0


```sql
ALTER TABLE customers
ADD COLUMN email TEXT;
```

**Output:**

<img width="1153" height="363" alt="image" src="https://github.com/user-attachments/assets/df155873-efce-4bfa-8d08-4ad36191f0dd" />


**Question 8**
---
Create a table named Products with the following constraints:

ProductID should be the primary key.
ProductName should be NOT NULL.
Price is of real datatype and should be greater than 0.
Stock is of integer datatype and should be greater than or equal to 0.
For example:

Test	Result
INSERT INTO Products
VALUES (1, NULL,0,5);
Error: NOT NULL constraint failed: Products.ProductName

```sql
CREATE TABLE Products (
    ProductID    INTEGER PRIMARY KEY,
    ProductName  TEXT NOT NULL,
    Price        REAL,
    Stock        INTEGER,
    CHECK (Price > 0),
    CHECK (Stock >= 0)
);
```

**Output:**

<img width="1157" height="360" alt="image" src="https://github.com/user-attachments/assets/a198c6fb-db69-479e-a672-98339f70d1d2" />


**Question 9**
---
Create a new table named item with the following specifications and constraints:
item_id as TEXT and as primary key.
item_desc as TEXT.
rate as INTEGER.
icom_id as TEXT with a length of 4.
icom_id is a foreign key referencing com_id in the company table.
The foreign key should set NULL on updates and deletes.
item_desc and rate should not accept NULL.
For example:

Test	Result
INSERT INTO item VALUES("ITM5","Charlie Gold",700,"COM4");
UPDATE company SET com_id='COM5' WHERE com_id='COM4';
SELECT * FROM item;
item_id     item_desc     rate        icom_id
----------  ------------  ----------  ----------
ITM5        Charlie Gold  700

```sql
CREATE TABLE item (
    item_id    TEXT PRIMARY KEY,
    item_desc  TEXT NOT NULL,
    rate       INTEGER NOT NULL,
    icom_id    TEXT(4),
    FOREIGN KEY (icom_id) REFERENCES company(com_id)
        ON UPDATE SET NULL
        ON DELETE SET NULL
);
```

**Output:**

<img width="1207" height="448" alt="image" src="https://github.com/user-attachments/assets/89dd510c-0a82-42f7-bda9-bd2396ee59a3" />


**Question 10**
---
Create a table named ProjectAssignments with the following constraints:
AssignmentID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
ProjectID as INTEGER should be a foreign key referencing Projects(ProjectID).
AssignmentDate as DATE should be NOT NULL.
For example:

Test	Result
INSERT INTO ProjectAssignments (AssignmentID, EmployeeID, ProjectID, AssignmentDate) VALUES (2, 99, 1, '2024-01-03');
Error: FOREIGN KEY constraint failed

```sql
CREATE TABLE ProjectAssignments (
    AssignmentID    INTEGER PRIMARY KEY,
    EmployeeID      INTEGER,
    ProjectID       INTEGER,
    AssignmentDate  DATE NOT NULL,
    FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID),
    FOREIGN KEY (ProjectID) REFERENCES Projects(ProjectID)
);
```

**Output:**

<img width="1155" height="381" alt="image" src="https://github.com/user-attachments/assets/ddec57cf-af3e-422f-bd17-6e42ded3fb79" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
