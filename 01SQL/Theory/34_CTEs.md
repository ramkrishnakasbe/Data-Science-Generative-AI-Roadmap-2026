# Common Table Expressions (CTEs) in SQL

## What is a CTE?

CTE stands for Common Table Expression.

A CTE is a temporary named result set that exists only during the execution of a query.

CTEs improve:

- Readability
- Maintainability
- Debugging
- Complex Query Writing

---

# Why Do We Need CTEs?

Suppose you have a complex query with:

- Multiple Joins
- Aggregations
- Subqueries
- Filters

Instead of writing nested queries, you can break them into logical blocks using CTEs.

Think of a CTE as a temporary table created inside a query.

---

# Basic Syntax

```sql
WITH cte_name AS
(
    SELECT *
    FROM table_name
)
SELECT *
FROM cte_name;
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

# Simple CTE

## Example

```sql
WITH employee_cte AS
(
    SELECT *
    FROM employees
)
SELECT *
FROM employee_cte;
```

---

## Output

| employee_id | employee_name | department | salary |
|------------|---------------|------------|---------|
| 101 | Ram | Sales | 50000 |
| 102 | Amit | IT | 70000 |
| 103 | Neha | HR | 45000 |
| 104 | Priya | IT | 90000 |
| 105 | Raj | Sales | 30000 |

---

# CTE with Filtering

## Example

Employees earning more than 50000.

```sql
WITH high_salary AS
(
    SELECT *
    FROM employees
    WHERE salary > 50000
)
SELECT *
FROM high_salary;
```

---

## Output

| employee_name | salary |
|---------------|---------|
| Amit | 70000 |
| Priya | 90000 |

---

# CTE with Aggregation

## Example

Department-wise average salary.

```sql
WITH dept_avg_salary AS
(
    SELECT
        department,
        AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department
)
SELECT *
FROM dept_avg_salary;
```

---

## Output

| department | avg_salary |
|------------|------------|
| Sales | 40000 |
| IT | 80000 |
| HR | 45000 |

---

# Using CTE Multiple Times

One major advantage of CTEs is reusability.

```sql
WITH dept_avg_salary AS
(
    SELECT
        department,
        AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department
)
SELECT *
FROM dept_avg_salary
WHERE avg_salary > 50000;
```

---

# Multiple CTEs

You can define multiple CTEs in a single query.

---

## Example

```sql
WITH total_salary AS
(
    SELECT
        department,
        SUM(salary) AS total_salary
    FROM employees
    GROUP BY department
),

employee_count AS
(
    SELECT
        department,
        COUNT(*) AS total_employees
    FROM employees
    GROUP BY department
)

SELECT
    ts.department,
    ts.total_salary,
    ec.total_employees
FROM total_salary ts
JOIN employee_count ec
ON ts.department = ec.department;
```

---

## Output

| department | total_salary | total_employees |
|------------|--------------|----------------|
| Sales | 80000 | 2 |
| IT | 160000 | 2 |
| HR | 45000 | 1 |

---

# CTE vs Subquery

## Subquery Version

```sql
SELECT *
FROM
(
    SELECT
        department,
        AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department
) x;
```

---

## CTE Version

```sql
WITH dept_avg AS
(
    SELECT
        department,
        AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department
)
SELECT *
FROM dept_avg;
```

---

# Why CTE is Better?

✔ Easier to read

✔ Easier to debug

✔ Easier to maintain

✔ Better for complex SQL

---

# Recursive CTE

## What is a Recursive CTE?

A Recursive CTE references itself.

Used for:

- Employee Hierarchy
- Organization Charts
- Tree Structures
- Parent-Child Relationships
- Category Hierarchies

---

# Example Dataset

## Employees

| employee_id | employee_name | manager_id |
|------------|---------------|------------|
| 1 | Ram | NULL |
| 2 | Amit | 1 |
| 3 | Neha | 1 |
| 4 | Priya | 2 |
| 5 | Raj | 2 |

---

## Recursive CTE Syntax

```sql
WITH RECURSIVE employee_hierarchy AS
(
    -- Anchor Query

    SELECT
        employee_id,
        employee_name,
        manager_id
    FROM employees
    WHERE manager_id IS NULL

    UNION ALL

    -- Recursive Query

    SELECT
        e.employee_id,
        e.employee_name,
        e.manager_id
    FROM employees e
    JOIN employee_hierarchy eh
    ON e.manager_id = eh.employee_id
)
SELECT *
FROM employee_hierarchy;
```

---

## Output

| employee_id | employee_name |
|------------|---------------|
| 1 | Ram |
| 2 | Amit |
| 3 | Neha |
| 4 | Priya |
| 5 | Raj |

---

# How Recursive CTE Works

Step 1

Anchor Query

```sql
SELECT *
FROM employees
WHERE manager_id IS NULL;
```

Returns:

```text
Ram
```

---

Step 2

Recursive Query

Find employees reporting to Ram.

Returns:

```text
Amit
Neha
```

---

Step 3

Find employees reporting to Amit.

Returns:

```text
Priya
Raj
```

---

Process continues until no rows remain.

---

# CTE vs Temporary Table

| Feature | CTE | Temp Table |
|----------|----------|-----------|
| Lifetime | Query Only | Session |
| Storage | Memory | Database |
| Reusable | Same Query | Multiple Queries |
| Faster Setup | Yes | No |
| Indexing | No | Yes |

---

# Real-World Data Science Use Cases

## Sales Analytics

```sql
WITH regional_sales AS (...)
```

---

## Customer Segmentation

```sql
WITH customer_segments AS (...)
```

---

## Funnel Analysis

```sql
WITH user_events AS (...)
```

---

## Churn Analysis

```sql
WITH churned_users AS (...)
```

---

## Feature Engineering

```sql
WITH engineered_features AS (...)
```

---

# Common Interview Questions

## Q1. What is a CTE?

A temporary named result set used within a query.

---

## Q2. What does WITH keyword do?

Creates a CTE.

---

## Q3. Why use CTE instead of Subquery?

Better readability and maintainability.

---

## Q4. Can a CTE call another CTE?

Yes.

---

## Q5. Can a CTE reference itself?

Yes.

Recursive CTE.

---

## Q6. Difference Between CTE and Temp Table?

CTE exists only during query execution.

Temp Table exists for the session.

---

## Q7. Are CTEs Faster than Subqueries?

Not always.

Primarily used for readability.

---

# Common Mistakes

## Missing CTE Name

❌ Wrong

```sql
WITH
(
    SELECT *
    FROM employees
)
```

---

## Correct

```sql
WITH employee_cte AS
(
    SELECT *
    FROM employees
)
```

---

## Infinite Recursive CTE

❌ Wrong

```sql
WITH RECURSIVE test AS
(
    SELECT 1

    UNION ALL

    SELECT 1
)
```

Can create infinite recursion.

---

# Practice Questions

1. Create a CTE for high-salary employees.
2. Calculate department-wise average salary using CTE.
3. Create multiple CTEs and join them.
4. Rewrite a subquery using CTE.
5. Build employee hierarchy using recursive CTE.
6. Find total salary by department using CTE.
7. Find top-performing regions using CTE.
8. Use CTEs for customer segmentation.

---

# Key Takeaways

✔ CTE stands for Common Table Expression.

✔ Created using WITH keyword.

✔ Improves readability and maintainability.

✔ Can replace complex subqueries.

✔ Multiple CTEs can be used together.

✔ Recursive CTEs solve hierarchical problems.

✔ Commonly used in Data Science, Analytics, Data Engineering, and BI projects.

✔ Frequently asked in SQL interviews.
