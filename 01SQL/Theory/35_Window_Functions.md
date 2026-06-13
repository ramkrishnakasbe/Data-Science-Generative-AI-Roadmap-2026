# Window Functions in SQL

## What are Window Functions?

Window Functions perform calculations across a set of rows related to the current row without collapsing rows like GROUP BY.

Unlike Aggregate Functions:

- GROUP BY reduces rows.
- Window Functions keep all rows.

Window Functions are heavily used in:

- Data Science
- Analytics
- Business Intelligence
- Reporting
- Ranking
- Time Series Analysis

---

# Why Do We Need Window Functions?

Suppose we need:

- Rank employees by salary
- Find previous month's sales
- Find next transaction
- Compare current salary with department average

Window Functions solve these efficiently.

---

# Basic Syntax

```sql
FUNCTION_NAME()
OVER (
    PARTITION BY column_name
    ORDER BY column_name
)
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

# OVER()

## What is OVER()?

OVER() defines the window on which the function operates.

Without OVER():

```sql
SELECT AVG(salary)
FROM employees;
```

Output:

| avg_salary |
|------------|
| 57000 |

Only one row.

---

With OVER():

```sql
SELECT
    employee_name,
    salary,
    AVG(salary) OVER()
FROM employees;
```

Output:

| employee_name | salary | avg_salary |
|---------------|---------|------------|
| Ram | 50000 | 57000 |
| Amit | 70000 | 57000 |
| Neha | 45000 | 57000 |
| Priya | 90000 | 57000 |
| Raj | 30000 | 57000 |

---

# PARTITION BY

## What is PARTITION BY?

Creates groups similar to GROUP BY but keeps rows.

---

## Example

Department-wise average salary.

```sql
SELECT
    employee_name,
    department,
    salary,
    AVG(salary)
    OVER(PARTITION BY department)
    AS avg_salary
FROM employees;
```

---

## Output

| employee_name | department | salary | avg_salary |
|---------------|------------|---------|------------|
| Ram | Sales | 50000 | 40000 |
| Raj | Sales | 30000 | 40000 |
| Amit | IT | 70000 | 80000 |
| Priya | IT | 90000 | 80000 |
| Neha | HR | 45000 | 45000 |

---

# ROW_NUMBER()

## What is ROW_NUMBER()?

Assigns unique sequential numbers.

---

## Example

```sql
SELECT
    employee_name,
    salary,
    ROW_NUMBER()
    OVER(ORDER BY salary DESC)
    AS row_num
FROM employees;
```

---

## Output

| employee_name | salary | row_num |
|---------------|---------|---------|
| Priya | 90000 | 1 |
| Amit | 70000 | 2 |
| Ram | 50000 | 3 |
| Neha | 45000 | 4 |
| Raj | 30000 | 5 |

---

## Use Cases

- Top N Records
- Pagination
- Deduplication

---

# RANK()

## What is RANK()?

Assigns rank with gaps.

---

## Example

### Data

| employee | salary |
|-----------|---------|
| A | 100 |
| B | 100 |
| C | 90 |

```sql
SELECT
    employee,
    salary,
    RANK()
    OVER(ORDER BY salary DESC)
    AS rank_num
FROM employees;
```

---

## Output

| employee | rank |
|----------|------|
| A | 1 |
| B | 1 |
| C | 3 |

Notice:

Rank 2 skipped.

---

# DENSE_RANK()

## What is DENSE_RANK()?

Assigns rank without gaps.

---

## Example

```sql
SELECT
    employee,
    salary,
    DENSE_RANK()
    OVER(ORDER BY salary DESC)
    AS rank_num
FROM employees;
```

---

## Output

| employee | rank |
|----------|------|
| A | 1 |
| B | 1 |
| C | 2 |

No skipped rank.

---

# ROW_NUMBER vs RANK vs DENSE_RANK

| Salary | ROW_NUMBER | RANK | DENSE_RANK |
|---------|------------|------|------------|
| 100 | 1 | 1 | 1 |
| 100 | 2 | 1 | 1 |
| 90 | 3 | 3 | 2 |

---

# NTILE()

## What is NTILE()?

Divides data into buckets.

---

## Example

Split employees into 4 groups.

```sql
SELECT
    employee_name,
    salary,
    NTILE(4)
    OVER(ORDER BY salary DESC)
    AS quartile
