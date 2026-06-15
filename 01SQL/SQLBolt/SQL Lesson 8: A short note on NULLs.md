# SQLBolt Lesson 8 — A Short Note on NULLs

## Dataset

### buildings

| building_name | capacity |
|--------------|----------|
| 1e | 24 |
| 1w | 32 |
| 2e | 16 |
| 2w | 20 |

---

### employees

| role | name | building | years_employed |
|----------|-----------|----------|---------------|
| Engineer | Becky A. | 1e | 4 |
| Engineer | Dan B. | 1e | 2 |
| Engineer | Sharon F. | 1e | 6 |
| Engineer | Dan M. | 1e | 4 |
| Engineer | Malcom S. | 1e | 1 |
| Artist | Tylar S. | 2w | 2 |
| Artist | Sherman D. | 2w | 8 |
| Artist | Jakob J. | 2w | 6 |
| Artist | Lillia A. | 2w | 7 |
| Artist | Brandon J. | 2w | 7 |
| Manager | Scott K. | 1e | 9 |
| Manager | Shirlee M. | 1e | 3 |
| Manager | Daria O. | 2w | 6 |
| Engineer | Yancy I. | NULL | 0 |
| Artist | Oliver P. | NULL | 0 |

---

# Task 1

## Question

Find the name and role of all employees who have not been assigned to a building.

### SQL Query

```sql
SELECT
    name,
    role
FROM employees
WHERE building IS NULL;
```

### Output

| name | role |
|--------|----------|
| Yancy I. | Engineer |
| Oliver P. | Artist |

### Explanation

- `NULL` represents a missing or unknown value.
- To check for NULL values, use `IS NULL`.
- Using `= NULL` will not work.

Incorrect:

```sql
SELECT *
FROM employees
WHERE building = NULL;
```

Correct:

```sql
SELECT *
FROM employees
WHERE building IS NULL;
```

---

# Task 2

## Question

Find the names of the buildings that hold no employees.

### SQL Query

```sql
SELECT
    b.building_name
FROM buildings b
LEFT JOIN employees e
ON b.building_name = e.building
WHERE e.building IS NULL;
```

### Output

| building_name |
|---------------|
| 1w |
| 2e |

### Explanation

- `LEFT JOIN` returns all buildings.
- Matching employees are joined where available.
- Buildings without employees receive `NULL` values from the employee table.
- `WHERE e.building IS NULL` filters those unmatched buildings.

### JOIN Visualization

```text
Buildings          Employees

1e  -----------> Employees Found

1w  -----------> NULL

2e  -----------> NULL

2w  -----------> Employees Found
```

---

## Key Concept: NULL

NULL does NOT mean:

- 0
- Empty String ('')
- False

NULL means:

```text
Unknown
Missing
Not Assigned
Not Available
```

Examples:

| Value | Meaning |
|---------|----------|
| 0 | Actual numeric value |
| '' | Empty string |
| NULL | Unknown / Missing |

---

## Common NULL Operations

### Find NULL Values

```sql
SELECT *
FROM table_name
WHERE column_name IS NULL;
```

### Find Non-NULL Values

```sql
SELECT *
FROM table_name
WHERE column_name IS NOT NULL;
```

### Replace NULL Values

```sql
SELECT
    COALESCE(column_name, 'N/A')
FROM table_name;
```

---

## Concepts Covered

- NULL
- IS NULL
- IS NOT NULL
- LEFT JOIN
- Finding Missing Records
- Anti Join Pattern
