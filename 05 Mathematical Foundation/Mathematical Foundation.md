# Mathematical Foundations for Data Science

## Overview

Mathematical Foundations provide the core concepts required to understand how Data Science and Machine Learning algorithms work internally.

The most important areas are:

* Calculus
* Optimization
* Linear Algebra

These concepts are used in Linear Regression, Logistic Regression, Gradient Descent, Neural Networks, PCA, Support Vector Machines, Recommendation Systems, and Deep Learning.

---

# Table of Contents

1. Optimization
2. Slope, Rate of Change, and Derivatives
3. Slope of a Curve
4. Differentiation Rules
5. Local Maxima and Local Minima
6. Critical Values
7. First Derivative Test
8. Second Derivative Test
9. Linear Algebra
10. Matrix Operations
11. Eigenvalues and Eigenvectors
12. Applications in Data Science

---

# 1. Optimization

## Definition

Optimization is the process of finding the best possible value of a function under given conditions.

In Data Science, optimization is used to find the best model parameters, such as:

* Regression coefficients
* Neural network weights
* Bias values
* Hyperparameters
* Cluster centers

The function that needs to be optimized is called the **objective function**.

---

## Objective Function

An objective function measures how good or bad a solution is.

Examples:

```text
Loss Function
Cost Function
Error Function
Utility Function
Profit Function
Likelihood Function
```

---

## Minimization

Minimization means finding the smallest value of a function.

In Machine Learning, most algorithms try to minimize loss or error.

### Example: Mean Squared Error

```text
MSE = (1/n) × Σ(y - ŷ)²
```

Where:

```text
y  = Actual value
ŷ  = Predicted value
n  = Number of observations
```

The goal of Linear Regression is to find parameter values that minimize MSE.

---

## Maximization

Maximization means finding the largest value of a function.

Examples:

* Maximize profit
* Maximize accuracy
* Maximize customer retention
* Maximize likelihood
* Maximize revenue

### Example

```text
Maximize Profit = Revenue - Cost
```

---

## Global and Local Optimum

### Global Minimum

The lowest value across the complete function.

### Local Minimum

The lowest value only within a nearby region.

### Global Maximum

The highest value across the complete function.

### Local Maximum

The highest value only within a nearby region.

---

## Optimization in Machine Learning

| Algorithm           | Optimization Goal                      |
| ------------------- | -------------------------------------- |
| Linear Regression   | Minimize MSE                           |
| Logistic Regression | Minimize Log Loss                      |
| K-Means             | Minimize Within-Cluster Sum of Squares |
| SVM                 | Maximize Margin / Minimize Hinge Loss  |
| Neural Networks     | Minimize Loss Function                 |
| PCA                 | Maximize Variance                      |

---

# 2. Slope, Rate of Change, and Derivatives

## Slope

Slope measures the change in one variable relative to the change in another variable.

For a straight line:

```text
Slope = Change in y / Change in x
```

```text
m = Δy / Δx
```

Where:

```text
Δy = Change in y
Δx = Change in x
```

---

## Interpretation of Slope

| Slope Value     | Meaning                    |
| --------------- | -------------------------- |
| Positive        | y increases as x increases |
| Negative        | y decreases as x increases |
| Zero            | y does not change          |
| Large magnitude | Steep line                 |
| Small magnitude | Flat line                  |

---

## Rate of Change

Rate of change explains how one quantity changes with respect to another quantity.

### Examples

```text
Speed = Change in Distance / Change in Time
```

```text
Growth Rate = Change in Population / Change in Time
```

```text
Revenue Growth = Change in Revenue / Change in Time
```

---

## Derivative

A derivative measures the instantaneous rate of change of a function.

For:

```text
y = f(x)
```

The derivative is written as:

```text
f'(x)
```

or:

```text
dy/dx
```

The derivative tells us:

* Whether a function is increasing or decreasing
* How quickly the function changes
* The slope of a curve at a specific point
* Where maximum and minimum values may occur

---

# 3. Slope of a Curve

For a straight line, slope is constant.

For a curve, slope changes at each point.

The average rate of change between two points is:

