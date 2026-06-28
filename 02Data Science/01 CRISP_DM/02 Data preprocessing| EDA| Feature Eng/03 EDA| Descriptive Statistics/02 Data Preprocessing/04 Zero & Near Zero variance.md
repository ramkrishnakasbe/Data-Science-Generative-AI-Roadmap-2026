# 04. Zero and Near Zero Variance

# Overview

Zero Variance and Near Zero Variance are feature selection techniques used to identify variables that contain little or no useful information. Such features contribute very little to model learning and are usually removed before training machine learning models.

---

# Why Remove Zero and Near Zero Variance Features?

Features with very low variation:

* Do not help distinguish between observations.
* Add unnecessary complexity to the dataset.
* Increase computational time.
* May negatively affect certain machine learning algorithms.
* Increase memory usage without adding predictive value.

Removing these features helps build simpler and more efficient models.

---

# What is Variance?

Variance measures how much the values of a feature vary from their mean.

* **High Variance:** Values are spread out.
* **Low Variance:** Values are similar.
* **Zero Variance:** All values are identical.

---

# 1. Zero Variance

## Definition

A **Zero Variance** feature is a feature where **all observations have exactly the same value**.

Since there is no variation, the feature provides **no information** for prediction.

---

## Example

| Country |
| ------- |
| India   |
| India   |
| India   |
| India   |
| India   |

Every record has the same value (**India**), so this feature has **zero variance**.

Other examples:

| Feature | Values                 |
| ------- | ---------------------- |
| Gender  | Male, Male, Male, Male |
| Status  | Active, Active, Active |
| Marks   | 100, 100, 100          |

---

## Characteristics

* Only one unique value.
* Variance equals **0**.
* Does not help separate different classes.
* Usually removed before model training.

---

# Detecting Zero Variance

### Using Pandas

Count unique values:

```python
df["Country"].nunique()
```

If the result is:

```text
1
```

then the feature has **Zero Variance**.

---

Check all columns:

```python
df.nunique()
```

---

# Removing Zero Variance Features

```python
df = df.loc[:, df.nunique() > 1]
```

This keeps only columns having more than one unique value.

---

# 2. Near Zero Variance

## Definition

A **Near Zero Variance** feature has **very little variation**.

Most observations contain the same value, while only a few observations contain different values.

Although not completely constant, these features contribute very little information.

---

## Example

| Country |
| ------- |
| India   |
| India   |
| India   |
| India   |
| India   |
| India   |
| India   |
| USA     |

Here,

* India = 7 observations
* USA = 1 observation

The feature has **Near Zero Variance** because almost every value is the same.

---

## Another Example

| Purchased |
| --------- |
| Yes       |
| Yes       |
| Yes       |
| Yes       |
| Yes       |
| Yes       |
| No        |

Since almost every observation belongs to one category, this feature has very low variance.

---

# Characteristics

* Majority of observations are identical.
* Very few unique values.
* Highly imbalanced distribution.
* Provides little predictive information.

---

# How to Detect Near Zero Variance?

Common indicators include:

* Frequency Ratio
* Percentage of Unique Values
* Variance Threshold
* Domain Knowledge

---

## Frequency Ratio

Frequency Ratio compares the count of the most frequent value with the second most frequent value.

### Formula

```text
Frequency Ratio =
Most Frequent Value Count
-------------------------
Second Most Frequent Value Count
```

Higher ratios indicate a greater likelihood of a Near Zero Variance feature.

---

## Percentage of Unique Values

```text
Unique Percentage =
(Number of Unique Values / Total Observations) × 100
```

Very low percentages suggest Near Zero Variance.

---

# Variance Threshold Method

A feature is removed if its variance is below a specified threshold.

For example,

```text
Threshold = 0
```

removes only Zero Variance features.

A threshold greater than zero can remove both Zero and Near Zero Variance features.

---

# Using Scikit-learn

```python
from sklearn.feature_selection import VarianceThreshold

selector = VarianceThreshold(threshold=0)

X_new = selector.fit_transform(X)
```

---

Remove features with variance less than **0.01**:

```python
selector = VarianceThreshold(threshold=0.01)

X_new = selector.fit_transform(X)
```

---

# Using Pandas

Calculate variance for numerical columns:

```python
df.var(numeric_only=True)
```

Identify low variance columns:

```python
df.var(numeric_only=True) < 0.01
```

---

# When Should These Features Be Removed?

Remove them when:

* Building Machine Learning models.
* Performing Feature Selection.
* Improving training speed.
* Reducing unnecessary dimensions.

---

# When Should They Be Retained?

Keep them when:

* They have business importance.
* They act as identifiers.
* The feature is required for reporting or auditing.
* Domain experts consider them valuable.

---

# Advantages

* Reduces dataset size.
* Improves model efficiency.
* Reduces computation time.
* Removes uninformative features.
* Simplifies feature selection.

---

# Disadvantages

* Useful business information may be removed.
* Threshold selection is subjective.
* Some algorithms are less affected by low variance features.

---

# Real-World Example

Suppose a customer dataset contains the following feature:

| Country |
| ------- |
| India   |
| India   |
| India   |
| India   |
| India   |
| India   |

Since every customer belongs to **India**, the feature has **Zero Variance** and provides no information for predicting customer behavior.

Another feature:

| Membership |
| ---------- |
| Gold       |
| Gold       |
| Gold       |
| Gold       |
| Gold       |
| Silver     |

This feature has **Near Zero Variance** because almost every customer belongs to the **Gold** category. Depending on the business problem, it may be removed if it contributes little to the model.

---

# Zero Variance vs Near Zero Variance

| Feature         | Zero Variance       | Near Zero Variance       |
| --------------- | ------------------- | ------------------------ |
| Variation       | No variation        | Very little variation    |
| Unique Values   | One                 | Few                      |
| Information     | None                | Very Low                 |
| Usually Removed | Yes                 | Usually Yes              |
| Example         | India, India, India | India, India, India, USA |

---

# Summary

Zero Variance features contain **only one unique value**, while Near Zero Variance features contain **very little variation**, with most observations having the same value. These features generally add little or no predictive power and are often removed during data preprocessing to improve model performance, reduce computational cost, and simplify the dataset. Common techniques for identifying them include checking unique values, calculating variance, using frequency ratios, and applying Scikit-learn's `VarianceThreshold`.
