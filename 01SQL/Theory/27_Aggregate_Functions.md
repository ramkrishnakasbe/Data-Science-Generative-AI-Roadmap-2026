# Aggregate Functions in SQL

## What are Aggregate Functions?

Aggregate Functions perform calculations on multiple rows and return a single summarized result.

Instead of returning individual records, aggregate functions summarize data and provide meaningful insights.

They are heavily used in:

* Business Reporting
* Dashboards
* Analytics
* Data Science
* KPI Tracking
* Data Warehousing

---

## Why Do We Need Aggregate Functions?

Suppose a company has 10 million sales records.

Management does not want to see all transactions.

Instead, they need answers like:

* Total Revenue
* Average Sales
* Number of Customers
* Highest Sale
* Lowest Sale

Aggregate Functions help answer these questions efficiently.

---

# Example Dataset

## Employees

| employee_id | employee_name | department | salary |
| ----------- | ------------- | ---------- | ------ |
| 101         | Ram           | Sales      | 50000  |
| 102         | Amit          | IT         | 70000  |
| 103         | Neha          | HR         | 45000  |
| 104         | Priya         | IT         | 90000  |
| 105         | Raj           | Sales      | 30000  |

---

# COUNT()

## What is COUNT()?

COUNT() returns the number of rows.

---

## Syntax

```sql
SELECT COUNT(*)
FROM employees;
```

---

## COUNT(*)

Counts all rows.

```sql
SELECT COUNT(*)
FROM employees;
```

### Output

| count |
| ----- |
| 5     |

---

## COUNT(column_name)

Counts only non-null values.

Example:

| employee_id | bonus |
| ----------- | ----- |
| 1           | 1000  |
| 2           | NULL  |
| 3           | 2000  |

```sql
SELECT COUNT(bonus)
FROM employees;
```

### Output

| count |
| ----- |
| 2     |

NULL values are ignored.

---

## COUNT(DISTINCT)

Counts unique values.

```sql
SELECT COUNT(DISTINCT department)
FROM employees;
```

### Output

| count |
| ----- |
| 3     |

Unique Departments:

* Sales
* IT
* HR

---

## Business Use Cases

### Total Employees

```sql
SELECT COUNT(*)
FROM employees;
```

### Total Orders

```sql
SELECT COUNT(*)
FROM orders;
```

### Active Users

```sql
SELECT COUNT(DISTINCT user_id)
FROM login_logs;
```

---

# SUM()

## What is SUM()?

SUM() calculates the total of a numeric column.

---

## Syntax

```sql
SELECT SUM(column_name)
FROM table_name;
```

---

## Example

```sql
SELECT SUM(salary)
FROM employees;
```

### Calculation

```text
50000
70000
45000
90000
30000
------
285000
```

### Output

| total_salary |
| ------------ |
| 285000       |

---

## Business Use Cases

### Total Revenue

```sql
SELECT SUM(revenue)
FROM sales;
```

### Total Profit

```sql
SELECT SUM(profit)
FROM finance;
```

### Inventory Value

```sql
SELECT SUM(quantity * unit_price)
FROM products;
```

---

## Important Notes

* Works only on numeric columns
* Ignores NULL values

---

# AVG()

## What is AVG()?

AVG() calculates the average value of a numeric column.

---

## Syntax

```sql
SELECT AVG(column_name)
FROM table_name;
```

---

## Example

```sql
SELECT AVG(salary)
FROM employees;
```

### Calculation

```text
285000 / 5 = 57000
```

### Output

| avg_salary |
| ---------- |
| 57000      |

---

## AVG with NULL Values

Example:

| salary |
| ------ |
| 50000  |
| NULL   |
| 70000  |

AVG:

```text
(50000 + 70000) / 2
```

Not divided by 3.

NULL values are ignored.

---

## Business Use Cases

### Average Salary

```sql
SELECT AVG(salary)
FROM employees;
```

### Average Revenue

```sql
SELECT AVG(revenue)
FROM sales;
```

### Average Order Value

```sql
SELECT AVG(order_amount)
FROM orders;
```

---

# MIN()

## What is MIN()?

MIN() returns the smallest value.

---

## Syntax

```sql
SELECT MIN(column_name)
FROM table_name;
```

---

## Example

```sql
SELECT MIN(salary)
FROM employees;
```

