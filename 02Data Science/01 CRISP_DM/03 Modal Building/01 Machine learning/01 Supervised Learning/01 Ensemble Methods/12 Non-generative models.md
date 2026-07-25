# Non-Generative Ensemble Models (Voting & Stacking)

> **Level:** Beginner → Advanced  
> **Prerequisites:** Ensemble Learning, Classification, Regression, Probability  
> **Goal:** Understand Voting and Stacking Ensemble techniques including Hard Voting, Soft Voting, Simple Average, and Weighted Average.

---

# Table of Contents

1. Introduction
2. What are Non-Generative Ensemble Models?
3. Why Ensemble Multiple Models?
4. Voting Ensemble
5. Hard Voting
6. Soft Voting
7. Simple Average
8. Weighted Average
9. Stacking Ensemble
10. Voting vs Stacking
11. Advantages
12. Disadvantages
13. Python Implementation
14. Interview Questions
15. Summary

---

# 1. Introduction

Ensemble Learning combines multiple Machine Learning models to create a stronger model.

The idea is:

> Multiple weak or diverse models together can produce better predictions than a single model.

Examples of Ensemble Techniques:

- Bagging
- Boosting
- Voting
- Stacking

This document focuses on:

- Voting Ensemble
- Stacking Ensemble

---

# 2. What are Non-Generative Ensemble Models?

Non-generative ensemble models do not learn a probability distribution or generate new data.

They combine predictions from existing Machine Learning models.

Examples:

- Voting Classifier
- Voting Regressor
- Stacking Classifier
- Stacking Regressor

They use already trained models and combine their outputs.

---

# 3. Why Ensemble Multiple Models?

Different algorithms have different strengths.

Example:

| Model | Strength |
|---|---|
| Random Forest | Handles nonlinear relationships |
| SVM | Works well in high-dimensional data |
| XGBoost | Excellent for tabular data |
| Logistic Regression | Simple and interpretable |

Instead of selecting only one model,

we combine them.

Benefits:

- Higher accuracy
- Better generalization
- Reduced variance
- Reduced model bias

---

# 4. Voting Ensemble

## Definition

Voting combines predictions from multiple independent models and selects the final prediction based on voting strategy.

Architecture:

```
                Training Data

                    |
    --------------------------------
    |              |               |
    ↓              ↓               ↓

 Model 1       Model 2        Model 3

    |              |               |

 Prediction   Prediction    Prediction

            ↓

       Voting Mechanism

            ↓

       Final Prediction
```

---

# Types of Voting

Voting is mainly divided into:

1. Hard Voting
2. Soft Voting

---

# 5. Hard Voting

## Definition

Hard Voting selects the class that receives the maximum number of votes.

It uses only predicted labels.

Example:

Three models predict:

| Model | Prediction |
|---|---|
| Random Forest | Cat |
| SVM | Dog |
| XGBoost | Dog |

Voting:

```
Cat = 1 vote

Dog = 2 votes
```

Final Prediction:

```
Dog
```

---

## Mathematical Representation

Final Class:

```
Mode(Predictions)
```

The majority class wins.

---

## Example

Models:

```
Model A → Yes

Model B → No

Model C → Yes
```

Final output:

```
Yes
```

because

```
Yes = 2 votes
No = 1 vote
```

---

## Advantages of Hard Voting

- Simple
- Easy to implement
- Does not require probability estimates
- Works with any classifier

---

## Disadvantages

- Ignores prediction confidence
- Treats all models equally
- Less accurate compared to Soft Voting

---

# 6. Soft Voting

## Definition

Soft Voting uses the probability predictions from each model.

Instead of only considering class labels,

it considers model confidence.

Example:

Model Predictions:

| Model | Cat Probability | Dog Probability |
|-|-|-|
| RF | 0.70 | 0.30 |
| XGB | 0.60 | 0.40 |
| SVM | 0.40 | 0.60 |

Average probability:

Cat:

```
(0.70 + 0.60 + 0.40)/3

= 0.56
```

Dog:

```
(0.30 + 0.40 + 0.60)/3

= 0.43
```

Final prediction:

```
Cat
```

---

## Formula

Average Probability:

```
P(final class)

=

(P1 + P2 + P3) / N
```

---

## Advantages

- Uses model confidence
- Usually performs better than Hard Voting
- More flexible

---

## Disadvantages

- Requires probability output
- Some models need probability calibration
- All models have equal importance

---

# Hard Voting vs Soft Voting

| Feature | Hard Voting | Soft Voting |
|-|-|-|
| Uses | Class Labels | Probabilities |
| Confidence | No | Yes |
| Accuracy | Lower | Higher |
| Requirement | Any classifier | Probability support required |
| Example | Majority Vote | Average Probability |

---

# 7. Simple Average

Simple Average is mainly used in regression problems.

Each model prediction receives equal importance.

Example:

Three regression models predict house price:

| Model | Prediction |
|-|-:|
| Random Forest | ₹50 Lakh |
| XGBoost | ₹55 Lakh |
| Linear Regression | ₹45 Lakh |

Final Prediction:

```
(50 + 55 + 45) / 3

= ₹50 Lakh
```

---

## Formula

```
Final Prediction

=

(y1 + y2 + y3 + ... + yn) / n
```

---

## Advantages

