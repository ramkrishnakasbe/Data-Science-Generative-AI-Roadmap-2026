# Stacking (Stacked Generalization)

> **Level:** Beginner → Advanced  
> **Prerequisites:** Decision Trees, Ensemble Learning, Bagging, Boosting, Cross Validation  
> **Goal:** Understand how Stacking combines multiple machine learning models using a Meta Learner to improve predictive performance.

---

# Table of Contents

1. Introduction
2. What is Stacking?
3. Why Do We Need Stacking?
4. Architecture
5. Base Learners
6. Meta Learner
7. Cross Validation in Stacking
8. Working of Stacking
9. Classification Example
10. Regression Example
11. Advantages
12. Disadvantages
13. Python Implementation
14. Stacking vs Bagging vs Boosting
15. Interview Questions
16. Summary

---

# 1. Introduction

Stacking, also known as **Stacked Generalization**, is an Ensemble Learning technique that combines the predictions of multiple Machine Learning models using another model called the **Meta Learner**.

Unlike Bagging and Boosting,

Stacking allows completely different algorithms to work together.

For example,

- Random Forest
- XGBoost
- Support Vector Machine
- Logistic Regression

can all be combined into one powerful model.

---

# 2. What is Stacking?

## Definition

Stacking is an ensemble technique where

- Multiple models are trained independently.
- Their predictions become inputs for another model.
- The final prediction is produced by the Meta Learner.

---

## Formula

```
Training Data

↓

Base Learners

↓

Predictions

↓

Meta Learner

↓

Final Prediction
```

---

# 3. Why Do We Need Stacking?

Every Machine Learning algorithm has strengths and weaknesses.

Example

Random Forest

- Good with nonlinear data

Support Vector Machine

- Good with high-dimensional data

XGBoost

- Excellent for structured data

Instead of choosing only one,

Stacking combines all of them.

Result

- Better Accuracy
- Better Generalization
- Reduced Model Bias

---

# 4. Architecture

A typical stacking architecture has two levels.

```
                 Training Data
                      │
      ┌───────────────┼───────────────┐
      │               │               │
      ▼               ▼               ▼
 Random Forest      XGBoost         SVM
      │               │               │
      └─────── Predictions ───────────┘
                      │
                      ▼
             Meta Learner
        (Logistic Regression)
                      │
                      ▼
             Final Prediction
```

The first level contains **Base Learners**.

The second level contains the **Meta Learner**.

---

# 5. Base Learners

Base Learners are the first-level models.

They learn directly from the original training data.

Examples

- Decision Tree
- Random Forest
- Extra Trees
- XGBoost
- LightGBM
- CatBoost
- SVM
- KNN
- Logistic Regression
- Neural Network

Each model makes independent predictions.

These predictions become new features.

Example

| Sample | RF | XGB | SVM |
|----------|----|-----|-----|
| 1 | Yes | Yes | No |
| 2 | No | No | No |
| 3 | Yes | Yes | Yes |

These outputs are passed to the Meta Learner.

---

# 6. Meta Learner

The Meta Learner is the second-level model.

Its job is to learn

> **Which Base Learner should be trusted more for different observations?**

Common Meta Learners

- Logistic Regression
- Linear Regression
- Random Forest
- XGBoost
- LightGBM

Example

Input to Meta Learner

| RF | XGB | SVM |
|----|-----|-----|
| Yes | Yes | No |
| No | No | No |
| Yes | Yes | Yes |

Output

```
Final Prediction
```

The Meta Learner discovers relationships among the predictions of the Base Learners.

---

# 7. Cross Validation in Stacking

Cross Validation is one of the most important components of Stacking.

Without Cross Validation,

the Meta Learner may simply memorize predictions and overfit.

The standard approach is **K-Fold Cross Validation**.

Example (5-Fold)

```
Dataset

↓

Fold 1

Fold 2

Fold 3

Fold 4

Fold 5
```

For each fold

- Train Base Learners on 4 folds.
- Predict on the remaining fold.
- Store Out-of-Fold (OOF) predictions.

After all folds,

combine all OOF predictions.

These become the training data for the Meta Learner.

```
Original Data

↓

Base Learners

↓

Out-of-Fold Predictions

↓

Meta Learner

↓

Final Model
```

### Why Out-of-Fold Predictions?

Using predictions on the same data used for training causes **data leakage**.

OOF predictions simulate unseen data and help the Meta Learner generalize better.

---

# 8. Working of Stacking

```
Training Dataset

↓

Train Base Models

↓

Generate OOF Predictions

↓

Create New Dataset

↓

Train Meta Learner

↓

Final Model

↓

Prediction on New Data
```