```text
[f(x + Δx) - f(x)] / Δx
```

To find the exact slope at one point, make `Δx` extremely small.

```text
f'(x) = lim Δx→0 [f(x + Δx) - f(x)] / Δx
```

This is called the **limit definition of derivative**.

---

## Example

```text
f(x) = x²
```

Using the derivative rule:

```text
f'(x) = 2x
```

At:

```text
x = 3
```

```text
f'(3) = 2 × 3 = 6
```

Therefore, the slope of `y = x²` at `x = 3` is `6`.

---

# 4. Differentiation Rules

Differentiation rules make it easier to calculate derivatives without using the limit definition every time.

---

## 4.1 Power Rule

For:

```text
f(x) = xⁿ
```

```text
f'(x) = n × xⁿ⁻¹
```

### Examples

```text
f(x) = x³
f'(x) = 3x²
```

```text
f(x) = x⁵
f'(x) = 5x⁴
```

```text
f(x) = x
f'(x) = 1
```

---

## 4.2 Constant Rule

The derivative of a constant is zero.

```text
f(x) = c
```

```text
f'(x) = 0
```

### Example

```text
f(x) = 25
f'(x) = 0
```

---

## 4.3 Constant Multiple Rule

If a function is multiplied by a constant:

```text
f(x) = c × g(x)
```

Then:

```text
f'(x) = c × g'(x)
```

### Example

```text
f(x) = 5x³
f'(x) = 5 × 3x²
f'(x) = 15x²
```

---

## 4.4 Sum Rule

```text
d/dx [f(x) + g(x)] = f'(x) + g'(x)
```

### Example

```text
f(x) = x² + x³
```

```text
f'(x) = 2x + 3x²
```

---

## 4.5 Difference Rule

```text
d/dx [f(x) - g(x)] = f'(x) - g'(x)
```

### Example

```text
f(x) = x³ - x²
```

```text
f'(x) = 3x² - 2x
```

---

## 4.6 Product Rule

Used when two functions are multiplied.

```text
d/dx [f(x) × g(x)] = f(x)g'(x) + g(x)f'(x)
```

### Example

```text
h(x) = x²(x + 1)
```

Let:

```text
f(x) = x²
g(x) = x + 1
```

Then:

```text
f'(x) = 2x
g'(x) = 1
```

```text
h'(x) = x²(1) + (x + 1)(2x)
```

```text
h'(x) = x² + 2x² + 2x
```

```text
h'(x) = 3x² + 2x
```

---

## 4.7 Quotient Rule

Used when one function is divided by another.

```text
d/dx [f(x) / g(x)] =
[g(x)f'(x) - f(x)g'(x)] / [g(x)]²
```

### Example

```text
h(x) = x² / (x + 1)
```

Let:

```text
f(x) = x²
g(x) = x + 1
```

Then:

```text
f'(x) = 2x
g'(x) = 1
```

```text
h'(x) = [(x + 1)(2x) - x²(1)] / (x + 1)²
```

```text
h'(x) = [2x² + 2x - x²] / (x + 1)²
```

```text
h'(x) = [x² + 2x] / (x + 1)²
```

---

# 5. Relative Maximum and Relative Minimum

## Relative Maximum / Local Maximum

A local maximum is a point where the function value is greater than nearby values.

At a possible local maximum:

```text
f'(x) = 0
```

The slope changes from:

```text
Positive → Negative
```

This means the function increases and then decreases.

---

## Relative Minimum / Local Minimum

A local minimum is a point where the function value is smaller than nearby values.

At a possible local minimum:

```text
f'(x) = 0
```

The slope changes from:

```text
Negative → Positive
```

This means the function decreases and then increases.

---

## Important Note

```text
f'(x) = 0
```

does not always mean maximum or minimum.

It may also be:

* Saddle Point
* Flat Point
* Inflection Point

Therefore, derivative tests are required.

---

# 6. Critical Values

A critical value is an `x` value where:

```text
f'(x) = 0
```

or:

```text
f'(x) does not exist
```

Critical values are possible points for:

* Local Maximum
* Local Minimum
* Turning Point
* Saddle Point

---

## Example

