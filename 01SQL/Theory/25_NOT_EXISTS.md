# NOT EXISTS

## What is NOT EXISTS?

Returns records where no matching rows exist.

---

## Syntax

SELECT *
FROM customers c
WHERE NOT EXISTS
(
SELECT 1
FROM orders o
WHERE c.customer_id=o.customer_id
);

---

## Business Use Cases

- Customers without orders
- Employees without projects
- Products without sales

---

## Interview Questions

Q1. NOT EXISTS vs NOT IN?

Q2. Which performs better on large datasets?
