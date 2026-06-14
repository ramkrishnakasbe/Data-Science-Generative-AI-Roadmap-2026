# SQLBolt Review 1

## Dataset

### north_american_cities

| city | country | population | latitude | longitude |
|------|---------|------------|----------|-----------|
| Guadalajara | Mexico | 1500800 | 20.659699 | -103.349609 |
| Toronto | Canada | 2795060 | 43.653226 | -79.383184 |
| Houston | United States | 2195914 | 29.760427 | -95.369803 |
| New York | United States | 8405837 | 40.712784 | -74.005941 |
| Philadelphia | United States | 1553165 | 39.952584 | -75.165222 |
| Havana | Cuba | 2106146 | 23.054070 | -82.345189 |
| Mexico City | Mexico | 8555500 | 19.432608 | -99.133208 |
| Phoenix | United States | 1513367 | 33.448377 | -112.074037 |
| Los Angeles | United States | 3884307 | 34.052234 | -118.243685 |
| Ecatepec de Morelos | Mexico | 1742000 | 19.601841 | -99.050674 |
| Montreal | Canada | 1717767 | 45.501689 | -73.567256 |
| Chicago | United States | 2718782 | 41.878114 | -87.629798 |

---

# Task 1

## Question

List all the Canadian cities and their populations.

### SQL Query

```sql
SELECT
    city,
    population
FROM north_american_cities
WHERE country = 'Canada';
```

### Output

| city | population |
|---------|------------|
| Toronto | 2795060 |
| Montreal | 1717767 |

### Explanation

- `WHERE country = 'Canada'` filters cities located in Canada.
- Only the `city` and `population` columns are returned.

---

# Task 2

## Question

Order all the cities in the United States by their latitude from north to south.

### SQL Query

```sql
SELECT
    city,
    latitude
FROM north_american_cities
WHERE country = 'United States'
ORDER BY latitude DESC;
```

### Output

| city | latitude |
|---------|----------|
| Chicago | 41.878114 |
| New York | 40.712784 |
| Philadelphia | 39.952584 |
| Los Angeles | 34.052234 |
| Phoenix | 33.448377 |
| Houston | 29.760427 |

### Explanation

- Higher latitude values indicate locations farther north.
- `ORDER BY latitude DESC` sorts cities from north to south.

---

# Task 3

## Question

List all the cities west of Chicago, ordered from west to east.

### SQL Query

```sql
SELECT
    city,
    longitude
FROM north_american_cities
WHERE longitude < -87.629798
ORDER BY longitude ASC;
```

### Output

| city | longitude |
|---------|------------|
| Los Angeles | -118.243685 |
| Phoenix | -112.074037 |
| Guadalajara | -103.349609 |
| Mexico City | -99.133208 |
| Ecatepec de Morelos | -99.050674 |
| Houston | -95.369803 |

### Explanation

- Chicago's longitude is `-87.629798`.
- Cities with smaller longitude values are farther west.
- `ORDER BY longitude ASC` sorts cities from west to east.

---

# Task 4

## Question

List the two largest cities in Mexico (by population).

### SQL Query

```sql
SELECT
    city,
    population
FROM north_american_cities
WHERE country = 'Mexico'
ORDER BY population DESC
LIMIT 2;
```

### Output

| city | population |
|---------|------------|
| Mexico City | 8555500 |
| Ecatepec de Morelos | 1742000 |

### Explanation

- `ORDER BY population DESC` sorts cities from largest to smallest population.
- `LIMIT 2` returns only the top two cities.

---

# Task 5

## Question

List the third and fourth largest cities (by population) in the United States and their population.

### SQL Query

```sql
SELECT
    city,
    population
FROM north_american_cities
WHERE country = 'United States'
ORDER BY population DESC
LIMIT 2 OFFSET 2;
```

### Output

| city | population |
|---------|------------|
| Chicago | 2718782 |
| Houston | 2195914 |

### Explanation

- `ORDER BY population DESC` ranks cities by population.
- `OFFSET 2` skips the first two largest cities:
  - New York
  - Los Angeles
- `LIMIT 2` returns the next two cities:
  - Chicago
  - Houston

---
