# First Moment Business

## What is First Moment?

The First Moment of a distribution measures the **Central Tendency** of data.

It helps answer:

```text
Where is the center of the data?
```

The First Moment tells us what value best represents the dataset.

---

# Why is it Called First Moment?

In statistics, moments describe the characteristics of a distribution.

```text
1st Moment → Center
2nd Moment → Spread
3rd Moment → Skewness
4th Moment → Kurtosis
```

The First Moment focuses on the average location of observations.

---

# First Moment Business Roadmap

```text
First Moment Business
│
├── 1. Mean
│
├── 2. Median
│
├── 3. Mode
│
├── 4. Choosing the Right Measure
│
├── 5. Business Applications
│
└── 6. Interview Questions
```

---

# 1. Mean

## Definition

Mean is the arithmetic average of all observations.

### Formula

[
Mean = \frac{\sum X}{N}
]

Where:

* X = Observation
* N = Number of Observations

---

## Example

Employee Salaries:

```text
30000
35000
40000
45000
50000
```

Calculation:

```text
Mean =
(30000 + 35000 + 40000 + 45000 + 50000)
---------------------------------------
5

= 40000
```

### Result

```text
Mean Salary = 40,000
```

---

## Advantages

* Easy to calculate
* Uses all observations
* Most widely used measure

---

## Limitations

Sensitive to outliers.

Example:

```text
30000
35000
40000
45000
500000
```

Mean becomes:

```text
130000
```

This does not represent most employees.

---

# 2. Median

## Definition

Median is the middle value after sorting the data.

---

## Example 1 (Odd Observations)

```text
10
20
30
40
50
```

Middle Value:

```text
30
```

Median:

```text
30
```

---

## Example 2 (Even Observations)

```text
10
20
30
40
```

Middle Values:

```text
20 and 30
```

Median:

```text
(20 + 30) / 2

= 25
```

---

## Advantages

* Not affected by outliers
* Better for skewed data

---

## Business Example

Income Distribution:

```text
25000
30000
35000
40000
1000000
```

Median:

```text
35000
```

This better represents typical income than the mean.

---

# 3. Mode

## Definition

Mode is the most frequently occurring value.

---

## Example

Customer Purchases:

```text
1
2
2
2
3
4
5
```

Most Frequent Value:

```text
2
```

Mode:

```text
2
```

---

## Types of Mode

### Unimodal

One mode.

```text
1 2 2 3 4
```

Mode:

```text
2
```

---

### Bimodal

Two modes.

```text
1 2 2 3 3 4
```

Modes:

```text
2 and 3
```

---

### Multimodal

More than two modes.

```text
1 1 2 2 3 3
```

Modes:

```text
1, 2, 3
```

---

### No Mode

All values appear once.

```text
1 2 3 4 5
```

No Mode.

---

## Business Usage

Used extensively in categorical data.

Examples:

```text
Most Purchased Product
Most Common City
Most Preferred Payment Method
Most Common Complaint Category
```

---

# 4. Choosing the Right Measure

| Situation                   | Preferred Measure |
| --------------------------- | ----------------- |
| Symmetric Data              | Mean              |
| Skewed Data                 | Median            |
| Categorical Data            | Mode              |
| Outliers Present            | Median            |
| Most Common Category Needed | Mode              |

---

# 5. Business Applications

## Banking

Average account balance.

```text
Mean
```

---

## Retail

Most sold product.

```text
Mode
```

---

## HR Analytics

Typical employee salary.

```text
Median
```

---

## Healthcare

Average patient waiting time.

```text
Mean
```

---

## E-Commerce

Most preferred payment method.

```text
Mode
```

---

# Example Dataset

| Employee | Salary |
| -------- | ------ |
| E1       | 30000  |
| E2       | 35000  |
| E3       | 40000  |
| E4       | 45000  |
| E5       | 500000 |

---

## Mean

```text
130000
```

---

## Median

```text
40000
```

---

## Mode

```text
No Mode
```

---

## Business Interpretation

The mean is heavily influenced by the outlier salary.

Median provides a more realistic representation of employee salaries.

---

# Python Example

```python
import numpy as np

salary = [30000,35000,40000,45000,500000]

np.mean(salary)

np.median(salary)
```

---

# Pandas Example

```python
import pandas as pd

df['salary'].mean()

df['salary'].median()

df['salary'].mode()
```

---

# SQL Example

## Mean

```sql
SELECT AVG(salary)
FROM employees;
```

---

## Median

```sql
SELECT PERCENTILE_CONT(0.5)
WITHIN GROUP (ORDER BY salary)
FROM employees;
```

---

## Mode

```sql
SELECT salary, COUNT(*)
FROM employees
GROUP BY salary
ORDER BY COUNT(*) DESC;
```

---

# Interview Questions

## Q1. What is the First Moment of a Distribution?

The First Moment measures the central tendency or center of the data.

---

## Q2. What are the measures of Central Tendency?

* Mean
* Median
* Mode

---

## Q3. Difference between Mean and Median?

Mean uses all observations and is affected by outliers.

Median represents the middle value and is resistant to outliers.

---

## Q4. When should Median be preferred over Mean?

When the dataset contains outliers or is highly skewed.

---

## Q5. What is Mode?

Mode is the most frequently occurring value.

---

## Q6. Can a dataset have multiple modes?

Yes.

It can be:

* Bimodal
* Multimodal

---

## Q7. Which measure is suitable for categorical data?

Mode.

---

## Q8. Which measure is most affected by outliers?

Mean.

---

## Q9. Which measure is best for income data?

Median.

Income distributions are usually positively skewed.

---

## Q10. What happens to the Mean when an extreme value is added?

The mean shifts toward the extreme value and may become misleading.

---

# Key Takeaways

* First Moment measures the center of the data.
* Mean is the arithmetic average.
* Median is the middle observation.
* Mode is the most frequent observation.
* Mean is sensitive to outliers.
* Median is preferred for skewed distributions.
* Mode is useful for categorical data.
* Choosing the correct measure improves business decision-making.
