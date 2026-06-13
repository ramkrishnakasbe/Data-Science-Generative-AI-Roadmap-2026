# Set Operators in SQL

## What are Set Operators?

Set Operators are used to combine the results of two or more SELECT statements.

Unlike Joins, which combine columns, Set Operators combine rows.

---

## Why Do We Need Set Operators?

Imagine a company has:

### Current Employees

| employee_id | employee_name |
| ----------- | ------------- |
| 101         | Ram           |
| 102         | Amit          |
| 103         | Neha          |

### Former Employees

| employee_id | employee_name |
| ----------- | ------------- |
| 103         | Neha          |
| 104         | Priya         |
| 105         | Raj           |

Business Questions:

* Show all employees
* Show unique employees
* Show common employees
* Show employees who left

Set Operators help answer these questions.

---

# Types of Set Operators

1. UNION
2. UNION ALL
3. INTERSECT
4. EXCEPT (MINUS in Oracle)

---

# Rules for Set Operators

Before using Set Operators:

### Rule 1

Number of columns must be same.

✅ Correct

```sql
SELECT employee_id
FROM current_employees

UNION

SELECT employee_id
FROM former_employees;
```

❌ Wrong

```sql
SELECT employee_id,
       employee_name
FROM current_employees

UNION

SELECT employee_id
FROM former_employees;
```

---

### Rule 2

Data types should be compatible.

✅

```sql
INT ↔ INT
VARCHAR ↔ VARCHAR
DATE ↔ DATE
```

---

### Rule 3

Column names are taken from the first query.

---

# UNION

## What is UNION?

Combines results and removes duplicates.

---

## Syntax

```sql
SELECT column_name
FROM table1

UNION

SELECT column_name
FROM table2;
```

---

## Example

### Current Employees

| employee_name |
| ------------- |
| Ram           |
| Amit          |
| Neha          |

### Former Employees

| employee_name |
| ------------- |
| Neha          |
| Priya         |
| Raj           |

---

## Query

```sql
SELECT employee_name
FROM current_employees

UNION

SELECT employee_name
FROM former_employees;
```

---

## Output

| employee_name |
| ------------- |
| Ram           |
| Amit          |
| Neha          |
| Priya         |
| Raj           |

---

Notice:

Neha appears only once.

Duplicates removed automatically.

---

## Business Use Cases

### Combine Customers

```sql
Current Customers
+
Former Customers
```

### Combine Regional Data

```sql
North Region
+
South Region
```

### Combine Multiple Sources

```sql
Website Users
+
Mobile App Users
```

---

# UNION ALL

## What is UNION ALL?

Combines results and keeps duplicates.

---

## Syntax

```sql
SELECT column_name
FROM table1

UNION ALL

SELECT column_name
FROM table2;
```

---

## Example

```sql
SELECT employee_name
FROM current_employees

UNION ALL

SELECT employee_name
FROM former_employees;
```

---

## Output

| employee_name |
| ------------- |
| Ram           |
| Amit          |
| Neha          |
| Neha          |
| Priya         |
| Raj           |

---

Notice:

Neha appears twice.

---

## Performance

UNION ALL is faster than UNION.

Reason:

No duplicate checking.

---

## Interview Question

### Which is faster?

✅ UNION ALL

Because duplicate elimination is not required.

---

# UNION vs UNION ALL

| Feature            | UNION | UNION ALL |
| ------------------ | ----- | --------- |
| Removes Duplicates | Yes   | No        |
| Faster             | No    | Yes       |
| Sorting Required   | Yes   | No        |
| Most Used          | Yes   | Yes       |

---

# INTERSECT

## What is INTERSECT?

Returns only common rows from both queries.

---

## Syntax

```sql
SELECT column_name
FROM table1

INTERSECT

SELECT column_name
FROM table2;
```

---

## Example

### Current Employees

| employee_name |
| ------------- |
| Ram           |
| Amit          |
| Neha          |

### Former Employees

| employee_name |
| ------------- |
| Neha          |
| Priya         |
| Raj           |

---

## Query

