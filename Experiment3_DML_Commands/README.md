# Experiment 3: DML Commands

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
--
Write a SQL statement to change the first_name column of employees table with 'John' for those employees whose department_id is 80 and gets a commission_pct below 0.35.

Employees table

---------------
employee_id
first_name
last_name
email
phone_number
hire_date
job_id
salary
commission_pct
manager_id
department_id
For example:

```sql
update employees
set first_name = 'John'
where department_id = 80
and commission_pct<0.35;
```

**Output:**

![Output1]![image](https://github.com/user-attachments/assets/94375e14-6e23-4da1-a33c-adcdad40e93e)


**Question 2**
---
Write a SQL statement to Double the salary for employees in department 20 who have a job_id ending with 'MAN'

Employees table

---------------
employee_id
first_name
last_name
email
phone_number
hire_date
job_id
salary
commission_pct
manager_id
department_id

```sql
update employees
set salary= salary * 2
where department_id = 20
and job_id LIKE '%MAN';
```

**Output:**

![Output2]![image](https://github.com/user-attachments/assets/e94762a8-ad0c-492f-9093-4c882dcc6471)


**Question 3**
---
Write a SQL statement to increase the salary of employees under the department 40, 90 and 110 according to the company rules.

Salary will be increased by 25% for the department 40, 15% for department 90 and 10% for the department 110 and the rest of the departments will remain same.

Employees table

---------------
employee_id
first_name
last_name
email
phone_number
hire_date
job_id
salary
commission_pct
manager_id
department_id

```sql
update employees
set salary=
case
    when department_id=40 then salary *1.25
    when department_id=90 then salary *1.15
    when department_id=110 then salary *1.10
    else salary
end    
```

**Output:**

![Output3]![image](https://github.com/user-attachments/assets/bd8cc915-6990-44dd-aea7-30de9d795741)


**Question 4**
---
Write a SQL statement to Update the per_unit_price to 25 and total_price accordingly in purchases table where purchase_date is '2022-08-15' and product_id is 12.

```sql
update purchases
set per_unit_price=25,
total_price=quantity*25
where purchase_date='2022-08-15'
and product_id = 12;
```

**Output:**

![Output4]![image](https://github.com/user-attachments/assets/19932988-8e73-46e6-a2ba-0b45564a424c)


**Question 5**
---
Write a SQL statement to Increase the selling price by 10% for all products in the 'Bakery' category in the products table.

Products table

---------------
product_id
product_name
category
cost_price
sell_price
reorder_lvl
quantity
supplier_id
Answer:(penalty

```sql
update products
set sell_price=sell_price*1.10
where category='Bakery'
```

**Output:**

![Output5]![image](https://github.com/user-attachments/assets/c10e6f3e-e7fc-4b85-aa79-a221edaadbf2)


**Question 6**
---
Write a SQL query to Delete customers with 'GRADE' 3 or 'AGENT_CODE' 'A008' whose 'OUTSTANDING_AMT' is less than 5000

Sample table: Customer

```sql
delete from customer
where (GRADE=3 OR AGENT_CODE='A008')
AND OUTSTANDING_AMT<5000;
```

**Output:**

![Output6]![image](https://github.com/user-attachments/assets/6a71fdcd-2ecb-4a1e-a1ea-7f2a32bdf8ae)


**Question 7**
---
Write a SQL query to Delete customers from 'customer' table where 'CUST_NAME' contains the substring 'Holmes'.

Sample table: Customer

```sql
DELETE FROM Customer
WHERE CUST_NAME LIKE'%Holmes%';
```

**Output:**

![Output7]![image](https://github.com/user-attachments/assets/d3a55e8a-6209-4d3e-aa23-1454b5e75f2a)


**Question 8**
---
Write a SQL query to delete a doctor from Doctors table whose Specialization is 'Pediatrics' and First name is 'Michael'.

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization

```sql
DELETE FROM Doctors
WHERE specialization='Pediatrics'
AND First_name = 'Michael';
```

**Output:**

![Output8]![image](https://github.com/user-attachments/assets/acec2d50-eb02-435f-9b28-841936a58fde)


**Question 9**
---
Write a SQL query to Delete customers with 'CUST_COUNTRY' 'UK' and 'WORKING_AREA' 'London' whose 'GRADE' is less than 3

Sample table: Customer

```sql
DELETE FROM Customer 
where CUST_COUNTRY='UK'
and WORKING_AREA= 'London'
and GRADE<3;
```

**Output:**

![Output9]![image](https://github.com/user-attachments/assets/dc3f579d-8af1-4730-86df-cb4f451e0ba2)


**Question 10**
---
Write a SQL query to Delete customers with 'GRADE' 3 and whose 'CUST_NAME' contains the substring 'BBB', and 'PAYMENT_AMT' is greater than 2000

Sample table: Customer

```sql
delete from Customer
where GRADE=3
and CUST_NAME like '%BBB%'
AND PAYMENT_AMT > 2000;
```

**Output:**

![Output10]![image](https://github.com/user-attachments/assets/35b84411-6b60-49db-b77a-69a047f3a465)


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
