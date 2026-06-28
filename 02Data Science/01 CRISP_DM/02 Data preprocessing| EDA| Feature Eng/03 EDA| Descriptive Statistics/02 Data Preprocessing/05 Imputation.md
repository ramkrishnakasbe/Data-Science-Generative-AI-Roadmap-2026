# 05. Missing Value Imputation

# Overview

Missing Value Imputation is the process of identifying and handling missing (null/NaN) values in a dataset. Missing values are common in real-world datasets and can negatively affect statistical analysis and machine learning models.# 05. Missing Value Imputation

# Overview

Missing Value Imputation is the process of identifying and handling missing (null/NaN) values in a dataset. Missing values are common in real-world datasets and can negatively affect statistical analysis and machine learning models.

Instead of simply removing records, imputation techniques estimate and replace missing values with appropriate values.

---

# Why Handle Missing Values?

Missing values can:

- Reduce data quality
- Bias statistical analysis
- Decrease model accuracy
- Cause errors in machine learning algorithms
- Reduce the amount of usable data

Proper imputation preserves valuable information while improving model performance.

---

# What are Missing Values?

Missing values represent the absence of information for one or more observations.

### Example

| ID | Age | Salary |
|----|-----|---------|
|1|25|45000|
|2|NaN|52000|
|3|30|NaN|
|4|28|48000|

---

# Detecting Missing Values

## Check Missing Values

```python
df.isnull()
```

## Count Missing Values

```python
df.isnull().sum()
```

## Total Missing Values

```python
df.isnull().sum().sum()
```

## Percentage of Missing Values

```python
(df.isnull().sum()/len(df))*100
```

---

# Types (Variants) of Missing Data

Understanding why data is missing is important before selecting an imputation technique.

---

# 1. MCAR (Missing Completely At Random)

## Definition

The probability of missing data is completely random and independent of every variable.

### Example

A survey form gets damaged during transportation.

| Age | Salary |
|-----|---------|
|25|45000|
|NaN|52000|
|30|60000|

The missing Age has no relationship with any variable.

### Characteristics

- Completely random
- Least problematic
- Produces unbiased analysis

---

# 2. MAR (Missing At Random)

## Definition

Missing values depend on another observed variable but not on the missing value itself.

### Example

Older employees are less likely to disclose their salary.

| Age | Salary |
|-----|---------|
|25|45000|
|55|NaN|
|60|NaN|

Salary depends on Age.

### Characteristics

- Depends on another variable
- Most common in practice
- Can usually be handled using imputation

---

# 3. MNAR (Missing Not At Random)

## Definition

Missing values depend on the missing value itself.

### Example

People with higher salaries choose not to reveal their income.

| Salary |
|---------|
|45000|
|NaN|
|NaN|

### Characteristics

- Most difficult to handle
- Can introduce bias
- Requires domain knowledge

---

# Comparison of Missing Data Types

| Type | Depends On | Example |
|------|------------|---------|
| MCAR | Nothing | Random survey loss |
| MAR | Other variables | Salary missing because of Age |
| MNAR | Missing value itself | High-income people hide salary |

---

# Missing Value Handling Techniques

## 1. Deletion Method

Instead of filling missing values, remove observations or variables containing missing data.

### a) Listwise Deletion (Complete Case Analysis)

Removes every row containing at least one missing value.

```python
df.dropna()
```

#### Advantages

- Simple
- No imputation bias

#### Disadvantages

- Large loss of data

---

### b) Pairwise Deletion (Available Case Analysis)

Uses only available observations for each calculation.

Example:

- Correlation between Age and Salary uses only rows where both exist.
- Correlation between Salary and Experience uses another subset.

#### Advantages

- Preserves more observations

#### Disadvantages

- Different analyses use different sample sizes

---

# 2. Simple Imputation Techniques

---

## Mean Imputation

Missing values are replaced with the mean.

### Formula

```
Mean = ΣX / n
```

### Example

| Age |
|-----|
|20|
|25|
|NaN|
|35|

