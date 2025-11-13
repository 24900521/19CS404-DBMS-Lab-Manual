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
Write an SQL query to retrieve all columns from the 'customer' table (aliased as 'c') using a LEFT JOIN with the 'orders' table on the 'customer_id' column, and filter the results to include only those orders placed between '2012-07-01' and '2012-07-30'.

'customer' Table: (customer_id, cust_name, city, grade, salesman_id)

'orders' Table: (ord_no, purch_amt, ord_date, customer_id, salesman_id)

```sql
select c.*
from customer c
left join orders o
on c.customer_id=o.customer_id
where o.ord_date between '2012-07-01' and '2012-07-30';
```

**Output:**

<img width="1699" height="498" alt="image" src="https://github.com/user-attachments/assets/a5e43980-8323-4b98-8565-2e92950cf58b" />


**Question 2**
---
Write a SQL statement to make a report with customer name, city, order number, order date, and order amount in ascending order according to the order date to determine whether any of the existing customers have placed an order or not.

```sql
select c.cust_name,c.city,o.ord_no,o.ord_date,o.purch_amt as "Order Amount"
from customer c
left join orders o
on c.customer_id=o.customer_id
order by o.ord_date asc;
```

**Output:**

<img width="1236" height="863" alt="image" src="https://github.com/user-attachments/assets/416c6b59-374c-4763-ab37-465d81bf7937" />

**Question 3**
---
write a SQL query to find the salesperson and customer who reside in the same city. Return Salesman, cust_name and city.

```sql
select s.name as "Salesman",c.cust_name,c.city
from salesman s
inner join customer c
on c.city=s.city;
```

**Output:**

<img width="927" height="532" alt="image" src="https://github.com/user-attachments/assets/3c40ecc4-c2f1-487c-88fc-f6fb0095284f" />


**Question 4**
---
Write the SQL query that achieves the selection of all columns from the "patients" table (aliased as "p"), with an inner join on the "patient_id" column and a condition filtering for test results with a test date between '2024-03-01' and '2024-03-31'.

```sql
SELECT p.*
FROM PATIENTS  p
INNER JOIN test_results t
ON p.patient_id = t.patient_id
WHERE t.test_date BETWEEN '2024-03-01' AND '2024-03-31';

```

**Output:**

<img width="1587" height="354" alt="image" src="https://github.com/user-attachments/assets/ae75879c-a4bc-49fd-b040-ce4a1a4a8277" />

**Question 5**
---
Write the SQL query that achieves the selection of the first name from the "patients" table and all columns from the "surgeries" table, with an inner join on the "patient_id" column and a condition filtering for patients with a date of birth after '1990-01-01'.
```sql
SELECT p.first_name, 
       s.*
FROM patients p
INNER JOIN surgeries s
ON p.patient_id = s.patient_id
WHERE p.date_of_birth > '1990-01-01';

```

**Output:**

<img width="1811" height="527" alt="image" src="https://github.com/user-attachments/assets/e8e8801f-0377-4316-a741-9dde74da4b0a" />


**Question 6**
---
write a SQL query to locate those salespeople who do not live in the same city where their customers live and have received a commission of more than 12% from the company. Return Customer Name, customer city, Salesman, salesman city, commission.  



```sql
SELECT c.cust_name AS "Customer Name",
       c.city AS "city",
       s.name AS "Salesman",
       s.city AS "city",
       s.commission
FROM customer c
JOIN salesman s
ON c.salesman_id = s.salesman_id
WHERE c.city <> s.city
  AND s.commission > 0.12;

```

**Output:**
<img width="1784" height="765" alt="image" src="https://github.com/user-attachments/assets/9a832c66-bbe0-4e99-8500-56b19737fdf1" />


**Question 7**
---
Write the SQL query that achieves the selection of the "nurse_id" from the "nurses" table (aliased as "n") and the "department_name" from the "departments" table, with an inner join on the "department_id" column and conditions filtering for a nurse with the first name 'David' and last name 'Moore'.

```sql
SELECT n.nurse_id, 
       d.department_name
FROM nurses n
INNER JOIN departments d
ON n.department_id = d.department_id
WHERE n.first_name = 'David'
  AND n.last_name = 'Moore';

```

**Output:**

<img width="943" height="524" alt="image" src="https://github.com/user-attachments/assets/dda1fc93-ae4d-4da9-a9ea-4dd069f98d7b" />


**Question 8**
---
Write the SQL query that achieves the selection of the "cust_name" column from the "customer" table (aliased as "c"), with a left join on the "customer_id" column and a condition filtering for orders with a purchase amount less than 100.

'customer' Table: (customer_id, cust_name, city, grade, salesman_id)

'orders' Table: (ord_no, purch_amt, ord_date, customer_id, salesman_id)

```sql
SELECT c.cust_name
FROM customer c
LEFT JOIN orders o
ON c.customer_id = o.customer_id
WHERE o.purch_amt < 100;

```

**Output:**

<img width="714" height="589" alt="image" src="https://github.com/user-attachments/assets/c0c9f670-d97a-4dd2-8bcd-a2ad1c401741" />


**Question 9**
---
Write the SQL query that achieves the selection of all columns from the "customer" table (aliased as "c"), with a left join on the "salesman_id" column and a condition filtering for salesman with the name 'Mc Lyon'.

Customer Table: (customer_id, cust_name, city, grade, salesman_id)

Salesman Table: (salesman_id, name, city, commission)

```sql
select c.*
from Customer c
left join Salesman s on c.salesman_id=s.salesman_id
where s.name='Mc Lyon';
```

**Output:**

<img width="1411" height="414" alt="image" src="https://github.com/user-attachments/assets/38f035eb-4758-446e-af6d-8d7d5ef9323b" />


**Question 10**
---
Write the SQL query that achieves the selection of all columns from the "test_results" table (aliased as "t"), with an inner join on the "patient_id" column and a condition filtering for patients with the first name 'Alice'.

```sql
select t.*
from test_results t
inner join PATIENTS p
on t.patient_id=p.patient_id
where p.first_name='Alice';
```

**Output:**

<img width="1390" height="418" alt="image" src="https://github.com/user-attachments/assets/40a32528-2142-43d7-87d0-09620cc1781e" />



## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
