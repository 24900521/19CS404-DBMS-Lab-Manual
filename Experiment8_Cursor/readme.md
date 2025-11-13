# Experiment 8: PL/SQL Cursor Programs

## AIM
To write and execute PL/SQL programs using cursors and exception handling to manage runtime errors effectively and display appropriate messages.

## THEORY

In PL/SQL, cursors are used to handle query result sets row-by-row. 

There are two types of cursors:

- Implicit Cursors: Automatically created by PL/SQL for single-row queries.
- Explicit Cursors: Declared and controlled by the programmer for multi-row queries.

Types of Explicit Cursors:

1. Simple Cursor: Basic cursor to iterate over multiple rows.

2. Parameterized Cursor: Accepts parameters to filter the result dynamically.

3. Cursor FOR Loop: Simplifies cursor operations (open, fetch, close).

4. %ROWTYPE Cursor: Fetches entire row into a record using %ROWTYPE.

5. Cursor with FOR UPDATE: Used for row-level locking and updating the rows while looping.

**Syntax:**
```sql
DECLARE 
   <declarations section> 
BEGIN 
   <executable command(s)>
EXCEPTION 
   <exception handling> 
END;
```

### Basic Components of PL/SQL Block:

- DECLARE: Section to declare variables and constants.
- BEGIN: The execution section that contains PL/SQL statements.
- EXCEPTION: Handles errors or exceptions that occur in the program.
- END: Marks the end of the PL/SQL block.

**Exception Handling**

PL/SQL provides a robust mechanism to handle runtime errors using exception handling blocks. When an error occurs during execution, control is passed to the EXCEPTION section, where specific or general errors can be handled gracefully.

### Components of Exception Handling:
- Predefined Exceptions: Automatically raised by PL/SQL for common errors (e.g., NO_DATA_FOUND, TOO_MANY_ROWS, ZERO_DIVIDE).
- User-defined Exceptions: Declared explicitly in the declaration section using the EXCEPTION keyword.
- WHEN OTHERS: A generic handler for all exceptions not handled explicitly.

```sql
BEGIN
   -- Statements
EXCEPTION
   WHEN exception_name THEN
      -- Handling code
   WHEN OTHERS THEN
      -- Handling for unknown errors
END;
```

### **Question 1: Simple Cursor with Exception Handling**

**Write a PL/SQL program using a simple cursor to fetch employee names and designations from the `employees` table. Implement exception handling for the following cases:**

1. **NO_DATA_FOUND**: When no rows are fetched.
2. **OTHERS**: Any other unexpected errors during execution.

**Steps:**

- Create an `employees` table with fields `emp_id`, `emp_name`, and `designation`.
- Insert some sample data into the table.
- Use a simple cursor to fetch and display employee names and designations.
- Implement exception handling to catch the relevant exceptions and display appropriate messages.
# Program
```sql
SET SERVEROUTPUT ON;

DECLARE
    CURSOR emp_cursor IS
        SELECT first_name || ' ' || last_name AS emp_name, job_id AS designation
        FROM hr.employees;

    v_name hr.employees.first_name%TYPE;
    v_designation hr.employees.job_id%TYPE;
    v_count NUMBER := 0;

BEGIN
    FOR rec IN emp_cursor LOOP
        v_count := v_count + 1;
        DBMS_OUTPUT.PUT_LINE('Employee Name: ' || rec.emp_name || ' | Designation: ' || rec.designation);
    END LOOP;

    IF v_count = 0 THEN
        RAISE NO_DATA_FOUND;
    END IF;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No employee records found.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('An unexpected error occurred: ' || SQLERRM);
END;
/
```
**Output:**  
The program should display the employee details or an error message.

<img width="749" height="266" alt="image" src="https://github.com/user-attachments/assets/71761dd5-02fc-4c55-b1d9-04b4df2cc6fa" />


---

### **Question 2: Parameterized Cursor with Exception Handling**

**Write a PL/SQL program using a parameterized cursor to retrieve and display employees with a salary in a given range. Implement exception handling for the following errors:**

1. **NO_DATA_FOUND**: When no employees meet the salary criteria.
2. **OTHERS**: For any unexpected errors during the execution.

**Steps:**

- Modify the `employees` table by adding a `salary` column.
- Insert sample salary values for the employees.
- Use a parameterized cursor to accept a salary range as input and fetch employees within that range.
- Implement exception handling to catch and display relevant error messages.

# program
```sql
SET SERVEROUTPUT ON;

DECLARE
    CURSOR emp_cursor(p_min_sal NUMBER, p_max_sal NUMBER) IS
        SELECT first_name || ' ' || last_name AS emp_name, salary
        FROM hr.employees
        WHERE salary BETWEEN p_min_sal AND p_max_sal;

    v_count NUMBER := 0;

BEGIN
    FOR rec IN emp_cursor(5000, 10000) LOOP
        v_count := v_count + 1;
        DBMS_OUTPUT.PUT_LINE('Employee Name: ' || rec.emp_name || ' | Salary: ' || rec.salary);
        EXIT WHEN v_count = 3;
    END LOOP;

    IF v_count = 0 THEN
        RAISE NO_DATA_FOUND;
    END IF;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No employees found in the specified salary range.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('An unexpected error occurred: ' || SQLERRM);
END;
/
```
**Output:**  
The program should display the employee details within the specified salary range or an error message if no data is found.
<img width="575" height="107" alt="image" src="https://github.com/user-attachments/assets/a0b458a1-8b29-458d-b03d-9a0860fca7da" />

