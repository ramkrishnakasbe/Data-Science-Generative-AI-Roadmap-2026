# 03_Model_Evaluation_&_Diagnostics.md

> **Level:** Beginner → Advanced
>
> **Prerequisites:** Simple Linear Regression Fundamentals, Statistical Concepts
>
> **Goal:** Learn how to evaluate, diagnose, validate, and improve a Linear Regression model using statistical metrics, validation techniques, and diagnostic plots.

---

# Table of Contents

1. Introduction
2. Why Model Evaluation?
3. Types of Errors
4. Evaluation Metrics
5. MAE
6. MSE
7. RMSE
8. RMSLE
9. MAPE
10. R² Score
11. Adjusted R²
12. Explained Variance Score
13. Residual Analysis
14. Diagnostic Plots
15. Underfitting
16. Overfitting
17. Train-Test Split
18. Cross Validation
19. K-Fold Cross Validation
20. LOOCV
21. Learning Curve
22. Feature Scaling
23. Missing Values
24. Outlier Treatment
25. Feature Engineering
26. Model Improvement Techniques
27. Best Practices
28. Interview Questions
29. Summary

---

# 1. Introduction

Building a regression model is only the first step.

The next step is to determine whether the model is:

- Accurate
- Reliable
- Stable
- Generalizable

This process is called **Model Evaluation**.

---

# 2. Why Model Evaluation?

A model should perform well not only on training data but also on unseen data.

Model evaluation helps to:

- Measure prediction accuracy
- Compare multiple models
- Detect overfitting
- Detect underfitting
- Improve model performance
- Select the best model

---

# 3. Types of Prediction Errors

For every prediction,

```
Error = Actual − Predicted
```

Errors can be:

- Small
- Large
- Positive
- Negative

Good models have smaller errors.

---

# Example

| Actual | Predicted | Error |
|---------|-----------|------:|
| 50 | 48 | 2 |
| 70 | 73 | -3 |
| 40 | 39 | 1 |

---

# 4. Evaluation Metrics

Common regression metrics:

- MAE
- MSE
- RMSE
- RMSLE
- MAPE
- R² Score
- Adjusted R²
- Explained Variance Score

---

# 5. Mean Absolute Error (MAE)

## Definition

Average absolute prediction error.

Formula

```
MAE = Σ|Actual − Predicted| / n
```

Example

| Actual | Predicted |
|---------|-----------|
| 10 | 8 |
| 20 | 18 |
| 30 | 28 |

Absolute Errors

```
2

2

2
```

MAE

```
(2+2+2)/3 = 2
```

### Advantages

- Easy to understand
- Same unit as target
- Less sensitive to outliers

### Disadvantages

- Doesn't penalize large errors heavily

---

# 6. Mean Squared Error (MSE)

## Definition

Average squared error.

Formula

```
MSE = Σ(Actual − Predicted)² / n
```

Advantages

- Penalizes large errors
- Smooth optimization function
- Used in OLS

Disadvantages

- Sensitive to outliers
- Unit becomes squared

---

# 7. Root Mean Squared Error (RMSE)

Definition

Square root of MSE.

Formula

```
RMSE = √MSE
```

Advantages

- Same unit as target
- Easy interpretation
- Most popular regression metric

Disadvantages

- Sensitive to outliers

---

# MAE vs MSE vs RMSE

| Metric | Outlier Sensitive | Unit |
|---------|------------------|------|
| MAE | Low | Original |
| MSE | High | Squared |
| RMSE | High | Original |

---

# 8. Root Mean Squared Log Error (RMSLE)

Used when target values vary significantly.

Formula

```
RMSE on log-transformed values
```

Applications

- Sales Forecasting
- Demand Prediction
- Population Growth

Advantages

- Reduces effect of extremely large values

---

# 9. Mean Absolute Percentage Error (MAPE)

Formula

```
MAPE

=

Average

(|Actual − Predicted| / Actual)

×

100
```

Example

Actual

```
100
```

Prediction

```
90
```

Error

```
10%
```

Advantages

- Easy interpretation
- Percentage based

Limitations

- Cannot handle Actual = 0

---

# 10. R² Score (Coefficient of Determination)

Definition

Measures how much variance in the target variable is explained by the model.

Formula

```
R²

=

1 −

(Residual Sum of Squares)

/

(Total Sum of Squares)
```

Range

```
0 → Poor

1 → Perfect
```

Interpretation

| R² | Meaning |
|----|---------|
| 0 | Explains nothing |
| 0.60 | Explains 60% variance |
| 0.90 | Excellent model |
| 1.00 | Perfect fit |

---

# Limitations of R²

- Always increases when new features are added
- Does not detect overfitting
- Should not be used alone

---

# 11. Adjusted R²

Adjusted R² penalizes unnecessary variables.

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

- n = observations
- p = predictors

Advantages

- Better than R²
- Used in feature selection

---

# R² vs Adjusted R²

| Feature | R² | Adjusted R² |
|----------|----|-------------|
| Penalizes Extra Features | No | Yes |
| Feature Selection | Poor | Better |
| Multiple Regression | Limited | Preferred |

---

# 12. Explained Variance Score

Measures how much variation is captured by the model.

Range

```
0 → Poor

1 → Perfect
```

Higher value is better.

---

# 13. Residual Analysis

Residual

```
Residual

=

Actual − Predicted
```

A good model produces residuals that are:

- Random
- Small
- Independent
- Normally distributed

