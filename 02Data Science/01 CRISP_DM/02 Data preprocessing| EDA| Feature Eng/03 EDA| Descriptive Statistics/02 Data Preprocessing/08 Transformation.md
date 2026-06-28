# 08. Data Transformation 

# Overview

Data Transformation is a preprocessing technique used to modify the scale, distribution, or structure of data to make it suitable for machine learning models.

It helps in:
- Reducing skewness
- Normalizing distributions
- Scaling features
- Improving model convergence
- Handling outliers

---

# Why Data Transformation is Important?

- Many ML models assume normal distribution
- Features may be on different scales
- Skewed data affects model performance
- Gradient-based models converge faster with scaling
- Improves statistical stability

---

# Types of Data Transformation

---

# 1. Log Transformation

## Definition

Log transformation compresses large values and reduces right-skewness.

---

## Formula

```
log(x)  or  log(1 + x)
```

---

## Why log(1 + x)?

Used when data contains zero values because:

```
log(0) is undefined
```

So:

```
log(1 + x) handles zero safely
```

---

## Example

| Value | log(x) |
|------|--------|
| 10   | 2.30 |
| 100  | 4.60 |
| 1000 | 6.90 |

---

## Python Implementation

```python
import numpy as np

data = np.array([10, 100, 1000])

log_data = np.log(data)

print(log_data)
```

---

## Use Cases

- Income data
- Sales data
- Population data
- Highly skewed distributions

---

# 2. Square Root Transformation

## Definition

Used to reduce moderate skewness.

---

## Formula

```
sqrt(x)
```

---

## Example

| Value | Sqrt |
|------|------|
| 4    | 2 |
| 9    | 3 |
| 16   | 4 |

---

## Python Implementation

```python
import numpy as np

data = np.array([4, 9, 16, 25])

sqrt_data = np.sqrt(data)

print(sqrt_data)
```

---

# 3. Reciprocal Transformation

## Definition

Strong transformation used to reduce extreme skewness.

---

## Formula

```
1 / x
```

---

## Example

| Value | Reciprocal |
|------|------------|
| 2    | 0.5 |
| 4    | 0.25 |
| 10   | 0.1 |

---

## Python Implementation

```python
import numpy as np

data = np.array([2, 4, 10])

reciprocal = 1 / data

print(reciprocal)
```

---

## Limitation

- Cannot handle zero values
- Hard to interpret

---

# 4. Box-Cox Transformation

## Definition

Box-Cox transformation makes data more Gaussian-like and stabilizes variance.

Only works for positive values.

---

## Formula

```
y(λ) = (x^λ - 1) / λ
```

---

## Python Implementation

```python
from scipy import stats

data = [1, 2, 3, 4, 5]

transformed_data, lambda_value = stats.boxcox(data)

print(transformed_data)
```

---

## Use Cases

- Linear regression
- Statistical modeling
- Normality assumption improvement

---

# 5. Yeo-Johnson Transformation

## Definition

Extension of Box-Cox that works with:
- Zero values
- Negative values

---

## Python Implementation

```python
from sklearn.preprocessing import PowerTransformer

data = [[-1], [0], [1], [2], [3]]

pt = PowerTransformer(method='yeo-johnson')

transformed = pt.fit_transform(data)

print(transformed)
```

---

# 6. Standardization (Z-Score Scaling)

## Definition

Transforms data to:
- Mean = 0
- Standard deviation = 1

---

## Formula

```
Z = (X - mean) / std
```

---

## Python Implementation

```python
from sklearn.preprocessing import StandardScaler

data = [[10], [20], [30]]

scaler = StandardScaler()

scaled = scaler.fit_transform(data)

print(scaled)
```

---

## Use Cases

- Logistic Regression
- SVM
- Neural Networks
- PCA

---

# 7. Min-Max Scaling

## Definition

Scales data between 0 and 1.

---

## Formula

```
X' = (X - min) / (max - min)
```

---

## Python Implementation

```python
from sklearn.preprocessing import MinMaxScaler

data = [[10], [20], [30]]

scaler = MinMaxScaler()

scaled = scaler.fit_transform(data)

print(scaled)
```

---

## Use Cases

- Neural networks
- Image processing
- Distance-based models

---

## Limitation

- Sensitive to outliers

---

# 8. Robust Scaling

## Definition

Uses median and IQR instead of mean and standard deviation.

---

## Formula

```
X' = (X - median) / IQR
```

---

## Python Implementation

```python
from sklearn.preprocessing import RobustScaler

data = [[10], [20], [30]]

scaler = RobustScaler()

scaled = scaler.fit_transform(data)

print(scaled)
```

---

## Use Cases

- Data with outliers
- Real-world noisy datasets

---

# Comparison of Transformations

| Method | Best For | Advantage | Limitation |
|-------|----------|----------|------------|
| Log | Right skewed data | Reduces skewness | Cannot handle zero |
| Sqrt | Moderate skew | Simple | Less powerful |
| Reciprocal | Strong skew | Compresses large values | Hard interpretation |
| Box-Cox | Positive data | Normal distribution | Only positive values |
| Yeo-Johnson | Any data | Flexible | Complex |
| StandardScaler | ML models | Centered data | Outlier sensitive |
| MinMaxScaler | Neural networks | Fixed range | Outliers affect scaling |
| RobustScaler | Outliers | Robust to outliers | Less intuitive |

---

# Summary

Data Transformation is a crucial preprocessing step that modifies data distribution, reduces skewness, and improves model performance. It includes Log, Square Root, Reciprocal, Box-Cox, Yeo-Johnson, Standardization, Min-Max Scaling, and Robust Scaling.
