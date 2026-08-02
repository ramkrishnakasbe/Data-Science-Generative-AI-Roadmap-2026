# 04_Model_Selection_&_Regularization.md

> **Level:** Intermediate → Advanced
>
> **Prerequisites:** Multiple Linear Regression Fundamentals, Multicollinearity & Feature Selection
>
> **Goal:** Learn how to choose the best Multiple Linear Regression model, compare models, understand model selection criteria, and solve overfitting using Regularization.

---

# Table of Contents

1. Why Model Selection?
2. Good Model vs Bad Model
3. Model Selection Criteria
4. Adjusted R²
5. AIC (Akaike Information Criterion)
6. BIC (Bayesian Information Criterion)
7. Mallows' Cp
8. PRESS Statistic
9. Partial F-Test
10. Nested Models
11. Comparing Multiple Models
12. Bias-Variance Tradeoff
13. Why Regularization?
14. Ridge Regression (L2)
15. Lasso Regression (L1)
16. Elastic Net
17. Choosing Between Ridge, Lasso & Elastic Net
18. Practical Workflow
19. Advantages & Limitations
20. Interview Questions
21. Summary

---

# 1. Why Model Selection?

Adding more features does **not** always produce a better model.

Example

```
Model A

5 Features

Accuracy = 91%
```

```
Model B

30 Features

Accuracy = 91.2%
```

Model B is

- More complex
- Harder to interpret
- More likely to overfit

The objective is to build the **simplest model that performs well**.

---

# 2. Good Model vs Bad Model

A good regression model should

- Explain the data well
- Generalize to unseen data
- Avoid overfitting
- Use only useful predictors
- Have stable coefficients

A bad model

- Memorizes training data
- Contains unnecessary variables
- Has unstable coefficients
- Performs poorly on new data

---

# 3. Model Selection Criteria

Common criteria

```
Adjusted R²

↓

AIC

↓

BIC

↓

Mallows' Cp

↓

PRESS Statistic

↓

Cross Validation
```

Each criterion balances **model fit** and **model complexity**.

---

# 4. Adjusted R²

Unlike R²,

Adjusted R² penalizes unnecessary predictors.

Formula

```
Adjusted R²

=

1 -

((1-R²)(n-1))

/

(n-p-1)
```

Where

```
n = Number of observations

p = Number of predictors
```

Advantages

- Penalizes extra variables
- Better than R² for MLR
- Useful for comparing models

Rule

```
Higher Adjusted R²

↓

Better Model
```

---

# 5. Akaike Information Criterion (AIC)

AIC measures

```
Goodness of Fit

+

Model Complexity
```

Formula

```
AIC

=

2k

-

2ln(L)
```

Where

```
k

=

Number of Parameters

L

=

Likelihood
```

Interpretation

```
Lower AIC

↓

Better Model
```

AIC is widely used in

- Regression
- Time Series
- Statistical Modeling

---

# 6. Bayesian Information Criterion (BIC)

BIC is similar to AIC

but penalizes complex models **more strongly**.

Formula

```
BIC

=

k ln(n)

-

2ln(L)
```

Rule

```
Lower BIC

↓

Better Model
```

Comparison

| Metric | Penalty |
|----------|---------|
| AIC | Moderate |
| BIC | Strong |

BIC generally prefers simpler models.

---

# 7. Mallows' Cp

Used to determine

whether unnecessary variables exist.

Ideal value

```
Cp

≈

p
```

Where

```
p

=

Number of Parameters
```

Interpretation

| Cp | Meaning |
|----|---------|
| Close to p | Good Model |
| Much Larger | Too Complex |
| Much Smaller | Possibly Underfitting |

---

# 8. PRESS Statistic

PRESS

=

Prediction Sum of Squares

Purpose

Measures

```
Prediction Error

on

Unseen Data
```

Computed using

Leave-One-Out Cross Validation (LOOCV).

Rule

```
Lower PRESS

↓

Better Prediction
```

Useful for

- Small datasets
- Model comparison
- Regression diagnostics

---

# 9. Partial F-Test

Used to compare

two regression models.

Question

```
Does adding new variables

significantly improve

the model?
```

Example

Model 1

```
Salary

~

Experience
```

Model 2

```
Salary

~

Experience

+

Education

+

Skill
```

If

```
p-value < 0.05
```

The larger model is statistically better.

---

# 10. Nested Models

A model is nested if

one model contains all variables of another.

Example

Model A

```
Salary

~

Experience
```

Model B

```
Salary

~

Experience

+

Education
```

Model A

is nested inside

Model B.

Nested models are compared using

- Partial F-Test
- AIC
- BIC

---

# 11. Comparing Multiple Models

Suppose

| Model | Adj R² | AIC | BIC |
|--------|--------|-----|-----|
| A | 0.84 | 540 | 565 |
| B | 0.90 | 498 | 520 |
| C | 0.89 | 510 | 525 |

