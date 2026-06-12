# LIMIT

## What is LIMIT?

LIMIT restricts the number of rows returned by a query.

---

## Why Do We Need LIMIT?

Large tables may contain millions of records.

LIMIT helps:

- Preview data
- Improve performance
- Build dashboards
- Return top records

---

## Syntax

```sql
SELECT *
FROM employees
LIMIT 5;
```

---

## Example Dataset

| employee_id | employee_name |
|------------|---------------|
| 101 | Ram |
| 102 | Amit |
| 103 | Neha |
| 104 | Priya |
| 105 | Raj |

---

## Example Query

```sql
SELECT *
FROM employees
LIMIT 3;
```

---

## Output

| employee_id | employee_name |
|------------|---------------|
| 101 | Ram |
| 102 | Amit |
| 103 | Neha |

---

## Top N Records

```sql
SELECT *
FROM employees
ORDER BY salary DESC
LIMIT 5;
```

---

## Business Use Cases

### Dashboard

Show Top 10 products.

### HR

Show Top 5 salaries.

### Finance

Show latest 20 transactions.

---

## Common Mistakes

### LIMIT Without ORDER BY

```sql
SELECT *
FROM employees
LIMIT 5;
```

Results may vary.

Better:

```sql
SELECT *
FROM employees
ORDER BY salary DESC
LIMIT 5;
```

---

## Performance Considerations

✔ Improves performance

✔ Reduces network traffic

✔ Common in pagination

---

## Interview Questions

Q1. What does LIMIT do?

Restricts number of rows.

Q2. Can LIMIT work without ORDER BY?

Yes, but results are unpredictable.

Q3. Difference between LIMIT and TOP?

LIMIT → PostgreSQL/MySQL

TOP → SQL Server

---

## Practice Questions

1. Top 10 employees.
2. Top 5 customers.
3. Latest 20 orders.

---

## Key Takeaways

✔ Restricts result size

✔ Frequently used with ORDER BY

✔ Improves performance
