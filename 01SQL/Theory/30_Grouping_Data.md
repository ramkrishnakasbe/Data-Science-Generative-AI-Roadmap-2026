# Grouping Data in SQL

## What is Grouping Data?

Grouping data means combining rows that have the same values into summary groups.

SQL uses:

- GROUP BY
- HAVING

to perform aggregation and analysis on grouped data.

---

## Why Do We Need Grouping?

Suppose a company has millions of sales records.

Instead of viewing every row individually, management wants answers like:

- Total sales by region
- Average salary by department
- Number of employees per department
- Highest sales by product category

Grouping helps answer these business questions.

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

# GROUP BY

## What is GROUP BY?

GROUP BY groups rows having the same values into a single summary row.

Usually used with:

- COUNT()
- SUM()
- AVG()
- MIN()
- MAX()

---

## Syntax

```sql
SELECT column_name,
       aggregate_function(column_name)
FROM table_name
GROUP BY column_name;
```

---

## Example 1

Department-wise Employee Count

```sql
SELECT
    department,
    COUNT(*) AS total_employees
FROM employees
GROUP BY department;
```

### Output

| department | total_employees |
|------------|----------------|
| Sales | 2 |
| IT | 2 |
| HR | 1 |

---

## Example 2

Department-wise Salary

```sql
SELECT
    department,
    SUM(salary) AS total_salary
FROM employees
GROUP BY department;
```

### Output

| department | total_salary |
|------------|-------------|
| Sales | 80000 |
| IT | 160000 |
| HR | 45000 |

---

## Example 3

Department-wise Average Salary

```sql
SELECT
    department,
    AVG(salary) AS avg_salary
FROM employees
GROUP BY department;
```

### Output

| department | avg_salary |
|------------|------------|
| Sales | 40000 |
| IT | 80000 |
| HR | 45000 |

---

## Example 4

Department-wise Highest Salary

```sql
SELECT
    department,
    MAX(salary) AS highest_salary
FROM employees
GROUP BY department;
```

### Output

| department | highest_salary |
|------------|---------------|
| Sales | 50000 |
| IT | 90000 |
| HR | 45000 |

---

# Multiple Column GROUP BY

## Example

Department and Salary Grouping

```sql
SELECT
    department,
    salary,
    COUNT(*)
FROM employees
GROUP BY department, salary;
```

---

## Output

| department | salary | count |
|------------|---------|-------|
| Sales | 50000 | 1 |
| Sales | 30000 | 1 |
| IT | 70000 | 1 |
| IT | 90000 | 1 |
| HR | 45000 | 1 |

---

# Common Error with GROUP BY

## Wrong Query

```sql
SELECT
    department,
    employee_name,
    SUM(salary)
FROM employees
GROUP BY department;
```

Error:

employee_name is neither grouped nor aggregated.

---

## Correct Query

```sql
SELECT
    department,
    SUM(salary)
FROM employees
GROUP BY department;
```

---

# Execution Order

Many interviewers ask this.

```text
FROM
WHERE
GROUP BY
HAVING
SELECT
ORDER BY
LIMIT
```

---

# HAVING

## What is HAVING?

HAVING filters grouped data.

WHERE filters rows.

HAVING filters groups.

---

# Difference Between WHERE and HAVING

| WHERE | HAVING |
|---------|---------|
| Filters rows | Filters groups |
| Before GROUP BY | After GROUP BY |
| Cannot use aggregate functions | Can use aggregate functions |

---

# Example Dataset

| department | salary |
|------------|---------|
| Sales | 50000 |
| Sales | 30000 |
| IT | 70000 |
| IT | 90000 |
| HR | 45000 |

---

# Example 1

Departments with Total Salary > 100000

```sql
SELECT
    department,
    SUM(salary) AS total_salary
FROM employees
GROUP BY department
HAVING SUM(salary) > 100000;
```

### Output