Observation

Model B has

- Highest Adjusted R²
- Lowest AIC
- Lowest BIC

Therefore,

Model B is preferred.

---

# 12. Bias-Variance Tradeoff

Increasing model complexity

↓

Bias decreases

↓

Variance increases

```
Simple Model

↓

High Bias

↓

Low Variance
```

```
Complex Model

↓

Low Bias

↓

High Variance
```

Goal

```
Balanced Model
```

Regularization helps achieve this balance.

---

# 13. Why Regularization?

Large coefficients often indicate

- Overfitting
- Multicollinearity
- Poor generalization

Regularization

adds a penalty

to the loss function.

Objective

```
Reduce coefficient magnitude

↓

Improve generalization
```

---

# 14. Ridge Regression (L2)

Ridge Regression

adds the squared magnitude of coefficients as a penalty.

Loss Function

```
RSS

+

λ Σβ²
```

Characteristics

- Shrinks coefficients
- Does not remove features
- Handles multicollinearity well

Advantages

- Stable coefficients
- Better prediction
- Works with correlated variables

Disadvantages

- Less interpretable
- Keeps all variables

---

# 15. Lasso Regression (L1)

Lasso Regression

adds the absolute value of coefficients.

Loss Function

```
RSS

+

λ Σ|β|
```

Characteristics

- Shrinks coefficients
- Can make coefficients exactly zero
- Performs feature selection automatically

Advantages

- Simpler model
- Removes unnecessary variables
- Easy interpretation

Disadvantages

- Can remove useful correlated features

---

# Ridge vs Lasso

| Feature | Ridge | Lasso |
|----------|--------|--------|
| Penalty | L2 | L1 |
| Removes Features | No | Yes |
| Shrinks Coefficients | Yes | Yes |
| Feature Selection | No | Yes |

---

# 16. Elastic Net

Elastic Net

combines

```
L1

+

L2
```

Loss Function

```
RSS

+

λ₁ Σ|β|

+

λ₂ Σβ²
```

Advantages

- Handles multicollinearity
- Performs feature selection
- More stable than Lasso

Commonly used

when many correlated variables exist.

---

# 17. Choosing Between Ridge, Lasso & Elastic Net

| Situation | Recommended |
|-----------|-------------|
| Many correlated variables | Ridge |
| Automatic feature selection | Lasso |
| Correlated variables + Feature selection | Elastic Net |
| High-dimensional datasets | Elastic Net |

---

# 18. Practical Workflow

```
Build Initial Model

↓

Check Adjusted R²

↓

Compare AIC & BIC

↓

Perform Partial F-Test

↓

Check Overfitting

↓

Apply Regularization (if needed)

↓

Compare Models

↓

Select Best Model
```

---

# 19. Advantages & Limitations

## Advantages

- Prevents overfitting
- Improves prediction accuracy
- Produces simpler models
- Reduces multicollinearity effects
- Improves generalization

---

## Limitations

- Requires hyperparameter tuning (λ)
- Coefficients become harder to interpret
- Regularization introduces bias
- Model selection metrics may disagree

---

# 20. Interview Questions

## Beginner

1. Why is Adjusted R² preferred over R²?
2. What is AIC?
3. What is BIC?
4. What is Regularization?
5. Why is Regularization needed?

---

## Intermediate

1. Difference between AIC and BIC.
2. Difference between Ridge and Lasso.
3. What is Elastic Net?
4. What is a Nested Model?
5. Explain the Partial F-Test.

---

## Advanced

1. Why does Ridge not perform feature selection?
2. Why can Lasso remove important correlated variables?
3. Explain Bias-Variance Tradeoff using Regularization.
4. When would you choose Elastic Net over Ridge?
5. How would you compare two regression models in production?

---

# 21. Summary

- Model selection aims to balance **accuracy** and **simplicity**.
- **Adjusted R²**, **AIC**, **BIC**, **PRESS**, and **Mallows' Cp** help compare regression models.
- **Partial F-Test** determines whether adding predictors significantly improves the model.
- **Nested Models** allow statistical comparison between simpler and more complex models.
- **Regularization** reduces overfitting by penalizing large coefficients.
- **Ridge Regression** addresses multicollinearity, **Lasso Regression** performs feature selection, and **Elastic Net** combines both approaches.

---

# Key Takeaways

- **Higher Adjusted R² is better.**
- **Lower AIC, BIC, PRESS, and Mallows' Cp generally indicate better models.**
- **Partial F-Test compares nested regression models.**
- **Regularization improves generalization by shrinking coefficients.**
- **Ridge = L2 penalty (keeps all features).**
- **Lasso = L1 penalty (can remove features).**
- **Elastic Net = L1 + L2 (best for many correlated predictors).**
- **Always compare multiple models before selecting the final regression model.**
