# FETCH

## What is FETCH?

FETCH is used to retrieve a specified number of rows.

Often used with OFFSET for pagination.

---

## Syntax

```sql
SELECT *
FROM employees
ORDER BY employee_id
FETCH FIRST 5 ROWS ONLY;
```

---

## Why Do We Need FETCH?

Useful for:

- Pagination
- Dashboards
- APIs
- Reporting

---

## Example

```sql
SELECT *
FROM employees
ORDER BY salary DESC
FETCH FIRST 3 ROWS ONLY;
```

---

## Output

Returns highest-paid 3 employees.

---

## FETCH with OFFSET

```sql
SELECT *
FROM employees
ORDER BY employee_id
OFFSET 10 ROWS
FETCH NEXT 5 ROWS ONLY;
```

---

## Business Use Cases

### E-Commerce

Product pages.

### Reporting

Paginated reports.

### Applications

User lists.

---

## Interview Questions

Q1. Difference between LIMIT and FETCH?

Both limit rows.

FETCH follows SQL standard.

Q2. Why use OFFSET?

Pagination.

---

## Key Takeaways

✔ Standard SQL feature

✔ Used with OFFSET

✔ Supports pagination
