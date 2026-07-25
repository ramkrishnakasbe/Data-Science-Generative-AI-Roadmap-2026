# Random Forest

> **Level:** Beginner → Advanced  
> **Prerequisites:** Decision Trees, Ensemble Learning, Bagging, Bootstrap Sampling, Bias-Variance Tradeoff  
> **Goal:** Master the Random Forest algorithm, its mathematical intuition, hyperparameters, feature importance, Out-of-Bag (OOB) score, advantages, disadvantages, and interview concepts.

---

# Table of Contents

1. Introduction
2. What is Random Forest?
3. Why Do We Need Random Forest?
4. Intuition Behind Random Forest
5. Random Forest vs Decision Tree
6. Core Concepts
7. Working of Random Forest
8. Random Feature Selection
9. Bootstrap Sampling in Random Forest
10. Mathematical Intuition
11. Classification using Random Forest
12. Regression using Random Forest
13. Out-of-Bag (OOB) Score
14. Feature Importance
15. Hyperparameters
16. Advantages
17. Disadvantages
18. Applications
19. Python Implementation
20. Hyperparameter Tuning
21. Interview Questions
22. Summary

---

# 1. Introduction

Random Forest is one of the most popular Machine Learning algorithms used for both **Classification** and **Regression** problems.

It belongs to the **Bagging (Bootstrap Aggregating)** family of Ensemble Learning algorithms.

Instead of building a single Decision Tree,

Random Forest builds **many Decision Trees** and combines their predictions.

---

# 2. What is Random Forest?

## Definition

Random Forest is an ensemble algorithm that creates multiple Decision Trees using:

- Bootstrap Sampling
- Random Feature Selection

and combines their predictions using

- Majority Voting (Classification)
- Average Prediction (Regression)

---

## Formula

```
Random Forest

=

Bootstrap Sampling

+

Decision Trees

+

Random Feature Selection

+

Aggregation
```

---

# 3. Why Do We Need Random Forest?

Decision Trees suffer from

- High Variance
- Overfitting
- Instability

Small changes in data may create a completely different tree.

Random Forest solves this problem by averaging predictions from many trees.

Result:

- Lower Variance
- Better Accuracy
- Better Generalization

---

# 4. Intuition Behind Random Forest

Imagine asking only one doctor to diagnose a patient.

The diagnosis may be incorrect.

Instead,

ask 100 experienced doctors.

Each doctor gives an opinion.

Final diagnosis is based on majority opinion.

```
Doctor 1

Doctor 2

Doctor 3

...

Doctor 100

↓

Majority Decision

↓

Better Diagnosis
```

Random Forest follows exactly the same idea.

---

# 5. Random Forest vs Decision Tree

| Feature | Decision Tree | Random Forest |
|----------|---------------|---------------|
| Trees | 1 | Many |
| Variance | High | Low |
| Bias | Low | Low |
| Accuracy | Moderate | High |
| Overfitting | High | Low |
| Stability | Low | High |
| Feature Selection | All Features | Random Features |
| Parallel Training | No | Yes |

---

# 6. Core Concepts

Random Forest is built using four important concepts.

## 1. Bootstrap Sampling

Creates different datasets.

---

## 2. Decision Trees

Each bootstrap sample trains one Decision Tree.

---

## 3. Random Feature Selection

At every split,

only a random subset of features is considered.

---

## 4. Aggregation

Combine predictions from all trees.

---

# 7. Working of Random Forest

```
Original Dataset

        │
        ▼

Bootstrap Sampling

        │
        ▼

Dataset 1 → Tree 1

Dataset 2 → Tree 2

Dataset 3 → Tree 3

Dataset 4 → Tree 4

...

Dataset N → Tree N

        │
        ▼

Combine Predictions

        │
        ▼

Final Prediction
```

Every tree is trained independently.

Therefore,

Random Forest supports parallel computation.

---

# 8. Random Feature Selection

This is the biggest difference between Bagging and Random Forest.

Suppose the dataset has

```
10 Features
```

Instead of considering all 10 features,

Random Forest randomly selects a subset.

Example

```
Feature Set

A B C D E F G H I J

↓

Random Selection

B D F I
```

The best split is chosen only from these selected features.

---

## Why Random Feature Selection?

Without random feature selection,

