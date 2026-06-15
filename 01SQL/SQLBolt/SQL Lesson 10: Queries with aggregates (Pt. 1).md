# SQLBolt Lesson 10 — Queries with Aggregates (Pt. 1)

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

Find the longest time that an employee has been at the studio.

### SQL Query

```sql
SELECT MAX(years_employed) AS longest_employment
FROM employees;
```

### Output

| longest_employment |
|-------------------|
| 9 |

### Explanation

- `MAX()` returns the highest value in a column.
- Here, it finds the maximum value from `years_employed`.
- The longest-serving employee has worked for **9 years**.

---

# Task 2

## Question

For each role, find the average number of years employed by employees in that role.

### SQL Query

```sql
SELECT
    role,
    AVG(years_employed) AS average_years
FROM employees
GROUP BY role;
```

### Output

| role | average_years |
|----------|--------------|
| Engineer | 3.4 |
| Artist | 6.0 |
| Manager | 6.0 |

### Explanation

- `AVG()` calculates the average value.
- `GROUP BY role` creates separate groups for each role.
- SQL calculates the average years employed within each role.

#### Calculation Example

##### Engineers

```text
(4 + 2 + 6 + 4 + 1) / 5
= 17 / 5
= 3.4
```

##### Artists

```text
(2 + 8 + 6 + 7 + 7) / 5
= 30 / 5
= 6.0
```

##### Managers

```text
(9 + 3 + 6) / 3
= 18 / 3
= 6.0
```

---

# Task 3

## Question

Find the total number of employee years worked in each building.

### SQL Query

```sql
SELECT
    building,
    SUM(years_employed) AS total_years_worked
FROM employees
GROUP BY building;
```

### Output

| building | total_years_worked |
|----------|-------------------|
| 1e | 29 |
| 2w | 30 |

### Explanation

- `SUM()` adds all values in a column.
- `GROUP BY building` creates a group for each building.
- SQL calculates the total years worked by employees in each building.

#### Calculation Example

##### Building 1e

```text
4 + 2 + 6 + 4 + 1 + 9 + 3
= 29
```

##### Building 2w

```text
2 + 8 + 6 + 7 + 7 + 6
= 36
```

---

## Concepts Covered

- MAX()
- AVG()
- SUM()
- Aggregate Functions
- GROUP BY
- Column Aliases (`AS`)
- Aggregation by Category

---

## Common Aggregate Functions

| Function | Description |
|-----------|------------|
| COUNT() | Counts rows |
| SUM() | Adds values |
| AVG() | Calculates average |
| MIN() | Finds smallest value |
| MAX() | Finds largest value |

### Examples

#### Count Employees

```sql
SELECT COUNT(*)
FROM employees;
```

#### Total Years Worked

```sql
SELECT SUM(years_employed)
FROM employees;
```

#### Average Years Worked

```sql
SELECT AVG(years_employed)
FROM employees;
```

#### Minimum Years Worked

```sql
SELECT MIN(years_employed)
FROM employees;
```

#### Maximum Years Worked

```sql
SELECT MAX(years_employed)
FROM employees;
```

---

## Aggregate Function Visualization

```text
Employees

4
2
6
4
1

MAX() = 6
MIN() = 1
SUM() = 17
AVG() = 3.4
COUNT() = 5
```

---
