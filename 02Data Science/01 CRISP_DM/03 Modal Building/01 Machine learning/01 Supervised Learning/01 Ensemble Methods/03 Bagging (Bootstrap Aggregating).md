# Bagging (Bootstrap Aggregating)

> **Level:** Beginner → Intermediate  
> **Prerequisites:** Decision Trees, Bias-Variance Tradeoff, Ensemble Learning Fundamentals  
> **Goal:** Understand the Bagging algorithm, Bootstrap Sampling, Out-of-Bag (OOB) Error, mathematical intuition, implementation, advantages, disadvantages, and interview concepts.

---

# Table of Contents

1. Introduction
2. What is Bagging?
3. Why Do We Need Bagging?
4. Bootstrap Sampling
5. Aggregation
6. Working of Bagging
7. Mathematical Intuition
8. Bagging Algorithm
9. Bagging for Classification
10. Bagging for Regression
11. Out-of-Bag (OOB) Samples
12. OOB Error
13. Hyperparameters
14. Advantages
15. Disadvantages
16. Applications
17. Python Implementation
18. Scikit-learn Implementation
19. Comparison with Single Decision Tree
20. Bagging vs Pasting
21. Bagging vs Boosting
22. Common Interview Questions
23. Summary

---

# 1. Introduction

Bagging stands for

> **Bootstrap Aggregating**

It is one of the earliest and most popular Ensemble Learning techniques.

Bagging combines multiple models trained independently on different subsets of data and combines their predictions.

The main objective is to

- Reduce Variance
- Improve Stability
- Improve Generalization
- Reduce Overfitting

---

# 2. What is Bagging?

## Definition

Bagging is an ensemble technique where

- Multiple datasets are created using **Bootstrap Sampling**.
- A separate model is trained on each dataset.
- Predictions from all models are combined.

Instead of relying on one model,

```
One Decision Tree

↓

Prediction
```

Bagging uses

```
Tree 1
Tree 2
Tree 3
...
Tree N

↓

Combine Predictions

↓

Final Prediction
```

---

# 3. Why Do We Need Bagging?

Decision Trees have

- Low Bias
- High Variance

Small changes in training data may produce a completely different tree.

Example

Dataset A

↓

Decision Tree A

Dataset B

↓

Decision Tree B

Predictions may differ significantly.

Bagging reduces this instability by averaging predictions from many trees.

---

# 4. Bootstrap Sampling

Bootstrap Sampling is the heart of Bagging.

## Definition

Bootstrap Sampling means

> Randomly selecting observations **with replacement** from the original dataset.

---

Suppose we have

```
Dataset

A
B
C
D
E
```

One bootstrap sample may be

```
A
B
B
D
E
```

Another sample

```
C
C
A
D
E
```

Notice

- Some observations appear multiple times.
- Some observations are missing.

This is perfectly normal.

---

## Why Sampling With Replacement?

Sampling with replacement creates different training datasets.

Different datasets

↓

Different models

↓

Different errors

↓

Better Ensemble

---

# 5. Aggregation

Aggregation means combining predictions.

### Classification

Use

- Majority Voting

Example

| Tree | Prediction |
|------|------------|
| Tree 1 | Yes |
| Tree 2 | No |
| Tree 3 | Yes |
| Tree 4 | Yes |
| Tree 5 | No |

Final Prediction

```
Yes
```

---

### Regression

Use

Average Prediction

Example

| Tree | Prediction |
|------|-----------|
| Tree 1 | 120 |
| Tree 2 | 130 |
| Tree 3 | 110 |
| Tree 4 | 125 |

Average

```
121.25
```

---

# 6. Working of Bagging

```
Original Dataset

        │
        ▼

Bootstrap Sampling

        │
        ▼

Dataset 1
Dataset 2
Dataset 3
Dataset 4
Dataset 5

        │
        ▼

Train Independent Models

Tree1
Tree2
Tree3
Tree4
Tree5

        │
        ▼

Combine Predictions

        │
        ▼

Final Prediction
```

Every model is trained independently.

This allows Bagging to be parallelized.

---

# 7. Mathematical Intuition

Suppose

```
f₁(x)
f₂(x)
f₃(x)
...
fₙ(x)
```

are predictions from different models.

For Regression

```
Final Prediction

= (f₁ + f₂ + ... + fₙ)/n
```

For Classification

```
Final Prediction

=

Majority Vote
```

The averaging process reduces prediction variance.

---

# 8. Bagging Algorithm

Step 1

Take original dataset.

↓

Step 2

Generate multiple bootstrap samples.

↓

Step 3

Train one model on each sample.

↓

Step 4

Predict using every model.

↓

Step 5

Aggregate predictions.

↓

Final Prediction.

---

# 9. Bagging for Classification

Prediction is based on majority voting.

Example

```
Tree1 → Cat

Tree2 → Dog

Tree3 → Dog

Tree4 → Dog

Tree5 → Cat
```

Majority

```
Dog
```

---

# 10. Bagging for Regression

Prediction is obtained using averaging.

Example

```
Tree1 → 500

Tree2 → 510

Tree3 → 490

Tree4 → 505
```

Average

```
501.25
```

---

# 11. Out-of-Bag (OOB) Samples

Not every observation appears in a bootstrap sample.

Those observations that are **not selected** are called

> **Out-of-Bag Samples**

Example

Original Dataset

```
A
B
C
D
E
```

Bootstrap Sample

```
A
B
B
D
E
```

Observation

```
C
```

was never selected.

Therefore

```
C

↓

Out-of-Bag Sample
```

---

# 12. OOB Error

Instead of using a separate validation set,

