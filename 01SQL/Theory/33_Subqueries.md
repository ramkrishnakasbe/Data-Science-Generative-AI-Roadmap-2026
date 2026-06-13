# Subqueries in SQL

## What is a Subquery?

A Subquery (Nested Query) is a query inside another SQL query.

The inner query executes first and its result is used by the outer query.

---

## Why Do We Need Subqueries?

Business questions often depend on results from another query.

Examples:

- Find employees earning above average salary.
- Find customers who placed orders.
- Find products with maximum sales.
- Find departments with highest salary.

Subqueries help solve these problems.

---

# General Syntax

```sql
SELECT column_name
FROM table_name
WHERE column_name OPERATOR
(
    SELECT column_name
    FROM another_table
);
```

---

# Example Dataset

## Employees

| employee_id | employee_name | department | salary |
|------------|---------------|------------|---------|
| 101 | Ram | Sales | 50000 |
| 102 | Amit | IT | 70000 |
| 103 | Neha | HR | 45000 |
| 104 | Priya | IT | 90000 |
| 105 | Raj | Sales | 30000 |

---

# Types of Subqueries

1. Scalar Subquery
2. Multi-row Subquery
3. Multi-column Subquery
4. Correlated Subquery
5. Nested Subquery

---

# Scalar Subquery

## What is Scalar Subquery?

Returns exactly one value.

---

## Example

Find employees earning above average salary.

```sql
SELECT *
FROM employees
WHERE salary >
(
    SELECT AVG(salary)
    FROM employees
);
```

---

## Step 1

Inner Query

```sql
SELECT AVG(salary)
FROM employees;
```

Output

```text
57000
```

---

## Step 2

Outer Query

```sql
SELECT *
FROM employees
WHERE salary > 57000;
```

---

## Output

| employee_name | salary |
|---------------|---------|
| Amit | 70000 |
| Priya | 90000 |

---

# Multi-row Subquery

## What is Multi-row Subquery?

Returns multiple rows.

Usually used with:

- IN
- ANY
- ALL

---

## Example

Employees from IT and HR departments.

```sql
SELECT *
FROM employees
WHERE department IN
(
    SELECT department
    FROM employees
    WHERE salary > 60000
);
```

---

## Inner Query Result

```text
IT
IT
```

---

## Output

All employees from IT department.

---

# Subquery in SELECT Clause

## Example

Display employee salary and average salary.

```sql
SELECT
    employee_name,
    salary,
    (
        SELECT AVG(salary)
        FROM employees
    ) AS avg_salary
FROM employees;
```

---

## Output

| employee_name | salary | avg_salary |
|---------------|---------|------------|
| Ram | 50000 | 57000 |
| Amit | 70000 | 57000 |

---

# Subquery in FROM Clause

## Example

```sql
SELECT *
FROM
(
    SELECT
        department,
        AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department
) dept_salary;
```

---

## Output

| department | avg_salary |
|------------|------------|
| Sales | 40000 |
| IT | 80000 |
| HR | 45000 |

---

# Correlated Subquery

## What is Correlated Subquery?

A correlated subquery depends on the outer query.

It executes once for every row.

---

# Example

Find employees earning more than their department average.

```sql
SELECT *
FROM employees e1
WHERE salary >
(
    SELECT AVG(salary)
    FROM employees e2
    WHERE e1.department = e2.department
);
```

---

## Explanation

For each employee:

1. Calculate department average
2. Compare salary
3. Return qualifying employees

---

## Output

| employee_name | department | salary |
|---------------|------------|---------|
| Ram | Sales | 50000 |
| Priya | IT | 90000 |

---

# EXISTS

## What is EXISTS?

Checks whether a subquery returns rows.

Returns TRUE if rows exist.

---

## Example

Find customers who placed orders.

### Customers

| customer_id | customer_name |
|------------|---------------|
| 1 | Ram |
| 2 | Amit |
| 3 | Neha |

### Orders

| order_id | customer_id |
|----------|-------------|
| 101 | 1 |
| 102 | 2 |

---

