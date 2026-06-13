# Date and Time Functions in SQL

## What are Date and Time Functions?

Date and Time Functions are used to:

- Work with dates
- Work with timestamps
- Calculate differences between dates
- Add or subtract dates
- Extract date components
- Perform time-based analysis

These functions are extremely important in:

- Data Science
- Analytics
- Business Intelligence
- Reporting
- Data Engineering

---

# Why Are Date Functions Important?

Most business data contains dates.

Examples:

- Customer Signup Date
- Order Date
- Transaction Timestamp
- Employee Joining Date

Businesses ask questions like:

- How many orders were placed this month?
- How many days since signup?
- Monthly sales trend?
- Customer retention after 30 days?

Date Functions help answer these questions.

---

# Sample Dataset

## Orders

| order_id | customer_id | order_date |
|-----------|-------------|------------|
| 101 | 1 | 2025-01-10 |
| 102 | 2 | 2025-02-15 |
| 103 | 3 | 2025-03-20 |

---

# CURRENT_DATE

## What is CURRENT_DATE?

Returns today's date.

---

## Syntax

```sql
SELECT CURRENT_DATE;
```

---

## Output

```text
2026-06-13
```

(Current date when query runs)

---

## Use Cases

### Today's Orders

```sql
SELECT *
FROM orders
WHERE order_date = CURRENT_DATE;
```

---

# CURRENT_TIMESTAMP

## What is CURRENT_TIMESTAMP?

Returns current date and time.

---

## Syntax

```sql
SELECT CURRENT_TIMESTAMP;
```

---

## Output

```text
2026-06-13 10:45:30
```

---

# NOW()

## What is NOW()?

Returns current date and time.

Common in:

- PostgreSQL
- MySQL

---

## Syntax

```sql
SELECT NOW();
```

---

## Output

```text
2026-06-13 10:45:30
```

---

# EXTRACT()

## What is EXTRACT()?

Extracts parts from a date.

---

## Syntax

```sql
EXTRACT(part FROM date_column)
```

---

# Extract Year

```sql
SELECT
    EXTRACT(YEAR FROM order_date)
FROM orders;
```

---

## Output

| year |
|------|
| 2025 |
| 2025 |
| 2025 |

---

# Extract Month

```sql
SELECT
    EXTRACT(MONTH FROM order_date)
FROM orders;
```

---

## Output

| month |
|-------|
| 1 |
| 2 |
| 3 |

---

# Extract Day

```sql
SELECT
    EXTRACT(DAY FROM order_date)
FROM orders;
```

---

# Common Parts

```text
YEAR
MONTH
DAY
HOUR
MINUTE
SECOND
QUARTER
WEEK
DOW
```

---

# DATE_PART()

## What is DATE_PART()?

Alternative to EXTRACT.

Used mainly in PostgreSQL.

---

## Example

```sql
SELECT
DATE_PART('year', order_date)
FROM orders;
```

---

## Output

```text
2025
```

---

# DATE_TRUNC()

## What is DATE_TRUNC()?

Rounds a timestamp to a specific precision.

---

## Syntax

```sql
DATE_TRUNC('month', timestamp)
```

---

# Example

```sql
SELECT
DATE_TRUNC('month', CURRENT_TIMESTAMP);
```

---

## Output

```text
2026-06-01 00:00:00
```

---

# Monthly Sales Analysis

```sql
SELECT
    DATE_TRUNC('month', order_date) AS month,
    COUNT(*)
FROM orders
GROUP BY month;
```

---

# DATEDIFF()

## What is DATEDIFF()?

Returns difference between two dates.

---

## Syntax (SQL Server)

```sql
DATEDIFF(unit,start_date,end_date)
```

---

## Example

```sql
SELECT
DATEDIFF(day,
         '2025-01-01',
         '2025-01-10');
```

---

## Output

```text
9
```

---

# Common Units

```text
DAY
MONTH
YEAR
HOUR
MINUTE
SECOND
```

---

# Customer Retention Example

```sql
SELECT
DATEDIFF(day,
         signup_date,
         last_login_date)
FROM customers;
```

---

# DATEADD()

## What is DATEADD()?

Adds a date interval.

---

## Syntax

```sql
DATEADD(unit,
        value,
        date)
```

---

## Example