---

### **Question 3: Cursor FOR Loop with Exception Handling**

**Write a PL/SQL program using a cursor FOR loop to retrieve and display all employee names and their department numbers from the `employees` table. Implement exception handling for the following cases:**

1. **NO_DATA_FOUND**: If no employees are found in the database.
2. **OTHERS**: For any other unexpected errors.

**Steps:**

- Modify the `employees` table by adding a `dept_no` column.
- Insert sample department numbers for employees.
- Use a cursor FOR loop to fetch and display employee names along with their department numbers.
- Implement exception handling to catch the relevant exceptions.
# Program
```sql
SET SERVEROUTPUT ON;

DECLARE
    v_count NUMBER := 0;

BEGIN
    FOR rec IN (SELECT first_name || ' ' || last_name AS emp_name, department_id AS dept_no 
                FROM hr.employees) LOOP
        v_count := v_count + 1;
        DBMS_OUTPUT.PUT_LINE('Employee Name: ' || rec.emp_name || ' | Department No: ' || rec.dept_no);
        EXIT WHEN v_count = 3;
    END LOOP;

    IF v_count = 0 THEN
        RAISE NO_DATA_FOUND;
    END IF;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No employees found in the database.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('An unexpected error occurred: ' || SQLERRM);
END;
/
```
**Output:**  
The program should display employee names with their department numbers or the appropriate error message if no data is found.
<img width="475" height="93" alt="image" src="https://github.com/user-attachments/assets/f06c2d44-49bc-42cb-b574-a634254243b3" />

---

### **Question 4: Cursor with `%ROWTYPE` and Exception Handling**

**Write a PL/SQL program that uses a cursor with `%ROWTYPE` to fetch and display complete employee records (emp_id, emp_name, designation, salary). Implement exception handling for the following errors:**

1. **NO_DATA_FOUND**: When no employees are found in the database.
2. **OTHERS**: For any other errors that occur.

**Steps:**

- Modify the `employees` table by adding `emp_id`, `emp_name`, `designation`, and `salary` fields.
- Insert sample data into the `employees` table.
- Declare a cursor using `%ROWTYPE` to fetch complete rows from the `employees` table.
- Implement exception handling to catch the relevant exceptions and display appropriate messages.
# Program
```sql
SET SERVEROUTPUT ON;

DECLARE
    CURSOR emp_cursor IS
        SELECT employee_id AS emp_id,
               first_name || ' ' || last_name AS emp_name,
               job_id AS designation,
               salary
        FROM hr.employees;

    emp_record emp_cursor%ROWTYPE;
    v_count NUMBER := 0;

BEGIN
    OPEN emp_cursor;
    LOOP
        FETCH emp_cursor INTO emp_record;
        EXIT WHEN emp_cursor%NOTFOUND;

        v_count := v_count + 1;
        DBMS_OUTPUT.PUT_LINE('Emp ID: ' || emp_record.emp_id ||
                             ' | Name: ' || emp_record.emp_name ||
                             ' | Designation: ' || emp_record.designation ||
                             ' | Salary: ' || emp_record.salary);

        EXIT WHEN v_count = 3;
    END LOOP;
    CLOSE emp_cursor;

    IF v_count = 0 THEN
        RAISE NO_DATA_FOUND;
    END IF;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No employee records found in the database.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('An unexpected error occurred: ' || SQLERRM);
END;
/

```
**Output:**  
The program should display employee records or the appropriate error message if no data is found.
<img width="651" height="85" alt="image" src="https://github.com/user-attachments/assets/40c6a022-c75b-4c6c-b4b8-ba6ef2144848" />

---

### **Question 5: Cursor with FOR UPDATE Clause and Exception Handling**

**Write a PL/SQL program using a cursor with the `FOR UPDATE` clause to update the salary of employees in a specific department. Implement exception handling for the following cases:**

1. **NO_DATA_FOUND**: If no rows are affected by the update.
2. **OTHERS**: For any unexpected errors during execution.

**Steps:**

- Modify the `employees` table to include a `dept_no` and `salary` field.
- Insert sample data into the `employees` table with different department numbers.
- Use a cursor with the `FOR UPDATE` clause to lock the rows of employees in a specific department and update their salary.
- Implement exception handling to handle `NO_DATA_FOUND` or other errors that may occur.
# program
```sql
SET SERVEROUTPUT ON;

DECLARE
    CURSOR emp_cursor IS
        SELECT employee_id, salary, department_id
        FROM hr.employees
        WHERE department_id = 60;

    v_count NUMBER := 0;

BEGIN
    FOR rec IN emp_cursor LOOP
        v_count := v_count + 1;

        DBMS_OUTPUT.PUT_LINE('Employee ID: ' || rec.employee_id ||
                             ' | Old Salary: ' || rec.salary ||
                             ' | New Salary (after +1000): ' || (rec.salary + 1000));

        EXIT WHEN v_count = 3;
    END LOOP;

    IF v_count = 0 THEN
        RAISE NO_DATA_FOUND;
    END IF;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No employees found in the specified department.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('An unexpected error occurred: ' || SQLERRM);
END;
/

```
**Output:**  
The program should update employee salaries and display a message, or it should display an error message if no data is found.
<img width="614" height="96" alt="image" src="https://github.com/user-attachments/assets/718d1836-b701-454f-ac71-7e97d16b9607" />

---

## RESULT
Thus, the program successfully executed and displayed employee details using a cursor. 

