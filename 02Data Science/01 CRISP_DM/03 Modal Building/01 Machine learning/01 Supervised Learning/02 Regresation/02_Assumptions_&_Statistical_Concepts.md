# 02_Assumptions_&_Statistical_Concepts.md

> **Level:** Beginner → Advanced
>
> **Prerequisites:** Simple Linear Regression Fundamentals
>
> **Goal:** Understand the statistical assumptions behind Linear Regression, hypothesis testing, statistical significance, residual analysis, and common diagnostic tests.

---

# Table of Contents

1. Introduction
2. Why Assumptions Matter?
3. Linear Regression Assumptions (LINE)
4. Linearity
5. Independence of Errors
6. Normality of Residuals
7. Homoscedasticity
8. Heteroscedasticity
9. Residuals
10. Residual Analysis
11. Types of Residual Plots
12. Outliers
13. Leverage Points
14. Influential Points
15. Cook's Distance
16. Multicollinearity
17. Variance Inflation Factor (VIF)
18. Hypothesis Testing
19. Null & Alternative Hypothesis
20. t-Test
21. F-Test
22. p-value
23. Confidence Interval
24. Prediction Interval
25. Statistical Significance
26. Assumption Checking Workflow
27. Advantages
28. Limitations
29. Interview Questions
30. Summary

---

# 1. Introduction

Linear Regression is based on statistical assumptions.

If these assumptions are violated:

- Predictions become unreliable
- Confidence intervals become inaccurate
- Statistical tests may become invalid
- Model performance decreases

A regression model should always be validated before deployment.

---

# 2. Why Assumptions Matter?

Assumptions help ensure that:

- Model coefficients are unbiased
- Predictions are reliable
- Statistical inference is valid
- Confidence intervals are meaningful

Ignoring assumptions may lead to incorrect business decisions.

---

# 3. Linear Regression Assumptions (LINE)

The four most important assumptions are remembered using **LINE**.

| Letter | Assumption |
|---------|------------|
| L | Linearity |
| I | Independence |
| N | Normality |
| E | Equal Variance (Homoscedasticity) |

---

# 4. Linearity

## Definition

The relationship between the independent variable (X) and dependent variable (Y) should be linear.

Example

```
Increase in Experience

↓

Increase in Salary
```

Graph

```
Y

|

|          *

|       *

|    *

| *

+----------------------> X
```

### How to Check?

- Scatter Plot
- Residual Plot
- Correlation Analysis

### If Violated

Possible solutions:

- Polynomial Regression
- Feature Transformation
- Log Transformation

---

# 5. Independence of Errors

Residuals should be independent of each other.

This assumption is especially important in:

- Time Series
- Forecasting
- Sequential Data

Violation leads to **Autocorrelation**.

Example

Today's prediction error should not depend on yesterday's error.

---

## Durbin-Watson Test

Used to detect autocorrelation.

| Value | Interpretation |
|---------|---------------|
| ≈2 | No Autocorrelation |
| <2 | Positive Autocorrelation |
| >2 | Negative Autocorrelation |

Ideal value

```
≈ 2
```

---

# 6. Normality of Residuals

Residuals should approximately follow a Normal Distribution.

Graph

```
          *
       *     *
     *         *
   *             *
 *                 *
--------------------------
```

### Why?

Normal residuals make:

- Confidence intervals valid
- t-tests valid
- F-tests valid

### How to Check?

- Histogram
- QQ Plot
- Shapiro-Wilk Test
- Anderson-Darling Test

---

# 7. Homoscedasticity

## Definition

Residuals should have constant variance across all predicted values.

Good Example

```
     *
   *  *
 *  *  *
  * * *
 *  * *
```

Variance remains constant.

---

### Why Important?

- Stable predictions
- Reliable standard errors
- Better confidence intervals

---

# 8. Heteroscedasticity

Variance changes as prediction changes.

Example

```
*

 *

   *

      *

          *

              *

                   *
```

Residual spread increases.

### Causes

- Outliers
- Incorrect model
- Missing variables
- Large data variation

### Solutions

- Log Transformation
- Feature Engineering
- Weighted Least Squares
- Robust Regression

---

# 9. Residuals

Residual

```
Residual

=

Actual − Predicted
```

Example

Actual Salary

```
50
```

Predicted Salary

```
45
```

Residual

```
5
```

Residuals measure prediction error.

---

# 10. Residual Analysis

Residual analysis checks whether assumptions are satisfied.

Good residuals should be:

- Random
- Independent
- Normally distributed
- Constant variance

---

# 11. Types of Residual Plots

## Residual vs Predicted

Used to check

- Linearity
- Homoscedasticity

Ideal Pattern

```
  *  * *  *

* * * * *

  * * *

```

Random scatter around zero.

---

## Histogram

Checks normality.

---

## QQ Plot

Compares residual distribution with Normal Distribution.

Points should lie approximately on a straight line.

---

# 12. Outliers

Outliers are observations far away from other data points.

Example

```
5

6

7

8

150
```

150 is an outlier.

### Effects

- Changes regression line
- Reduces accuracy
- Increases error

