# SQLBolt Lesson 4 — Filtering and Sorting Query Results

## Dataset

### movies

| id | title | director | year | length_minutes |
| -- | ------------------- | -------------- | ---- | -------------- |
| 1 | Monsters University | Dan Scanlon | 2013 | 110 |
| 2 | Finding Nemo | Andrew Stanton | 2003 | 107 |
| 3 | Cars | John Lasseter | 2006 | 117 |
| 4 | Ratatouille | Brad Bird | 2007 | 115 |
| 5 | A Bug's Life | John Lasseter | 1998 | 95 |
| 6 | Toy Story 2 | John Lasseter | 1999 | 93 |
| 7 | The Incredibles | Brad Bird | 2004 | 116 |
| 8 | Monsters, Inc. | Pete Docter | 2001 | 92 |
| 9 | WALL-E | Andrew Stanton | 2008 | 104 |
| 10 | Cars 2 | John Lasseter | 2011 | 120 |
| 11 | Brave | Brenda Chapman | 2012 | 102 |
| 12 | Toy Story | John Lasseter | 1995 | 81 |
| 13 | Toy Story 3 | Lee Unkrich | 2010 | 103 |
| 14 | Up | Pete Docter | 2009 | 101 |

---

# Task 1

## Question

List all directors of Pixar movies (alphabetically), without duplicates.

### SQL Query

```sql
SELECT DISTINCT director
FROM movies
ORDER BY director ASC;
```

### Output

| director |
|----------|
| Andrew Stanton |
| Brad Bird |
| Brenda Chapman |
| Dan Scanlon |
| John Lasseter |
| Lee Unkrich |
| Pete Docter |

### Explanation

- `DISTINCT` removes duplicate values.
- `ORDER BY director ASC` sorts the results alphabetically in ascending order.

---

# Task 2

## Question

List the last four Pixar movies released (ordered from most recent to least).

### SQL Query

```sql
SELECT
    title,
    year
FROM movies
ORDER BY year DESC
LIMIT 4;
```

### Output

| title | year |
|---------|------|
| Monsters University | 2013 |
| Brave | 2012 |
| Cars 2 | 2011 |
| Toy Story 3 | 2010 |

### Explanation

- `ORDER BY year DESC` sorts movies from newest to oldest.
- `LIMIT 4` returns only the first four rows after sorting.

---

# Task 3

## Question

List the first five Pixar movies sorted alphabetically.

### SQL Query

```sql
SELECT
    title
FROM movies
ORDER BY title ASC
LIMIT 5;
```

### Output

| title |
|---------|
| A Bug's Life |
| Brave |
| Cars |
| Cars 2 |
| Finding Nemo |

### Explanation

- `ORDER BY title ASC` sorts movie titles alphabetically.
- `LIMIT 5` returns the first five rows from the sorted result.

---

# Task 4

## Question

List the next five Pixar movies sorted alphabetically.

### SQL Query

```sql
SELECT
    title
FROM movies
ORDER BY title ASC
LIMIT 5 OFFSET 5;
```

### Output

| title |
|---------|
| Monsters University |
| Monsters, Inc. |
| Ratatouille |
| The Incredibles |
| Toy Story |

### Explanation

- `ORDER BY title ASC` sorts movie titles alphabetically.
- `LIMIT 5` returns five rows.
- `OFFSET 5` skips the first five rows and starts returning records from the sixth row.

---

```sql
LIMIT 5 OFFSET 5
```

Meaning:

- Skip the first 5 rows.
- Return the next 5 rows.

---
