# IS NULL

## What is IS NULL?

Checks for NULL values.

---

## Syntax

SELECT *
FROM employees
WHERE salary IS NULL;

---

## Why Not = NULL?

Wrong:

salary = NULL

Correct:

salary IS NULL

---

## Interview Questions

Q1. Why can't we use = NULL?