every Decision Tree becomes very similar.

Random feature selection creates diversity among trees.

Greater Diversity

↓

Lower Correlation

↓

Better Ensemble

---

## Common Values

Classification

```
sqrt(Number of Features)
```

Regression

```
Number of Features / 3
```

Scikit-learn automatically selects suitable defaults.

---

# 9. Bootstrap Sampling in Random Forest

Every tree receives a different bootstrap dataset.

Example

Original Dataset

```
A
B
C
D
E
```

Tree 1

```
A
B
B
D
E
```

Tree 2

```
A
A
C
D
D
```

Tree 3

```
C
D
E
A
E
```

Different datasets

↓

Different trees

↓

Different predictions

↓

Better accuracy

---

# 10. Mathematical Intuition

Suppose we have

```
N Decision Trees
```

For Classification

```
Final Prediction

=

Majority Vote
```

For Regression

```
Final Prediction

=

Average Prediction
```

If

```
Tree1 = 120

Tree2 = 125

Tree3 = 118

Tree4 = 121
```

Prediction

```
(120 + 125 +118 +121)/4

=

121
```

Averaging reduces variance significantly.

---

# 11. Classification using Random Forest

Every tree predicts a class.

Example

| Tree | Prediction |
|------|------------|
| Tree 1 | Cat |
| Tree 2 | Dog |
| Tree 3 | Dog |
| Tree 4 | Dog |
| Tree 5 | Cat |

Majority Vote

```
Dog
```

becomes the final prediction.

---

# 12. Regression using Random Forest

Each tree predicts a numeric value.

Example

| Tree | Prediction |
|------|-----------|
| Tree 1 | 510 |
| Tree 2 | 500 |
| Tree 3 | 505 |
| Tree 4 | 495 |

Average

```
502.5
```

becomes the final prediction.

---

# 13. Out-of-Bag (OOB) Score

Every bootstrap sample leaves approximately

```
36.8%
```

of observations unused.

These are called

```
Out-of-Bag Samples
```

These samples can be used for validation.

Advantages

- No separate validation dataset
- Faster evaluation
- Better use of available data

Enable in Scikit-learn

```python
RandomForestClassifier(
    oob_score=True
)
```

---

# 14. Feature Importance

Random Forest can estimate which features contribute the most to predictions.

Scikit-learn provides

```python
model.feature_importances_
```

---

## How is Feature Importance Calculated?

Feature importance is commonly computed using **Mean Decrease in Impurity (MDI)**.

A feature receives a higher importance score if it consistently reduces impurity (such as Gini Impurity or Entropy) across many trees.

The scores are normalized so that their sum equals **1**.

---

## Example

| Feature | Importance |
|----------|-----------|
| Age | 0.42 |
| Salary | 0.28 |
| Experience | 0.18 |
| City | 0.07 |
| Gender | 0.05 |

Interpretation

Age contributes the most to model predictions.

---

## Limitation

MDI feature importance can be biased toward:

- Continuous variables
- Features with many unique values

An alternative is **Permutation Feature Importance**, which measures how model performance changes when a feature is randomly shuffled.

---

# 15. Hyperparameters

## n_estimators

Number of trees.

Typical Range

```
100 – 1000
```

---

## max_depth

Maximum tree depth.

Higher depth

↓

More complex trees

↓

Higher risk of overfitting

---

## max_features

Number of randomly selected features considered at each split.

Options

```
sqrt

log2

None

Integer

Float
```

---

## min_samples_split

Minimum samples required to split a node.

---

## min_samples_leaf

Minimum samples required at a leaf node.

---

## criterion

Classification

- gini
- entropy
- log_loss (supported in newer versions of Scikit-learn)

Regression

- squared_error
- absolute_error
- friedman_mse
- poisson

---

## bootstrap

```
True
```

Use Bootstrap Sampling.

```
False
```

Use the complete dataset for each tree.

---

## oob_score

Calculates Out-of-Bag score.

---

## random_state

Ensures reproducible results.

---

## n_jobs

```
-1
```

Uses all CPU cores.

---

# 16. Advantages

- High Accuracy
- Reduces Overfitting
- Reduces Variance
- Handles Missing Values reasonably well (after appropriate preprocessing if required)
- Handles Large Datasets
- Works for Classification and Regression
- Provides Feature Importance
- Parallelizable
- Robust to Noise
- Less Hyperparameter Sensitive than a single Decision Tree

