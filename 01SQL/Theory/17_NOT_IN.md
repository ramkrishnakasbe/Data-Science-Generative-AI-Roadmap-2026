# NOT IN

## What is NOT IN?

Returns records whose values do not exist in a given list.

---

## Syntax

SELECT *
FROM employees
WHERE department NOT IN ('HR','Finance');

---

## Business Use Cases

- Exclude specific regions
- Exclude inactive customers
- Exclude categories

---

## Interview Questions

Q1. NOT IN vs NOT EXISTS?

Q2. How does NULL affect NOT IN?
