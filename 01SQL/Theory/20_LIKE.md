# LIKE

## What is LIKE?

Used for pattern matching.

---

## Syntax

SELECT *
FROM employees
WHERE employee_name LIKE 'R%';

---

## Common Patterns

R%   Starts with R

%R   Ends with R

%R%  Contains R

_R%  Second character R

---

## Business Use Cases

- Customer search
- Product search
- Email filtering

---

## Interview Questions

Q1. Difference between LIKE and = ?

Q2. Can LIKE use indexes?
