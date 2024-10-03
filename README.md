# Employment Management System

### Introduction

The Employment Management System is a database-driven application designed to efficiently manage and organize employee information within an organization. This system provides a robust framework for handling essential data related to employees, departments, and job titles, facilitating easy retrieval and manipulation of records.

### 1. Conceptual Diagram

![image alt](https://github.com/Manzidarius/oracle-sql-tests/blob/d931bebf92854a466896dca0e449105275ed74c9/Screenshot%202024-10-03%20091020.png)

### 2. Create the Tables in SQL

```sql
-- Create the Departments table
CREATE TABLE Departments (
    department_id NUMBER PRIMARY KEY,
    department_name VARCHAR2(50) NOT NULL
);

-- Create the Job_Titles table
CREATE TABLE Job_Titles (
    job_id NUMBER PRIMARY KEY,
    job_title VARCHAR2(50) NOT NULL
);

-- Create the Employees table with foreign keys to Departments and Job_Titles
CREATE TABLE Employees (
    employee_id NUMBER PRIMARY KEY,
    employee_name VARCHAR2(100) NOT NULL,
    department_id NUMBER,
    job_id NUMBER,
    salary NUMBER,
    FOREIGN KEY (department_id) REFERENCES Departments(department_id),
    FOREIGN KEY (job_id) REFERENCES Job_Titles(job_id)
);
```

### 3. Insert Data into the Tables

```sql
-- Insert data into the Departments table
INSERT INTO Departments (department_id, department_name)
VALUES (1, 'Human Resources'), (2, 'Engineering'), (3, 'Sales');

-- Insert data into the Job_Titles table
INSERT INTO Job_Titles (job_id, job_title)
VALUES (1, 'Manager'), (2, 'Engineer'), (3, 'Sales Representative');

-- Insert data into the Employees table
INSERT INTO Employees (employee_id, employee_name, department_id, job_id, salary)
VALUES (101, 'Alice Smith', 1, 1, 60000),
       (102, 'Bob Johnson', 2, 2, 75000),
       (103, 'Charlie Brown', 3, 3, 50000);
```

### 4. Update and Delete Data

```sql
-- Update employee salary
UPDATE Employees
SET salary = 65000
WHERE employee_id = 101;

-- Delete an employee record
DELETE FROM Employees
WHERE employee_id = 103;
```

### 5. Perform Joins to Retrieve Related Data

```sql
-- Retrieve data with a JOIN between Employees, Departments, and Job_Titles
SELECT e.employee_name, d.department_name, j.job_title, e.salary
FROM Employees e
JOIN Departments d ON e.department_id = d.department_id
JOIN Job_Titles j ON e.job_id = j.job_id;
```

### 6. DCL Operations

```sql

GRANT SELECT ON Employees TO john_doe;

```

### Revoking Privileges

```sql
REVOKE SELECT ON Employees FROM john_doe;
```

### 7.TCL Operations

```sql
-- Start a transaction
INSERT INTO Employees (employee_id, employee_name, department_id, job_id, salary)
VALUES (104, 'David Green', 2, 2, 78000);

-- Save a transaction point
SAVEPOINT add_employee;

-- Update employee details
UPDATE Employees
SET salary = 80000
WHERE employee_id = 104;

-- If needed, you can rollback to the savepoint before committing the transaction
ROLLBACK TO add_employee;

-- Commit the transaction (saves all changes made so far)
COMMIT;
```