```sql
SELECT employee_name
FROM current_employees

INTERSECT

SELECT employee_name
FROM former_employees;
```

---

## Output

| employee_name |
| ------------- |
| Neha          |

---

## Business Use Cases

### Common Customers

Present in two systems.

### Common Products

Sold in multiple regions.

### Common Users

Website and Mobile App users.

---

## Visualization

```text
Table A ∩ Table B
```

Only common values returned.

---

# EXCEPT

## What is EXCEPT?

Returns records from first query that do not exist in second query.

---

## Syntax

```sql
SELECT column_name
FROM table1

EXCEPT

SELECT column_name
FROM table2;
```

---

## Example

```sql
SELECT employee_name
FROM current_employees

EXCEPT

SELECT employee_name
FROM former_employees;
```

---

## Output

| employee_name |
| ------------- |
| Ram           |
| Amit          |

---

Meaning:

Employees present in current table but not former table.

---

## Business Use Cases

### Active Customers

Customers not churned.

### Unsold Products

Products without sales.

### Employees Not Resigned

Current employees only.

---

## Visualization

```text
Table A - Table B
```

---

# Oracle Equivalent

Oracle uses:

```sql
MINUS
```

instead of:

```sql
EXCEPT
```

Example:

```sql
SELECT employee_name
FROM current_employees

MINUS

SELECT employee_name
FROM former_employees;
```

---

# Order of Execution

```text
SELECT

UNION /
UNION ALL /
INTERSECT /
EXCEPT

ORDER BY
```

---

# ORDER BY with Set Operators

ORDER BY can be applied only once at the end.

✅ Correct

```sql
SELECT employee_name
FROM current_employees

UNION

SELECT employee_name
FROM former_employees

ORDER BY employee_name;
```

---

❌ Wrong

```sql
SELECT employee_name
FROM current_employees
ORDER BY employee_name

UNION

SELECT employee_name
FROM former_employees;
```

---

# Real-World Data Science Use Cases

## Customer Analytics

Combine customer records from:

* Website
* Mobile App
* CRM

---

## Fraud Detection

Find common transactions across systems.

Using:

```sql
INTERSECT
```

---

## Marketing Analytics

Find users who:

* Registered
* Never Purchased

Using:

```sql
EXCEPT
```

---

## Data Warehousing

Merge datasets using:

```sql
UNION ALL
```

---

# Common Interview Questions

## Q1. Difference Between UNION and UNION ALL?

UNION removes duplicates.

UNION ALL keeps duplicates.

---

## Q2. Which is Faster?

UNION ALL.

---

## Q3. Difference Between JOIN and UNION?

JOIN combines columns.

UNION combines rows.

---

## Q4. What Does INTERSECT Do?

Returns common rows.

---

## Q5. What Does EXCEPT Do?

Returns rows in first query but not second query.

---

## Q6. What is Oracle's Equivalent of EXCEPT?

MINUS.

---

## Q7. Can ORDER BY Be Used Multiple Times?

No.

Only once at the end.

---

# Practice Questions

1. Combine current and former employees.
2. Find duplicate employees across tables.
3. Find customers present in both systems.
4. Find customers not present in CRM.
5. Compare sales regions using INTERSECT.
6. Merge transaction data using UNION ALL.
7. Find products available in one warehouse but not another.
8. Compare customer lists from different years.

---

# Common Mistakes

## Different Number of Columns

❌

```sql
SELECT employee_id
UNION
SELECT employee_id,
       employee_name;
```

---

## Different Data Types

❌

```sql
INT
UNION
VARCHAR
```

---

## Using UNION Instead of UNION ALL

Can reduce performance unnecessarily.

---

# Key Takeaways

✔ Set Operators combine rows from multiple queries.

✔ UNION removes duplicates.

✔ UNION ALL keeps duplicates.

✔ INTERSECT returns common records.

✔ EXCEPT returns records from first query only.

✔ UNION ALL is faster than UNION.

✔ Frequently asked in SQL interviews.

✔ Widely used in Data Warehousing, Analytics, and ETL pipelines.