| department |
|------------|
| IT |

---

# Example 2

Departments Having More Than One Employee

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department
HAVING COUNT(*) > 1;
```

### Output

| department |
|------------|
| Sales |
| IT |

---

# Example 3

Departments with Average Salary > 50000

```sql
SELECT
    department,
    AVG(salary)
FROM employees
GROUP BY department
HAVING AVG(salary) > 50000;
```

### Output

| department |
|------------|
| IT |

---

# WHERE + GROUP BY + HAVING

Find departments having average salary greater than 40000 for employees earning more than 30000.

```sql
SELECT
    department,
    AVG(salary) AS avg_salary
FROM employees
WHERE salary > 30000
GROUP BY department
HAVING AVG(salary) > 40000;
```

---

# Real Business Example

## Sales Table

| region | sales_amount |
|---------|-------------|
| North | 5000 |
| North | 7000 |
| South | 2000 |
| South | 3000 |

---

Total Sales by Region

```sql
SELECT
    region,
    SUM(sales_amount) AS total_sales
FROM sales
GROUP BY region;
```

### Output

| region | total_sales |
|---------|------------|
| North | 12000 |
| South | 5000 |

---

Find Regions with Sales Greater Than 10000

```sql
SELECT
    region,
    SUM(sales_amount)
FROM sales
GROUP BY region
HAVING SUM(sales_amount) > 10000;
```

### Output

| region |
|---------|
| North |

---

# Common Interview Questions

## Q1. Difference Between WHERE and HAVING?

WHERE filters rows.

HAVING filters groups.

---

## Q2. Can HAVING be Used Without GROUP BY?

Yes.

```sql
SELECT COUNT(*)
FROM employees
HAVING COUNT(*) > 0;
```

---

## Q3. Why Can't Aggregate Functions Be Used in WHERE?

Because WHERE executes before aggregation.

---

## Q4. Which Clause Executes First?

```text
FROM
WHERE
GROUP BY
HAVING
SELECT
ORDER BY
LIMIT
```

---

## Q5. Which Aggregate Functions Are Commonly Used with GROUP BY?

- COUNT()
- SUM()
- AVG()
- MIN()
- MAX()

---

# Data Scientist Interview Questions

### Easy

1. Count employees by department.
2. Find average salary by department.
3. Find maximum salary by department.

### Medium

4. Departments having more than 5 employees.
5. Departments with average salary greater than 60000.

### Advanced

6. Top 3 departments by total salary.
7. Departments contributing more than 20% of total revenue.

---

# Real-World Data Science Use Cases

## Customer Analytics

```sql
GROUP BY customer_segment
```

---

## Sales Analytics

```sql
GROUP BY region
```

---

## HR Analytics

```sql
GROUP BY department
```

---

## Product Analytics

```sql
GROUP BY category
```

---

## Dashboard KPIs

```sql
COUNT()
SUM()
AVG()
GROUP BY
```

---

# Common Mistakes

## Using Aggregate Functions in WHERE

❌ Wrong

```sql
SELECT *
FROM employees
WHERE SUM(salary) > 100000;
```

---

## Correct

```sql
SELECT
    department,
    SUM(salary)
FROM employees
GROUP BY department
HAVING SUM(salary) > 100000;
```

---

## Missing GROUP BY

❌ Wrong

```sql
SELECT department,
       SUM(salary)
FROM employees;
```

---

## Correct

```sql
SELECT department,
       SUM(salary)
FROM employees
GROUP BY department;
```

---

# Key Takeaways

✔ GROUP BY groups similar records.

✔ HAVING filters grouped results.

✔ WHERE filters rows before grouping.

✔ HAVING filters groups after aggregation.

✔ GROUP BY is one of the most important SQL concepts for Data Scientists.

✔ GROUP BY + Aggregate Functions are asked in almost every SQL interview.

✔ Understanding execution order is critical for advanced SQL questions.