---

# 17. Disadvantages

- Computationally Expensive
- Large Memory Requirement
- Less Interpretable
- Slower Prediction
- Large Model Size
- Feature Importance may be biased toward high-cardinality features
- Not ideal for very high-dimensional sparse data (e.g., some text applications)

---

# 18. Applications

Random Forest is widely used in

- Fraud Detection
- Credit Risk Prediction
- Disease Diagnosis
- Customer Churn Prediction
- Recommendation Systems
- Stock Market Analysis
- Sales Forecasting
- Image Classification
- Spam Detection
- Insurance Risk Analysis

---

# 19. Python Implementation

## Classification

```python
from sklearn.ensemble import RandomForestClassifier

model = RandomForestClassifier(
    n_estimators=200,
    random_state=42
)

model.fit(X_train, y_train)

pred = model.predict(X_test)
```

---

## Regression

```python
from sklearn.ensemble import RandomForestRegressor

model = RandomForestRegressor(
    n_estimators=200,
    random_state=42
)

model.fit(X_train, y_train)

pred = model.predict(X_test)
```

---

## Feature Importance

```python
import pandas as pd

importance = pd.DataFrame({
    "Feature": X.columns,
    "Importance": model.feature_importances_
})

importance.sort_values(
    by="Importance",
    ascending=False,
    inplace=True
)
```

---

# 20. Hyperparameter Tuning

Common parameters to tune:

- n_estimators
- max_depth
- max_features
- min_samples_split
- min_samples_leaf
- bootstrap

Example using GridSearchCV

```python
from sklearn.model_selection import GridSearchCV
from sklearn.ensemble import RandomForestClassifier

params = {
    "n_estimators": [100, 200, 300],
    "max_depth": [5, 10, None],
    "max_features": ["sqrt", "log2"]
}

grid = GridSearchCV(
    RandomForestClassifier(random_state=42),
    param_grid=params,
    cv=5,
    scoring="accuracy"
)

grid.fit(X_train, y_train)

print(grid.best_params_)
```

---

# 21. Interview Questions

## Beginner

1. What is Random Forest?
2. Why is it called a Random Forest?
3. What problem does Random Forest solve?
4. What is Bootstrap Sampling?
5. How are predictions combined?

---

## Intermediate

1. Difference between Bagging and Random Forest?
2. Why is Random Feature Selection important?
3. What is OOB Score?
4. Why does Random Forest reduce overfitting?
5. How is Feature Importance calculated?

---

## Advanced

1. Why does Random Forest have low variance?
2. Why is Random Forest more stable than a Decision Tree?
3. Explain Mean Decrease in Impurity (MDI).
4. When should you use Permutation Feature Importance instead of MDI?
5. How do `max_features` and `n_estimators` influence bias and variance?
6. Why can Random Forest struggle with extrapolation in regression tasks?
7. Can Random Forest be used for feature selection? Explain the advantages and limitations.

---

# 22. Summary

- **Random Forest** is a Bagging-based ensemble algorithm that combines many Decision Trees.
- It uses **Bootstrap Sampling** to create diverse training datasets and **Random Feature Selection** to reduce correlation between trees.
- Predictions are combined using **Majority Voting** (classification) or **Averaging** (regression).
- It significantly **reduces variance** and improves generalization compared to a single Decision Tree.
- Random Forest supports **Out-of-Bag (OOB) validation**, reducing the need for a separate validation dataset.
- It also provides **Feature Importance**, making it useful for feature selection and model interpretation.
- Due to its strong performance, robustness, and ease of use, Random Forest is one of the most widely used algorithms for structured/tabular data.

---

# Key Takeaways

- **Random Forest = Bagging + Random Feature Selection**
- **Builds many independent Decision Trees.**
- **Uses Bootstrap Sampling (with replacement).**
- **Classification → Majority Voting**
- **Regression → Averaging**
- **Primary objective: Reduce Variance and Improve Generalization**
- **Random Feature Selection reduces correlation among trees.**
- **Supports Out-of-Bag (OOB) validation.**
- **Provides Feature Importance for model interpretation.**
- **One of the best baseline algorithms for tabular machine learning problems.**