```text
f(x) = x² - 4x + 3
```

First derivative:

```text
f'(x) = 2x - 4
```

Set derivative equal to zero:

```text
2x - 4 = 0
```

```text
x = 2
```

Therefore, `x = 2` is a critical value.

---

# 7. First Derivative Test

The First Derivative Test identifies whether a critical value is a local maximum or local minimum.

## Steps

1. Find the first derivative `f'(x)`.
2. Find critical values.
3. Choose values before and after each critical value.
4. Check whether the sign of `f'(x)` changes.

| Before Critical Point | After Critical Point | Result                |
| --------------------- | -------------------- | --------------------- |
| Positive              | Negative             | Local Maximum         |
| Negative              | Positive             | Local Minimum         |
| Positive              | Positive             | No Maximum or Minimum |
| Negative              | Negative             | No Maximum or Minimum |

---

## Example

```text
f(x) = x² - 4x + 3
```

```text
f'(x) = 2x - 4
```

Critical value:

```text
x = 2
```

Test values:

```text
x = 1 → f'(1) = -2
x = 3 → f'(3) = 2
```

The derivative changes:

```text
Negative → Positive
```

Therefore:

```text
x = 2 is a Local Minimum
```

---

# 8. Second Derivative Test

The Second Derivative Test uses the second derivative to classify critical points.

## Steps

1. Find `f'(x)`.
2. Find critical values where `f'(x) = 0`.
3. Find `f''(x)`.
4. Substitute critical values into `f''(x)`.

| Condition  | Meaning              |
| ---------- | -------------------- |
| f''(x) > 0 | Local Minimum        |
| f''(x) < 0 | Local Maximum        |
| f''(x) = 0 | Test is inconclusive |

---

## Example

```text
f(x) = x² - 4x + 3
```

```text
f'(x) = 2x - 4
```

```text
f''(x) = 2
```

At:

```text
x = 2
```

```text
f''(2) = 2 > 0
```

Therefore:

```text
x = 2 is a Local Minimum
```

---

# 9. Linear Algebra

Linear Algebra is the branch of mathematics that studies vectors, matrices, and transformations.

It is essential because Data Science datasets, model parameters, and neural-network computations are represented using vectors and matrices.

---

## Scalar

A scalar is a single numerical value.

Examples:

```text
5
-2
3.14
```

Data Science examples:

```text
Learning Rate = 0.01
Accuracy = 0.92
Loss = 0.45
```

---

## Vector

A vector is an ordered collection of numbers.

```text
v = [2, 4, 6]
```

A vector may represent one data record.

```text
Customer = [Age, Income, SpendingScore]
```

Example:

```text
Customer = [30, 50000, 75]
```

---

## Matrix

A matrix is a rectangular arrangement of values in rows and columns.

```text
A = [ [1, 2],
      [3, 4] ]
```

In Data Science:

```text
Rows = Observations
Columns = Features
```

Example dataset:

```text
X = [ [25, 40000],
      [30, 55000],
      [35, 70000] ]
```

Where:

```text
Column 1 = Age
Column 2 = Income
```

---

# 10. Matrix Operations

## Matrix Addition

Matrices can be added only when they have the same dimensions.

```text
A + B
```

Example:

```text
A = [ [1, 2],
      [3, 4] ]

B = [ [5, 6],
      [7, 8] ]
```

```text
A + B = [ [6, 8],
          [10, 12] ]
```

---

## Scalar Multiplication

A scalar can multiply every value in a matrix.

```text
2A
```

Example:

```text
A = [ [1, 2],
      [3, 4] ]
```

```text
2A = [ [2, 4],
       [6, 8] ]
```

---

## Matrix Transpose

Transpose converts rows into columns.

```text
Aᵀ
```

Example:

```text
A = [ [1, 2],
      [3, 4],
      [5, 6] ]
```

```text
Aᵀ = [ [1, 3, 5],
       [2, 4, 6] ]
```

---

## Matrix Multiplication

Matrix multiplication is possible when:

```text
Columns of A = Rows of B
```

If:

```text
A = m × n
B = n × p
```

Then:

```text
AB = m × p
```

