# SQLBolt Lesson 3 — Queries with Constraints (Part 2)

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

Find all the Toy Story movies.

### SQL Query

```sql
SELECT *
FROM movies
WHERE title LIKE 'Toy Story%';
```

### Output

| id | title       | director      | year | length_minutes |
| -- | ----------- | ------------- | ---- | -------------- |
| 1  | Toy Story   | John Lasseter | 1995 | 81             |
| 3  | Toy Story 2 | John Lasseter | 1999 | 93             |
| 11 | Toy Story 3 | Lee Unkrich   | 2010 | 103            |

### Explanation

* `LIKE` is used to search for a specific pattern.
* `%` is a wildcard that represents zero or more characters.
* `'Toy Story%'` matches:

  * Toy Story
  * Toy Story 2
  * Toy Story 3

---

# Task 2

## Question

Find all the movies directed by John Lasseter.

### SQL Query

```sql
SELECT *
FROM movies
WHERE director = 'John Lasseter';
```

### Output

| id | title        | director      | year | length_minutes |
| -- | ------------ | ------------- | ---- | -------------- |
| 1  | Toy Story    | John Lasseter | 1995 | 81             |
| 2  | A Bug's Life | John Lasseter | 1998 | 95             |
| 3  | Toy Story 2  | John Lasseter | 1999 | 93             |
| 7  | Cars         | John Lasseter | 2006 | 117            |
| 12 | Cars 2       | John Lasseter | 2011 | 120            |

### Explanation

* `=` is used for exact matching.
* Only rows where the director is exactly `'John Lasseter'` are returned.

---

# Task 3

## Question

Find all the movies (and director) not directed by John Lasseter.

### SQL Query

```sql
SELECT
    title,
    director
FROM movies
WHERE director != 'John Lasseter';
```

### Output

| title               | director       |
| ------------------- | -------------- |
| Monsters, Inc.      | Pete Docter    |
| Finding Nemo        | Andrew Stanton |
| The Incredibles     | Brad Bird      |
| Ratatouille         | Brad Bird      |
| WALL-E              | Andrew Stanton |
| Up                  | Pete Docter    |
| Toy Story 3         | Lee Unkrich    |
| Brave               | Brenda Chapman |
| Monsters University | Dan Scanlon    |

### Explanation

* `!=` means "not equal to".
* Returns all movies whose director is not John Lasseter.

Alternative syntax:

```sql
SELECT
    title,
    director
FROM movies
WHERE director <> 'John Lasseter';
```

---

# Task 4

## Question

Find all the WALL-* movies.

### SQL Query

```sql
SELECT *
FROM movies
WHERE title LIKE 'WALL-%';
```

### Output

| id | title  | director       | year | length_minutes |
| -- | ------ | -------------- | ---- | -------------- |
| 9  | WALL-E | Andrew Stanton | 2008 | 104            |

### Explanation

* `LIKE` searches for matching text patterns.
* `'WALL-%'` means:

  * Title starts with `WALL-`
  * Followed by any characters

The `%` wildcard matches zero or more characters after `WALL-`.

---
