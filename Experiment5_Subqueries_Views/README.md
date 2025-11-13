# Experiment 5: Subqueries and Views

## AIM
To study and implement subqueries and views.

## THEORY

### Subqueries
A subquery is a query inside another SQL query and is embedded in:
- WHERE clause
- HAVING clause
- FROM clause

**Types:**
- **Single-row subquery**:
  Sub queries can also return more than one value. Such results should be made use along with the operators in and any.
- **Multiple-row subquery**:
  Here more than one subquery is used. These multiple sub queries are combined by means of ‘and’ & ‘or’ keywords.
- **Correlated subquery**:
  A subquery is evaluated once for the entire parent statement whereas a correlated Sub query is evaluated once per row processed by the parent statement.

**Example:**
```sql
SELECT * FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```
### Views
A view is a virtual table based on the result of an SQL SELECT query.
**Create View:**
```sql
CREATE VIEW view_name AS
SELECT column1, column2 FROM table_name WHERE condition;
```
**Drop View:**
```sql
DROP VIEW view_name;
```

**Question 1**
--
From the following tables, write a SQL query to find all the orders generated in New York city. Return ord_no, purch_amt, ord_date, customer_id and salesman_id.

SALESMAN TABLE

|name|               type|
|----| ----------|
|salesman_id | numeric(5)|
|name   |          varchar(30)|
|city      |           varchar(15)|
|commission|   decimal(5,2)|

ORDERS TABLE

|name |           type|
|----|      ----------|
|ord_no |         int|
|purch_amt  |  real|
|ord_date |      text|
|customer_id|  int|
|salesman_id|  int|

```sql
SELECT ord_no, 
       purch_amt, 
       ord_date, 
       customer_id, 
       salesman_id
FROM ORDERS 

where salesman_id in(select salesman_id from SALESMAN
WHERE city = 'New York');

```

**Output:**

<img width="1206" height="511" alt="image" src="https://github.com/user-attachments/assets/3d7eeff7-7ac2-4bb4-a64f-c5d43ee3d77c" />

**Question 2**
---
Write a query to display all the customers whose ID is the difference between the salesperson ID of Mc Lyon and 2001.

salesman table

|name|  type|
|-----|-----|
|salesman_id |     numeric(5)|
|name    |             varchar(30)|
|city    |                varchar(15)|
|commission |      decimal(5,2)|

customer table

|name |        type|
|-----|--------|
|customer_id|  int|
|cust_name |   text|
|city  |       text|
|grade |       int|
|salesman_id | int|
 
```sql
SELECT *
FROM customer
WHERE customer_id = (
    (SELECT salesman_id FROM salesman WHERE name = 'Mc Lyon') - 2001);

```

**Output:**

<img width="1209" height="357" alt="image" src="https://github.com/user-attachments/assets/4613e74d-37c9-42c8-87d7-337e137834db" />


**Question 3**
---
Write a SQL query to Retrieve the medications with dosages equal to the lowest dosage

Table Name: Medications (attributes: medication_id, medication_name, dosage)

```sql
SELECT *
FROM Medications
WHERE dosage = (
    SELECT MIN(dosage)
    FROM Medications
);

```

**Output:**

<img width="929" height="436" alt="image" src="https://github.com/user-attachments/assets/fe063361-e34e-4668-967f-19c3541ad252" />


**Question 4**
---
From the following tables write a SQL query to count the number of customers with grades above the average in New York City. Return grade and count.

```sql
SELECT grade, COUNT(*) 
FROM customer
WHERE grade > (
      SELECT AVG(grade)
      FROM customer
      where city = 'New York'
  )
GROUP BY grade;

```

**Output:**

<img width="697" height="375" alt="image" src="https://github.com/user-attachments/assets/378b684b-0da2-4fb0-826d-227e0b7237f2" />


**Question 5**
---
Write a SQL query that retrieves the names of students and their corresponding grades, where the grade is equal to the minimum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)

```sql
SELECT student_name, grade
FROM Grades g
WHERE grade = (
    SELECT MIN(grade)
    FROM Grades
    WHERE subject = g.subject
);


```

**Output:**

<img width="965" height="479" alt="image" src="https://github.com/user-attachments/assets/49cfe2a4-2850-4940-8855-afb8e2b841af" />


**Question 6**
---
Write a SQL query that retrieves the all the columns from the Table Grades, where the grade is equal to the minimum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)

```sql
SELECT *
FROM Grades g
WHERE grade = (
    SELECT MIN(grade)
    FROM Grades
    WHERE subject = g.subject
);

```

**Output:**

<img width="1276" height="488" alt="image" src="https://github.com/user-attachments/assets/9cd2ddaf-c338-4c57-8e7c-2a64f937abf8" />


**Question 7**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is LESS than $2500.

```sql
SELECT *
FROM Customers
WHERE Salary < 2500;

```

**Output:**

<img width="1164" height="487" alt="image" src="https://github.com/user-attachments/assets/3d6670fb-e018-439a-b273-3bb5be7f1ad2" />


**Question 8**
---
From the following tables write a SQL query to find all orders generated by New York-based salespeople. Return ord_no, purch_amt, ord_date, customer_id, salesman_id.

salesman table

|name |type|
|-----|----|
|salesman_id |     numeric(5)|
|name  |               varchar(30)|
|city   |                 varchar(15)|
|commission   |    decimal(5,2)|

orders table

|name| type|
|----|----|
|order_no |        int|
|purch_amt  |      real|
|order_date  |     text|
|customer_id |     int|
|salesman_id  |    int|
 

```sql
SELECT ord_no,purch_amt,ord_date,customer_id,salesman_id from orders
where salesman_id in(select salesman_id from salesman
where city = 'New York');

```

**Output:**

<img width="1186" height="503" alt="image" src="https://github.com/user-attachments/assets/307aed34-b064-4b7f-b763-945a7579d9d4" />


**Question 9**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is greater than $4500.

```sql
SELECT *
FROM Customers
WHERE Salary > 4500;

```

**Output:**

<img width="1135" height="462" alt="image" src="https://github.com/user-attachments/assets/80b8bf97-4c99-47dd-804a-2d69d8bda42c" />


**Question 10**
---
Write a SQL query that retrieve all the columns from the table "Grades", where the grade is equal to the maximum grade achieved in each subject.
```sql
SELECT *
FROM Grades g
WHERE grade = (
    SELECT MAX(grade)
    FROM Grades
    WHERE subject = g.subject
);


```

**Output:**

<img width="1290" height="482" alt="image" src="https://github.com/user-attachments/assets/54b4e80d-f12f-42b0-a38d-04f3b01cf527" />



## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