Example:

```text
A = [ [1, 2],
      [3, 4] ]

B = [ [5, 6],
      [7, 8] ]
```

```text
AB = [ [19, 22],
       [43, 50] ]
```

Important:

```text
AB ≠ BA
```

in most cases.

---

## Identity Matrix

An identity matrix has:

```text
1 on diagonal
0 everywhere else
```

Example:

```text
I = [ [1, 0],
      [0, 1] ]
```

Property:

```text
AI = IA = A
```

---

## Matrix Inverse

The inverse of a matrix is written as:

```text
A⁻¹
```

For an invertible matrix:

```text
AA⁻¹ = A⁻¹A = I
```

A matrix must be:

* Square
* Non-singular
* Have determinant not equal to zero

```text
det(A) ≠ 0
```

For a 2 × 2 matrix:

```text
A = [ [a, b],
      [c, d] ]
```

```text
A⁻¹ = 1 / (ad - bc)
      [ [ d, -b],
        [-c,  a] ]
```

Matrix inverse is used in:

* Linear Regression
* Solving systems of equations
* Matrix transformations

---

## Orthogonal Matrix

A square matrix `A` is orthogonal when:

```text
AᵀA = AAᵀ = I
```

### Property 1: Transpose Equals Inverse

```text
A⁻¹ = Aᵀ
```

### Property 2: Rows and Columns Are Orthonormal

* Each row/column has length `1`.
* Different rows/columns have dot product `0`.

```text
u · v = 0
```

Orthogonal matrices preserve:

* Length
* Angles
* Distance

Applications:

* PCA
* Rotations
* QR Decomposition
* Numerical stability

---

# 11. Eigenvalues and Eigenvectors

## Definition

For a square matrix `A`, an eigenvector `v` and eigenvalue `λ` satisfy:

```text
Av = λv
```

Where:

```text
A = Transformation Matrix
v = Eigenvector
λ = Eigenvalue
```

An eigenvector keeps its direction after transformation, while its magnitude may change.

---

## Finding Eigenvalues

Starting with:

```text
Av = λv
```

```text
Av - λv = 0
```

```text
(A - λI)v = 0
```

For a non-zero vector `v`:

```text
det(A - λI) = 0
```

This equation is called the **characteristic equation**.

---

## Example

```text
A = [ [2, 0],
      [0, 3] ]
```

Eigenvalues:

```text
λ₁ = 2
λ₂ = 3
```

Eigenvectors:

```text
v₁ = [1, 0]
v₂ = [0, 1]
```

---

## Applications of Eigenvalues and Eigenvectors

* Principal Component Analysis (PCA)
* Dimensionality Reduction
* Image Compression
* Recommendation Systems
* Spectral Clustering
* Google PageRank
* Markov Chains

---

# 12. Mathematical Foundations in Data Science

| Concept               | Data Science Application |
| --------------------- | ------------------------ |
| Derivative            | Gradient Descent         |
| Partial Derivative    | Neural Networks          |
| Optimization          | Loss Minimization        |
| Vector                | Feature Representation   |
| Matrix                | Dataset Representation   |
| Matrix Multiplication | Neural Network Layers    |
| Matrix Inverse        | Linear Regression        |
| Eigenvalues           | PCA                      |
| Eigenvectors          | Principal Components     |
| Orthogonal Matrix     | PCA and Rotations        |

---

# Recommended Learning Order

1. Functions and Graphs
2. Slope and Rate of Change
3. Derivatives
4. Differentiation Rules
5. Maxima and Minima
6. Optimization
7. Scalars, Vectors, and Matrices
8. Matrix Operations
9. Eigenvalues and Eigenvectors
10. Gradient Descent
11. Partial Derivatives
12. PCA

---

# Summary

Calculus helps measure change and optimize machine learning models. Derivatives help identify the direction in which model parameters should move to reduce loss. Linear Algebra helps represent datasets and perform efficient calculations using vectors and matrices.

Together, Calculus, Optimization, and Linear Algebra form the mathematical foundation for Machine Learning, Deep Learning, PCA, Regression, Neural Networks, and many other Data Science techniques.