```sql
SELECT
DATEADD(day,
        30,
        '2025-01-01');
```

---

## Output

```text
2025-01-31
```

---

# Business Use Cases

### Next Billing Date

```sql
SELECT
DATEADD(month,1,billing_date)
```

---

### Trial Expiry Date

```sql
SELECT
DATEADD(day,30,signup_date)
```

---

# INTERVAL

## What is INTERVAL?

Used mainly in PostgreSQL.

Adds or subtracts time periods.

---

## Example

```sql
SELECT
CURRENT_DATE + INTERVAL '7 day';
```

---

## Output

```text
2026-06-20
```

---

# Subtract Days

```sql
SELECT
CURRENT_DATE - INTERVAL '30 day';
```

---

## Output

```text
2026-05-14
```

---

# AGE()

## What is AGE()?

Returns age between dates.

(PostgreSQL)

---

## Example

```sql
SELECT
AGE(
    CURRENT_DATE,
    '1995-05-20'
);
```

---

## Output

```text
31 years 24 days
```

---

# Time Zone Functions

## Current Time Zone

```sql
SHOW timezone;
```

---

## Convert Time Zone

```sql
SELECT
CURRENT_TIMESTAMP
AT TIME ZONE 'Asia/Tokyo';
```

---

# Date Formatting

## PostgreSQL

```sql
SELECT
TO_CHAR(
    CURRENT_DATE,
    'DD-MM-YYYY'
);
```

---

## Output

```text
13-06-2026
```

---

# Monthly Sales Example

## Orders

| order_id | order_date | amount |
|-----------|------------|---------|
| 101 | 2025-01-01 | 100 |
| 102 | 2025-01-15 | 200 |
| 103 | 2025-02-01 | 300 |

---

```sql
SELECT
    DATE_TRUNC('month', order_date) AS month,
    SUM(amount)
FROM orders
GROUP BY month;
```

---

## Output

| month | total_sales |
|--------|------------|
| Jan | 300 |
| Feb | 300 |

---

# Common Interview Questions

## Q1. Difference Between CURRENT_DATE and CURRENT_TIMESTAMP?

CURRENT_DATE

Returns date only.

CURRENT_TIMESTAMP

Returns date and time.

---

## Q2. Difference Between EXTRACT and DATE_PART?

Same purpose.

DATE_PART mostly PostgreSQL.

---

## Q3. Difference Between DATEADD and INTERVAL?

DATEADD

SQL Server.

INTERVAL

PostgreSQL.

---

## Q4. How to Find Difference Between Two Dates?

```sql
DATEDIFF()
```

---

## Q5. How to Get Current Date?

```sql
CURRENT_DATE
```

---

## Q6. How to Extract Month?

```sql
EXTRACT(MONTH FROM order_date)
```

---

# Real-World Data Science Use Cases

## Customer Retention

```sql
DATEDIFF()
```

---

## Monthly Revenue

```sql
DATE_TRUNC()
```

---

## Cohort Analysis

```sql
EXTRACT()
```

---

## Churn Prediction

```sql
DATEDIFF()
```

---

## Feature Engineering

```sql
signup_age_days
```

using

```sql
DATEDIFF()
```

---

# Practice Questions

1. Find today's date.
2. Find current timestamp.
3. Extract month from order date.
4. Extract year from order date.
5. Find customer age in days.
6. Add 30 days to signup date.
7. Find difference between two dates.
8. Calculate monthly sales.
9. Group orders by year.
10. Find users inactive for 90+ days.

---

# Common Mistakes

## Comparing String with Date

❌ Wrong

```sql
WHERE order_date='01-01-2025'
```

---

✅ Correct

```sql
WHERE order_date='2025-01-01'
```

---

## Ignoring Time Zones

Can lead to incorrect reporting.

---

# Key Takeaways

✔ CURRENT_DATE returns current date.

✔ CURRENT_TIMESTAMP returns date and time.

✔ EXTRACT gets date parts.

✔ DATE_PART is PostgreSQL alternative.

✔ DATE_TRUNC groups dates.

✔ DATEDIFF calculates date differences.

✔ DATEADD adds intervals.

✔ INTERVAL adds/subtracts time periods.

✔ AGE calculates age between dates.

✔ Date Functions are among the most important SQL topics for Data Scientists and Analysts.