---

# 14. Diagnostic Plots

## Scatter Plot

Checks linear relationship.

---

## Regression Line Plot

Shows

- Actual values
- Predicted line

---

## Residual Plot

Good Plot

```
* * * *

 * * *

* * *

```

Random scatter around zero.

Bad Plot

```
*

 *

   *

      *

         *
```

Pattern indicates assumption violation.

---

## Histogram

Checks residual distribution.

---

## QQ Plot

Checks normality.

Points should lie on a straight line.

---

# 15. Underfitting

Definition

Model is too simple.

Characteristics

- High Bias
- Low Variance
- Poor Training Accuracy
- Poor Testing Accuracy

Solutions

- Add Features
- Polynomial Regression
- Better Algorithm

---

# 16. Overfitting

Definition

Model memorizes training data.

Characteristics

- Very High Training Accuracy
- Low Testing Accuracy
- High Variance

Solutions

- More Data
- Cross Validation
- Feature Selection
- Regularization

---

# Underfitting vs Overfitting

| Feature | Underfitting | Overfitting |
|----------|--------------|-------------|
| Bias | High | Low |
| Variance | Low | High |
| Training Accuracy | Low | Very High |
| Testing Accuracy | Low | Low |

---

# 17. Train-Test Split

Dataset

```
↓

Training Data

+

Testing Data
```

Common Splits

- 70:30
- 80:20
- 75:25

Advantages

- Simple
- Fast

Disadvantages

- Depends on one split

---

# 18. Cross Validation

Instead of one split,

multiple train-test splits are used.

Advantages

- Better estimate
- Lower variance
- More reliable

---

# 19. K-Fold Cross Validation

Example

```
Dataset

↓

Fold1

Fold2

Fold3

Fold4

Fold5
```

Every fold becomes the validation set once.

Final score

```
Average of all folds
```

Most common

```
K = 5

K = 10
```

---

# 20. Leave-One-Out Cross Validation (LOOCV)

Extreme case of K-Fold.

```
K = Number of Samples
```

Advantages

- Uses maximum training data

Disadvantages

- Very slow

---

# 21. Learning Curve

Learning curves compare

- Training Performance
- Validation Performance

Used to detect

- Underfitting
- Overfitting

---

# 22. Feature Scaling

Simple Linear Regression **does not require feature scaling** when using Ordinary Least Squares (OLS).

Scaling becomes useful when using:

- Gradient Descent
- Regularization
- Distance-based algorithms

Common methods

- Standardization
- Min-Max Scaling

---

# 23. Missing Values

Missing values should be handled before training.

Methods

- Mean Imputation
- Median Imputation
- Mode
- KNN Imputation
- Remove Rows
- Remove Columns

---

# 24. Outlier Treatment

Methods

- IQR Method
- Z-score
- Winsorization
- Capping
- Transformation

Removing unnecessary outliers often improves regression performance.

---

# 25. Feature Engineering

Improves model performance.

Examples

- Log Transformation
- Polynomial Features
- Interaction Features
- Date Features
- Ratio Features

---

# 26. Model Improvement Techniques

- Collect more data
- Remove noisy data
- Feature Engineering
- Feature Selection
- Handle Outliers
- Handle Missing Values
- Cross Validation
- Polynomial Regression
- Regularization
- Hyperparameter Tuning (when applicable)

---

# 27. Best Practices

- Visualize data before modeling
- Check assumptions
- Remove duplicate records
- Handle missing values
- Detect outliers
- Evaluate using multiple metrics
- Never rely only on R²
- Validate using Cross Validation
- Interpret residual plots
- Compare multiple models

---

# 28. Interview Questions

## Beginner

1. What is Model Evaluation?
2. What is MAE?
3. Difference between MAE and RMSE?
4. What is R²?
5. What is Adjusted R²?

---

## Intermediate

1. Why is RMSE preferred over MSE?
2. Difference between R² and Adjusted R².
3. Explain residual analysis.
4. Why is Cross Validation important?
5. Difference between Hold-Out and K-Fold.

---

## Advanced

1. Why can a model have high R² but poor predictions?
2. Explain Explained Variance Score.
3. How do you detect overfitting?
4. Why shouldn't R² be the only evaluation metric?
5. Which metric would you use for house price prediction and why?

---

# 29. Summary

- Model evaluation measures how well a regression model predicts unseen data.
- Common metrics include **MAE, MSE, RMSE, RMSLE, MAPE, R², and Adjusted R²**.
- **MAE** is robust to outliers, while **MSE** and **RMSE** penalize large errors more heavily.
- **R²** measures the proportion of variance explained by the model, whereas **Adjusted R²** accounts for the number of predictors.
- Residual analysis and diagnostic plots help verify model assumptions.
- **Cross Validation** provides a more reliable estimate of model performance than a single train-test split.
- Proper handling of missing values, outliers, and feature engineering can significantly improve model accuracy.

---

# Key Takeaways

- **Lower MAE, MSE, RMSE → Better Model**
- **Higher R² & Adjusted R² → Better Fit**
- **Residuals should be random around zero**
- **RMSE is one of the most widely used regression metrics**
- **Adjusted R² is preferred when comparing models with different numbers of predictors**
- **Cross Validation improves confidence in model performance**
- **Diagnostic plots reveal assumption violations**
- **Good evaluation requires multiple metrics, not just one**
- **Feature engineering and data quality often improve performance more than changing algorithms**
