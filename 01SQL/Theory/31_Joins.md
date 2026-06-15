# SQL Joins

## What are Joins?

Joins are used to combine data from multiple tables based on a related column.

In real-world databases, data is usually stored across multiple tables.

Example:

- Customers Table
- Orders Table
- Products Table

To analyze business data, we need to combine information from these tables.

That's where Joins come in.

---

# Why Do We Need Joins?

Imagine an E-commerce Company.

### Customers Table

| customer_id | customer_name |
|------------|---------------|
| 1 | Ram |
| 2 | Amit |
| 3 | Neha |
| 4 | Priya |

---

### Orders Table

| order_id | customer_id | amount |
|-----------|------------|---------|
| 101 | 1 | 500 |
| 102 | 2 | 700 |
| 103 | 1 | 300 |
| 104 | 5 | 900 |

---

Question:

Which customer placed which order?

Information is stored in separate tables.

Joins help combine them.

---

# Types of SQL Joins

1. INNER JOIN
2. LEFT JOIN
3. RIGHT JOIN
4. FULL JOIN
5. CROSS JOIN
6. SELF JOIN

---

# Visual Representation

```text
INNER JOIN
      A ∩ B

LEFT JOIN
      A + Matching B

RIGHT JOIN
      B + Matching A

FULL JOIN
      A + B

CROSS JOIN
      Every Possible Combination

SELF JOIN
      Table Joined With Itself
```

---

# INNER JOIN

## What is INNER JOIN?

Returns only matching records from both tables.

Most commonly used join.

---

## Syntax

```sql
SELECT *
FROM table1 t1
INNER JOIN table2 t2
ON t1.id = t2.id;
```

---

## Example

```sql
SELECT
    c.customer_name,
    o.order_id,
    o.amount
FROM customers c
INNER JOIN orders o
ON c.customer_id = o.customer_id;
```

---

## Output

| customer_name | order_id | amount |
|--------------|----------|---------|
| Ram | 101 | 500 |
| Amit | 102 | 700 |
| Ram | 103 | 300 |

---

## Visualization

```text
Customers      Orders

1 Ram      ←→  1
2 Amit     ←→  2
3 Neha
4 Priya

Only Matching Records Returned
```

---

# LEFT JOIN

## What is LEFT JOIN?

Returns:

- All records from Left Table
- Matching records from Right Table

If no match exists:

NULL values are returned.

---

## Syntax

```sql
SELECT *
FROM table1
LEFT JOIN table2
ON table1.id = table2.id;
```

---

## Example

```sql
SELECT
    c.customer_name,
    o.order_id
FROM customers c
LEFT JOIN orders o
ON c.customer_id = o.customer_id;
```

---

## Output

| customer_name | order_id |
|--------------|----------|
| Ram | 101 |
| Ram | 103 |
| Amit | 102 |
| Neha | NULL |
| Priya | NULL |

---

## Visualization

```text
Customers

Ram
Amit
Neha
Priya

ALL Returned
```

---

## Business Use Cases

Find customers who never placed orders.

```sql
SELECT *
FROM customers c
LEFT JOIN orders o
ON c.customer_id=o.customer_id
WHERE o.order_id IS NULL;
```

---

# RIGHT JOIN

## What is RIGHT JOIN?

Returns:

- All records from Right Table
- Matching records from Left Table

---

## Syntax

```sql
SELECT *
FROM table1
RIGHT JOIN table2
ON table1.id = table2.id;
```

---

## Example

```sql
SELECT
    c.customer_name,
    o.order_id
FROM customers c
RIGHT JOIN orders o
ON c.customer_id=o.customer_id;
```

---

## Output

| customer_name | order_id |
|--------------|----------|
| Ram | 101 |
| Amit | 102 |
| Ram | 103 |
| NULL | 104 |

---

## Why NULL?

Order 104 belongs to customer_id = 5.

Customer doesn't exist in Customers table.

---

# FULL JOIN

## What is FULL JOIN?

Returns:

- All rows from Left Table
- All rows from Right Table

Matching records are merged.

Non-matching records show NULL.

---

## Syntax

```sql
SELECT *
FROM table1
FULL JOIN table2
ON table1.id = table2.id;
```

---

## Example

```sql
SELECT
    c.customer_name,
    o.order_id
FROM customers c
FULL JOIN orders o
ON c.customer_id=o.customer_id;
```

