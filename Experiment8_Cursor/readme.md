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

## Query:
```
SET SERVEROUTPUT ON;

DECLARE
    CURSOR emp_cursor IS
        SELECT first_name, job_id
        FROM HR.EMPLOYEES;

    v_emp_name HR.EMPLOYEES.FIRST_NAME%TYPE;
    v_designation HR.EMPLOYEES.JOB_ID%TYPE;
    v_count NUMBER := 0;

BEGIN
    OPEN emp_cursor;

    LOOP
        FETCH emp_cursor INTO v_emp_name, v_designation;

        EXIT WHEN emp_cursor%NOTFOUND;

        v_count := v_count + 1;

        DBMS_OUTPUT.PUT_LINE(
            'Employee Name: ' || v_emp_name ||
            ' | Designation: ' || v_designation
        );
    END LOOP;

    CLOSE emp_cursor;

    IF v_count = 0 THEN
        RAISE NO_DATA_FOUND;
    END IF;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('Error: No employee records found.');

    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE(
            'Unexpected Error: ' || SQLERRM
        );

        IF emp_cursor%ISOPEN THEN
            CLOSE emp_cursor;
        END IF;
END;
/
```

**Output:**  
<img width="381" height="316" alt="640676741-bd808b36-4858-439d-8318-46ff0855a26b" src="https://github.com/user-attachments/assets/10a4c866-cc6e-49f3-b0b9-146581968a26" />


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

## Query:
```
SET SERVEROUTPUT ON;

DECLARE
    -- Variables for salary range
    v_min_salary NUMBER := 5000;
    v_max_salary NUMBER := 15000;

    -- Variable to check whether records are found
    v_count NUMBER := 0;

    -- Parameterized cursor
    CURSOR emp_cursor(p_min_salary NUMBER, p_max_salary NUMBER) IS
        SELECT employee_id, first_name, last_name, job_id, salary
        FROM HR.EMPLOYEES
        WHERE salary BETWEEN p_min_salary AND p_max_salary;

    -- Variables to store employee details
    v_emp_id HR.EMPLOYEES.EMPLOYEE_ID%TYPE;
    v_first_name HR.EMPLOYEES.FIRST_NAME%TYPE;
    v_last_name HR.EMPLOYEES.LAST_NAME%TYPE;
    v_job_id HR.EMPLOYEES.JOB_ID%TYPE;
    v_salary HR.EMPLOYEES.SALARY%TYPE;

BEGIN
    OPEN emp_cursor(v_min_salary, v_max_salary);

    LOOP
        FETCH emp_cursor
        INTO v_emp_id, v_first_name, v_last_name, v_job_id, v_salary;

        EXIT WHEN emp_cursor%NOTFOUND;

        v_count := v_count + 1;

        DBMS_OUTPUT.PUT_LINE(
            'Employee ID: ' || v_emp_id ||
            ' | Name: ' || v_first_name || ' ' || v_last_name ||
            ' | Job: ' || v_job_id ||
            ' | Salary: ' || v_salary
        );
    END LOOP;

    CLOSE emp_cursor;

    -- Raise NO_DATA_FOUND if no employees are found
    IF v_count = 0 THEN
        RAISE NO_DATA_FOUND;
    END IF;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE(
            'Error: No employees found in the salary range ' ||
            v_min_salary || ' to ' || v_max_salary
        );

    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE(
            'Unexpected Error: ' || SQLERRM
        );

        IF emp_cursor%ISOPEN THEN
            CLOSE emp_cursor;
        END IF;
END;
/
```

**Output:**  
<img width="501" height="305" alt="640678046-62d12eb0-52a2-4c74-93f4-5c8a424b533c" src="https://github.com/user-attachments/assets/26572b0e-db95-442d-9a0c-f2e5523a9d52" />


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

