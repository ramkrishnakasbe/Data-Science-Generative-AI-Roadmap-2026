# DISTINCT

## What is DISTINCT?

DISTINCT removes duplicate values from the result set.

It returns only unique records.

---

## Why Do We Need DISTINCT?

Business data often contains duplicate values.

Examples:

* Cities
* Product Categories
* Departments

DISTINCT helps identify unique values.

---

## Syntax

```sql
SELECT DISTINCT column_name
FROM table_name;
```

---

## Example Dataset

### Employees

| employee_id | employee_name | department |
| ----------- | ------------- | ---------- |
| 101         | Ram           | Sales      |
| 102         | Amit          | IT         |
| 103         | Neha          | Sales      |
| 104         | Priya         | HR         |

---

## Example Query

```sql
SELECT DISTINCT department
FROM employees;
```

---

## Output

| department |
| ---------- |
| Sales      |
| IT         |
| HR         |

---

## Business Use Cases

### Marketing

Identify unique customer locations.

### HR

Identify departments.

### Retail

Identify product categories.

---

## Common Mistakes

### Assuming DISTINCT Removes Duplicate Rows Only

DISTINCT works on selected columns.

Example:

```sql
SELECT DISTINCT department
FROM employees;
```

Not entire records.

---

## Performance Considerations

DISTINCT can be expensive on very large datasets.

Use only when necessary.

---

## Interview Questions

### What is DISTINCT?

Used to remove duplicate values.

### DISTINCT vs GROUP BY?

Both can return unique values.

GROUP BY is mainly used with aggregate functions.

### Can DISTINCT be used on multiple columns?

Yes.

```sql
SELECT DISTINCT department,
                city
FROM employees;
```

---

## Practice Questions

1. Find unique cities.
2. Find unique departments.
3. Find unique product categories.

---

## Key Takeaways

✔ Removes duplicates

✔ Returns unique values

✔ Useful for data exploration
