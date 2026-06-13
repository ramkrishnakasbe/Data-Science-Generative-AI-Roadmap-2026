# SQLBolt Lesson 2 — Queries with Constraints (Part 1)

## Dataset

### movies

| id | title               | director       | year | length_minutes |
| -- | ------------------- | -------------- | ---- | -------------- |
| 1  | Toy Story           | John Lasseter  | 1995 | 81             |
| 2  | A Bug's Life        | John Lasseter  | 1998 | 95             |
| 3  | Toy Story 2         | John Lasseter  | 1999 | 93             |
| 4  | Monsters, Inc.      | Pete Docter    | 2001 | 92             |
| 5  | Finding Nemo        | Andrew Stanton | 2003 | 107            |
| 6  | The Incredibles     | Brad Bird      | 2004 | 116            |
| 7  | Cars                | John Lasseter  | 2006 | 117            |
| 8  | Ratatouille         | Brad Bird      | 2007 | 115            |
| 9  | WALL-E              | Andrew Stanton | 2008 | 104            |
| 10 | Up                  | Pete Docter    | 2009 | 101            |
| 11 | Toy Story 3         | Lee Unkrich    | 2010 | 103            |
| 12 | Cars 2              | John Lasseter  | 2011 | 120            |
| 13 | Brave               | Brenda Chapman | 2012 | 102            |
| 14 | Monsters University | Dan Scanlon    | 2013 | 110            |

---

# Task 1

## Question

Find the movie with a row id of 6.

### SQL Query

```sql
SELECT *
FROM movies
WHERE id = 6;
```

### Output

| id | title           | director  | year | length_minutes |
| -- | --------------- | --------- | ---- | -------------- |
| 6  | The Incredibles | Brad Bird | 2004 | 116            |

### Explanation

* `WHERE` is used to filter rows.
* Only the row where `id = 6` is returned.

---

# Task 2

## Question

Find the movies released in the years between 2000 and 2010.

### SQL Query

```sql
SELECT *
FROM movies
WHERE year BETWEEN 2000 AND 2010;
```

### Output

| id | title           | director       | year | length_minutes |
| -- | --------------- | -------------- | ---- | -------------- |
| 4  | Monsters, Inc.  | Pete Docter    | 2001 | 92             |
| 5  | Finding Nemo    | Andrew Stanton | 2003 | 107            |
| 6  | The Incredibles | Brad Bird      | 2004 | 116            |
| 7  | Cars            | John Lasseter  | 2006 | 117            |
| 8  | Ratatouille     | Brad Bird      | 2007 | 115            |
| 9  | WALL-E          | Andrew Stanton | 2008 | 104            |
| 10 | Up              | Pete Docter    | 2009 | 101            |
| 11 | Toy Story 3     | Lee Unkrich    | 2010 | 103            |

### Explanation

* `BETWEEN` filters values within a specified range.
* Both boundary values (`2000` and `2010`) are included.

Equivalent query:

```sql
SELECT *
FROM movies
WHERE year >= 2000
AND year <= 2010;
```

---

# Task 3

## Question

Find the movies not released in the years between 2000 and 2010.

### SQL Query

```sql
SELECT *
FROM movies
WHERE year NOT BETWEEN 2000 AND 2010;
```

### Output

| id | title               | director       | year | length_minutes |
| -- | ------------------- | -------------- | ---- | -------------- |
| 1  | Toy Story           | John Lasseter  | 1995 | 81             |
| 2  | A Bug's Life        | John Lasseter  | 1998 | 95             |
| 3  | Toy Story 2         | John Lasseter  | 1999 | 93             |
| 12 | Cars 2              | John Lasseter  | 2011 | 120            |
| 13 | Brave               | Brenda Chapman | 2012 | 102            |
| 14 | Monsters University | Dan Scanlon    | 2013 | 110            |

### Explanation

* `NOT BETWEEN` excludes values within a specified range.
* Returns movies released before 2000 and after 2010.

Equivalent query:

```sql
SELECT *
FROM movies
WHERE year < 2000
OR year > 2010;
```

---

# Task 4

## Question

Find the first 5 Pixar movies and their release year.

### SQL Query

```sql
SELECT
    title,
    year
FROM movies
ORDER BY year
LIMIT 5;
```

### Output

| title          | year |
| -------------- | ---- |
| Toy Story      | 1995 |
| A Bug's Life   | 1998 |
| Toy Story 2    | 1999 |
| Monsters, Inc. | 2001 |
| Finding Nemo   | 2003 |

### Explanation

* `ORDER BY year` sorts movies from oldest to newest.
* `LIMIT 5` returns only the first five rows after sorting.
* Useful when retrieving a subset of records from a large dataset.

---
