# Aliases

## What is an Alias?

An alias is a temporary name assigned to a column or table.

Aliases improve readability.

---

## Why Do We Need Aliases?

Without aliases:

```sql
SELECT SUM(sales_amount)
FROM sales;
```

Output:

```text
sum
```

With alias:

```sql
SELECT SUM(sales_amount) AS total_sales
FROM sales;
```

Output:

```text
total_sales
```

---

## Column Alias

```sql
SELECT employee_name AS name
FROM employees;
```

---

## Table Alias

```sql
SELECT e.employee_name
FROM employees e;
```

---

## Example Dataset

Employees

| employee_id | employee_name |
|------------|---------------|
| 101 | Ram |
| 102 | Amit |

---

## Example Query

```sql
SELECT employee_name AS employee
FROM employees;
```

---

## Output

| employee |
|----------|
| Ram |
| Amit |

---

## Aliases in Joins

```sql
SELECT c.customer_name,
       o.order_id
FROM customers c
INNER JOIN orders o
ON c.customer_id = o.customer_id;
```

---

## Business Use Cases

### Reporting

Readable column names.

### Dashboards

User-friendly outputs.

### Analytics

Complex query simplification.

---

## Common Mistakes

### Using Reserved Keywords

```sql
SELECT salary AS SELECT
FROM employees;
```

Invalid.

---

## Performance Considerations

Aliases do not affect performance.

Used only for readability.

---

## Interview Questions

Q1. What is an alias?

Temporary name for a column or table.

Q2. Does alias change actual column name?

No.

Q3. Why use table aliases?

Simplify joins.

---

## Practice Questions

1. Rename salary as employee_salary.
2. Rename customer_name as customer.
3. Use aliases in joins.

---

## Key Takeaways

✔ Improves readability

✔ Temporary name only

✔ Very useful in joins and reporting
