# SQLBolt Lesson 9 — Queries with Expressions

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

List all movies and their combined sales in millions of dollars.

### SQL Query

```sql
SELECT
    m.title,
    (b.domestic_sales + b.international_sales) / 1000000 AS sales_millions
FROM movies m
JOIN boxoffice b
ON m.id = b.movie_id;
```

### Output

| title | sales_millions |
|---------|---------------|
| Toy Story | 361.96 |
| A Bug's Life | 363.40 |
| Toy Story 2 | 485.02 |
| Monsters, Inc. | 562.82 |
| Finding Nemo | 936.74 |
| The Incredibles | 631.44 |
| Cars | 461.98 |
| Ratatouille | 623.72 |
| WALL-E | 521.31 |
| Up | 731.34 |
| Toy Story 3 | 1063.17 |
| Cars 2 | 559.85 |
| Brave | 538.98 |
| Monsters University | 743.56 |

### Explanation

- Sales are stored in dollars.
- Combined sales are calculated using:

```sql
domestic_sales + international_sales
```

- Dividing by `1,000,000` converts dollars into millions.

---

# Task 2

## Question

List all movies and their ratings in percent.

### SQL Query

```sql
SELECT
    m.title,
    b.rating * 10 AS rating_percent
FROM movies m
JOIN boxoffice b
ON m.id = b.movie_id;
```

### Output

| title | rating_percent |
|---------|---------------|
| Toy Story | 83 |
| A Bug's Life | 72 |
| Toy Story 2 | 79 |
| Monsters, Inc. | 81 |
| Finding Nemo | 82 |
| The Incredibles | 80 |
| Cars | 72 |
| Ratatouille | 80 |
| WALL-E | 85 |
| Up | 83 |
| Toy Story 3 | 84 |
| Cars 2 | 64 |
| Brave | 72 |
| Monsters University | 74 |

### Explanation

- Ratings are stored on a scale of 0–10.
- Multiplying by 10 converts ratings into percentages.

Example:

```text
8.5 × 10 = 85%
```

---

# Task 3

## Question

List all movies that were released on even number years.

### SQL Query

```sql
SELECT *
FROM movies
WHERE year % 2 = 0;
```

### Output

| id | title | director | year | length_minutes |
|----|-----------------|----------------|------|---------------|
| 2 | A Bug's Life | John Lasseter | 1998 | 95 |
| 6 | The Incredibles | Brad Bird | 2004 | 116 |
| 7 | Cars | John Lasseter | 2006 | 117 |
| 9 | WALL-E | Andrew Stanton | 2008 | 104 |
| 11 | Toy Story 3 | Lee Unkrich | 2010 | 103 |
| 13 | Brave | Brenda Chapman | 2012 | 102 |

### Explanation

The modulus operator `%` returns the remainder after division.

```sql
year % 2
```

If the remainder is:

```text
0 → Even Number
1 → Odd Number
```

Therefore:

```sql
WHERE year % 2 = 0
```

returns all movies released in even-numbered years.

---

## Concepts Covered

- Arithmetic Expressions
- Mathematical Operators
- Column Calculations
- Aliases (`AS`)
- Percentage Calculations
- Modulus Operator (`%`)
- JOIN + Expressions

---

## Common SQL Operators

| Operator | Meaning |
|-----------|---------|
| + | Addition |
| - | Subtraction |
| * | Multiplication |
| / | Division |
| % | Modulus (Remainder) |

### Examples

```sql
salary + bonus
```

```sql
price * quantity
```

```sql
marks * 100
```

```sql
year % 2
```

---
