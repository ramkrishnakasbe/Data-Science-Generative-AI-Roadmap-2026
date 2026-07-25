# Extra Trees (Extremely Randomized Trees)

> **Level:** Beginner → Advanced  
> **Prerequisites:** Decision Trees, Bagging, Random Forest, Ensemble Learning Fundamentals  
> **Goal:** Understand the Extra Trees algorithm, how it differs from Random Forest, its mathematical intuition, hyperparameters, feature importance, advantages, disadvantages, and interview concepts.

---

# Table of Contents

1. Introduction
2. What are Extra Trees?
3. Why Do We Need Extra Trees?
4. Intuition Behind Extra Trees
5. Extra Trees vs Random Forest
6. Core Concepts
7. Working of Extra Trees
8. Random Split Selection
9. Mathematical Intuition
10. Classification using Extra Trees
11. Regression using Extra Trees
12. Feature Importance
13. Hyperparameters
14. Advantages
15. Disadvantages
16. Applications
17. Python Implementation
18. Hyperparameter Tuning
19. Extra Trees vs Random Forest vs Decision Tree
20. Interview Questions
21. Summary

---

# 1. Introduction

Extra Trees stands for

> **Extremely Randomized Trees**

It is an Ensemble Learning algorithm introduced by Pierre Geurts, Damien Ernst, and Louis Wehenkel in 2006.

Like Random Forest,

Extra Trees builds multiple Decision Trees and combines their predictions.

However,

Extra Trees introduces **even more randomness** during tree construction.

This often leads to

- Faster training
- Lower variance
- Better generalization

---

# 2. What are Extra Trees?

## Definition

Extra Trees is a Bagging-based ensemble algorithm where

- Multiple Decision Trees are built.
- Features are selected randomly.
- Split thresholds are selected **randomly** instead of searching for the best split.
- Predictions are combined using voting or averaging.

Unlike Random Forest,

Extra Trees generally **uses the entire training dataset by default** (`bootstrap=False` in Scikit-learn), although bootstrap sampling can optionally be enabled.

---

## Formula

```
Extra Trees

=

Decision Trees

+

Random Feature Selection

+

Random Split Selection

+

Aggregation
```

---

# 3. Why Do We Need Extra Trees?

Random Forest still searches for the **best split** among randomly selected features.

Searching for the best split increases computation.

Extra Trees avoids this expensive search.

Instead,

it chooses a random split point.

Benefits

- Faster Training
- Lower Variance
- More Diversity
- Reduced Overfitting

---

# 4. Intuition Behind Extra Trees

Imagine 100 interviewers evaluating candidates.

Random Forest

Every interviewer carefully chooses the best questions.

Extra Trees

Every interviewer selects random questions from an approved list.

Although each interviewer is less optimized individually,

the combined decision is often highly accurate because of increased diversity.

---

# 5. Extra Trees vs Random Forest

| Feature | Random Forest | Extra Trees |
|----------|---------------|-------------|
| Bootstrap Sampling | Yes (Default) | No (Default) |
| Random Features | Yes | Yes |
| Best Split Search | Yes | No |
| Random Split Threshold | No | Yes |
| Training Speed | Fast | Faster |
| Variance | Low | Lower |
| Bias | Low | Slightly Higher |
| Overfitting | Low | Lower |
| Diversity | High | Very High |

---

# 6. Core Concepts

Extra Trees combines

- Multiple Decision Trees
- Random Feature Selection
- Random Split Selection
- Aggregation

Unlike Random Forest,

there is **no exhaustive search for the optimal split** at every node.

---

# 7. Working of Extra Trees

```
Training Dataset

        │
        ▼

Random Feature Selection

        │
        ▼

Random Split Selection

        │
        ▼

Decision Tree

        │
        ▼

Repeat for Many Trees

        │
        ▼

Combine Predictions

        │
        ▼

Final Prediction
```

Each tree is built independently.

Training can therefore be parallelized.

---

# 8. Random Split Selection

This is the key idea behind Extra Trees.

Suppose

```
Selected Feature

Age
```

Possible split values

```
20

25

30

35

40
```

Random Forest

Computes impurity for every split and selects the best one.

Extra Trees

Randomly selects one split.

Example

```
Age < 30
```

without evaluating every candidate threshold.

This significantly speeds up training.

---

# 9. Mathematical Intuition

Suppose

```
N Trees
```

Each tree predicts

```
f₁(x)

f₂(x)

...

fₙ(x)
```

Regression

```
Prediction

=

(f₁ + f₂ + ... + fₙ)/N
```

Classification

```
Prediction

=

Majority Voting
```

Although each tree may be slightly weaker,

the increased diversity often improves overall performance.

---

# 10. Classification using Extra Trees

Example

| Tree | Prediction |
|------|------------|
| Tree 1 | Spam |
| Tree 2 | Spam |
| Tree 3 | Not Spam |
| Tree 4 | Spam |
| Tree 5 | Spam |

Final Prediction

```
Spam
```

---

# 11. Regression using Extra Trees

Example

| Tree | Prediction |
|------|-----------|
| Tree 1 | 82 |
| Tree 2 | 85 |
| Tree 3 | 81 |
| Tree 4 | 84 |

Average

```
83
```

becomes the final prediction.

---

# 12. Feature Importance

Extra Trees also estimates feature importance using

**Mean Decrease in Impurity (MDI)**.

Example

| Feature | Importance |
|----------|-----------|
| Age | 0.39 |
| Salary | 0.31 |
| Experience | 0.17 |
| Education | 0.08 |
| Gender | 0.05 |