- Simple
- Reduces variance
- Works well with diverse models

---

## Disadvantages

- Assumes all models are equally important
- Weak models can reduce performance

---

# 8. Weighted Average

Weighted Average assigns different importance to different models.

Models with better performance receive higher weights.

Example:

| Model | Prediction | Weight |
|-|-|-|
| XGBoost | 55 | 0.5 |
| Random Forest | 50 | 0.3 |
| Linear Regression | 45 | 0.2 |

Final Prediction:

```
(55 × 0.5)

+

(50 × 0.3)

+

(45 × 0.2)

=

52.5
```

---

## Formula

```
Final Prediction

=

w1*y1 + w2*y2 + ... + wn*yn
```

where:

- y = Model prediction
- w = Model weight

Sum of weights:

```
w1+w2+w3+...=1
```

---

# Simple Average vs Weighted Average

| Feature | Simple Average | Weighted Average |
|-|-|-|
| Model Importance | Equal | Different |
| Complexity | Low | Higher |
| Accuracy | Good | Usually Better |
| Requires Validation | No | Yes |

---

# 9. Stacking Ensemble

## Definition

Stacking combines multiple models using another model called a **Meta Learner**.

Architecture:

```
                 Input Data

                     |
     --------------------------------

     Model 1     Model 2     Model 3

        |           |           |

        Predictions

              |

        Meta Learner

              |

        Final Prediction
```

---

# Components of Stacking

## 1. Base Learners

First-level models.

Examples:

- Random Forest
- XGBoost
- SVM
- Neural Network

They learn from original data.

---

## 2. Meta Learner

Second-level model.

It learns how to combine predictions.

Examples:

- Logistic Regression
- Linear Regression
- XGBoost

---

# 10. Cross Validation in Stacking

Cross Validation prevents data leakage.

Process:

```
Dataset

↓

K-Fold Split

↓

Train Base Models

↓

Generate Out-of-Fold Predictions

↓

Train Meta Learner

↓

Final Model
```

---

# Out-of-Fold Predictions

Instead of using predictions from training data,

we generate predictions on unseen folds.

This helps Meta Learner learn realistic patterns.

---

# 11. Voting vs Stacking

| Feature | Voting | Stacking |
|-|-|-|
| Combination Method | Voting/Average | Meta Model |
| Complexity | Simple | Complex |
| Training | Faster | Slower |
| Base Models | Independent | Independent |
| Learns Model Importance | No | Yes |
| Performance | Good | Usually Better |

---

# 12. Advantages

## Voting

- Simple
- Fast
- Easy deployment
- Improves stability

## Stacking

- Combines different algorithms
- Learns best combination
- Often improves accuracy
- Handles complex relationships

---

# 13. Disadvantages

## Voting

- Equal importance assumption
- Cannot learn model relationships

## Stacking

- Computationally expensive
- More complex
- Requires careful validation
- Higher risk of overfitting

---

# 14. Python Implementation

## Hard Voting

```python
from sklearn.ensemble import VotingClassifier

model = VotingClassifier(
    estimators=[
        ('rf', RandomForestClassifier()),
        ('xgb', XGBClassifier()),
        ('svm', SVC())
    ],
    voting='hard'
)

model.fit(X_train, y_train)
```

---

## Soft Voting

```python
model = VotingClassifier(
    estimators=[
        ('rf', RandomForestClassifier()),
        ('xgb', XGBClassifier()),
        ('lr', LogisticRegression())
    ],
    voting='soft'
)
```

---

## Stacking

```python
from sklearn.ensemble import StackingClassifier

model = StackingClassifier(
    estimators=[
        ('rf', RandomForestClassifier()),
        ('xgb', XGBClassifier())
    ],
    final_estimator=LogisticRegression(),
    cv=5
)

model.fit(X_train,y_train)
```

---

# 15. Interview Questions

## Beginner

1. What is Voting Ensemble?
2. Difference between Hard and Soft Voting?
3. What is Simple Average?
4. What is Weighted Average?
5. What is Stacking?

---

## Intermediate

1. Why is Soft Voting better than Hard Voting?
2. Why do we use probability in Soft Voting?
3. What is a Meta Learner?
4. Why is Cross Validation important in Stacking?
5. Difference between Voting and Stacking?

---

## Advanced

1. Explain the architecture of Stacking.
2. How do you assign weights in Weighted Average?
3. Why can Stacking outperform Voting?
4. What is data leakage in Stacking?
5. When should you prefer Voting over Stacking?

---

# 16. Summary

- Ensemble models combine multiple models to improve performance.
- Voting combines predictions directly.
- Hard Voting uses class labels and majority voting.
- Soft Voting uses probability predictions.
- Simple Average gives equal importance to all models.
- Weighted Average assigns different importance to models.
- Stacking uses a Meta Learner to learn the best combination of models.
- Cross Validation is essential in Stacking to avoid overfitting.

---

# Key Takeaways

- **Hard Voting → Majority Class**
- **Soft Voting → Average Probability**
- **Simple Average → Equal Weight**
- **Weighted Average → Different Importance**
- **Voting combines predictions**
- **Stacking learns how to combine predictions**
- **Stacking uses Base Learners + Meta Learner**
- **Cross Validation prevents leakage**
- **Both are powerful Non-Generative Ensemble Techniques**