### Detection

- Box Plot
- Z-score
- IQR Method

---

# 13. Leverage Points

Leverage points have unusual X values.

Example

```
1

2

3

4

100
```

100 has high leverage.

A leverage point may or may not be an outlier.

---

# 14. Influential Points

Influential observations significantly change the regression line when removed.

Not every outlier is influential.

---

# 15. Cook's Distance

Measures the influence of an observation.

Rule of Thumb

```
Cook's Distance > 1

↓

Potentially Influential
```

Used to identify observations affecting model coefficients.

---

# 16. Multicollinearity

Occurs when independent variables are highly correlated.

**Important:**

Simple Linear Regression has only **one predictor**, so multicollinearity does **not** occur.

It becomes important in Multiple Linear Regression.

---

# 17. Variance Inflation Factor (VIF)

Used to measure multicollinearity.

Interpretation

| VIF | Meaning |
|------|---------|
| 1 | No Correlation |
| 1-5 | Moderate |
| >5 | High |
| >10 | Serious Problem |

---

# 18. Hypothesis Testing

Used to determine whether the independent variable significantly affects the dependent variable.

---

# 19. Null & Alternative Hypothesis

Null Hypothesis

```
H₀

β₁ = 0
```

Meaning

Independent variable has **no effect**.

---

Alternative Hypothesis

```
H₁

β₁ ≠ 0
```

Meaning

Independent variable significantly affects the target.

---

# 20. t-Test

Tests the significance of an individual regression coefficient.

Decision Rule

```
p-value < 0.05

↓

Reject H₀
```

Coefficient is statistically significant.

---

# 21. F-Test

Tests whether the regression model as a whole is significant.

Large F-statistic indicates a useful model.

---

# 22. p-value

Definition

Probability of observing the result if the Null Hypothesis is true.

Interpretation

| p-value | Decision |
|----------|----------|
| <0.05 | Significant |
| >0.05 | Not Significant |

Smaller p-value means stronger evidence against H₀.

---

# 23. Confidence Interval

Represents the range within which the true regression coefficient is expected to lie.

Example

```
Coefficient

5

95% CI

4.3 – 5.7
```

---

# 24. Prediction Interval

Used to estimate the range for a **future observation**.

Prediction intervals are always wider than confidence intervals because they include both model uncertainty and random error.

---

# Confidence Interval vs Prediction Interval

| Feature | Confidence Interval | Prediction Interval |
|----------|---------------------|---------------------|
| Estimates | Mean Response | Individual Prediction |
| Width | Narrow | Wider |
| Used For | Coefficient Estimation | Future Predictions |

---

# 25. Statistical Significance

A variable is statistically significant if:

- p-value < 0.05
- Confidence interval does not contain zero

Significance does **not** always imply practical importance.

---

# 26. Assumption Checking Workflow

```
Build Regression Model

↓

Residual Plot

↓

QQ Plot

↓

Durbin-Watson Test

↓

Cook's Distance

↓

Hypothesis Testing

↓

Model Validation
```

---

# 27. Advantages

- Ensures reliable predictions
- Valid statistical inference
- Better model interpretation
- Detects modeling problems early

---

# 28. Limitations

- Some assumptions are difficult to verify
- Real-world data rarely satisfies all assumptions perfectly
- Sensitive to outliers
- Time series often violate independence

---

# 29. Interview Questions

## Beginner

1. What are the assumptions of Linear Regression?
2. What is homoscedasticity?
3. What is heteroscedasticity?
4. What are residuals?
5. Why are residuals important?

### Intermediate

1. Explain the LINE assumptions.
2. Difference between confidence interval and prediction interval.
3. What is Cook's Distance?
4. What is leverage?
5. What is the Durbin-Watson test?

### Advanced

1. How do you detect heteroscedasticity?
2. How do you handle violated assumptions?
3. Explain hypothesis testing in Linear Regression.
4. Why doesn't multicollinearity affect Simple Linear Regression?
5. When would you reject a regression model?

---

# 30. Summary

- Linear Regression relies on the **LINE** assumptions: **Linearity, Independence, Normality, and Equal Variance**.
- Residual analysis is essential for validating model assumptions.
- Outliers, leverage points, and influential observations can significantly affect model performance.
- Hypothesis testing (t-test and F-test) helps determine the statistical significance of predictors.
- Confidence intervals estimate coefficient uncertainty, while prediction intervals estimate the range of future observations.
- Checking assumptions before interpreting results ensures reliable and trustworthy regression models.

---

# Key Takeaways

- **LINE = Linearity, Independence, Normality, Equal Variance**
- **Residuals = Actual − Predicted**
- **Homoscedasticity = Constant Residual Variance**
- **Heteroscedasticity = Changing Residual Variance**
- **Durbin-Watson ≈ 2 → No Autocorrelation**
- **Cook's Distance identifies influential observations**
- **Multicollinearity is not a concern in Simple Linear Regression**
- **p-value < 0.05 indicates statistical significance**
- **Confidence Interval estimates coefficients; Prediction Interval estimates future values**
- **Always validate assumptions before deploying a regression model**
