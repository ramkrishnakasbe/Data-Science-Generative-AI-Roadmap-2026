# SQL Query Optimization

## What is SQL Optimization?

SQL Optimization means improving query performance while reducing:

- CPU Usage
- Memory Usage
- Execution Time
- Disk Reads

---

# Why Is Optimization Important?

Imagine:

```text
1 Million Rows
```

Bad Query:

```text
20 Seconds
```

Optimized Query:

```text
0.2 Seconds
```

---

# Query Execution Plan

Database creates an execution plan.

Shows:

- Table Scans
- Index Usage
- Joins
- Costs

---

# EXPLAIN

Used to view execution plan.

---

## Example

```sql
EXPLAIN
SELECT *
FROM employees
WHERE employee_id=101;
```

---

# EXPLAIN ANALYZE

Executes query and shows actual performance.

---

## Example

```sql
EXPLAIN ANALYZE
SELECT *
FROM employees
WHERE employee_id=101;
```

---

# Full Table Scan

## Problem

```sql
SELECT *
FROM employees
WHERE employee_name='Ram';
```

Without index:

```text
Checks Every Row
```

---

# Solution

```sql
CREATE INDEX idx_name
ON employees(employee_name);
```

---

# Avoid SELECT *

❌ Bad

```sql
SELECT *
FROM employees;
```

---

✅ Good

```sql
SELECT
employee_id,
employee_name
FROM employees;
```

---

# Use Proper WHERE Conditions

❌ Bad

```sql
SELECT *
FROM employees
WHERE UPPER(name)='RAM';
```

May ignore indexes.

---

✅ Better

```sql
SELECT *
FROM employees
WHERE name='Ram';
```

---

# Limit Returned Rows

```sql
SELECT *
FROM employees
LIMIT 10;
```

---

# Optimize JOINs

❌ Bad

```sql
SELECT *
FROM table1
CROSS JOIN table2;
```

---

✅ Better

```sql
SELECT *
FROM table1 t1
JOIN table2 t2
ON t1.id=t2.id;
```

---

# Use EXISTS Instead of IN

Large Dataset:

```sql
WHERE EXISTS(...)
```

Often faster than:

```sql
WHERE IN(...)
```

---

# Use UNION ALL

❌

```sql
UNION
```

Removes duplicates.

---

✅

```sql
UNION ALL
```

Faster.

---

# Index Frequently Used Columns

Ideal Candidates:

```sql
WHERE
JOIN
GROUP BY
ORDER BY
```

---

# Example

```sql
CREATE INDEX idx_customer
ON orders(customer_id);
```

---

# Avoid Functions in WHERE

❌

```sql
WHERE YEAR(order_date)=2025
```

---

✅

```sql
WHERE order_date
BETWEEN '2025-01-01'
AND '2025-12-31'
```

---

# Partition Large Tables

Useful for:

- Billion-row datasets
- Historical data

---

# Query Cost

Database assigns estimated cost.

Lower cost generally means better performance.

---

# Common Bottlenecks

1. Missing Indexes
2. Full Table Scans
3. Large Joins
4. Too Many Subqueries
5. Poor Data Types

---

# SQL Optimization Checklist

## Before Running Query

✔ Use proper indexes

✔ Avoid SELECT *

✔ Filter early

✔ Use LIMIT

✔ Optimize joins

✔ Check execution plan

✔ Use UNION ALL when possible

✔ Avoid unnecessary subqueries

---

# Real World Example

## Slow Query

```sql
SELECT *
FROM orders
WHERE customer_id=5000;
```

Time:

```text
5 Seconds
```

---

## Add Index

```sql
CREATE INDEX idx_customer
ON orders(customer_id);
```

Time:

```text
0.02 Seconds
```

---

# Real World Data Science Use Cases

## Feature Engineering

Large aggregations.

---

## ETL Pipelines

Fast data processing.

---

## Dashboard Queries

Sub-second response times.

---

## Model Training Data

Efficient extraction.

---

# Common Interview Questions

## What is Query Optimization?

Improving SQL performance.

---

## What is EXPLAIN?

Shows execution plan.

---

## What is EXPLAIN ANALYZE?

Runs query and shows actual execution statistics.

---

## What Causes Full Table Scan?

Missing indexes.

---

## Why Avoid SELECT *?

Unnecessary data retrieval.

---

## Why Use Indexes?

Faster lookups.

---

## Why Is UNION ALL Faster?

No duplicate removal.

---

# Performance Tuning Workflow

Step 1

```sql
EXPLAIN
```

Step 2

Identify bottlenecks.

Step 3

Add indexes.

Step 4

Rewrite query.

Step 5

Validate with:

```sql
EXPLAIN ANALYZE
```

---

# Key Takeaways

✔ Optimization improves performance.

✔ Use EXPLAIN and EXPLAIN ANALYZE.

✔ Avoid full table scans.

✔ Create proper indexes.

✔ Avoid SELECT *.

✔ Optimize joins and filters.

✔ SQL Optimization is a common senior-level interview topic.
