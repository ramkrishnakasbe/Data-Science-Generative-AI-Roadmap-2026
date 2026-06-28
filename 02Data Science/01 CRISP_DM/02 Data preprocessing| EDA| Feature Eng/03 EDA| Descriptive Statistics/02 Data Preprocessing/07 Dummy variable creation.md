# 07. Dummy Variable Creation (Categorical Encoding Techniques)

# Overview

Dummy Variable Creation is the process of converting categorical variables into numerical format so that machine learning models can understand them.

Since ML algorithms work only with numbers, categorical features like "Red", "Blue", "Male", "Female" must be encoded properly.

---

# Why Encoding is Required?

Machine Learning models require encoding because:

- They perform mathematical operations
- They cannot understand text data
- They require numerical input for training
- Distance-based algorithms need numeric values

---

# 1. Label Encoding

## Definition

Label Encoding assigns a unique integer to each category.

---

## Example

| Color | Encoded |
|------|--------|
| Red   | 0 |
| Blue  | 1 |
| Green | 2 |

---

## Python Implementation

```python
from sklearn.preprocessing import LabelEncoder

colors = ["Red", "Blue", "Green", "Blue"]

encoder = LabelEncoder()

encoded = encoder.fit_transform(colors)

print(encoded)
```

---

## Limitation

It introduces fake ordering:

```
Red < Blue < Green ❌ (not meaningful)
```

---

# 2. One-Hot Encoding

## Definition

One-Hot Encoding converts each category into a binary vector (0/1).

---

## Example

| Color | Red | Blue | Green |
|------|-----|------|-------|
| Red   | 1   | 0    | 0 |
| Blue  | 0   | 1    | 0 |
| Green | 0   | 0    | 1 |

---

## Python Implementation (Pandas)

```python
import pandas as pd

df = pd.DataFrame({"Color": ["Red", "Blue", "Green", "Blue"]})

one_hot = pd.get_dummies(df["Color"])

print(one_hot)
```

---

## Python Implementation (Sklearn)

```python
from sklearn.preprocessing import OneHotEncoder
import numpy as np

colors = np.array(["Red", "Blue", "Green", "Blue"]).reshape(-1,1)

encoder = OneHotEncoder()

result = encoder.fit_transform(colors).toarray()

print(result)
```

---

## Dummy Variable Trap

When all categories are included, one column becomes redundant.

```
Red + Blue + Green = 1 (always)
```

This causes multicollinearity.

---

## Solution

Drop one column:

```python
pd.get_dummies(df, drop_first=True)
```

---

# 3. Dummy Coding Scheme

## Definition

Dummy coding is similar to One-Hot Encoding but uses a reference (baseline) category.

---

## Example

If "Blue" is baseline:

| Red | Green |
|-----|-------|
| 1   | 0 |
| 0   | 0 |
| 0   | 1 |

---

## Use Case

- Linear regression
- Statistical models

---

# 4. Effect Coding

## Definition

Effect coding compares each category to the overall mean instead of a baseline.

---

## Example

| Red | Blue | Green |
|-----|------|-------|
| 1   | 0    | -1 |
| 0   | 1    | -1 |
| -1  | -1   | -1 |

---

## Use Case

- ANOVA
- Statistical interpretation

---

# 5. Bin-Counting Scheme

## Definition

Replaces categories with their frequency counts.

---

## Example

| City | Count |
|------|------|
| Delhi | 50 |
| Mumbai | 30 |
| Pune | 20 |

---

## Use Case

- High-cardinality features
- CTR prediction systems

---

# 6. Feature Hashing Scheme

## Definition

Feature hashing converts categories into fixed-length numeric vectors using a hash function.

---

## Example

```
Delhi → 101010
Mumbai → 110001
```

---

## Advantages

- Memory efficient
- Works for large datasets
- No mapping storage needed

---

## Disadvantages

- Hash collisions
- Not interpretable

---

# Comparison of Encoding Techniques

| Method | Use Case | Advantage | Disadvantage |
|-------|----------|----------|-------------|
| Label Encoding | Tree models | Simple | Fake ordering |
| One-Hot Encoding | Nominal data | No ordering issue | High dimensionality |
| Dummy Coding | Regression models | Baseline comparison | Interpretation needed |
| Effect Coding | Statistical analysis | Mean comparison | Complex |
| Bin Counting | High cardinality | Simple | Loses meaning |
| Feature Hashing | Large datasets | Memory efficient | Collisions |

---

# When to Use What?

- Label Encoding → Tree-based models (Random Forest, XGBoost)
- One-Hot Encoding → Small categorical variables
- Dummy Coding → Linear regression
- Effect Coding → Statistical analysis
- Bin Counting → High-cardinality features
- Feature Hashing → Large-scale datasets

---

# Real-World Example

### City Feature

| City |
|------|
| Delhi |
| Mumbai |
| Pune |

After One-Hot Encoding:

| Delhi | Mumbai | Pune |
|------|--------|------|
| 1 | 0 | 0 |
| 0 | 1 | 0 |
| 0 | 0 | 1 |

---

# Summary

Dummy Variable Creation is a key preprocessing step used to convert categorical variables into numerical form. It includes Label Encoding, One-Hot Encoding, Dummy Coding, Effect Coding, Bin Counting, and Feature Hashing.

Each method has different use cases depending on data size, model type, and interpretability requirements.
