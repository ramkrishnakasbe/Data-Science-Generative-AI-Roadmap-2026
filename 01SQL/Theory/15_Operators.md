# SQL Operators

## What are SQL Operators?

SQL operators are special symbols or keywords used to perform operations on data and evaluate conditions.

Operators are commonly used in:

* WHERE clause
* HAVING clause
* CASE statements
* JOIN conditions

---

# Types of SQL Operators

1. Arithmetic Operators
2. Comparison Operators
3. Logical Operators
4. Set Operators
5. Special Operators

---

# 1. Arithmetic Operators

Used for mathematical calculations.

| Operator | Description    | Example            |
| -------- | -------------- | ------------------ |
| +        | Addition       | salary + 1000      |
| -        | Subtraction    | salary - 1000      |
| *        | Multiplication | quantity * price   |
| /        | Division       | revenue / quantity |
| %        | Modulus        | salary % 2         |

---

## Examples

```sql
SELECT salary + 5000 AS revised_salary
FROM employees;
```

```sql
SELECT quantity * unit_price AS total_amount
FROM orders;
```

---

# 2. Comparison Operators

Used to compare values.

| Operator | Description           |
| -------- | --------------------- |
| =        | Equal To              |
| !=       | Not Equal To          |
| <>       | Not Equal To          |
| >        | Greater Than          |
| <        | Less Than             |
| >=       | Greater Than Equal To |
| <=       | Less Than Equal To    |

---

## Examples

### Equal To

```sql
SELECT *
FROM employees
WHERE department = 'IT';
```

### Greater Than

```sql
SELECT *
FROM employees
WHERE salary > 50000;
```

### Less Than

```sql
SELECT *
FROM employees
WHERE salary < 50000;
```

### Not Equal To

```sql
SELECT *
FROM employees
WHERE department <> 'HR';
```

---

# 3. Logical Operators

Used to combine conditions.

| Operator | Description                  |
| -------- | ---------------------------- |
| AND      | Both conditions must be true |
| OR       | Any condition can be true    |
| NOT      | Negates condition            |

---

## AND Example

```sql
SELECT *
FROM employees
WHERE department='IT'
AND salary > 60000;
```

---

## OR Example

```sql
SELECT *
FROM employees
WHERE department='IT'
OR department='HR';
```

---

## NOT Example

```sql
SELECT *
FROM employees
WHERE NOT department='HR';
```

---

# 4. Set Operators

Combine results from multiple queries.

| Operator  | Description                   |
| --------- | ----------------------------- |
| UNION     | Removes duplicates            |
| UNION ALL | Keeps duplicates              |
| INTERSECT | Common records                |
| EXCEPT    | Records from first query only |

---

## UNION Example

```sql
SELECT city FROM customers
UNION
SELECT city FROM suppliers;
```

---

## UNION ALL Example

```sql
SELECT city FROM customers
UNION ALL
SELECT city FROM suppliers;
```

---

# 5. Special Operators

* IN
* NOT IN
* BETWEEN
* NOT BETWEEN
* LIKE
* EXISTS
* IS NULL

---

# Operator Precedence

Highest Priority:

```text
()
NOT
AND
OR
```

Example:

```sql
SELECT *
FROM employees
WHERE department='IT'
OR department='HR'
AND salary > 50000;
```

Always use parentheses.

```sql
SELECT *
FROM employees
WHERE (department='IT'
OR department='HR')
AND salary > 50000;
```

---

# Business Use Cases

### Sales

Find products with sales above target.

### HR

Find employees meeting salary criteria.

### Finance

Calculate profit margins.

### Supply Chain

Identify low-stock items.

---

# Common Mistakes

### Using OR instead of AND

Wrong filtering results.

### Ignoring Precedence

Produces incorrect output.

### Using = NULL

Incorrect.

Use:

```sql
IS NULL
```

---

# Interview Questions

Q1. Difference between = and IN?

Q2. Difference between UNION and UNION ALL?

Q3. What is operator precedence?

Q4. Difference between AND and OR?

Q5. Why is IS NULL used instead of = NULL?

---

# Key Takeaways

✔ Operators perform calculations and comparisons

✔ Essential for filtering and analysis

✔ Understanding precedence is critical

✔ Frequently asked in interviews
