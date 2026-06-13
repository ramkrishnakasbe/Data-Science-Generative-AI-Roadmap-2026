# SQLBolt Lesson 1 — SELECT Queries

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

Find the title of each film.

### SQL Query

```sql
SELECT title
FROM movies;
```

### Output

| title               |
| ------------------- |
| Toy Story           |
| A Bug's Life        |
| Toy Story 2         |
| Monsters, Inc.      |
| Finding Nemo        |
| The Incredibles     |
| Cars                |
| Ratatouille         |
| WALL-E              |
| Up                  |
| Toy Story 3         |
| Cars 2              |
| Brave               |
| Monsters University |

### Explanation

* `SELECT` is used to retrieve data from a table.
* `title` specifies the column to return.
* `FROM movies` tells SQL where to fetch data from.

---

# Task 2

## Question

Find the director of each film.

### SQL Query

```sql
SELECT director
FROM movies;
```

### Output

| director       |
| -------------- |
| John Lasseter  |
| John Lasseter  |
| John Lasseter  |
| Pete Docter    |
| Andrew Stanton |
| Brad Bird      |
| John Lasseter  |
| Brad Bird      |
| Andrew Stanton |
| Pete Docter    |
| Lee Unkrich    |
| John Lasseter  |
| Brenda Chapman |
| Dan Scanlon    |

### Explanation

* Returns all values from the `director` column.
* Duplicate values are included because `DISTINCT` is not used.

---

# Task 3

## Question

Find the title and director of each film.

### SQL Query

```sql
SELECT
    title,
    director
FROM movies;
```

### Output

| title               | director       |
| ------------------- | -------------- |
| Toy Story           | John Lasseter  |
| A Bug's Life        | John Lasseter  |
| Toy Story 2         | John Lasseter  |
| Monsters, Inc.      | Pete Docter    |
| Finding Nemo        | Andrew Stanton |
| The Incredibles     | Brad Bird      |
| Cars                | John Lasseter  |
| Ratatouille         | Brad Bird      |
| WALL-E              | Andrew Stanton |
| Up                  | Pete Docter    |
| Toy Story 3         | Lee Unkrich    |
| Cars 2              | John Lasseter  |
| Brave               | Brenda Chapman |
| Monsters University | Dan Scanlon    |

### Explanation

* Multiple columns can be selected by separating them with commas.
* SQL returns both columns side by side.

---

# Task 4

## Question

Find the title and year of each film.

### SQL Query

```sql
SELECT
    title,
    year
FROM movies;
```

### Output

| title               | year |
| ------------------- | ---- |
| Toy Story           | 1995 |
| A Bug's Life        | 1998 |
| Toy Story 2         | 1999 |
| Monsters, Inc.      | 2001 |
| Finding Nemo        | 2003 |
| The Incredibles     | 2004 |
| Cars                | 2006 |
| Ratatouille         | 2007 |
| WALL-E              | 2008 |
| Up                  | 2009 |
| Toy Story 3         | 2010 |
| Cars 2              | 2011 |
| Brave               | 2012 |
| Monsters University | 2013 |

### Explanation

* SQL can retrieve any combination of columns.
* Useful when analyzing movie release timelines.

---

# Task 5

## Question

Find all information about each film.

### SQL Query

```sql
SELECT *
FROM movies;
```

### Output

Returns all columns:

* id
* title
* director
* year
* length_minutes

### Explanation

* `*` means all columns.
* Convenient for exploration.
* Avoid using `SELECT *` in production systems because it may return unnecessary data.

---