Mean

```
(20+25+35)/3 = 26.67
```

### Scikit-learn

```python
import numpy as np
from sklearn.impute import SimpleImputer

imputer = SimpleImputer(
    missing_values=np.nan,
    strategy="mean"
)

df["Age"] = imputer.fit_transform(df[["Age"]])
```

#### Suitable For

- Numerical data
- Normally distributed data

---

## Median Imputation

Missing values are replaced with the median.

### Example

| Income |
|---------|
|20|
|25|
|NaN|
|100|

Median = **25**

```python
from sklearn.impute import SimpleImputer

imputer = SimpleImputer(strategy="median")
```

#### Suitable For

- Numerical data
- Skewed distributions
- Presence of outliers

---

## Mode Imputation

Missing values are replaced using the most frequent value.

### Example

| Gender |
|---------|
|Male|
|Female|
|Male|
|NaN|

Mode = **Male**

```python
from sklearn.impute import SimpleImputer

imputer = SimpleImputer(strategy="most_frequent")
```

#### Suitable For

- Categorical variables

---

# Random Imputation

## Definition

Randomly select one existing value from the same feature and replace the missing value.

### Example

Original

```
20
25
30
NaN
35
```

Possible Result

```
20
25
30
25
35
```

#### Advantages

- Preserves data distribution better than mean imputation

#### Disadvantages

- Results may vary because of randomness

---

# Hot Deck Imputation

## Definition

Replace missing values using values from similar observations in the same dataset.

### Example

If two customers have similar:

- Age
- Occupation
- City

Then the missing salary of one customer may be replaced using the salary of the other.

#### Advantages

- Uses realistic values
- Maintains relationships

#### Disadvantages

- Computationally expensive

---

# Regression Imputation

## Definition

Predict missing values using a regression model.

### Example

Predict Salary using:

- Age
- Experience
- Education

```
Salary = β₀ + β₁(Age) + β₂(Experience)
```

#### Advantages

- More accurate
- Uses relationships between variables

#### Disadvantages

- Depends on regression assumptions

---

# KNN Imputation

## Definition

K-Nearest Neighbor (KNN) Imputation replaces missing values using the values of the nearest observations.

### Working

1. Find K nearest records.
2. Compute similarity.
3. Estimate the missing value using neighbors.

### Example

| Age | Salary |
|-----|---------|
|25|40000|
|26|42000|
|27|NaN|
|28|43000|

Predicted Salary ≈ **42500**

### Scikit-learn

```python
from sklearn.impute import KNNImputer

imputer = KNNImputer(n_neighbors=3)

df = imputer.fit_transform(df)
```

#### Advantages

- Preserves feature relationships
- Better than simple imputation

#### Disadvantages

- Computationally expensive
- Sensitive to feature scaling

---

# Comparison of Imputation Techniques

| Technique | Suitable For | Advantages | Disadvantages |
|-----------|--------------|------------|---------------|
| Listwise Deletion | Few missing values | Simple | Data loss |
| Pairwise Deletion | Statistical analysis | Preserves more data | Different sample sizes |
| Mean | Numerical | Easy | Sensitive to outliers |
| Median | Numerical | Robust to outliers | Ignores feature relationships |
| Mode | Categorical | Simple | May introduce bias |
| Random | Numerical/Categorical | Preserves distribution | Random results |
| Hot Deck | Similar observations | Realistic values | Computationally expensive |
| Regression | Numerical | Accurate | Model dependent |
| KNN | Numerical | Preserves relationships | Slow for large datasets |

---

# Real-World Example

A banking dataset contains missing values in **Annual Income**.

- Few missing values → Listwise Deletion
- Normal distribution → Mean Imputation
- Skewed distribution → Median Imputation
- Similar customers available → Hot Deck or KNN Imputation
- Income depends on Age and Experience → Regression Imputation

The choice of technique depends on the amount of missing data, its distribution, and the business problem.

---

# Summary

