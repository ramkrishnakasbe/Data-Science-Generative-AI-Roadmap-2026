# Indexes in SQL

## What is an Index?

An Index is a database object that improves query performance.

Think of an index like a book's index page.

Instead of reading every page, you directly jump to the required section.

---

# Why Do We Need Indexes?

Without Index:

```text
Full Table Scan
```

Database checks every row.

With Index:

```text
Direct Lookup
```

Database quickly finds required records.

---

# Example

## Employees

| employee_id | employee_name | salary |
|------------|---------------|---------|
| 101 | Ram | 50000 |
| 102 | Amit | 70000 |
| ... | ... | ... |
| 1000000 | Raj | 30000 |

---

## Query

```sql
SELECT *
FROM employees
WHERE employee_id = 1000000;
```

Without Index:

```text
1 Million Rows Checked
```

With Index:

```text
Direct Search
```

---

# Create Index

```sql
CREATE INDEX idx_employee_id
ON employees(employee_id);
```

---

# Types of Indexes

1. Clustered Index
2. Non-Clustered Index
3. Composite Index
4. Unique Index
5. Covering Index
6. B-Tree Index

---

# Clustered Index

## Definition

Determines physical order of data.

Only one Clustered Index per table.

---

## Example

```sql
PRIMARY KEY(employee_id)
```

Usually creates Clustered Index.

---

# Non-Clustered Index

Stores pointers to actual rows.

Multiple Non-Clustered Indexes allowed.

---

## Example

```sql
CREATE INDEX idx_department
ON employees(department);
```

---

# Composite Index

Index on multiple columns.

---

## Example

```sql
CREATE INDEX idx_dept_salary
ON employees(department,salary);
```

---

## Useful For

```sql
WHERE department='IT'
AND salary > 50000
```

---

# Unique Index

Prevents duplicate values.

---

## Example

```sql
CREATE UNIQUE INDEX idx_email
ON customers(email);
```

---

# Covering Index

Contains all columns required by query.

---

## Example

```sql
CREATE INDEX idx_cover
ON employees(department,salary);
```

Query:

```sql
SELECT department,salary
FROM employees;
```

Database may avoid table access.

---

# B-Tree Index

Most commonly used index structure.

Advantages:

✔ Fast Search

✔ Fast Insert

✔ Fast Delete

✔ Fast Range Queries

---

# Index Performance

## Good For

```sql
WHERE
JOIN
ORDER BY
GROUP BY
```

---

## Example

```sql
SELECT *
FROM employees
WHERE employee_id=100;
```

---

# Bad For

Very small tables.

---

## Example

10-row table doesn't need indexes.

---

# Drawbacks of Indexes

❌ More Storage

❌ Slower Inserts

❌ Slower Updates

❌ Slower Deletes

---

# Real World Use Cases

## Customer Search

```sql
customer_id
```

---

## Product Search

```sql
product_id
```

---

## Banking Systems

```sql
account_number
```

---

## E-commerce

```sql
customer_id
order_id
```

---

# Interview Questions

## What is an Index?

Improves query performance.

---

## Clustered vs Non-Clustered?

Clustered affects physical order.

Non-Clustered stores pointers.

---

## How Many Clustered Indexes?

Only one.

---

## Why Are Indexes Fast?

Avoid full table scans.

---

## Can Too Many Indexes Be Bad?

Yes.

They slow write operations.

---

# Key Takeaways

✔ Indexes improve query speed.

✔ Most databases use B-Tree indexes.

✔ Clustered Index controls storage order.

✔ Non-Clustered Index stores pointers.

✔ Essential for performance tuning.
