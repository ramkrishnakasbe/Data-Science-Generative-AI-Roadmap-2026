# ORDER BY

## What is ORDER BY?

ORDER BY is used to sort query results in ascending or descending order.

Without ORDER BY, SQL does not guarantee the order of returned records.

---

## Why Do We Need ORDER BY?

Businesses often need:

- Top-selling products
- Highest-paid employees
- Recent transactions
- Lowest inventory items

ORDER BY helps organize results for analysis.

---

## Syntax

```sql
SELECT column_name
FROM table_name
ORDER BY column_name;
```

Ascending Order (Default)

```sql
SELECT *
FROM employees
ORDER BY salary ASC;
```

Descending Order

```sql
SELECT *
FROM employees
ORDER BY salary DESC;
```

---

## Example Dataset

| employee_id | employee_name | salary |
|------------|---------------|---------|
| 101 | Ram | 50000 |
| 102 | Amit | 70000 |
| 103 | Neha | 45000 |

---

## Example Query

```sql
SELECT employee_name,
       salary
FROM employees
ORDER BY salary DESC;
```

---

## Output

| employee_name | salary |
|---------------|---------|
| Amit | 70000 |
| Ram | 50000 |
| Neha | 45000 |

---

## Multiple Column Sorting

```sql
SELECT *
FROM employees
ORDER BY department ASC,
         salary DESC;
```

---

## Business Use Cases

### HR

Top-paid employees.

### Sales

Highest revenue products.

### Finance

Largest transactions.

### Supply Chain

Low-stock inventory.

---

## Common Mistakes

### Assuming ORDER BY is Automatic

SQL does not guarantee order unless ORDER BY is specified.

### Wrong ASC/DESC Usage

Always verify business requirement.

---

## Performance Considerations

✔ Sorting large datasets can be expensive

✔ Indexes improve sorting performance

✔ Avoid unnecessary ORDER BY on huge tables

---

## Interview Questions

Q1. What is default sorting order?

Answer: ASC

Q2. Can ORDER BY use multiple columns?

Answer: Yes

Q3. Does ORDER BY execute before WHERE?

Answer: No

Execution Order:

FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY

---

## Practice Questions

1. Sort employees by salary.
2. Sort products by price.
3. Sort orders by order date.

---

## Key Takeaways

✔ Sorts query results

✔ ASC is default

✔ Supports multiple columns
