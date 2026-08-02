# 02_Multicollinearity_&_Feature_Selection.md

> **Level:** Intermediate → Advanced
>
> **Prerequisites:** Multiple Linear Regression Fundamentals
>
> **Goal:** Learn one of the most important concepts in Multiple Linear Regression—**Multicollinearity**—its detection, impact, and methods to select the best features.

---

# Table of Contents

1. What is Multicollinearity?
2. Why Does Multicollinearity Occur?
3. Types of Multicollinearity
4. Effects of Multicollinearity
5. Detecting Multicollinearity
6. Correlation Matrix
7. Variance Inflation Factor (VIF)
8. Tolerance
9. Condition Number
10. Eigenvalues (Brief)
11. Feature Selection
12. Filter Methods
13. Wrapper Methods
14. Embedded Methods
15. Forward Selection
16. Backward Elimination
17. Stepwise Regression
18. Recursive Feature Elimination (RFE)
19. Sequential Feature Selection
20. Best Subset Selection
21. Practical Workflow
22. Advantages & Limitations
23. Interview Questions
24. Summary

---

# 1. What is Multicollinearity?

## Definition

Multicollinearity occurs when **two or more independent variables are highly correlated** with each other.

Instead of providing unique information, they provide **similar information**.

Example

Suppose a house price dataset contains:

- Area (sq.ft.)
- Number of Rooms
- Number of Bedrooms
- Built-up Area
- Carpet Area

Here,

```
Area

≈

Built-up Area

≈

Carpet Area
```

These variables contain overlapping information.

This leads to **Multicollinearity**.

---

# Why is it a Problem?

The model cannot clearly determine

> Which variable is actually responsible for predicting the target.

As a result,

Regression coefficients become unstable.

---

# 2. Why Does Multicollinearity Occur?

Common causes

## 1. Duplicate Features

Example

```
Height (cm)

Height (meter)
```

Both represent the same information.

---

## 2. Derived Features

Example

```
Area

Length

Width
```

Since

```
Area = Length × Width
```

The variables are related.

---

## 3. Poor Feature Engineering

Creating many similar features.

Example

```
Monthly Salary

Annual Salary

Daily Salary
```

---

## 4. Dummy Variable Trap

Creating dummy variables incorrectly.

Example

Gender

```
Male

Female
```

Both columns are not required.

Only one should be kept.

---

## 5. Small Dataset

Small datasets often produce artificially high correlations.

---

# 3. Types of Multicollinearity

## Perfect Multicollinearity

One variable is an exact linear combination of another.

Example

```
Y

=

2X
```

Regression cannot be computed.

---

## High Multicollinearity

Variables are strongly correlated but not identical.

Example

```
Correlation = 0.93
```

Regression works,

but interpretation becomes unreliable.

---

# 4. Effects of Multicollinearity

- Unstable coefficients
- Large standard errors
- Incorrect p-values
- Wide confidence intervals
- Difficult feature interpretation
- Reduced statistical significance
- Small data changes produce large coefficient changes

**Important**

Prediction accuracy may remain good,

but interpretation becomes poor.

This is one of the most asked interview questions.

---

# 5. Detecting Multicollinearity

Common techniques

- Correlation Matrix
- Heatmap
- Variance Inflation Factor (VIF)
- Tolerance
- Condition Number
- Eigenvalues

---

# 6. Correlation Matrix

Measures pairwise correlation.

Example

| Feature | Area | Bedrooms | Age |
|----------|------|-----------|-----|
| Area | 1.00 | 0.82 | -0.12 |
| Bedrooms | 0.82 | 1.00 | -0.08 |
| Age | -0.12 | -0.08 | 1.00 |

Observation

```
Area

Bedrooms

↓

0.82
```

High correlation.

Possible multicollinearity.

---

## Rule of Thumb

| Correlation | Interpretation |
|-------------|---------------|
| <0.50 | Low |
| 0.50–0.70 | Moderate |
| >0.80 | High |
| >0.90 | Very High |

Correlation only checks **two variables at a time**.

Use VIF for a complete analysis.

---

# 7. Variance Inflation Factor (VIF)

The most popular method.

## Definition

VIF measures

> How much the variance of a regression coefficient increases due to multicollinearity.

Formula

```
VIF

=

1

/

(1-R²)
```

Where

```
R²
```

comes from regressing one feature against all remaining features.

---

## Interpretation

| VIF | Meaning |
|-----|---------|
| 1 | No Multicollinearity |
| 1–5 | Acceptable |
| 5–10 | Moderate |
| >10 | Serious Problem |

---

### Example

| Feature | VIF |
|----------|----|
| Area | 12.5 |
| Bedrooms | 2.3 |
| Age | 1.5 |

Conclusion

```
Area
```

should be investigated.

---

# Why VIF Works

Suppose

```
Area
```

can be predicted almost perfectly using

```
Bedrooms

+

Built-up Area

+

Carpet Area
```

Then

```
R²

≈

1
```

Therefore

```
VIF

becomes

very large
```

Large VIF

↓

High multicollinearity.

---

# 8. Tolerance

Tolerance is the inverse of VIF.

Formula

```
Tolerance

=

1

/

VIF
```

Interpretation

| Tolerance | Meaning |
|------------|----------|
| >0.20 | Good |
| 0.10–0.20 | Moderate |
| <0.10 | Serious Multicollinearity |

Lower tolerance

↓

Higher multicollinearity.