```sql
SELECT *
FROM customers c
WHERE EXISTS
(
    SELECT 1
    FROM orders o
    WHERE c.customer_id=o.customer_id
);
```

---

## Output

| customer_name |
|---------------|
| Ram |
| Amit |

---

# Why SELECT 1?

Common Interview Question.

```sql
SELECT 1
```

Used because EXISTS only checks whether rows exist.

Actual values are ignored.

---

# NOT EXISTS

## What is NOT EXISTS?

Returns rows for which no matching record exists.

---

## Example

Customers who never ordered.

```sql
SELECT *
FROM customers c
WHERE NOT EXISTS
(
    SELECT 1
    FROM orders o
    WHERE c.customer_id=o.customer_id
);
```

---

## Output

| customer_name |
|---------------|
| Neha |

---

# IN vs EXISTS

## IN

```sql
SELECT *
FROM employees
WHERE department IN
(
    SELECT department
    FROM departments
);
```

---

## EXISTS

```sql
SELECT *
FROM employees e
WHERE EXISTS
(
    SELECT 1
    FROM departments d
    WHERE e.department=d.department
);
```

---

## Comparison

| Feature | IN | EXISTS |
|----------|---------|---------|
| Small Data | Good | Good |
| Large Data | Slower | Faster |
| Uses Indexes | Sometimes | Better |
| Stops Early | No | Yes |

---

## Interview Answer

For large datasets:

✅ EXISTS is generally preferred.

---

# ANY Operator

## Example

```sql
SELECT *
FROM employees
WHERE salary >
ANY
(
    SELECT salary
    FROM employees
    WHERE department='Sales'
);
```

---

# ALL Operator

## Example

```sql
SELECT *
FROM employees
WHERE salary >
ALL
(
    SELECT salary
    FROM employees
    WHERE department='Sales'
);
```

---

# Correlated vs Non-Correlated Subquery

| Feature | Correlated | Non-Correlated |
|-----------|-----------|---------------|
| Depends on Outer Query | Yes | No |
| Execution | Per Row | Once |
| Performance | Slower | Faster |
| Complexity | Higher | Lower |

---

# Real Business Examples

## HR Analytics

Employees above department average salary.

---

## Customer Analytics

Customers with purchases.

---

## Fraud Detection

Transactions matching suspicious patterns.

---

## Sales Analytics

Products selling above category average.

---

# Common Interview Questions

## Q1. What is a Subquery?

Query inside another query.

---

## Q2. What is a Scalar Subquery?

Returns one value.

---

## Q3. What is a Correlated Subquery?

Depends on outer query.

---

## Q4. Difference Between EXISTS and IN?

EXISTS is generally faster on large datasets.

---

## Q5. Why Use SELECT 1 in EXISTS?

Only row existence matters.

---

## Q6. Which is Faster?

Non-correlated subquery.

---

# Common Mistakes

## Returning Multiple Values in Scalar Subquery

❌ Wrong

```sql
SELECT *
FROM employees
WHERE salary =
(
    SELECT salary
    FROM employees
);
```

Returns multiple rows.

---

## Using = Instead of IN

❌ Wrong

```sql
WHERE department =
(
    SELECT department
    FROM departments
);
```

If multiple rows exist.

---

## Correct

```sql
WHERE department IN
(
    SELECT department
    FROM departments
);
```

---

# Practice Questions

1. Find employees above average salary.
2. Find highest paid employee.
3. Find employees earning more than department average.
4. Find customers who placed orders.
5. Find customers without orders.
6. Find products above category average price.
7. Find departments with highest average salary.
8. Compare IN vs EXISTS performance.
9. Find products never sold.
10. Find employees in top-performing departments.

---

# Key Takeaways

✔ Subqueries are queries inside another query.

✔ Scalar subqueries return one value.

✔ Multi-row subqueries return multiple rows.

✔ Correlated subqueries depend on outer queries.

✔ EXISTS checks for row existence.

✔ NOT EXISTS finds missing relationships.

✔ EXISTS is generally faster than IN on large datasets.

✔ Frequently asked in Data Scientist, Analyst, and Data Engineer interviews.
