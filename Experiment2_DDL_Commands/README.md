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
For example:

Test	Result
INSERT INTO item VALUES("ITM5","Charlie Gold",700,"COM4");
UPDATE company SET com_id='COM5' WHERE com_id='COM4';
SELECT * FROM item;
item_id     item_desc     rate        icom_id
----------  ------------  ----------  ----------
ITM5        Charlie Gold  700


-- Paste Question 1 here

```sql
CREATE TABLE item (
    item_id   TEXT PRIMARY KEY,
    item_desc TEXT NOT NULL,
    rate      INTEGER NOT NULL,
    icom_id   TEXT CHECK (length(icom_id) = 4),
    FOREIGN KEY (icom_id) REFERENCES company(com_id)
        ON UPDATE SET NULL
        ON DELETE SET NULL
);
```

**Output:**
<img width="1232" height="445" alt="image" src="https://github.com/user-attachments/assets/272afa3f-b9a6-429c-8d4d-6109ae13fe6f" />


**Question 2**
---
Write a SQL query to Add a new column named "discount" with the data type DECIMAL(5,2) to the "customer" table.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
 

For example:

Test	Result
pragma table_info('customer');
cid         name         type                               notnull     dflt_value  pk
----------  -----------  ---------------------------------  ----------  ----------  ----------
0           customer_id  integer primarykey auto increment  0                       0
1           cust_name    varchar2(30)                       0                       0
2           city         varchar(30)                        0                       0
3           grade        number                             0                       0
4           salesman_id  number                             0                       0
5           discount     DECIMAL(5,2)                       0                       0


```sql
ALTER TABLE customer
ADD COLUMN discount DECIMAL(5,2);
```

**Output:**
<img width="1233" height="453" alt="image" src="https://github.com/user-attachments/assets/4e9daf34-41fa-4202-8d95-8a3be6bd3814" />


**Question 3**
---
Write a SQL Query to add an attribute designation in the employee table with the data type VARCHAR(50).

For example:

Test	Result
pragma table_info('employee');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          integer     0                       0
1           salary      number      0                       0
2           designatio  varchar(50  0                       0

```sql
ALTER TABLE employee
ADD COLUMN designation varchar(50);
```

**Output:**
<img width="1231" height="375" alt="image" src="https://github.com/user-attachments/assets/1485d449-7320-4f43-898c-a9d0473a70d6" />


**Question 4**
---
Create a table named Orders with the following columns:

OrderID as INTEGER
OrderDate as TEXT
CustomerID as INTEGER
For example:

Test	Result
pragma table_info('Orders');
cid   name        type        notnull     dflt_value  pk
----  ----------  ----------  ----------  ----------  ----------
0     OrderID     INTEGER     0                       0
1     OrderDate   TEXT        0                       0
2     CustomerID  INTEGER     0                       0

```sql
CREATE TABLE Orders (
    OrderID    INTEGER,
    OrderDate  TEXT,
    CustomerID INTEGER
);
```

**Output:**
<img width="1228" height="470" alt="image" src="https://github.com/user-attachments/assets/ca00617e-36bc-431b-b009-a1133464883f" />


**Question 5**
---
Insert a customer with CustomerID 301, Name Michael Jordan, Address 123 Maple St, City Chicago, and ZipCode 60616 into the Customers table.

For example:

Test	Result
SELECT * FROM Customers WHERE CustomerID = 301;
CustomerID  Name            Address       City        ZipCode
----------  --------------  ------------  ----------  ----------
301         Michael Jordan  123 Maple St  Chicago     60616


```sql
INSERT INTO Customers (CustomerID, Name, Address, City, ZipCode)
VALUES (301, 'Michael Jordan', '123 Maple St', 'Chicago', 60616);
```

**Output:**
<img width="1233" height="316" alt="image" src="https://github.com/user-attachments/assets/40581703-5f8e-4284-96ff-ccec0023c858" />


**Question 6**
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
INSERT INTO Student_details (RollNo, Name, Gender)
VALUES (205, 'Olivia Green', 'F');

INSERT INTO Student_details (RollNo, Name, Gender, Subject, MARKS)
VALUES (207, 'Liam Smith', 'M', 'Mathematics', 85);

INSERT INTO Student_details (RollNo, Name, Gender, Subject)
VALUES (208, 'Sophia Johnson', 'F', 'Science');
```

**Output:**
<img width="1231" height="356" alt="image" src="https://github.com/user-attachments/assets/a424a3ff-278f-427c-8d1d-fdae95bdbf8b" />


**Question 7**
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
    InvoiceID   INTEGER PRIMARY KEY,
    InvoiceDate DATE,
    DueDate     DATE CHECK (DueDate > InvoiceDate),
    Amount      REAL CHECK (Amount > 0)
);
```

**Output:**
<img width="1236" height="373" alt="image" src="https://github.com/user-attachments/assets/d88b2d2a-f177-4e66-b6c7-21272c87ce96" />


**Question 8**
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
<img width="1237" height="503" alt="image" src="https://github.com/user-attachments/assets/a8a3b8fb-cbe6-4654-a432-c96c7d2e0026" />


**Question 9**
---
Create a table named Employees with the following constraints:

EmployeeID should be the primary key.
FirstName and LastName should be NOT NULL.
Email should be unique.
Salary should be greater than 0.
DepartmentID should be a foreign key referencing the Departments table.
For example:

Test	Result
-- Attempt to insert a record with NULL FirstName
INSERT INTO Employees (EmployeeID, FirstName, LastName, Email, Salary, DepartmentID)
VALUES (1, NULL, 'Doe', 'john.doe@example.com', 50000, 1);
Error: NOT NULL constraint failed: Employees.FirstName

```sql
CREATE TABLE Employees (
    EmployeeID   INTEGER PRIMARY KEY,
    FirstName    TEXT NOT NULL,
    LastName     TEXT NOT NULL,
    Email        TEXT UNIQUE,
    Salary       REAL CHECK (Salary > 0),
    DepartmentID INTEGER,
    FOREIGN KEY (DepartmentID) REFERENCES Departments(DepartmentID)
);

```

**Output:**
<img width="1234" height="512" alt="image" src="https://github.com/user-attachments/assets/07901a62-7f2b-4e56-a379-8b6289fcf16e" />


**Question 10**
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
For example:

Test	Result
INSERT INTO products (product_id, product_name, list_price) VALUES (2, 'Product B', 50.00);
SELECT * FROM products;
product_id  product_name  list_price  discount
----------  ------------  ----------  ----------
2           Product B     50          0


```sql
CREATE TABLE products (
    product_id   INTEGER PRIMARY KEY,
    product_name TEXT NOT NULL,
    list_price   DECIMAL(10,2) NOT NULL,
    discount     DECIMAL(10,2) NOT NULL DEFAULT 0,
    CHECK (
        list_price >= discount
        AND discount >= 0
        AND list_price >= 0
    )
);
```

**Output:**

<img width="1227" height="370" alt="image" src="https://github.com/user-attachments/assets/c7bcd892-6194-4c46-8357-ac982b4bef5e" />


## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