---

# 9. Condition Number

Measures dependency among multiple variables.

Formula

```
Largest Eigenvalue

/

Smallest Eigenvalue
```

Interpretation

| Condition Number | Meaning |
|-----------------|----------|
| <10 | Good |
| 10–30 | Moderate |
| >30 | Serious Multicollinearity |

Mostly used in advanced statistical analysis.

---

# 10. Eigenvalues (Brief)

Eigenvalues indicate how much information exists in each direction of the feature space.

Very small eigenvalues indicate

- Redundant information
- Nearly dependent variables

Used internally while computing the Condition Number.

---

# 11. Feature Selection

## Definition

Feature Selection is the process of selecting the **most useful predictors** while removing unnecessary ones.

Benefits

- Better interpretation
- Faster training
- Reduced overfitting
- Lower multicollinearity
- Better generalization

---

# Types of Feature Selection

```
Feature Selection

↓

Filter

Wrapper

Embedded
```

---

# 12. Filter Methods

Model-independent.

Features are selected before training.

Examples

- Correlation
- Chi-Square
- ANOVA
- Mutual Information

Advantages

- Fast
- Simple

Disadvantages

Ignores model performance.

---

# 13. Wrapper Methods

Model-based feature selection.

Different feature combinations are evaluated.

Examples

- Forward Selection
- Backward Elimination
- Stepwise Regression
- RFE

Advantages

Higher accuracy.

Disadvantages

Computationally expensive.

---

# 14. Embedded Methods

Feature selection occurs during model training.

Examples

- Lasso Regression
- Elastic Net
- Decision Trees

Advantages

- Efficient
- Automatic

---

# 15. Forward Selection

Workflow

```
No Features

↓

Add Best Feature

↓

Evaluate

↓

Add Next Best Feature

↓

Repeat
```

Stop when no improvement occurs.

Advantages

- Fast
- Useful for many predictors

---

# 16. Backward Elimination

Workflow

```
Start

↓

All Features

↓

Remove Least Important

↓

Evaluate

↓

Repeat
```

Often uses

```
Highest p-value
```

for removal.

---

# 17. Stepwise Regression

Combination of

- Forward Selection
- Backward Elimination

At every step

- Add useful variables
- Remove unnecessary variables

Produces a balanced model.

---

# 18. Recursive Feature Elimination (RFE)

Workflow

```
Train Model

↓

Rank Features

↓

Remove Lowest Ranked Feature

↓

Retrain

↓

Repeat
```

Widely used with Scikit-learn.

---

# 19. Sequential Feature Selection

Two approaches

### Forward Sequential

Keep adding features.

### Backward Sequential

Keep removing features.

Unlike RFE,

it evaluates performance after every step.

---

# 20. Best Subset Selection

Idea

Evaluate **every possible combination** of predictors.

Example

Features

```
A

B

C
```

Possible models

```
A

B

C

AB

AC

BC

ABC
```

Best-performing model is selected.

Limitation

Computationally expensive.

Not suitable for large datasets.

---

# 21. Practical Workflow

```
Collect Data

↓

EDA

↓

Correlation Matrix

↓

Remove Duplicate Features

↓

Calculate VIF

↓

Remove High VIF Variables

↓

Feature Selection

↓

Train Model

↓

Evaluate

↓

Repeat if Required
```

---

# 22. Advantages & Limitations

## Advantages

- Better model interpretation
- Reduced overfitting
- Faster computation
- Stable coefficients
- Better statistical significance

### Limitations

- Removing useful variables may reduce accuracy
- Wrapper methods are computationally expensive
- Correlation alone cannot detect all multicollinearity

---

# 23. Interview Questions

## Beginner

1. What is Multicollinearity?
2. Why is it a problem?
3. How do you detect Multicollinearity?
4. What is VIF?
5. What is Tolerance?

---

## Intermediate

1. Difference between Correlation and VIF.
2. Explain Forward Selection.
3. Explain Backward Elimination.
4. Explain Stepwise Regression.
5. Explain RFE.

---

## Advanced

1. Why can prediction accuracy remain high despite Multicollinearity?
2. Explain Condition Number.
3. Explain Eigenvalues in regression.
4. How would you remove Multicollinearity?
5. Which Feature Selection method would you choose for a dataset with 500 features?

---

# 24. Summary

- **Multicollinearity** occurs when independent variables are highly correlated.
- It mainly affects **coefficient interpretation**, not necessarily prediction accuracy.
- **VIF** is the most widely used metric for detecting multicollinearity.
- **Tolerance**, **Condition Number**, and **Eigenvalues** provide additional diagnostics.
- Feature Selection improves model simplicity, stability, and generalization.
- Common selection methods include **Forward Selection**, **Backward Elimination**, **Stepwise Regression**, **RFE**, and **Best Subset Selection**.
- Managing multicollinearity is essential for building interpretable and statistically reliable Multiple Linear Regression models.

---

# Key Takeaways

- **Correlation identifies pairwise relationships; VIF measures overall multicollinearity.**
- **VIF > 10 generally indicates serious multicollinearity.**
- **Tolerance = 1 / VIF.**
- **Prediction may remain accurate even when coefficients become unstable.**
- **Feature Selection improves both interpretability and model performance.**
- **Wrapper methods often provide better models but require more computation.**
- **Always check VIF before interpreting regression coefficients.**
- **Removing redundant features is usually better than keeping highly correlated predictors.**
