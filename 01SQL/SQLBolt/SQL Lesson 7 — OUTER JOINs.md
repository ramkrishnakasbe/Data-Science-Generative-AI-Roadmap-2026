# SQLBolt Lesson 7 — OUTER JOINs

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
|--------|-----------|----------|---------------|
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

---

# Task 1

## Question

Find the list of all buildings that have employees.

### SQL Query

```sql
SELECT DISTINCT building
FROM employees;
```

### Output

| building |
|----------|
| 1e |
| 2w |

### Explanation

- `DISTINCT` removes duplicate values.
- Only buildings that appear in the `employees` table are returned.
- Buildings without employees are excluded.

---

# Task 2

## Question

Find the list of all buildings and their capacity.

### SQL Query

```sql
SELECT *
FROM buildings;
```

### Output

| building_name | capacity |
|--------------|----------|
| 1e | 24 |
| 1w | 32 |
| 2e | 16 |
| 2w | 20 |

### Explanation

- Returns all rows and columns from the `buildings` table.
- Shows every building and its maximum employee capacity.

---

# Task 3

## Question

List all buildings and the distinct employee roles in each building (including empty buildings).

### SQL Query

```sql
SELECT DISTINCT
    b.building_name,
    e.role
FROM buildings b
LEFT JOIN employees e
ON b.building_name = e.building;
```

### Output

| building_name | role |
|--------------|----------|
| 1e | Engineer |
| 1e | Manager |
| 1w | NULL |
| 2e | NULL |
| 2w | Artist |
| 2w | Manager |

### Explanation

- `LEFT JOIN` returns all records from the left table (`buildings`).
- Matching records are returned from the right table (`employees`).
- If no matching employee exists, SQL returns `NULL`.
- `DISTINCT` removes duplicate building-role combinations.

---

### JOIN Visualization

```text
buildings                employees

1e --------------------> Engineer
1e --------------------> Manager

1w --------------------> NULL

2e --------------------> NULL

2w --------------------> Artist
2w --------------------> Manager
```

### Why LEFT JOIN?

Using an `INNER JOIN` would exclude:

- 1w
- 2e

because these buildings have no employees.

`LEFT JOIN` ensures that all buildings are included in the result.

---
