# 09. Feature Scaling / Feature Shrinking

# Overview

Feature Scaling (also called **Feature Shrinking**) is a data preprocessing technique used to bring all numerical features to a common scale without changing their relative information.

It makes the data **scale-free** and **unit-less**, ensuring that features with larger values do not dominate those with smaller values.

---

# What is Feature Scaling?

Different features in a dataset may have different units and ranges.

Example:

| Feature | Value |
|----------|-------:|
| Age | 25 |
| Salary | 750000 |
| Height (cm) | 175 |
| Weight (kg) | 70 |

Notice that:

- Age ranges from **18–60**
- Salary ranges from **20,000–2,000,000**
- Height ranges from **150–190**

Since Salary has much larger values, many machine learning algorithms will give it more importance.

Feature Scaling removes this problem.

---

# Why is Feature Scaling Required?

Feature Scaling is required because:

- Makes all features comparable
- Prevents large-valued features from dominating
- Speeds up gradient descent
- Improves convergence
- Improves model accuracy
- Makes distance calculations meaningful

---

# What Does "Scale-Free" Mean?

After scaling,

Original values

| Height | Salary |
|---------|--------:|
| 170 | 500000 |

become

| Height | Salary |
|---------|---------:|
| 0.42 | 0.51 |

Now both features are on nearly the same scale.

---

# What Does "Unit-less" Mean?

Original Data

| Feature | Unit |
|----------|------|
| Height | cm |
| Weight | kg |
| Salary | ₹ |

After scaling,

| Feature | Value |
|----------|------:|
| Height | 0.45 |
| Weight | -0.72 |
| Salary | 1.18 |

Units disappear.

Everything becomes dimensionless.

---

# Why is Feature Scaling Important?

Without scaling:

```
Salary = 800000
Age = 25
```

Euclidean distance becomes dominated by Salary.

With scaling:

```
Salary = 0.82
Age = 0.63
```

Both contribute fairly.

---

# Algorithms that Require Feature Scaling

Feature Scaling is highly recommended for:

- K-Nearest Neighbors (KNN)
- K-Means Clustering
- Support Vector Machine (SVM)
- Principal Component Analysis (PCA)
- Logistic Regression
- Linear Regression (Gradient Descent)
- Neural Networks
- Deep Learning
- DBSCAN

---

# Algorithms that Usually Do NOT Require Scaling

Tree-based algorithms are insensitive to feature scales.

Examples:

- Decision Tree
- Random Forest
- XGBoost
- LightGBM
- CatBoost

---

# Types of Feature Scaling

1. Standardization (Z-Score Scaling)
2. Min-Max Scaling (Range Method)
3. Robust Scaling

---

# 1. Standardization (Z-Score Scaling)

## Definition

Standardization transforms data so that:

- Mean = 0
- Standard Deviation = 1

Instead of restricting values between 0 and 1, it centers the data around zero.

---

## Formula

```
Z = (X − μ) / σ
```

Where:

- **X** = Original value
- **μ** = Mean
- **σ** = Standard deviation

---

## Example

Original Data

| Marks |
|------:|
| 40 |
| 50 |
| 60 |
| 70 |
| 80 |

Mean = 60

Standard Deviation = 14.14

After Standardization

| Marks | Z-Score |
|------:|---------:|
| 40 | -1.41 |
| 50 | -0.71 |
| 60 | 0 |
| 70 | 0.71 |
| 80 | 1.41 |

---

## Properties

- Mean becomes 0
- Standard deviation becomes 1
- Values may be negative
- No fixed range

---

## Advantages

- Handles different scales effectively
- Suitable for normally distributed data
- Required by many ML algorithms

---

## Disadvantages

- Sensitive to outliers
- Values are not bounded

---

## Python Implementation

```python
from sklearn.preprocessing import StandardScaler
import pandas as pd

df = pd.DataFrame({
    "Salary": [25000, 30000, 45000, 60000, 100000]
})

scaler = StandardScaler()

df["Salary_scaled"] = scaler.fit_transform(df[["Salary"]])

print(df)
```

---

## When to Use

- Linear Regression
- Logistic Regression
- Support Vector Machine
- Neural Networks
- PCA
- K-Means

---

# 2. Min-Max Scaling (Range Method)

## Definition

Min-Max Scaling transforms data into a fixed range.

Usually:

```
0 to 1
```

or

```
-1 to 1
```

---

## Formula

```
X' = (X − Xmin) / (Xmax − Xmin)
```

Where:

- X = Original value
- Xmin = Minimum value
- Xmax = Maximum value

---

## Example

Original Data

| Age |
|----:|
| 20 |
| 30 |
| 40 |
| 50 |
| 60 |

