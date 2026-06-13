# String Functions in SQL

## What are String Functions?

String Functions are built-in SQL functions used to manipulate, format, clean, and analyze text data.

They are commonly used in:

* Data Cleaning
* Data Transformation
* Reporting
* Customer Analytics
* ETL Pipelines
* Data Warehousing

---

## Why Do We Need String Functions?

Real-world data often contains:

* Extra spaces
* Inconsistent capitalization
* Missing formats
* Long text values
* Combined text fields

String functions help standardize and prepare data for analysis.

---

# Example Dataset

## Customers

| customer_id | first_name | last_name | city      | email                                     |
| ----------- | ---------- | --------- | --------- | ----------------------------------------- |
| 101         | Ram        | Kasbe     | pune      | [ram@gmail.com](mailto:ram@gmail.com)     |
| 102         | Amit       | Sharma    | MUMBAI    | [amit@gmail.com](mailto:amit@gmail.com)   |
| 103         | Neha       | Patil     | Delhi     | [neha@gmail.com](mailto:neha@gmail.com)   |
| 104         | Priya      | Singh     | Bangalore | [priya@gmail.com](mailto:priya@gmail.com) |

---

# CONCAT()

## What is CONCAT()?

CONCAT combines two or more strings into a single string.

---

## Syntax

```sql
CONCAT(string1, string2, ...)
```

---

## Example

```sql
SELECT
    CONCAT(first_name, ' ', last_name) AS full_name
FROM customers;
```

---

## Output

| full_name   |
| ----------- |
| Ram Kasbe   |
| Amit Sharma |
| Neha Patil  |
| Priya Singh |

---

## Business Use Cases

### Create Full Name

```sql
SELECT CONCAT(first_name,' ',last_name)
FROM customers;
```

### Create Address

```sql
SELECT CONCAT(city, ', India')
FROM customers;
```

---

## Common Mistakes

### NULL Handling

```sql
CONCAT('Ram', NULL)
```

Behavior depends on database.

Use:

```sql
CONCAT(first_name, COALESCE(last_name,''))
```

---

# UPPER()

## What is UPPER()?

Converts all characters to uppercase.

---

## Syntax

```sql
UPPER(column_name)
```

---

## Example

```sql
SELECT
    UPPER(city)
FROM customers;
```

---

## Output

| city      |
| --------- |
| PUNE      |
| MUMBAI    |
| DELHI     |
| BANGALORE |

---

## Business Use Cases

### Standardize Text

```sql
SELECT UPPER(customer_name)
FROM customers;
```

### Case-Insensitive Comparisons

```sql
WHERE UPPER(city)='PUNE'
```

---

# LOWER()

## What is LOWER()?

Converts text into lowercase.

---

## Syntax

```sql
LOWER(column_name)
```

---

## Example

```sql
SELECT LOWER(city)
FROM customers;
```

---

## Output

| city      |
| --------- |
| pune      |
| mumbai    |
| delhi     |
| bangalore |

---

## Business Use Cases

### Email Standardization

```sql
SELECT LOWER(email)
FROM customers;
```

### Data Cleaning

Normalize customer information.

---

# LENGTH()

## What is LENGTH()?

Returns the number of characters in a string.

---

## Syntax

```sql
LENGTH(column_name)
```

---

## Example

```sql
SELECT
    first_name,
    LENGTH(first_name)
FROM customers;
```

---

## Output

| first_name | length |
| ---------- | ------ |
| Ram        | 3      |
| Amit       | 4      |
| Neha       | 4      |
| Priya      | 5      |

---

## Business Use Cases

### Password Validation

Check minimum length.

### Data Quality

Identify unusually short names.

### Product Code Validation

Check code length.

---

# TRIM()

## What is TRIM()?

Removes leading and trailing spaces.

---

## Syntax

```sql
TRIM(column_name)
```

---

## Example

Original Data

| name     |
| -------- |
| " Ram "  |
| " Amit " |

```sql
SELECT TRIM(name)
FROM customers;
```

---

## Output

| name |
| ---- |
| Ram  |
| Amit |

---

## Business Use Cases

### Data Cleaning

Remove unwanted spaces.

### ETL Pipelines

Prepare data before loading.

