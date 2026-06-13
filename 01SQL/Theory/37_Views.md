# Views in SQL

## What is a View?

A View is a virtual table created from a SQL query.

A View does not store data itself.

Instead, it stores the SQL query and fetches data from underlying tables whenever accessed.

---

# Why Use Views?

Views help:

- Simplify complex queries
- Hide sensitive data
- Improve readability
- Standardize reporting

---

# Example Table

## Employees

| employee_id | employee_name | department | salary |
|------------|---------------|------------|---------|
| 101 | Ram | Sales | 50000 |
| 102 | Amit | IT | 70000 |
| 103 | Neha | HR | 45000 |

---

# CREATE VIEW

## Syntax

```sql
CREATE VIEW view_name AS
SELECT columns
FROM table_name;
```

---

## Example

```sql
CREATE VIEW employee_details AS
SELECT
    employee_id,
    employee_name,
    department
FROM employees;
```

---

# Querying a View

```sql
SELECT *
FROM employee_details;
```

---

# View with Conditions

```sql
CREATE VIEW high_salary_employees AS
SELECT *
FROM employees
WHERE salary > 60000;
```

---

# Updating Views

```sql
CREATE OR REPLACE VIEW employee_details AS
SELECT
    employee_id,
    employee_name,
    department,
    salary
FROM employees;
```

---

# DROP VIEW

```sql
DROP VIEW employee_details;
```

---

# Advantages of Views

✔ Simplifies SQL

✔ Data Security

✔ Reusability

✔ Better Reporting

---

# Materialized Views

## What is a Materialized View?

Unlike a normal View:

- Stores data physically
- Faster query performance
- Requires refresh

---

## Example

```sql
CREATE MATERIALIZED VIEW monthly_sales AS
SELECT
    DATE_TRUNC('month', order_date) AS month,
    SUM(amount) AS revenue
FROM sales
GROUP BY month;
```

---

# Refresh Materialized View

```sql
REFRESH MATERIALIZED VIEW monthly_sales;
```

---

# View vs Table

| Feature | View | Table |
|----------|-------|--------|
| Stores Data | No | Yes |
| Physical Storage | No | Yes |
| Query Stored | Yes | No |
| Faster | No | Yes |
| Security | High | Medium |

---

# View vs Materialized View

| Feature | View | Materialized View |
|----------|------|------------------|
| Stores Data | No | Yes |
| Refresh Required | No | Yes |
| Query Speed | Slower | Faster |
| Storage | None | Requires Storage |

---

# Real World Use Cases

## Dashboard Reporting

```sql
CREATE VIEW sales_summary AS ...
```

---

## HR Reporting

```sql
CREATE VIEW employee_summary AS ...
```

---

## Finance Analytics

```sql
CREATE VIEW profit_report AS ...
```

---

# Interview Questions

## What is a View?

Virtual table based on a query.

---

## Difference Between View and Table?

View stores query.

Table stores data.

---

## Difference Between View and Materialized View?

Materialized View stores data physically.

---

## Can We Insert Into Views?

Sometimes.

Depends on database and view complexity.

---

# Key Takeaways

✔ View is a virtual table.

✔ Improves readability and security.

✔ Materialized Views improve performance.

✔ Frequently used in Reporting and BI projects.