Missing Value Imputation is a critical data preprocessing step used to handle incomplete datasets. Missing values are categorized into **MCAR**, **MAR**, and **MNAR** based on their underlying cause. Common handling methods include **Deletion**, **Mean**, **Median**, **Mode**, **Random**, **Hot Deck**, **Regression**, and **KNN Imputation**. Choosing the right technique helps preserve data quality, reduce bias, and improve the performance of machine learning models.

Instead of simply removing records, imputation techniques estimate and replace missing values with appropriate values.

---

# Why Handle Missing Values?

Missing values can:

- Reduce data quality
- Bias statistical analysis
- Decrease model accuracy
- Cause errors in machine learning algorithms
- Reduce the amount of usable data

Proper imputation preserves valuable information while improving model performance.

---

# What are Missing Values?

Missing values represent the absence of information for one or more observations.

### Example

| ID | Age | Salary |
|----|-----|---------|
|1|25|45000|
|2|NaN|52000|
|3|30|NaN|
|4|28|48000|

---

# Detecting Missing Values

## Check Missing Values

```python
df.isnull()
```

## Count Missing Values

```python
df.isnull().sum()
```

## Total Missing Values

```python
df.isnull().sum().sum()
```

## Percentage of Missing Values

```python
(df.isnull().sum()/len(df))*100
```

---

# Types (Variants) of Missing Data

Understanding why data is missing is important before selecting an imputation technique.

---

# 1. MCAR (Missing Completely At Random)

## Definition

The probability of missing data is completely random and independent of every variable.

### Example

A survey form gets damaged during transportation.

| Age | Salary |
|-----|---------|
|25|45000|
|NaN|52000|
|30|60000|

The missing Age has no relationship with any variable.

### Characteristics

- Completely random
- Least problematic
- Produces unbiased analysis

---

# 2. MAR (Missing At Random)

## Definition

Missing values depend on another observed variable but not on the missing value itself.

### Example

Older employees are less likely to disclose their salary.

| Age | Salary |
|-----|---------|
|25|45000|
|55|NaN|
|60|NaN|

Salary depends on Age.

### Characteristics

- Depends on another variable
- Most common in practice
- Can usually be handled using imputation

---

# 3. MNAR (Missing Not At Random)

## Definition

Missing values depend on the missing value itself.

### Example

People with higher salaries choose not to reveal their income.

| Salary |
|---------|
|45000|
|NaN|
|NaN|

### Characteristics

- Most difficult to handle
- Can introduce bias
- Requires domain knowledge

---

# Comparison of Missing Data Types

| Type | Depends On | Example |
|------|------------|---------|
| MCAR | Nothing | Random survey loss |
| MAR | Other variables | Salary missing because of Age |
| MNAR | Missing value itself | High-income people hide salary |

---

# Missing Value Handling Techniques

## 1. Deletion Method

Instead of filling missing values, remove observations or variables containing missing data.

### a) Listwise Deletion (Complete Case Analysis)

Removes every row containing at least one missing value.

```python
df.dropna()
```

#### Advantages

- Simple
- No imputation bias

#### Disadvantages

- Large loss of data

---

### b) Pairwise Deletion (Available Case Analysis)

Uses only available observations for each calculation.

Example:

- Correlation between Age and Salary uses only rows where both exist.
- Correlation between Salary and Experience uses another subset.

#### Advantages

- Preserves more observations

#### Disadvantages

- Different analyses use different sample sizes

---

# 2. Simple Imputation Techniques

---

## Mean Imputation

Missing values are replaced with the mean.

### Formula

```
Mean = ΣX / n
```

### Example

| Age |
|-----|
|20|
|25|
|NaN|
|35|

Mean

```
(20+25+35)/3 = 26.67
```

### Scikit-learn

```python
import numpy as np
from sklearn.impute import SimpleImputer

imputer = SimpleImputer(
    missing_values=np.nan,
    strategy="mean"
)

df["Age"] = imputer.fit_transform(df[["Age"]])
```

#### Suitable For

- Numerical data
- Normally distributed data