Higher values indicate more influential features.

For a more reliable interpretation,

Permutation Feature Importance can also be used.

---

# 13. Hyperparameters

## n_estimators

Number of trees.

Typical values

```
100 – 1000
```

---

## criterion

Classification

- gini
- entropy
- log_loss

Regression

- squared_error
- absolute_error
- friedman_mse
- poisson

---

## max_depth

Maximum tree depth.

---

## max_features

Number of random features considered at each split.

Common values

```
sqrt

log2

None
```

---

## min_samples_split

Minimum number of samples required to split.

---

## min_samples_leaf

Minimum samples required at a leaf node.

---

## bootstrap

```
False
```

(Default)

Can optionally be set to

```
True
```

to enable bootstrap sampling.

---

## random_state

Controls reproducibility.

---

## n_jobs

```
-1
```

Uses all CPU cores.

---

# 14. Advantages

- Faster than Random Forest
- Simple to use
- Lower Variance
- Reduced Overfitting
- Handles Large Datasets
- Works for Classification and Regression
- Parallelizable
- Provides Feature Importance
- Less Sensitive to Noise

---

# 15. Disadvantages

- Slightly Higher Bias than Random Forest
- Less Interpretable
- Large Memory Usage
- Slower Prediction than a Single Tree
- Feature Importance may be biased toward continuous or high-cardinality features
- Random splits may occasionally reduce accuracy on some datasets

---

# 16. Applications

Extra Trees is commonly used for

- Fraud Detection
- Customer Churn Prediction
- Credit Scoring
- Disease Diagnosis
- Sales Forecasting
- Insurance Risk Prediction
- Manufacturing Quality Control
- Feature Selection
- Bioinformatics
- Recommendation Systems

---

# 17. Python Implementation

## Classification

```python
from sklearn.ensemble import ExtraTreesClassifier

model = ExtraTreesClassifier(
    n_estimators=200,
    random_state=42
)

model.fit(X_train, y_train)

pred = model.predict(X_test)
```

---

## Regression

```python
from sklearn.ensemble import ExtraTreesRegressor

model = ExtraTreesRegressor(
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

# 18. Hyperparameter Tuning

Example using GridSearchCV

```python
from sklearn.ensemble import ExtraTreesClassifier
from sklearn.model_selection import GridSearchCV

params = {
    "n_estimators": [100, 200, 300],
    "max_depth": [10, 20, None],
    "max_features": ["sqrt", "log2"]
}

grid = GridSearchCV(
    ExtraTreesClassifier(random_state=42),
    param_grid=params,
    cv=5,
    scoring="accuracy"
)

grid.fit(X_train, y_train)

print(grid.best_params_)
```

---

# 19. Extra Trees vs Random Forest vs Decision Tree

| Feature | Decision Tree | Random Forest | Extra Trees |
|----------|---------------|---------------|-------------|
| Number of Trees | 1 | Many | Many |
| Bootstrap Sampling | No | Yes (Default) | No (Default) |
| Random Features | No | Yes | Yes |
| Best Split Search | Yes | Yes | No |
| Random Split Threshold | No | No | Yes |
| Variance | High | Low | Lower |
| Bias | Low | Low | Slightly Higher |
| Overfitting | High | Low | Very Low |
| Training Speed | Fast | Fast | Faster |
| Generalization | Moderate | Excellent | Excellent |

---

# 20. Interview Questions

## Beginner

1. What are Extra Trees?
2. Why are they called Extremely Randomized Trees?
3. How do Extra Trees differ from Random Forest?
4. Are Extra Trees used for Classification or Regression?
5. Do Extra Trees use voting?

---

## Intermediate

1. Why are Extra Trees faster than Random Forest?
2. Why do Extra Trees introduce random split thresholds?
3. Does Extra Trees use Bootstrap Sampling?
4. How is Feature Importance calculated?
5. What are the default differences between Extra Trees and Random Forest in Scikit-learn?

---

## Advanced

1. Why can Extra Trees have slightly higher bias than Random Forest?
2. Explain how random split selection affects variance.
3. When would you choose Extra Trees over Random Forest?
4. Can bootstrap sampling be enabled in Extra Trees?
5. Compare the computational complexity of Decision Trees, Random Forest, and Extra Trees.

---

# 21. Summary

- **Extra Trees (Extremely Randomized Trees)** is a Bagging-based ensemble algorithm that builds multiple Decision Trees.
- It introduces additional randomness by selecting **random split thresholds** instead of searching for the optimal split.
- In Scikit-learn, Extra Trees **uses the full training dataset by default** (`bootstrap=False`), though bootstrap sampling can be enabled.
- Predictions are combined using **Majority Voting** (classification) or **Averaging** (regression).
- The increased randomness leads to **lower variance**, faster training, and excellent generalization, although bias may be slightly higher than Random Forest.
- Extra Trees also provides **Feature Importance**, making it useful for feature selection and model interpretation.

---

# Key Takeaways

- **Extra Trees = Decision Trees + Random Features + Random Split Thresholds**
- **Does not search for the best split at every node.**
- **Uses the full dataset by default (no bootstrap), unlike Random Forest.**
- **Classification → Majority Voting**
- **Regression → Averaging**
- **More randomness → Lower variance and faster training**
- **Typically trains faster than Random Forest**
- **Provides Feature Importance**
- **Excellent choice for large tabular datasets where training speed is important**
