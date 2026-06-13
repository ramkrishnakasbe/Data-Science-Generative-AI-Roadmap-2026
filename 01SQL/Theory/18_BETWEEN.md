# BETWEEN

## What is BETWEEN?

Filters records within a range.

---

## Syntax

SELECT *
FROM employees
WHERE salary BETWEEN 50000 AND 100000;

---

## Important

BETWEEN is inclusive.

50000 included.

100000 included.

---

## Business Use Cases

- Salary range

The following SQL returns all products with a price between 10 and 20:

Example

SELECT * FROM Products
WHERE Price BETWEEN 10 AND 20;

- Date range
- Price range

---

## Interview Questions

Q1. Is BETWEEN inclusive?

Answer: Yes.
