# Third Moment Business

## What is Third Moment?

The Third Moment of a distribution measures **Skewness**.

Skewness tells us:

```text
Is the data distributed symmetrically,
or is it leaning towards one side?
```

While:

```text
1st Moment → Center (Mean)
2nd Moment → Spread (Variance)
3rd Moment → Shape (Skewness)
```

---

# Why is Third Moment Important?

In real-world datasets, data is rarely perfectly balanced.

Examples:

- Salaries
- House Prices
- Customer Spending
- Insurance Claims

Most business datasets are skewed.

Understanding skewness helps:

- Select appropriate statistical measures
- Detect abnormal behavior
- Choose correct ML algorithms
- Identify outliers

---

# Third Moment Roadmap

```text
Third Moment Business
│
├── 1. Skewness
│
├── 2. Symmetric Distribution
│
├── 3. Positive Skewness
│
├── 4. Negative Skewness
│
├── 5. Mean-Median-Mode Relationship
│
├── 6. Business Applications
│
└── 7. Interview Questions
```

---

# 1. Skewness

## Definition

Skewness measures the degree of asymmetry in a distribution.

It indicates whether data is:

```text
Balanced
or
Leaning toward one side
```

---

## Formula

Population Skewness

```text
Skewness = Σ(X - Mean)³
           -------------
              Nσ³
```

Where:

```text
X  = Observation
N  = Number of Observations
σ  = Standard Deviation
```

---

## Interpretation

| Skewness Value | Interpretation |
|---------------|---------------|
| = 0 | Symmetric |
| > 0 | Positive Skew |
| < 0 | Negative Skew |

---

# 2. Symmetric Distribution

## Definition

A distribution is symmetric when both sides are approximately equal.

---

## Shape

```text
          *
        *   *
      *       *
    *           *
  *               *
-------------------------
```

---

## Characteristics

```text
Mean = Median = Mode
```

---

## Example

Student Heights

```text
165
168
170
172
175
```

Most observations lie around the center.

---

## Business Examples

- IQ Scores
- Human Heights
- Standardized Test Scores

---

# Mean-Median-Mode Relationship

```text
Mean
  =
Median
  =
Mode
```

---

# 3. Positive Skewness

## Definition

Data is concentrated on the left side.

Tail extends towards the right.

---

## Shape

```text
*
**
***
****
*****
*******
************
---------------------->
```

---

## Characteristics

Few extremely large values exist.

---

## Mean-Median-Mode Relationship

```text
Mode < Median < Mean
```

---

## Example

Employee Salaries

```text
25000
30000
35000
40000
50000
500000
```

Most employees earn normal salaries.

A few executives earn very high salaries.

Mean gets pulled right.

---

## Business Examples

### Salary Distribution

```text
Most employees → Normal Salary

Few employees → Very High Salary
```

---

### House Prices

```text
Most Houses → Moderate Price

Few Luxury Houses → Extremely Expensive
```

---

### Customer Spending

```text
Most Customers → Average Spending

Few Customers → Very High Spending
```

---

# Positive Skew Interpretation

```text
Mean > Median
```

If this happens:

```text
Outliers likely exist
```

Median often becomes the preferred measure.

---

# 4. Negative Skewness

## Definition

Data is concentrated on the right side.

Tail extends towards the left.

---

## Shape

```text
               *
             ***
           *****
         *******
      *********
<----------------
```

---

## Characteristics

Few extremely small values exist.

---

## Mean-Median-Mode Relationship

```text
Mean < Median < Mode
```

---

## Example

Easy Examination Scores

```text
95
96
97
98
99
60
```

Most students score high.

Few students score very low.

Mean gets pulled left.

---

## Business Examples

### Customer Satisfaction

```text
Most Customers → Highly Satisfied

Few Customers → Very Dissatisfied
```

---

### Product Ratings

```text
Most Ratings → 4 or 5

Few Ratings → 1
```

---

### Service Quality

```text
Majority Positive

Few Negative Experiences
```

---

# Negative Skew Interpretation

```text
Mean < Median
```

Usually indicates strong overall performance.

---

# 5. Mean-Median-Mode Relationship

This is one of the most frequently asked interview topics.

---

## Symmetric Distribution

```text
Mean = Median = Mode
```

---

## Positive Skew

```text
Mode < Median < Mean
```

---

## Negative Skew

```text
Mean < Median < Mode
```

---

## Summary Table

| Distribution | Relationship |
|-------------|-------------|
| Symmetric | Mean = Median = Mode |
| Positive Skew | Mode < Median < Mean |
| Negative Skew | Mean < Median < Mode |

---

# Real Dataset Example

## Dataset A

```text
10
20
30
40
50
```

Symmetric

```text
Mean = Median = Mode
```

---

## Dataset B

```text
20
25
30
35
40
500
```

Positive Skew

```text
Mean > Median
```

---

## Dataset C

```text
10
90
95
96
97
98
99
```

Negative Skew

```text
Mean < Median
```

---

# Business Applications

## Banking

Loan Amount Analysis

Large loans create positive skew.

---

## Insurance

Claim Amount Analysis

Few large claims produce positive skew.

---

## HR Analytics

Salary Distribution

Almost always positively skewed.

---

## E-Commerce

Customer Purchase Value

Few customers generate very high revenue.

---

## Healthcare

Patient Waiting Time

Long delays create positive skew.

---

# Python Example

## Skewness Calculation

```python
import pandas as pd

df['salary'].skew()
```

---

## Interpretation

```text
> 0  → Positive Skew

< 0  → Negative Skew

≈ 0  → Symmetric
```

---

# Visualization Example

```python
import seaborn as sns

sns.histplot(df['salary'], kde=True)
```

Observe:

- Tail Direction
- Distribution Shape

---

# SQL Example

Most SQL databases do not provide direct skewness functions.

Usually:

```sql
SELECT
AVG(salary),
MEDIAN(salary)
FROM employees;
```

Compare:

```text
Mean vs Median
```

to infer skewness.

---

# Interview Questions

## Q1. What is the Third Moment of a Distribution?

The Third Moment measures skewness or asymmetry in data.

---

## Q2. What is Skewness?

Skewness measures whether data leans toward the left or right side.

---

## Q3. What does Positive Skew mean?

Most observations are small and a few very large values pull the distribution to the right.

---

## Q4. What does Negative Skew mean?

Most observations are large and a few small values pull the distribution to the left.

---

## Q5. What is the skewness value for a perfectly symmetric distribution?

```text
0
```

---

## Q6. What is the relationship between Mean, Median, and Mode in Positive Skew?

```text
Mode < Median < Mean
```

---

## Q7. What is the relationship between Mean, Median, and Mode in Negative Skew?

```text
Mean < Median < Mode
```

---

## Q8. Why is Salary Data usually Positively Skewed?

A few employees earn extremely high salaries while most earn moderate salaries.

---

## Q9. Which measure is preferred for highly skewed data?

```text
Median
```

because it is less affected by outliers.

---

## Q10. How can you detect skewness visually?

Using:

- Histogram
- Density Plot
- Box Plot

Observe the direction of the tail.

---

# Key Takeaways

- Third Moment measures Skewness.
- Skewness explains the shape of data.
- Positive Skew → Tail on Right.
- Negative Skew → Tail on Left.
- Symmetric Distribution → Mean = Median = Mode.
- Positive Skew → Mean > Median.
- Negative Skew → Mean < Median.
- Salary, Income, House Prices are usually positively skewed.
- Median is preferred for highly skewed data.
- Understanding skewness is essential before modeling.
