# 01_Fundamentals_&_Mathematics.md

> **Level:** Beginner → Advanced
>
> **Prerequisites:** Basic Algebra, Statistics
>
> **Goal:** Understand the mathematical foundation of Simple Linear Regression, how it works, how the regression line is derived, and how predictions are made.

---

# Table of Contents

1. Introduction
2. What is Regression?
3. Why Regression?
4. Types of Regression
5. Simple Linear Regression
6. Terminologies
7. Regression Equation
8. Best Fit Line
9. Slope (Coefficient)
10. Intercept
11. Prediction
12. Real-world Examples
13. Assumptions of Best Fit Line
14. Cost Function
15. Sum of Squared Errors (SSE)
16. Mean Squared Error (MSE)
17. Root Mean Squared Error (RMSE)
18. Ordinary Least Squares (OLS)
19. How OLS Works
20. Gradient Descent
21. Learning Rate
22. Types of Gradient Descent
23. Normal Equation
24. Bias-Variance Tradeoff
25. Numerical Example
26. Advantages
27. Disadvantages
28. Summary

---

# 1. Introduction

Regression is one of the most fundamental supervised Machine Learning algorithms.

It is used to predict **continuous numerical values** by learning the relationship between an independent variable and a dependent variable.

Examples:

- Predict House Price
- Predict Salary
- Predict Temperature
- Predict Sales
- Predict Stock Price
- Predict Demand

---

# 2. What is Regression?

## Definition

Regression is a supervised learning technique used to predict a **continuous dependent variable** based on one or more independent variables.

Unlike classification, regression predicts numbers instead of categories.

Example

```
Experience (Years)

↓

Salary
```

Example

```
Advertising Budget

↓

Sales
```

---

# 3. Why Regression?

Regression helps us

- Predict future values
- Understand relationships between variables
- Estimate trends
- Forecast business metrics
- Support decision-making
- Identify important predictors

---

# 4. Types of Regression

| Regression | Description |
|------------|-------------|
| Simple Linear Regression | One Independent Variable |
| Multiple Linear Regression | Multiple Independent Variables |
| Polynomial Regression | Curved Relationship |
| Ridge Regression | L2 Regularization |
| Lasso Regression | L1 Regularization |
| Elastic Net | L1 + L2 |
| Logistic Regression | Classification |

---

# 5. What is Simple Linear Regression?

Simple Linear Regression predicts the value of one dependent variable using **one independent variable**.

It assumes a **linear relationship** between the variables.

Example

```
Study Hours

↓

Marks
```

```
Experience

↓

Salary
```

```
Area

↓

House Price
```

---

# 6. Terminologies

## Independent Variable (X)

Input feature used to predict the output.

Examples

- Experience
- Age
- Temperature
- Area

Also called

- Predictor
- Feature
- Input Variable
- Explanatory Variable

---

## Dependent Variable (Y)

Output that we want to predict.

Examples

- Salary
- House Price
- Sales
- Marks

Also called

- Target
- Response Variable
- Output Variable

---

## Observation

One row of data.

---

## Dataset

Collection of observations.

---

## Feature

Any input variable.

---

## Target

Variable to be predicted.

---

# 7. Regression Equation

Simple Linear Regression is represented as

```
Y = β₀ + β₁X
```

Where

```
Y

Dependent Variable

X

Independent Variable

β₀

Intercept

β₁

Slope (Coefficient)
```

Predicted value

```
Ŷ = β₀ + β₁X
```

---

# 8. Best Fit Line

The goal of Linear Regression is to find a line that minimizes prediction error.

```
        Y

        |

      *

    *

  *

*

-----------------------------> X
```

Regression Line

```
---------------------
```

This line is called

- Best Fit Line
- Regression Line

The algorithm tries to position this line such that the total prediction error is minimum.

---

# 9. Slope (β₁)

The slope tells us

> How much Y changes when X increases by one unit.

Formula

```
Slope

=

Change in Y

/

Change in X
```

Example

If

```
Slope = 5
```

Then

```
1 Year Experience

↓

Salary increases by 5 units
```

Interpretation

Positive Slope

```
X ↑

Y ↑
```

Negative Slope

```
X ↑

Y ↓
```

Zero Slope

```
No relationship
```

---

# 10. Intercept (β₀)

Intercept is the predicted value of Y when

```
X = 0
```

Example

```
Salary

=

20000

+

5000 × Experience
```

If

```
Experience = 0
```

Salary

```
20000
```

---

# 11. Prediction

Once the model is trained,

prediction becomes simple.

Example

Equation

```
Salary

=

25000

+

8000 × Experience
```

Suppose

```
Experience = 5
```

Prediction

```
25000

+

8000 × 5

=

65000
```

---

# 12. Real-world Examples

## House Price Prediction

```
Area

↓

Price
```

---

## Sales Forecasting

```
Advertisement Budget

↓

Sales
```

---

## Salary Prediction

```
Experience

↓

Salary
```

---

## Demand Forecasting

```
Historical Sales

↓

Future Demand
```

---

## Temperature Prediction

```
Time

↓

Temperature
```

---

# 13. Assumptions of Best Fit Line

