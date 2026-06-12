# EXISTS

## What is EXISTS?

Checks whether a subquery returns any rows.

---

## Syntax

SELECT *
FROM customers c
WHERE EXISTS
(
SELECT 1
FROM orders o
WHERE c.customer_id=o.customer_id
);

---

## Why EXISTS?

Efficient existence checking.

---

## Interview Questions

Q1. EXISTS vs IN?

Q2. Why SELECT 1 in EXISTS?