## Query:
```
SET SERVEROUTPUT ON;

DECLARE
    v_count NUMBER := 0;

    -- Cursor FOR loop
    CURSOR emp_cursor IS
        SELECT first_name, last_name, department_id
        FROM HR.EMPLOYEES;

BEGIN
    FOR emp IN emp_cursor LOOP

        v_count := v_count + 1;

        DBMS_OUTPUT.PUT_LINE(
            'Employee Name: ' || emp.first_name || ' ' || emp.last_name ||
            ' | Department No: ' || emp.department_id
        );

    END LOOP;

    -- Raise NO_DATA_FOUND if no employees exist
    IF v_count = 0 THEN
        RAISE NO_DATA_FOUND;
    END IF;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE(
            'Error: No employees found in the database.'
        );

    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE(
            'Unexpected Error: ' || SQLERRM
        );
END;
/
```

**Output:**  
<img width="407" height="300" alt="640678996-3fd80ea8-82c4-4b56-bbde-b3ed665ec6c4" src="https://github.com/user-attachments/assets/4004c833-708e-4a3a-b84d-f9cb5f172373" />

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

## Query:
```
SET SERVEROUTPUT ON;

DECLARE
    -- Declare cursor
    CURSOR emp_cursor IS
        SELECT employee_id, first_name, last_name, job_id, salary
        FROM HR.EMPLOYEES;

    -- Declare record using %ROWTYPE
    v_emp emp_cursor%ROWTYPE;

    v_count NUMBER := 0;

BEGIN
    OPEN emp_cursor;

    LOOP
        FETCH emp_cursor INTO v_emp;

        EXIT WHEN emp_cursor%NOTFOUND;

        v_count := v_count + 1;

        DBMS_OUTPUT.PUT_LINE(
            'Employee ID: ' || v_emp.employee_id
        );

        DBMS_OUTPUT.PUT_LINE(
            'Employee Name: ' || v_emp.first_name || ' ' || v_emp.last_name
        );

        DBMS_OUTPUT.PUT_LINE(
            'Designation: ' || v_emp.job_id
        );

        DBMS_OUTPUT.PUT_LINE(
            'Salary: ' || v_emp.salary
        );

        DBMS_OUTPUT.PUT_LINE('-----------------------------');
    END LOOP;

    CLOSE emp_cursor;

    -- Check whether any records were fetched
    IF v_count = 0 THEN
        RAISE NO_DATA_FOUND;
    END IF;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE(
            'Error: No employees found in the database.'
        );

    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE(
            'Unexpected Error: ' || SQLERRM
        );

        IF emp_cursor%ISOPEN THEN
            CLOSE emp_cursor;
        END IF;
END;
/
```
**Output:**  
<img width="402" height="267" alt="640681169-16721d34-fb1f-45e8-ac09-5b6ecca48587" src="https://github.com/user-attachments/assets/0d198765-4386-4ccc-8ba4-ab9004df2097" />

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

## Query:
```
SET SERVEROUTPUT ON;

DECLARE
    v_dept_no NUMBER := 60;
    v_count NUMBER := 0;

    CURSOR emp_cursor IS
        SELECT employee_id, first_name, last_name, salary
        FROM HR.EMPLOYEES
        WHERE department_id = v_dept_no;

BEGIN
    FOR emp IN emp_cursor LOOP

        v_count := v_count + 1;

        DBMS_OUTPUT.PUT_LINE(
            'Employee ID: ' || emp.employee_id ||
            ' | Name: ' || emp.first_name || ' ' || emp.last_name ||
            ' | Salary: ' || emp.salary
        );

    END LOOP;

    IF v_count = 0 THEN
        RAISE NO_DATA_FOUND;
    END IF;

    DBMS_OUTPUT.PUT_LINE(
        'Employees found: ' || v_count
    );

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE(
            'Error: No employees found in department ' || v_dept_no
        );

    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE(
            'Unexpected Error: ' || SQLERRM
        );
END;
/
```
**Output:**  
<img width="432" height="285" alt="640683786-da478c44-5682-4509-9ee6-c19518dfd4af" src="https://github.com/user-attachments/assets/1e308212-306d-4011-97eb-85b9d545ea37" />


## Result:
Thus, the program successfully executed and displayed employee details using a cursor.

---

## RESULT
Thus, the program successfully executed and displayed employee details using a cursor. 