The regression line should satisfy

- Linear Relationship
- Minimum Error
- Best Representation of Data

The complete statistical assumptions (LINE assumptions) are covered in the next file.

---

# 14. Cost Function

A model makes prediction errors.

The Cost Function measures how bad these errors are.

Objective

```
Find β₀ and β₁

such that

Cost is Minimum
```

---

# 15. Sum of Squared Errors (SSE)

Residual

```
Residual

=

Actual

-

Predicted
```

SSE

```
SSE

=

Σ

(Actual − Predicted)²
```

Why Square?

- Removes negative signs
- Penalizes large errors
- Easier mathematical optimization

Lower SSE indicates a better model.

---

# 16. Mean Squared Error (MSE)

Average squared error.

Formula

```
MSE

=

SSE

/

n
```

Properties

- Always non-negative
- Lower is better
- Sensitive to outliers

---

# 17. Root Mean Squared Error (RMSE)

Square root of MSE.

Formula

```
RMSE

=

√MSE
```

Advantages

- Same unit as target variable
- Easy to interpret
- Widely used

---

# 18. Ordinary Least Squares (OLS)

OLS is the most common method used to fit a regression line.

Goal

```
Find β₀ and β₁

that minimize

SSE
```

Instead of trying every possible line,

OLS computes the optimal line mathematically.

---

# 19. How OLS Works

Step 1

Guess a regression line.

↓

Step 2

Predict all observations.

↓

Step 3

Calculate residuals.

↓

Step 4

Square residuals.

↓

Step 5

Calculate SSE.

↓

Step 6

Adjust line until SSE is minimum.

---

# 20. Gradient Descent

Gradient Descent is an optimization algorithm used to minimize the Cost Function.

Idea

```
Current Cost

↓

Move towards

Lower Cost

↓

Repeat

↓

Minimum Cost
```

Steps

1. Initialize parameters.
2. Calculate predictions.
3. Compute cost.
4. Calculate gradients.
5. Update parameters.
6. Repeat until convergence.

---

# 21. Learning Rate

Learning Rate controls the step size during optimization.

Small Learning Rate

- Slow convergence
- More stable

Large Learning Rate

- Faster updates
- May overshoot the minimum

Choosing an appropriate learning rate is essential for efficient training.

---

# 22. Types of Gradient Descent

### Batch Gradient Descent

- Uses the entire dataset for each update.
- Stable but slower.

### Stochastic Gradient Descent (SGD)

- Updates parameters after each observation.
- Faster but noisier.

### Mini-Batch Gradient Descent

- Uses small batches of data.
- Most commonly used in practice.
- Balances speed and stability.

---

# 23. Normal Equation

The Normal Equation provides a direct mathematical solution for Linear Regression without iterative optimization.

Advantages

- Exact solution
- No learning rate required
- No iterations

Limitations

- Computationally expensive for very large datasets.

---

# 24. Bias-Variance Tradeoff

A good model balances **Bias** and **Variance**.

### High Bias

- Underfitting
- Poor performance on training and test data

### High Variance

- Overfitting
- Excellent training performance but poor generalization

Goal

```
Low Bias

+

Low Variance
```

---

# 25. Numerical Example

Dataset

| Experience | Salary |
|------------|--------|
| 1 | 30 |
| 2 | 35 |
| 3 | 40 |
| 4 | 45 |
| 5 | 50 |

Regression Equation

```
Salary = 25 + 5 × Experience
```

Prediction for

```
Experience = 6
```

```
Salary

=

25

+

5 × 6

=

55
```

---

# 26. Advantages

- Simple to understand
- Easy to implement
- Fast training
- Highly interpretable
- Works well for linear relationships
- Strong baseline model
- Widely used in business analytics

---

# 27. Disadvantages

- Assumes linear relationship
- Sensitive to outliers
- Affected by multicollinearity (in multiple regression)
- Cannot model complex nonlinear relationships
- Performance depends on assumptions being satisfied

---

# 28. Summary

- Simple Linear Regression predicts a continuous target using one independent variable.
- The model is represented by the equation **Ŷ = β₀ + β₁X**.
- **β₀** is the intercept and **β₁** is the slope.
- The **Best Fit Line** minimizes prediction error.
- **OLS** estimates the optimal regression line by minimizing the **Sum of Squared Errors (SSE)**.
- Common error metrics include **SSE**, **MSE**, and **RMSE**.
- **Gradient Descent** is an iterative optimization algorithm used to minimize the cost function.
- The **Normal Equation** provides a direct solution for model parameters.
- A good regression model achieves a balance between **Bias** and **Variance**.

---

# Key Takeaways

- **Regression predicts continuous values**
- **Simple Linear Regression uses one independent variable**
- **Regression Equation: Ŷ = β₀ + β₁X**
- **Slope represents the rate of change**
- **Intercept is the prediction when X = 0**
- **OLS minimizes SSE**
- **MSE and RMSE measure prediction error**
- **Gradient Descent minimizes the cost function iteratively**
- **Normal Equation computes parameters directly**
- **Understanding Bias–Variance Tradeoff is essential for building robust models**
```
