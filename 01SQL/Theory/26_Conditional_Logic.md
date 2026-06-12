# Conditional Logic in SQL

## What is Conditional Logic?

Conditional Logic allows SQL to make decisions based on conditions.

It helps:

* Categorize data
* Handle NULL values
* Create business rules
* Improve reporting

The three most commonly used conditional functions are:

1. CASE WHEN
2. COALESCE
3. NULLIF

---

# Example Dataset

## Employees

| employee_id | employee_name | department | salary | bonus |
| ----------- | ------------- | ---------- | ------ | ----- |
| 101         | Ram           | Sales      | 50000  | 5000  |
| 102         | Amit          | IT         | 75000  | NULL  |
| 103         | Neha          | HR         | 45000  | 2000  |
| 104         | Priya         | Finance    | 90000  | NULL  |
| 105         | Raj           | Sales      | 30000  | 1000  |

---

# 1. CASE WHEN

## What is CASE WHEN?

CASE WHEN works like IF-ELSE statements in programming languages.

It evaluates conditions and returns values based on those conditions.

---

## Syntax

```sql
CASE
    WHEN condition1 THEN result1
    WHEN condition2 THEN result2
    ELSE result3
END
```

---

## Example 1: Salary Classification

```sql
SELECT
    employee_name,
    salary,
    CASE
        WHEN salary >= 80000 THEN 'High Salary'
        WHEN salary >= 50000 THEN 'Medium Salary'
        ELSE 'Low Salary'
    END AS salary_category
FROM employees;
```

---

## Output

| employee_name | salary | salary_category |
| ------------- | ------ | --------------- |
| Ram           | 50000  | Medium Salary   |
| Amit          | 75000  | Medium Salary   |
| Neha          | 45000  | Low Salary      |
| Priya         | 90000  | High Salary     |
| Raj           | 30000  | Low Salary      |

---

## Example 2: Department Bonus Percentage

```sql
SELECT
    employee_name,
    department,
    CASE
        WHEN department='Sales' THEN 10
        WHEN department='IT' THEN 8
        ELSE 5
    END AS bonus_percent
FROM employees;
```

---

## Business Use Cases

### Customer Segmentation

```text
Premium
Gold
Silver
Basic
```

### Risk Classification

```text
High Risk
Medium Risk
Low Risk
```

### Sales Performance

```text
Excellent
Average
Poor
```

---

## Common Mistakes

### Missing ELSE

```sql
CASE
    WHEN salary > 50000 THEN 'High'
END
```

Rows not matching condition return NULL.

---

# 2. COALESCE

## What is COALESCE?

COALESCE returns the first non-NULL value from a list.

---

## Why Do We Need COALESCE?

NULL values often create issues in reports.

COALESCE provides default values.

---

## Syntax

```sql
COALESCE(value1, value2, value3)
```

Returns the first non-null value.

---

## Example Dataset

| employee_name | bonus |
| ------------- | ----- |
| Ram           | 5000  |
| Amit          | NULL  |
| Neha          | 2000  |
| Priya         | NULL  |

---

## Example 1

```sql
SELECT
    employee_name,
    COALESCE(bonus,0) AS final_bonus
FROM employees;
```

---

## Output

| employee_name | final_bonus |
| ------------- | ----------- |
| Ram           | 5000        |
| Amit          | 0           |
| Neha          | 2000        |
| Priya         | 0           |

---

## Example 2

```sql
SELECT
    employee_name,
    COALESCE(bonus,salary,0)
FROM employees;
```

Logic:

1. Bonus
2. Salary
3. Zero

Returns first available value.

---

## Business Use Cases

### Financial Reporting

Replace NULL revenue with 0.

### Customer Analytics

Replace missing city with "Unknown".

### Dashboards

Prevent blank values.

---

## Common Mistakes

### Confusing COALESCE with CASE

COALESCE only checks NULL values.

CASE handles all logical conditions.

---

# 3. NULLIF

## What is NULLIF?

NULLIF compares two expressions.

If both values are equal:

Returns NULL

Otherwise:

Returns first value

---

## Syntax

```sql
NULLIF(expression1, expression2)
```

---

## Example 1

```sql
SELECT NULLIF(100,100);
```

Output:

```text
NULL
```

---

## Example 2

```sql
SELECT NULLIF(100,50);
```

Output:

```text
100
```

---

## Practical Example

### Employees Table

| employee_name | bonus |
| ------------- | ----- |
| Ram           | 5000  |
| Amit          | 0     |
| Neha          | 2000  |

---

Convert zero bonuses to NULL.

```sql
SELECT
    employee_name,
    NULLIF(bonus,0) AS updated_bonus
FROM employees;
```

---

## Output

| employee_name | updated_bonus |
| ------------- | ------------- |
| Ram           | 5000          |
| Amit          | NULL          |
| Neha          | 2000          |

---

## Prevent Division by Zero

Very common interview question.

Wrong:

```sql
SELECT revenue/quantity
FROM sales;
```

Error if quantity = 0.

Correct:

```sql
SELECT revenue/NULLIF(quantity,0)
FROM sales;
```

---

## Business Use Cases

### Revenue Analysis

Prevent divide-by-zero errors.

### Data Cleaning

Convert default values to NULL.

### KPI Reporting

Handle missing values correctly.

---

# Comparison

| Function  | Purpose                         |
| --------- | ------------------------------- |
| CASE WHEN | Apply business logic            |
| COALESCE  | Replace NULL values             |
| NULLIF    | Convert matching values to NULL |

---

# Interview Questions

### Q1. Difference between CASE and COALESCE?

CASE handles conditions.

COALESCE handles NULL values.

---

### Q2. Difference between COALESCE and NULLIF?

COALESCE replaces NULL.

NULLIF creates NULL.

---

### Q3. Why is NULLIF used in division?

To prevent divide-by-zero errors.

---

### Q4. Can CASE be used in SELECT?

Yes.

Can also be used in:

* WHERE
* ORDER BY
* GROUP BY

---

### Q5. Which function is most common in reporting?

COALESCE

---

# Practice Questions

1. Categorize employees based on salary.
2. Replace NULL bonus with 0.
3. Replace missing city values with 'Unknown'.
4. Convert bonus=0 to NULL.
5. Prevent divide-by-zero errors using NULLIF.
6. Create customer tiers using CASE WHEN.

---

# Real World Data Scientist Use Cases

### Churn Analysis

CASE WHEN for customer classification.

### Revenue Dashboard

COALESCE for missing values.

### KPI Reporting

NULLIF for safe calculations.

### Customer Segmentation

CASE WHEN for Gold/Silver/Bronze classification.

---

# Key Takeaways

✔ CASE WHEN applies business rules.

✔ COALESCE replaces NULL values.

✔ NULLIF creates NULL values when expressions match.

✔ Frequently asked in SQL interviews.

✔ Used heavily in reporting and analytics projects.