### Customer Data Standardization

Improve matching accuracy.

---

# REPLACE()

## What is REPLACE()?

Replaces one substring with another.

---

## Syntax

```sql
REPLACE(column_name, old_value, new_value)
```

---

## Example

```sql
SELECT
    REPLACE(email,'gmail.com','company.com')
FROM customers;
```

---

## Output

| email                                       |
| ------------------------------------------- |
| [ram@company.com](mailto:ram@company.com)   |
| [amit@company.com](mailto:amit@company.com) |

---

## Business Use Cases

### Domain Migration

Replace old email domains.

### Text Cleaning

Correct spelling mistakes.

### Product Renaming

Update product descriptions.

---

# SUBSTRING()

## What is SUBSTRING()?

Extracts part of a string.

---

## Syntax

```sql
SUBSTRING(string, start_position, length)
```

---

## Example

```sql
SELECT
    SUBSTRING(first_name,1,3)
FROM customers;
```

---

## Output

| substring |
| --------- |
| Ram       |
| Ami       |
| Neh       |
| Pri       |

---

## Extract Email Username

```sql
SELECT
    SUBSTRING(email,1,3)
FROM customers;
```

---

## Business Use Cases

### Customer Initials

### Product Code Extraction

### Email Analysis

### Phone Number Parsing

---

# POSITION()

## What is POSITION()?

Returns the location of a character or substring.

---

## Syntax

```sql
POSITION(substring IN string)
```

---

## Example

```sql
SELECT
    POSITION('@' IN email)
FROM customers;
```

---

## Output

| position |
| -------- |
| 4        |
| 5        |
| 5        |
| 6        |

---

## Business Use Cases

### Email Validation

Check if '@' exists.

### Product Code Analysis

Find separators.

### Data Quality Checks

Locate invalid characters.

---

# Combining Multiple String Functions

## Example

```sql
SELECT
    UPPER(
        CONCAT(
            TRIM(first_name),
            ' ',
            TRIM(last_name)
        )
    ) AS customer_name
FROM customers;
```

---

## Output

| customer_name |
| ------------- |
| RAM KASBE     |
| AMIT SHARMA   |
| NEHA PATIL    |
| PRIYA SINGH   |

---

# Common Interview Questions

### Q1. Difference between UPPER() and LOWER()?

UPPER converts text to uppercase.

LOWER converts text to lowercase.

---

### Q2. Difference between LENGTH() and COUNT()?

LENGTH counts characters.

COUNT counts rows.

---

### Q3. What does TRIM() do?

Removes leading and trailing spaces.

---

### Q4. Difference between REPLACE() and SUBSTRING()?

REPLACE modifies text.

SUBSTRING extracts text.

---

### Q5. How can you find '@' in an email?

```sql
SELECT POSITION('@' IN email);
```

---

# Practice Questions

1. Create full customer names using CONCAT.
2. Convert all city names to uppercase.
3. Convert emails to lowercase.
4. Find length of customer names.
5. Remove extra spaces from names.
6. Replace gmail.com with company.com.
7. Extract first three characters from names.
8. Find position of '@' in email addresses.
9. Create customer initials using SUBSTRING.
10. Build standardized customer names using multiple string functions.

---

# Real-World Data Science Use Cases

### Customer Data Cleaning

TRIM, UPPER, LOWER

### Feature Engineering

SUBSTRING, LENGTH

### ETL Pipelines

REPLACE, TRIM

### Customer Analytics

CONCAT, POSITION

### Data Quality Validation

LENGTH, POSITION

---

# Performance Considerations

✔ String functions can slow queries on large datasets.

✔ Avoid using functions in WHERE clauses on indexed columns.

❌

```sql
SELECT *
FROM customers
WHERE UPPER(city)='PUNE';
```

May bypass indexes.

---

# Key Takeaways

✔ CONCAT combines strings.

✔ UPPER converts text to uppercase.

✔ LOWER converts text to lowercase.

✔ LENGTH returns character count.

✔ TRIM removes unwanted spaces.

✔ REPLACE substitutes text.

✔ SUBSTRING extracts text.

✔ POSITION finds character locations.

✔ String Functions are heavily used in ETL, Data Cleaning, Analytics, and Data Science projects.
