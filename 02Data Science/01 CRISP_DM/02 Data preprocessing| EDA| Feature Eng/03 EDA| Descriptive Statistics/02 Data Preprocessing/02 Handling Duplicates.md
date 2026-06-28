# 02. Duplicate Handling

# Overview

Duplicate handling is the process of identifying and removing repeated records from a dataset. Duplicate records can lead to biased analysis, incorrect statistics, and poor machine learning model performance.

Removing duplicates is an essential step in data preprocessing to ensure data quality and integrity.

---

# Why Handle Duplicates?

Duplicate records can:

* Increase dataset size unnecessarily
* Bias statistical analysis
* Affect model accuracy
* Increase training time
* Produce incorrect reports and insights

---

# Types of Duplicates

## 1. Complete (Exact) Duplicates

All column values are identical.

### Example

| ID  | Name | Age |
| --- | ---- | --- |
| 101 | John | 25  |
| 101 | John | 25  |

---

## 2. Partial Duplicates

Only some columns have identical values.

### Example

| ID  | Name | City  |
| --- | ---- | ----- |
| 101 | John | Delhi |
| 102 | John | Delhi |

Depending on the business requirement, these may or may not be considered duplicates.

---

# Detecting Duplicates

## Using Pandas

### Check Duplicate Rows

```python
import pandas as pd

df.duplicated()
```

Returns a Boolean Series indicating duplicate rows.

---

### Count Duplicate Rows

```python
df.duplicated().sum()
```

---

### Display Duplicate Records

```python
df[df.duplicated()]
```

---

### Check Duplicates Based on Specific Columns

```python
df.duplicated(subset=["Name"])
```

```python
df.duplicated(subset=["Name", "City"])
```

---

# Removing Duplicates

## Remove Duplicate Rows

```python
df = df.drop_duplicates()
```

---

## Remove Duplicates Based on Specific Columns

```python
df = df.drop_duplicates(subset=["Name"])
```

---

## Keep the First Occurrence (Default)

```python
df.drop_duplicates(keep="first")
```

---

## Keep the Last Occurrence

```python
df.drop_duplicates(keep="last")
```

---

## Remove All Duplicate Records

```python
df.drop_duplicates(keep=False)
```

---

# Example

### Original Dataset

| ID | Name  | Salary |
| -- | ----- | ------ |
| 1  | Ram   | 50000  |
| 2  | Amit  | 60000  |
| 2  | Amit  | 60000  |
| 3  | Rahul | 55000  |

Duplicate count:

```python
df.duplicated().sum()
```

Output

```text
1
```

Remove duplicates:

```python
df = df.drop_duplicates()
```

### Result

| ID | Name  | Salary |
| -- | ----- | ------ |
| 1  | Ram   | 50000  |
| 2  | Amit  | 60000  |
| 3  | Rahul | 55000  |

---

# Advantages

* Improves data quality
* Reduces storage requirements
* Prevents biased analysis
* Improves machine learning performance
* Reduces computation time

---

# Disadvantages

* Incorrect removal may result in data loss
* Partial duplicates require domain knowledge
* Removing duplicates without validation may discard valuable information

---

# Real-World Example

An e-commerce company may receive duplicate customer records due to multiple registrations using the same email or phone number. Removing duplicates ensures accurate customer counts, reporting, and personalized recommendations.

---

# Summary

Duplicate handling is the process of identifying and removing repeated records from a dataset. It improves data quality, reduces redundancy, and ensures accurate analysis. In Python, duplicate detection and removal are commonly performed using Pandas functions such as `duplicated()` and `drop_duplicates()`.