FROM employees;
```

---

## Output

| employee | quartile |
|-----------|----------|
| Priya | 1 |
| Amit | 1 |
| Ram | 2 |
| Neha | 3 |
| Raj | 4 |

---

## Use Cases

- Quartiles
- Percentiles
- Customer Segmentation

---

# LEAD()

## What is LEAD()?

Returns next row value.

---

## Example

```sql
SELECT
    employee_name,
    salary,
    LEAD(salary)
    OVER(ORDER BY salary)
    AS next_salary
FROM employees;
```

---

## Output

| employee | salary | next_salary |
|----------|---------|-------------|
| Raj | 30000 | 45000 |
| Neha | 45000 | 50000 |
| Ram | 50000 | 70000 |
| Amit | 70000 | 90000 |
| Priya | 90000 | NULL |

---

## Use Cases

- Next Transaction
- Future Sales
- Trend Analysis

---

# LAG()

## What is LAG()?

Returns previous row value.

---

## Example

```sql
SELECT
    employee_name,
    salary,
    LAG(salary)
    OVER(ORDER BY salary)
    AS previous_salary
FROM employees;
```

---

## Output

| employee | salary | previous_salary |
|----------|---------|----------------|
| Raj | 30000 | NULL |
| Neha | 45000 | 30000 |
| Ram | 50000 | 45000 |
| Amit | 70000 | 50000 |
| Priya | 90000 | 70000 |

---

## Use Cases

- Month-over-Month Analysis
- Previous Transactions
- Growth Calculations

---

# FIRST_VALUE()

## What is FIRST_VALUE()?

Returns first value in a partition.

---

## Example

```sql
SELECT
    employee_name,
    salary,
    FIRST_VALUE(salary)
    OVER(ORDER BY salary DESC)
    AS highest_salary
FROM employees;
```

---

## Output

All rows show:

```text
90000
```

---

# LAST_VALUE()

## What is LAST_VALUE()?

Returns last value in a partition.

---

## Example

```sql
SELECT
    employee_name,
    salary,
    LAST_VALUE(salary)
    OVER(
        ORDER BY salary
        ROWS BETWEEN
        UNBOUNDED PRECEDING
        AND UNBOUNDED FOLLOWING
    )
    AS highest_salary
FROM employees;
```

---

# Running Total

Very common interview question.

```sql
SELECT
    employee_name,
    salary,
    SUM(salary)
    OVER(
        ORDER BY employee_id
    ) AS running_total
FROM employees;
```

---

# Department Wise Ranking

```sql
SELECT
    employee_name,
    department,
    salary,
    RANK()
    OVER(
        PARTITION BY department
        ORDER BY salary DESC
    ) AS dept_rank
FROM employees;
```

---

# Real World Data Science Use Cases

## Customer Ranking

```sql
RANK()
```

---

## Sales Trends

```sql
LEAD()
LAG()
```

---

## Customer Segmentation

```sql
NTILE()
```

---

## Top Customers

```sql
ROW_NUMBER()
```

---

## Feature Engineering

```sql
LAG()
LEAD()
```

---

# Common Interview Questions

## Q1. Difference Between GROUP BY and Window Functions?

GROUP BY reduces rows.

Window Functions keep rows.

---

## Q2. Difference Between RANK and DENSE_RANK?

RANK skips numbers.

DENSE_RANK doesn't.

---

## Q3. Difference Between ROW_NUMBER and RANK?

ROW_NUMBER always unique.

RANK allows ties.

---

## Q4. Difference Between LEAD and LAG?

LEAD → next row.

LAG → previous row.

---

## Q5. What is PARTITION BY?

Creates logical groups without collapsing rows.

---

# Practice Questions

1. Rank employees by salary.
2. Find top 3 highest paid employees.
3. Find department-wise salary ranking.
4. Calculate running total salary.
5. Find previous month's sales.
6. Find next transaction amount.
7. Divide customers into quartiles.
8. Find highest salary in each department.
9. Compare salary against department average.
10. Create customer segmentation buckets.

---

# Key Takeaways

✔ Window Functions do not reduce rows.

✔ OVER() defines the window.

✔ PARTITION BY creates logical groups.

✔ ROW_NUMBER assigns unique sequence.

✔ RANK allows gaps.

✔ DENSE_RANK removes gaps.

✔ LEAD returns next row value.

✔ LAG returns previous row value.

✔ NTILE creates buckets.

✔ Frequently asked in Data Scientist and Data Analyst interviews.

✔ One of the most important advanced SQL topics.