---

## Median Imputation

Missing values are replaced with the median.

### Example

| Income |
|---------|
|20|
|25|
|NaN|
|100|

Median = **25**

```python
from sklearn.impute import SimpleImputer

imputer = SimpleImputer(strategy="median")
```

#### Suitable For

- Numerical data
- Skewed distributions
- Presence of outliers

---

## Mode Imputation

Missing values are replaced using the most frequent value.

### Example

| Gender |
|---------|
|Male|
|Female|
|Male|
|NaN|

Mode = **Male**

```python
from sklearn.impute import SimpleImputer

imputer = SimpleImputer(strategy="most_frequent")
```

#### Suitable For

- Categorical variables

---

# Random Imputation

## Definition

Randomly select one existing value from the same feature and replace the missing value.

### Example

Original

```
20
25
30
NaN
35
```

Possible Result

```
20
25
30
25
35
```

#### Advantages

- Preserves data distribution better than mean imputation

#### Disadvantages

- Results may vary because of randomness

---

# Hot Deck Imputation

## Definition

Replace missing values using values from similar observations in the same dataset.

### Example

If two customers have similar:

- Age
- Occupation
- City

Then the missing salary of one customer may be replaced using the salary of the other.

#### Advantages

- Uses realistic values
- Maintains relationships

#### Disadvantages

- Computationally expensive

---

# Regression Imputation

## Definition

Predict missing values using a regression model.

### Example

Predict Salary using:

- Age
- Experience
- Education

```
Salary = β₀ + β₁(Age) + β₂(Experience)
```

#### Advantages

- More accurate
- Uses relationships between variables

#### Disadvantages

- Depends on regression assumptions

---

# KNN Imputation

## Definition

K-Nearest Neighbor (KNN) Imputation replaces missing values using the values of the nearest observations.

### Working

1. Find K nearest records.
2. Compute similarity.
3. Estimate the missing value using neighbors.

### Example

| Age | Salary |
|-----|---------|
|25|40000|
|26|42000|
|27|NaN|
|28|43000|

Predicted Salary ≈ **42500**

### Scikit-learn

```python
from sklearn.impute import KNNImputer

imputer = KNNImputer(n_neighbors=3)

df = imputer.fit_transform(df)
```

#### Advantages

- Preserves feature relationships
- Better than simple imputation

#### Disadvantages

- Computationally expensive
- Sensitive to feature scaling

---

# Comparison of Imputation Techniques

| Technique | Suitable For | Advantages | Disadvantages |
|-----------|--------------|------------|---------------|
| Listwise Deletion | Few missing values | Simple | Data loss |
| Pairwise Deletion | Statistical analysis | Preserves more data | Different sample sizes |
| Mean | Numerical | Easy | Sensitive to outliers |
| Median | Numerical | Robust to outliers | Ignores feature relationships |
| Mode | Categorical | Simple | May introduce bias |
| Random | Numerical/Categorical | Preserves distribution | Random results |
| Hot Deck | Similar observations | Realistic values | Computationally expensive |
| Regression | Numerical | Accurate | Model dependent |
| KNN | Numerical | Preserves relationships | Slow for large datasets |

---

# Real-World Example

A banking dataset contains missing values in **Annual Income**.

- Few missing values → Listwise Deletion
- Normal distribution → Mean Imputation
- Skewed distribution → Median Imputation
- Similar customers available → Hot Deck or KNN Imputation
- Income depends on Age and Experience → Regression Imputation

The choice of technique depends on the amount of missing data, its distribution, and the business problem.

---

# Summary

Missing Value Imputation is a critical data preprocessing step used to handle incomplete datasets. Missing values are categorized into **MCAR**, **MAR**, and **MNAR** based on their underlying cause. Common handling methods include **Deletion**, **Mean**, **Median**, **Mode**, **Random**, **Hot Deck**, **Regression**, and **KNN Imputation**. Choosing the right technique helps preserve data quality, reduce bias, and improve the performance of machine learning models.