Bagging can evaluate performance using OOB samples.

Process

```
Observation not selected

↓

Test model on that observation

↓

Repeat for all trees

↓

Average Error

↓

OOB Error
```

Benefits

- No separate validation dataset needed
- Efficient use of training data
- Faster evaluation

---

## Why Approximately 36.8% OOB?

For a dataset with **N** samples, each bootstrap sample selects **N** observations **with replacement**.

The probability that a specific observation is **not selected** in one draw is:

```
1 - 1/N
```

The probability it is never selected after **N** draws is:

```
(1 - 1/N)^N
```

As **N** becomes large,

```
(1 - 1/N)^N ≈ e^-1 ≈ 0.368
```

Therefore,

- Approximately **63.2%** of unique observations appear in a bootstrap sample.
- Approximately **36.8%** remain Out-of-Bag.

---

# 13. Hyperparameters

Important parameters

### n_estimators

Number of models.

Higher value

- Better stability
- Longer training

---

### max_samples

Number of samples used for each bootstrap dataset.

---

### bootstrap

```
True
```

Sampling with replacement.

```
False
```

Sampling without replacement.

---

### max_features

Number of features used for training each estimator.

---

### random_state

Ensures reproducible results.

---

### n_jobs

Controls parallel execution.

```
-1
```

Uses all CPU cores.

---

# 14. Advantages

- Reduces Variance
- Reduces Overfitting
- Improves Accuracy
- Stable Predictions
- Easy to Parallelize
- Handles Noisy Data Well
- Simple Implementation
- Supports Classification and Regression
- Works well with high-variance models

---

# 15. Disadvantages

- Does not significantly reduce Bias
- Higher Memory Usage
- Slower Prediction
- Less Interpretable
- Requires Multiple Models
- Computationally Expensive for Large Ensembles

---

# 16. Applications

Bagging is widely used in

- Fraud Detection
- Medical Diagnosis
- Credit Scoring
- Customer Churn Prediction
- Loan Approval
- Disease Prediction
- Stock Market Prediction
- Sales Forecasting
- Image Classification

---

# 17. Python Implementation

```python
from sklearn.ensemble import BaggingClassifier
from sklearn.tree import DecisionTreeClassifier

model = BaggingClassifier(
    estimator=DecisionTreeClassifier(),
    n_estimators=100,
    bootstrap=True,
    random_state=42
)

model.fit(X_train, y_train)

pred = model.predict(X_test)
```

---

# 18. Scikit-learn Parameters

```python
BaggingClassifier(
    estimator=None,
    n_estimators=10,
    max_samples=1.0,
    max_features=1.0,
    bootstrap=True,
    bootstrap_features=False,
    oob_score=False,
    warm_start=False,
    n_jobs=None,
    random_state=None
)
```

---

# 19. Comparison with Single Decision Tree

| Feature | Decision Tree | Bagging |
|----------|--------------|----------|
| Models | One | Multiple |
| Variance | High | Low |
| Bias | Low | Low |
| Overfitting | High | Lower |
| Stability | Low | High |
| Accuracy | Moderate | Better |
| Parallel Training | No | Yes |

---

# 20. Bagging vs Pasting

| Feature | Bagging | Pasting |
|----------|----------|----------|
| Sampling | With Replacement | Without Replacement |
| Duplicate Samples | Yes | No |
| Bootstrap | Yes | No |
| Diversity | Higher | Lower |
| Popularity | High | Low |

---

# 21. Bagging vs Boosting

| Feature | Bagging | Boosting |
|----------|----------|-----------|
| Training | Parallel | Sequential |
| Main Goal | Reduce Variance | Reduce Bias |
| Sampling | Bootstrap | Reweighted Samples |
| Overfitting | Lower Risk | Higher Risk |
| Speed | Faster (Parallelizable) | Slower |
| Example | Random Forest | XGBoost |

---

# 22. Common Interview Questions

## Beginner

1. What is Bagging?
2. Why is it called Bootstrap Aggregating?
3. What is Bootstrap Sampling?
4. What is Majority Voting?
5. What is Averaging in Regression?

---

## Intermediate

1. Why does Bagging reduce variance?
2. Why are Decision Trees commonly used with Bagging?
3. What is OOB Error?
4. Why is Bagging parallelizable?
5. Difference between Bagging and Random Forest?

---

## Advanced

1. Why does Bagging not reduce Bias significantly?
2. Explain mathematically why OOB samples are approximately 36.8%.
3. How does Bagging improve generalization?
4. Can Bagging be used with algorithms other than Decision Trees?
5. When should you prefer Bagging over Boosting?

---

# 23. Summary

- **Bagging (Bootstrap Aggregating)** is an ensemble method that trains multiple models independently on different bootstrap samples.
- It primarily **reduces variance**, making predictions more stable and less prone to overfitting.
- **Bootstrap Sampling** creates diverse datasets by sampling **with replacement**.
- Predictions are combined using **majority voting** (classification) or **averaging** (regression).
- **Out-of-Bag (OOB) samples** provide an efficient way to estimate model performance without requiring a separate validation set.
- Bagging works especially well with **high-variance models** such as Decision Trees.
- **Random Forest** is the most widely used real-world implementation of the Bagging concept.

---

# Key Takeaways

- **Bagging = Bootstrap Sampling + Aggregation**
- **Sampling is done with replacement.**
- **Classification → Majority Voting**
- **Regression → Averaging**
- **Primary objective: Reduce Variance**
- **Decision Trees are the most common base learners.**
- **Approximately 36.8% of observations remain Out-of-Bag (OOB).**
- **Random Forest is an advanced Bagging algorithm with random feature selection.**
