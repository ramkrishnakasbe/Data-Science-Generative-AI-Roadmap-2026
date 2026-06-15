# SQLBolt Lesson 6 — Multi-table Queries with JOINs

## Dataset

### movies

| id | title | director | year | length_minutes |
|----|---------------------|----------------|------|---------------|
| 1 | Toy Story | John Lasseter | 1995 | 81 |
| 2 | A Bug's Life | John Lasseter | 1998 | 95 |
| 3 | Toy Story 2 | John Lasseter | 1999 | 93 |
| 4 | Monsters, Inc. | Pete Docter | 2001 | 92 |
| 5 | Finding Nemo | Andrew Stanton | 2003 | 107 |
| 6 | The Incredibles | Brad Bird | 2004 | 116 |
| 7 | Cars | John Lasseter | 2006 | 117 |
| 8 | Ratatouille | Brad Bird | 2007 | 115 |
| 9 | WALL-E | Andrew Stanton | 2008 | 104 |
| 10 | Up | Pete Docter | 2009 | 101 |
| 11 | Toy Story 3 | Lee Unkrich | 2010 | 103 |
| 12 | Cars 2 | John Lasseter | 2011 | 120 |
| 13 | Brave | Brenda Chapman | 2012 | 102 |
| 14 | Monsters University | Dan Scanlon | 2013 | 110 |

---

### boxoffice

| movie_id | rating | domestic_sales | international_sales |
|-----------|--------|----------------|---------------------|
| 5 | 8.2 | 380843261 | 555900000 |
| 14 | 7.4 | 268492764 | 475066843 |
| 8 | 8.0 | 206445654 | 417277164 |
| 12 | 6.4 | 191452396 | 368400000 |
| 3 | 7.9 | 245852179 | 239163000 |
| 6 | 8.0 | 261441092 | 370001000 |
| 9 | 8.5 | 223808164 | 297503696 |
| 11 | 8.4 | 415004880 | 648167031 |
| 1 | 8.3 | 191796233 | 170162503 |
| 7 | 7.2 | 244082982 | 217900167 |
| 10 | 8.3 | 293004164 | 438338580 |
| 4 | 8.1 | 289916256 | 272900000 |
| 2 | 7.2 | 162798565 | 200600000 |
| 13 | 7.2 | 237283207 | 301700000 |

---

# Task 1

## Question

Find the domestic and international sales for each movie.

### SQL Query

```sql
SELECT
    m.title,
    b.domestic_sales,
    b.international_sales
FROM movies m
JOIN boxoffice b
ON m.id = b.movie_id;
```

### Output

| title | domestic_sales | international_sales |
|---------|---------------|---------------------|
| Toy Story | 191796233 | 170162503 |
| A Bug's Life | 162798565 | 200600000 |
| Toy Story 2 | 245852179 | 239163000 |
| Monsters, Inc. | 289916256 | 272900000 |
| Finding Nemo | 380843261 | 555900000 |
| The Incredibles | 261441092 | 370001000 |
| Cars | 244082982 | 217900167 |
| Ratatouille | 206445654 | 417277164 |
| WALL-E | 223808164 | 297503696 |
| Up | 293004164 | 438338580 |
| Toy Story 3 | 415004880 | 648167031 |
| Cars 2 | 191452396 | 368400000 |
| Brave | 237283207 | 301700000 |
| Monsters University | 268492764 | 475066843 |

### Explanation

- `JOIN` combines data from multiple tables.
- `m.id = b.movie_id` links each movie with its box office record.
- The query returns movie titles along with domestic and international sales.

---

# Task 2

## Question

Show the sales numbers for each movie that did better internationally rather than domestically.

### SQL Query

```sql
SELECT
    m.title,
    b.domestic_sales,
    b.international_sales
FROM movies m
JOIN boxoffice b
ON m.id = b.movie_id
WHERE b.international_sales > b.domestic_sales;
```

### Output

| title | domestic_sales | international_sales |
|---------|---------------|---------------------|
| A Bug's Life | 162798565 | 200600000 |
| Finding Nemo | 380843261 | 555900000 |
| The Incredibles | 261441092 | 370001000 |
| Ratatouille | 206445654 | 417277164 |
| WALL-E | 223808164 | 297503696 |
| Up | 293004164 | 438338580 |
| Toy Story 3 | 415004880 | 648167031 |
| Cars 2 | 191452396 | 368400000 |
| Brave | 237283207 | 301700000 |
| Monsters University | 268492764 | 475066843 |

### Explanation

- The `WHERE` clause filters rows after the join.
- Only movies where `international_sales` is greater than `domestic_sales` are returned.

---

# Task 3

## Question

List all the movies by their ratings in descending order.

### SQL Query

```sql
SELECT
    m.title,
    b.rating
FROM movies m
JOIN boxoffice b
ON m.id = b.movie_id
ORDER BY b.rating DESC;
```

### Output

| title | rating |
|---------|--------|
| WALL-E | 8.5 |
| Toy Story 3 | 8.4 |
| Toy Story | 8.3 |
| Up | 8.3 |
| Finding Nemo | 8.2 |
| Monsters, Inc. | 8.1 |
| Ratatouille | 8.0 |
| The Incredibles | 8.0 |
| Toy Story 2 | 7.9 |
| Monsters University | 7.4 |
| Cars | 7.2 |
| A Bug's Life | 7.2 |
| Brave | 7.2 |
| Cars 2 | 6.4 |

### Explanation

- `ORDER BY b.rating DESC` sorts ratings from highest to lowest.
- `DESC` stands for descending order.
- Movies with the highest ratings appear first.

---