---

## Output

| customer_name | order_id |
|--------------|----------|
| Ram | 101 |
| Amit | 102 |
| Ram | 103 |
| Neha | NULL |
| Priya | NULL |
| NULL | 104 |

---

## Visualization

```text
Everything from Both Tables
```

---

# CROSS JOIN

## What is CROSS JOIN?

Returns every possible combination.

Cartesian Product.

---

## Example

### Table A

| color |
|---------|
| Red |
| Blue |

---

### Table B

| size |
|--------|
| Small |
| Large |

---

## Query

```sql
SELECT *
FROM colors
CROSS JOIN sizes;
```

---

## Output

| color | size |
|--------|------|
| Red | Small |
| Red | Large |
| Blue | Small |
| Blue | Large |

---

## Formula

```text
Rows Returned

Table A Rows × Table B Rows
```

---

## Business Use Cases

- Product combinations
- Recommendation systems
- Test data generation

---

# SELF JOIN

## What is SELF JOIN?

A table joined with itself.

Useful for hierarchical data.

---

# Employees Table

| employee_id | employee_name | manager_id |
|------------|---------------|------------|
| 1 | Ram | NULL |
| 2 | Amit | 1 |
| 3 | Neha | 1 |
| 4 | Priya | 2 |

---

## Query

```sql
SELECT column_name(s)
FROM table1 T1, table1 T2
WHERE condition;
```

---

## Output

| employee | manager |
|-----------|---------|
| Ram | NULL |
| Amit | Ram |
| Neha | Ram |
| Priya | Amit |

---

## Business Use Cases

- Employee hierarchy
- Organization charts
- Category hierarchy

---

# Join Execution Order

```text
FROM
JOIN
ON
WHERE
GROUP BY
HAVING
SELECT
ORDER BY
LIMIT
```

---

# Common Interview Questions

## Q1. Difference Between INNER and LEFT JOIN?

INNER JOIN:

Only matching records.

LEFT JOIN:

All records from left table.

---

## Q2. Difference Between LEFT and RIGHT JOIN?

LEFT JOIN:

Keeps all rows from left table.

RIGHT JOIN:

Keeps all rows from right table.

---

## Q3. Difference Between JOIN and UNION?

JOIN:

Combines columns.

UNION:

Combines rows.

---

## Q4. Which Join Returns Unmatched Records?

LEFT JOIN

RIGHT JOIN

FULL JOIN

---

## Q5. What is Cartesian Product?

Result of CROSS JOIN.

---

## Q6. What is SELF JOIN?

Joining a table with itself.

---

# Real-World Data Science Use Cases

## Customer Analytics

```sql
Customers + Orders
```

---

## Sales Analytics

```sql
Orders + Products
```

---

## HR Analytics

```sql
Employees + Departments
```

---

## Marketing Analytics

```sql
Customers + Campaigns
```

---

## Recommendation Systems

```sql
CROSS JOIN
```

---

# Common Mistakes

## Missing Join Condition

❌ Wrong

```sql
SELECT *
FROM customers
JOIN orders;
```

Produces huge Cartesian Product.

---

## Correct

```sql
SELECT *
FROM customers c
JOIN orders o
ON c.customer_id=o.customer_id;
```

---

## Using Wrong Join Type

Choosing INNER JOIN when unmatched records are required.

---

# Performance Considerations

## Fastest

```text
INNER JOIN
```

---

## Slower

```text
LEFT JOIN
RIGHT JOIN
```

---

## Most Expensive

```text
FULL JOIN
CROSS JOIN
```

---

# Practice Questions

1. Find all customer orders.
2. Find customers without orders.
3. Find orders without customers.
4. Find all records from both tables.
5. Generate all product combinations.
6. Find employee-manager hierarchy.
7. Find department-wise employee count using joins.
8. Find top customers by sales amount.
9. Join three tables together.
10. Build customer order reports.

---

# Key Takeaways

✔ INNER JOIN returns matching records only.

✔ LEFT JOIN returns all left table records.

✔ RIGHT JOIN returns all right table records.

✔ FULL JOIN returns everything from both tables.

✔ CROSS JOIN creates all possible combinations.

✔ SELF JOIN joins a table with itself.

✔ Joins are among the most frequently asked SQL interview topics.

✔ Every Data Scientist should be comfortable writing complex joins.
