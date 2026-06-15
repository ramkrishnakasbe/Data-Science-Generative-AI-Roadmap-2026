# SQLBolt Lesson 11 — Queries with Aggregates (Pt. 2)

## Dataset

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

---

# Task 1

## Question

Find the number of Artists in the studio (without a HAVING clause).

### SQL Query

```sql
SELECT COUNT(*) AS artist_count
FROM employees
WHERE role = 'Artist';
```

### Output

| artist_count |
|-------------|
| 5 |

### Explanation

- `COUNT(*)` counts the number of rows.
- `WHERE role = 'Artist'` filters only Artist records.
- SQL then counts the remaining rows.

### Calculation

```text
Tylar S.
Sherman D.
Jakob J.
Lillia A.
Brandon J.

Total = 5
```

---

# Task 2

## Question

Find the number of Employees of each role in the studio.

### SQL Query

```sql
SELECT
    role,
    COUNT(*) AS employee_count
FROM employees
GROUP BY role;
```

### Output

| role | employee_count |
|----------|---------------|
| Artist | 5 |
| Engineer | 5 |
| Manager | 3 |

### Explanation

- `GROUP BY role` creates separate groups.
- `COUNT(*)` counts employees within each group.
- One row is returned for each role.

### Grouping Visualization

```text
Engineer
---------
Becky A.
Dan B.
Sharon F.
Dan M.
Malcom S.

Count = 5


Artist
---------
Tylar S.
Sherman D.
Jakob J.
Lillia A.
Brandon J.

Count = 5


Manager
---------
Scott K.
Shirlee M.
Daria O.

Count = 3
```

---

# Task 3

## Question

Find the total number of years employed by all Engineers.

### SQL Query

```sql
SELECT
    SUM(years_employed) AS total_engineer_years
FROM employees
WHERE role = 'Engineer';
```

### Output

| total_engineer_years |
|---------------------|
| 17 |

### Explanation

- `SUM()` adds all values together.
- `WHERE role = 'Engineer'` filters only Engineers.
- SQL then calculates the total years employed.

### Calculation

```text
4 + 2 + 6 + 4 + 1

= 17
```

---

## Concepts Covered

- COUNT()
- SUM()
- WHERE
- GROUP BY
- Aggregation
- Filtering Before Aggregation
- Aggregate Aliases

---

## Aggregate Function Summary

| Function | Purpose | Example |
|-----------|----------|----------|
| COUNT() | Count rows | COUNT(*) |
| SUM() | Add values | SUM(salary) |
| AVG() | Average values | AVG(age) |
| MIN() | Smallest value | MIN(price) |
| MAX() | Largest value | MAX(score) |

---

## Aggregate Query Flow

```text
Step 1
Filter Rows
↓
WHERE role = 'Engineer'

Step 2
Aggregate Data
↓
SUM(years_employed)

Step 3
Return Result
↓
17
```

---

## Common Interview Questions

### Count employees by department

```sql
SELECT
    department,
    COUNT(*)
FROM employees
GROUP BY department;
```

### Total salary by department

```sql
SELECT
    department,
    SUM(salary)
FROM employees
GROUP BY department;
```

### Average experience by role

```sql
SELECT
    role,
    AVG(years_employed)
FROM employees
GROUP BY role;
```

---