### Output

| min_salary |
| ---------- |
| 30000      |

---

## Business Use Cases

### Lowest Salary

```sql
SELECT MIN(salary)
FROM employees;
```

### Cheapest Product

```sql
SELECT MIN(price)
FROM products;
```

### Earliest Order Date

```sql
SELECT MIN(order_date)
FROM orders;
```

---

## Important Notes

MIN works with:

* Numbers
* Dates
* Text (Alphabetical Order)

---

# MAX()

## What is MAX()?

MAX() returns the largest value.

---

## Syntax

```sql
SELECT MAX(column_name)
FROM table_name;
```

---

## Example

```sql
SELECT MAX(salary)
FROM employees;
```

### Output

| max_salary |
| ---------- |
| 90000      |

---

## Business Use Cases

### Highest Salary

```sql
SELECT MAX(salary)
FROM employees;
```

### Most Expensive Product

```sql
SELECT MAX(price)
FROM products;
```

### Latest Order Date

```sql
SELECT MAX(order_date)
FROM orders;
```

---

## Important Notes

MAX works with:

* Numbers
* Dates
* Text

---

# Using Multiple Aggregate Functions Together

```sql
SELECT
    COUNT(*) AS total_employees,
    SUM(salary) AS total_salary,
    AVG(salary) AS average_salary,
    MIN(salary) AS minimum_salary,
    MAX(salary) AS maximum_salary
FROM employees;
```

### Output

| total_employees | total_salary | average_salary | minimum_salary | maximum_salary |
| --------------- | ------------ | -------------- | -------------- | -------------- |
| 5               | 285000       | 57000          | 30000          | 90000          |

---

# Aggregate Functions with GROUP BY

```sql
SELECT
    department,
    SUM(salary) AS total_salary
FROM employees
GROUP BY department;
```

### Output

| department | total_salary |
| ---------- | ------------ |
| Sales      | 80000        |
| IT         | 160000       |
| HR         | 45000        |

---

# Aggregate Functions with HAVING

```sql
SELECT
    department,
    SUM(salary)
FROM employees
GROUP BY department
HAVING SUM(salary) > 100000;
```

### Output

| department |
| ---------- |
| IT         |

---

# Common Mistakes

## Using Aggregate Functions in WHERE

❌ Wrong

```sql
SELECT *
FROM employees
WHERE SUM(salary) > 100000;
```

✅ Correct

```sql
SELECT
    department,
    SUM(salary)
FROM employees
GROUP BY department
HAVING SUM(salary) > 100000;
```

---

## Forgetting GROUP BY

❌ Wrong

```sql
SELECT department,
       SUM(salary)
FROM employees;
```

✅ Correct

```sql
SELECT department,
       SUM(salary)
FROM employees
GROUP BY department;
```

---

# Interview Questions

### Q1. Difference between COUNT(*) and COUNT(column)?

COUNT(*) counts all rows.

COUNT(column) ignores NULL values.

---

### Q2. Does AVG() include NULL values?

No.

AVG ignores NULL values.

---

### Q3. Can MIN() and MAX() work on dates?

Yes.

---

### Q4. Which aggregate function is most commonly used?

COUNT()

---

### Q5. Can aggregate functions be used in WHERE?

No.

Use HAVING instead.

---

# Practice Questions

1. Count total employees.
2. Count distinct departments.
3. Find total salary expense.
4. Find average salary.
5. Find highest salary.
6. Find lowest salary.
7. Find department-wise salary totals.
8. Find departments with average salary greater than 50000.
9. Find total revenue by region.
10. Find average order value.

---

# Real-World Data Science Use Cases

### Customer Analytics

```sql
COUNT(DISTINCT customer_id)
```

### Revenue Analytics

```sql
SUM(revenue)
```

### Employee Analytics

```sql
AVG(salary)
```

### Product Analytics

```sql
MAX(price)
MIN(price)
```

### KPI Dashboards

```sql
COUNT()
SUM()
AVG()
```

---

# Key Takeaways

✔ COUNT() counts records

✔ SUM() calculates totals

✔ AVG() calculates averages

✔ MIN() returns smallest value

✔ MAX() returns largest value

✔ Aggregate Functions are essential for reporting and analytics

✔ Frequently asked in Data Scientist, Analyst, BI Developer, and Data Engineer interviews