After Min-Max Scaling

| Age | Scaled |
|----:|-------:|
| 20 | 0.00 |
| 30 | 0.25 |
| 40 | 0.50 |
| 50 | 0.75 |
| 60 | 1.00 |

---

## Properties

- Fixed range
- Easy interpretation
- Preserves original distribution

---

## Advantages

- Simple
- Fast
- Maintains relationships
- Works well for Neural Networks

---

## Disadvantages

- Extremely sensitive to outliers
- New data outside training range may exceed 0–1

---

## Python Implementation

```python
from sklearn.preprocessing import MinMaxScaler
import pandas as pd

df = pd.DataFrame({
    "Age": [20,30,40,50,60]
})

scaler = MinMaxScaler()

df["Age_scaled"] = scaler.fit_transform(df[["Age"]])

print(df)
```

---

## When to Use

- Deep Learning
- CNN
- ANN
- KNN
- Distance-based algorithms

---

# 3. Robust Scaling

## Definition

Robust Scaling uses:

- Median
- Interquartile Range (IQR)

instead of Mean and Standard Deviation.

This makes it resistant to outliers.

---

## Formula

```
X' = (X − Median) / IQR
```

Where

```
IQR = Q3 − Q1
```

---

## Example

Original Data

| Salary |
|-------:|
| 30000 |
| 35000 |
| 40000 |
| 45000 |
| 1000000 |

Notice that ₹1,000,000 is an outlier.

StandardScaler would be highly affected.

RobustScaler uses Median and IQR, so the outlier has much less influence.

---

## Advantages

- Resistant to outliers
- Better for skewed data
- Stable scaling

---

## Disadvantages

- Doesn't produce fixed range
- Less effective when no outliers exist

---

## Python Implementation

```python
from sklearn.preprocessing import RobustScaler
import pandas as pd

df = pd.DataFrame({
    "Salary": [30000,35000,40000,45000,1000000]
})

scaler = RobustScaler()

df["Salary_scaled"] = scaler.fit_transform(df[["Salary"]])

print(df)
```

---

## When to Use

- Financial data
- Medical datasets
- Sensor data
- Any dataset containing outliers

---

# Comparison of Feature Scaling Techniques

| Feature | Standardization | Min-Max Scaling | Robust Scaling |
|----------|-----------------|-----------------|----------------|
| Formula | (X−μ)/σ | (X−Min)/(Max−Min) | (X−Median)/IQR |
| Center | Mean | Minimum | Median |
| Spread | Standard Deviation | Range | IQR |
| Output Range | No fixed range | 0–1 | No fixed range |
| Handles Outliers | ❌ No | ❌ No | ✅ Yes |
| Best For | Normal distribution | Neural Networks | Data with outliers |

---

# Which Scaling Technique Should You Use?

| Scenario | Recommended Technique |
|----------|-----------------------|
| Normally distributed data | StandardScaler |
| Deep Learning | MinMaxScaler |
| KNN | MinMaxScaler |
| PCA | StandardScaler |
| SVM | StandardScaler |
| Logistic Regression | StandardScaler |
| Financial data | RobustScaler |
| Dataset with outliers | RobustScaler |

---

# Interview Questions

### Q1. Why do we perform feature scaling?

**Answer:** To make all features comparable, remove unit differences, improve convergence, and prevent features with large values from dominating the model.

---

### Q2. Which algorithms require feature scaling?

- KNN
- K-Means
- SVM
- PCA
- Logistic Regression
- Neural Networks

---

### Q3. Which algorithms do not require scaling?

- Decision Tree
- Random Forest
- XGBoost
- LightGBM
- CatBoost

---

### Q4. Difference between StandardScaler and MinMaxScaler?

| StandardScaler | MinMaxScaler |
|----------------|--------------|
| Mean = 0 | Range = 0–1 |
| Std = 1 | Fixed range |
| Sensitive to outliers | Sensitive to outliers |

---

### Q5. When should RobustScaler be preferred?

Whenever the dataset contains significant outliers.

---

# Summary

Feature Scaling (Feature Shrinking) transforms numerical features into a common scale, making them **scale-free** and **unit-less**. It ensures that each feature contributes equally during model training.

The three most widely used techniques are:

- **Standardization (Z-Score Scaling):** Centers data around a mean of 0 with a standard deviation of 1.
- **Min-Max Scaling (Range Method):** Rescales data to a fixed range, typically 0 to 1.
- **Robust Scaling:** Uses the median and IQR, making it resistant to outliers.

Choosing the right scaling method depends on the data distribution, the presence of outliers, and the machine learning algorithm being used.
