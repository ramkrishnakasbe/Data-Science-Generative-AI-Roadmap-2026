# TOP

## What is TOP?

TOP limits the number of rows returned by a query.

Used primarily in SQL Server.

---

## Syntax

```sql
SELECT TOP 5 *
FROM employees;
```

---

## Example

```sql
SELECT TOP 3
employee_name,
salary
FROM employees;
```

---

## Output

Returns first 3 rows.

---

## TOP with ORDER BY

```sql
SELECT TOP 5
employee_name,
salary
FROM employees
ORDER BY salary DESC;
```

---

## TOP Percentage

```sql
SELECT TOP 10 PERCENT *
FROM employees;
```

Returns top 10% rows.

---

## Business Use Cases

- Top customers
- Top products
- Highest revenue regions

---

## Interview Questions

Q1. TOP vs LIMIT?

TOP is SQL Server specific.

LIMIT is PostgreSQL/MySQL.

Q2. Can TOP return percentage?

Yes.

---

## Key Takeaways

✔ SQL Server equivalent of LIMIT

✔ Can return fixed rows or percentage12_TOP.md
