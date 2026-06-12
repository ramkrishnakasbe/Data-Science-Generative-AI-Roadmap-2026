# WHERE

## What is WHERE?

WHERE is used to filter records based on specific conditions.

It allows us to retrieve only relevant data.

---

## Why Do We Need WHERE?

Businesses rarely analyze all records.

Examples:

* Customers from Pune
* Employees earning above ₹50,000
* Orders placed this month

WHERE helps filter the data.

---

## Syntax

```sql
SELECT column_name
FROM table_name
WHERE condition;
```

---

## Example Dataset

### Employees

| employee_id | employee_name | department | salary |
| ----------- | ------------- | ---------- | ------ |
| 101         | Ram           | Sales      | 50000  |
| 102         | Amit          | IT         | 70000  |
| 103         | Neha          | HR         | 45000  |

---

## Example Query

```sql
SELECT employee_name,
       salary
FROM employees
WHERE salary > 50000;
```

---

## Output

| employee_name | salary |
| ------------- | ------ |
| Amit          | 70000  |

---

## Common Operators

### Equal To

```sql
WHERE department = 'IT'
```

### Greater Than

```sql
WHERE salary > 50000
```

### Less Than

```sql
WHERE salary < 50000
```

### Not Equal

```sql
WHERE department <> 'HR'
```

---

## Multiple Conditions

### AND

```sql
WHERE department = 'IT'
AND salary > 60000
```

### OR

```sql
WHERE department = 'IT'
OR department = 'HR'
```

---

## Business Use Cases

### Sales Analysis

Find sales above target.

### HR Analytics

Find high-performing employees.

### Supply Chain

Find low-stock products.

### Customer Analytics

Find premium customers.

---

## Common Mistakes

### Using HAVING Instead of WHERE

Wrong:

```sql
SELECT *
FROM employees
HAVING salary > 50000;
```

Correct:

```sql
SELECT *
FROM employees
WHERE salary > 50000;
```

### Comparing Text Incorrectly

Case sensitivity may vary across databases.

---

## Performance Considerations

✔ Filter early

✔ Use indexed columns

✔ Avoid unnecessary functions in WHERE clause

---

## Interview Questions

### What is WHERE?

Used to filter rows before processing.

### WHERE vs HAVING?

WHERE filters rows.

HAVING filters groups after aggregation.

### Can WHERE use aggregate functions?

No.

Use HAVING.

---

## Practice Questions

1. Find employees earning above ₹60,000.
2. Find IT employees.
3. Find orders above ₹10,000.
4. Find products with stock below 50.

---

## Key Takeaways

✔ Filters rows

✔ Executes before GROUP BY

✔ One of the most important SQL clauses
