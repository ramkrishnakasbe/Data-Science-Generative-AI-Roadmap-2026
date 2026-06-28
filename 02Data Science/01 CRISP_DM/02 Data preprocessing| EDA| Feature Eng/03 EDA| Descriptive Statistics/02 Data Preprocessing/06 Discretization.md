# 06. Discretization / Binning / Grouping

# Overview

Discretization is the process of converting continuous numerical variables into discrete categories (bins or groups).

It is a data preprocessing technique used to simplify data, reduce noise, and improve interpretability for machine learning models.

---

# Why Discretization is Important?

Discretization is used because:

- It converts continuous data into categorical form
- It reduces the effect of noise and small fluctuations
- It improves interpretability of data
- It helps certain ML models perform better (like Decision Trees, Naive Bayes)
- It enables data segmentation (Low / Medium / High)

---

# Types of Discretization

## 6.1 Binarisation

### Definition

Binarisation converts numerical values into only two categories:
- 0 and 1

based on a threshold.

---

### Working Rule

```
If value > threshold → 1
Else → 0
```

---

### Example

| Age | Output |
|-----|--------|
| 18  | 0 |
| 22  | 1 |
| 35  | 1 |
| 15  | 0 |

Threshold = 20

---

### Python Implementation

```python
from sklearn.preprocessing import Binarizer

data = [[18], [22], [35], [15]]

binarizer = Binarizer(threshold=20)

result = binarizer.fit_transform(data)

print(result)
```

---

### Use Cases

- Yes/No classification
- Risk detection (High/Low)
- Spam filtering
- Feature simplification

---

# 6.2 Rounding

## Definition

Rounding is a technique used to approximate numerical values to simpler forms such as nearest integer or reduced decimal precision.

---

## Example

| Value | Rounded |
|------|--------|
| 12.3 | 12 |
| 15.8 | 16 |
| 20.4 | 20 |
| 99.6 | 100 |

---

## Python Implementation

```python
import numpy as np

data = np.array([12.3, 15.8, 20.4, 99.6])

rounded = np.round(data)

print(rounded)
```

---

## Use Cases

- Financial data simplification
- Measurement noise reduction
- Data cleaning

---

# 6.3 Binning (Fixed and Adaptive)

## Definition

Binning is the process of dividing continuous data into intervals (bins) and assigning each value to a bin category.

---

# A) Fixed Binning

## Definition

Fixed binning divides data into equal-width intervals.

---

## Example

Age range: 0–60

```
0–20   → Young
21–40  → Adult
41–60  → Senior
```

---

## Python Implementation

```python
import pandas as pd

ages = [10, 25, 35, 50, 60]

bins = [0, 20, 40, 60]

labels = ["Young", "Adult", "Senior"]

result = pd.cut(ages, bins=bins, labels=labels)

print(result)
```

---

## Characteristics

- Equal interval width
- Easy to implement
- Sensitive to outliers
- May lead to uneven distribution of data

---

# B) Adaptive Binning

## Definition

Adaptive binning creates bins based on data distribution instead of fixed ranges.

---

## Types of Adaptive Binning

---

# 1. Equal Frequency Binning

Each bin contains approximately the same number of observations.

---

## Example

```
Data: [1,2,3,4,5,6,7,8,9,10]

Bin 1 → [1,2,3]
Bin 2 → [4,5,6]
Bin 3 → [7,8,9,10]
```

---

## Python Implementation

```python
import pandas as pd

data = [1,2,3,4,5,6,7,8,9,10]

result = pd.qcut(data, q=3)

print(result)
```

---

# 2. Quantile-Based Binning

Bins are created using quantile boundaries.

---

## Example

- 0–25% → Bin 1
- 25–50% → Bin 2
- 50–75% → Bin 3
- 75–100% → Bin 4

---

## Python Implementation

```python
pd.qcut(data, q=4)
```

---

# Fixed vs Adaptive Binning

| Feature | Fixed Binning | Adaptive Binning |
|--------|--------------|------------------|
| Basis | Equal range | Data distribution |
| Bin Size | Same width | Variable width |
| Outliers Impact | High | Low |
| Data Balance | May be imbalanced | More balanced |
| Complexity | Simple | Moderate |

---

# Advantages of Discretization

- Reduces noise in data
- Simplifies complex datasets
- Improves interpretability
- Helps categorical modeling
- Useful for segmentation

---

# Disadvantages

- Loss of information
- Choice of bins affects results
- Not suitable for all ML models
- Can reduce accuracy if not done properly

---

# Real-World Example

### Salary Dataset

| Salary |
|--------|
| 20000 |
| 30000 |
| 50000 |
| 80000 |
| 120000 |

After binning:

| Salary | Category |
|--------|----------|
| 20000  | Low |
| 30000  | Low |
| 50000  | Medium |
| 80000  | High |
| 120000 | High |

---

# Summary

Discretization is a preprocessing technique that converts continuous numerical variables into categorical bins. It includes Binarisation, Rounding, and Binning (Fixed and Adaptive). It helps simplify data, reduce noise, and improve interpretability for machine learning models.
