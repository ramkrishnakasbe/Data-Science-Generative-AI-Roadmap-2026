# SQL Stored Procedures

## Overview

A Stored Procedure is a precompiled collection of one or more SQL statements stored inside the database and executed as a single unit.

Stored Procedures help automate repetitive tasks, improve performance, enhance security, and simplify complex business logic.

---

# Why Use Stored Procedures?

* Reuse SQL code
* Reduce code duplication
* Improve performance through execution plan caching
* Enhance security by restricting direct table access
* Simplify maintenance
* Centralize business logic

---

# How Stored Procedures Work

1. Procedure is created and stored in the database.
2. Database compiles the SQL statements.
3. Users execute the procedure when needed.
4. Database executes the stored logic and returns results.

---

# Basic Syntax

```sql
CREATE PROCEDURE procedure_name
AS
BEGIN
    SQL Statements
END;
```

### Example

```sql
CREATE PROCEDURE GetEmployees
AS
BEGIN
    SELECT *
    FROM Employees;
END;
```

Execute:

```sql
EXEC GetEmployees;
```

---

# Stored Procedure with Parameters

Parameters allow users to pass values dynamically.

## Input Parameters

### Example

```sql
CREATE PROCEDURE GetEmployeeByID
    @EmployeeID INT
AS
BEGIN
    SELECT *
    FROM Employees
    WHERE EmployeeID = @EmployeeID;
END;
```

Execute:

```sql
EXEC GetEmployeeByID 101;
```

---

# Multiple Parameters

```sql
CREATE PROCEDURE GetEmployeeDetails
    @Department VARCHAR(50),
    @Salary DECIMAL(10,2)
AS
BEGIN
    SELECT *
    FROM Employees
    WHERE Department = @Department
      AND Salary > @Salary;
END;
```

Execute:

```sql
EXEC GetEmployeeDetails 'IT', 50000;
```

---

# Output Parameters

Used to return values from a procedure.

### Example

```sql
CREATE PROCEDURE GetEmployeeCount
    @TotalEmployees INT OUTPUT
AS
BEGIN
    SELECT @TotalEmployees = COUNT(*)
    FROM Employees;
END;
```

Execute:

```sql
DECLARE @Count INT;

EXEC GetEmployeeCount @Count OUTPUT;

PRINT @Count;
```

---

# Stored Procedure with INSERT

```sql
CREATE PROCEDURE AddEmployee
    @Name VARCHAR(100),
    @Department VARCHAR(50),
    @Salary DECIMAL(10,2)
AS
BEGIN
    INSERT INTO Employees
    (
        Name,
        Department,
        Salary
    )
    VALUES
    (
        @Name,
        @Department,
        @Salary
    );
END;
```

Execute:

```sql
EXEC AddEmployee
    'John',
    'IT',
    60000;
```

---

# Stored Procedure with UPDATE

```sql
CREATE PROCEDURE UpdateSalary
    @EmployeeID INT,
    @Salary DECIMAL(10,2)
AS
BEGIN
    UPDATE Employees
    SET Salary = @Salary
    WHERE EmployeeID = @EmployeeID;
END;
```

---

# Stored Procedure with DELETE

```sql
CREATE PROCEDURE DeleteEmployee
    @EmployeeID INT
AS
BEGIN
    DELETE FROM Employees
    WHERE EmployeeID = @EmployeeID;
END;
```

---

# Conditional Logic

Stored Procedures can contain business logic.

### Example

```sql
CREATE PROCEDURE CheckSalary
    @Salary DECIMAL(10,2)
AS
BEGIN

    IF @Salary > 100000
        PRINT 'High Salary';
    ELSE
        PRINT 'Normal Salary';

END;
```

---

# Using CASE Statement

```sql
CREATE PROCEDURE EmployeeCategory
AS
BEGIN

    SELECT
        Name,
        Salary,
        CASE
            WHEN Salary > 100000 THEN 'Senior'
            WHEN Salary > 50000 THEN 'Mid-Level'
            ELSE 'Junior'
        END AS Category
    FROM Employees;

END;
```

---

# Transactions in Stored Procedures

Transactions ensure data consistency.

### Example

```sql
CREATE PROCEDURE TransferAmount
AS
BEGIN

    BEGIN TRANSACTION;

    UPDATE Accounts
    SET Balance = Balance - 1000
    WHERE AccountID = 1;

    UPDATE Accounts
    SET Balance = Balance + 1000
    WHERE AccountID = 2;

    COMMIT TRANSACTION;

END;
```

---

# Error Handling

## TRY-CATCH Block

```sql
CREATE PROCEDURE SafeInsert
AS
BEGIN

    BEGIN TRY

        INSERT INTO Employees
        VALUES (1, 'John');

    END TRY

    BEGIN CATCH

        PRINT ERROR_MESSAGE();

    END CATCH

END;
```

---

# Dynamic SQL in Stored Procedures

Used when SQL statements need to be generated dynamically.

```sql
CREATE PROCEDURE DynamicTableSelect
    @TableName VARCHAR(100)
AS
BEGIN

    DECLARE @SQL VARCHAR(MAX);

    SET @SQL =
        'SELECT * FROM ' + @TableName;

    EXEC(@SQL);

END;
```

---

# Altering a Stored Procedure

Modify an existing procedure.

```sql
ALTER PROCEDURE GetEmployees
AS
BEGIN

    SELECT *
    FROM Employees
    ORDER BY Salary DESC;

END;
```

---

# Dropping a Stored Procedure

Delete a stored procedure permanently.

```sql
DROP PROCEDURE GetEmployees;
```

---

# Advantages

* Faster execution
* Reusable code
* Better security
* Reduced network traffic
* Easier maintenance
* Centralized business logic

---

# Disadvantages

* Database dependency
* Debugging can be difficult
* Version control challenges
* Complex procedures become harder to maintain

---

# Real-World Use Cases

## Banking Systems

* Fund transfer
* Balance calculation
* Interest calculation

## E-Commerce

* Order processing
* Inventory updates
* Customer management

## HR Systems

* Payroll calculation
* Employee management
* Attendance processing

## Data Warehousing

* ETL processes
* Data validation
* Scheduled reporting

---

# Interview Questions

### What is a Stored Procedure?

A precompiled set of SQL statements stored in the database and executed as a single unit.

---

### Difference Between Stored Procedure and Function?

| Stored Procedure                | Function                    |
| ------------------------------- | --------------------------- |
| Can perform DML operations      | Primarily returns a value   |
| Can return multiple result sets | Returns one value/table     |
| Can use transactions            | Limited transaction support |
| Called using EXEC               | Used inside SQL queries     |

---

### Why are Stored Procedures Faster?

Because execution plans are compiled and reused, reducing query parsing and optimization overhead.

---

### What are Input and Output Parameters?

* Input Parameter → Pass values into procedure.
* Output Parameter → Return values from procedure.

---

### Can Stored Procedures Call Other Procedures?

Yes.

```sql
EXEC Procedure_A;
EXEC Procedure_B;
```

---

# Best Practices

* Use meaningful names
* Avoid SELECT *
* Use parameters
* Implement error handling
* Use transactions when needed
* Follow naming conventions
* Document business logic
* Optimize queries inside procedures

---

# Summary

Stored Procedures are reusable, precompiled SQL programs that help automate business logic, improve performance, and enhance database security. They are widely used in enterprise applications, ETL pipelines, reporting systems, and transactional databases.