Prediction Phase

```
New Data

↓

Base Learners

↓

Predictions

↓

Meta Learner

↓

Final Prediction
```

---

# 9. Classification Example

Suppose three models predict

| Model | Prediction |
|--------|------------|
| Random Forest | Cat |
| XGBoost | Dog |
| SVM | Dog |

The Meta Learner receives

```
Cat

Dog

Dog
```

It predicts

```
Dog
```

---

# 10. Regression Example

Three models predict house price

| Model | Prediction |
|--------|-----------|
| Random Forest | 48 |
| XGBoost | 50 |
| Linear Regression | 47 |

Meta Learner predicts

```
49
```

instead of simply averaging the predictions.

---

# 11. Advantages

- High Prediction Accuracy
- Combines strengths of different algorithms
- Reduces Bias
- Better Generalization
- Flexible architecture
- Works for Classification and Regression
- Can outperform individual models

---

# 12. Disadvantages

- Computationally expensive
- Slower training
- More difficult to interpret
- Requires careful Cross Validation
- Higher memory usage
- More complex to deploy than a single model

---

# 13. Python Implementation

## Classification

```python
from sklearn.ensemble import StackingClassifier
from sklearn.ensemble import RandomForestClassifier
from sklearn.svm import SVC
from sklearn.linear_model import LogisticRegression
from xgboost import XGBClassifier

base_models = [
    ("rf", RandomForestClassifier(random_state=42)),
    ("xgb", XGBClassifier(random_state=42)),
    ("svm", SVC(probability=True))
]

model = StackingClassifier(
    estimators=base_models,
    final_estimator=LogisticRegression(),
    cv=5
)

model.fit(X_train, y_train)

pred = model.predict(X_test)
```

---

## Regression

```python
from sklearn.ensemble import StackingRegressor
from sklearn.ensemble import RandomForestRegressor
from sklearn.linear_model import LinearRegression
from xgboost import XGBRegressor

base_models = [
    ("rf", RandomForestRegressor(random_state=42)),
    ("xgb", XGBRegressor(random_state=42))
]

model = StackingRegressor(
    estimators=base_models,
    final_estimator=LinearRegression(),
    cv=5
)

model.fit(X_train, y_train)

pred = model.predict(X_test)
```

---

# 14. Stacking vs Bagging vs Boosting

| Feature | Bagging | Boosting | Stacking |
|----------|----------|----------|-----------|
| Training | Parallel | Sequential | Parallel |
| Model Type | Usually Same | Usually Same | Different Models |
| Main Goal | Reduce Variance | Reduce Bias | Improve Overall Performance |
| Final Prediction | Voting/Average | Weighted Combination | Meta Learner |
| Diversity | Moderate | Low | High |
| Complexity | Low | Medium | High |

---

# 15. Interview Questions

## Beginner

1. What is Stacking?
2. What is a Meta Learner?
3. What are Base Learners?
4. Can different algorithms be used in Stacking?
5. Is Stacking used for Classification and Regression?

---

## Intermediate

1. Why is Cross Validation important in Stacking?
2. What are Out-of-Fold (OOF) predictions?
3. Why is Logistic Regression commonly used as a Meta Learner?
4. Difference between Voting and Stacking?
5. Difference between Bagging and Stacking?

---

## Advanced

1. Explain the complete architecture of Stacking.
2. Why are OOF predictions preferred over training predictions?
3. Can XGBoost be used as a Meta Learner?
4. What is data leakage in Stacking?
5. When would you choose Stacking over Boosting?

---

# 16. Summary

- **Stacking (Stacked Generalization)** is an ensemble technique that combines predictions from multiple Base Learners using a **Meta Learner**.
- Base Learners can be different algorithms, making Stacking highly flexible.
- **Out-of-Fold (OOF) predictions** generated through Cross Validation are used to train the Meta Learner and avoid data leakage.
- The Meta Learner learns how to best combine the strengths of individual models.
- Stacking often achieves higher predictive performance than any single model but comes with increased computational complexity.

---

# Key Takeaways

- **Stacking = Base Learners + Meta Learner**
- **Supports heterogeneous models (different algorithms).**
- **Uses Out-of-Fold (OOF) predictions for training the Meta Learner.**
- **Cross Validation is essential to prevent data leakage.**
- **Works for both Classification and Regression.**
- **Generally provides better performance than individual models when properly designed.**
- **Frequently used in Kaggle competitions and production ML systems for maximizing predictive accuracy.**
