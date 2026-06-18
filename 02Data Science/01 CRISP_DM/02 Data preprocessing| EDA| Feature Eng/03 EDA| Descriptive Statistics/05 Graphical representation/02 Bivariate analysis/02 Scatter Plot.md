## 1. Scatter Plot

### Definition

A Scatter Plot visualizes the relationship between two numerical variables by representing observations as points on a two-dimensional plane.

### Primary Purpose

#### 1. Direction of Relationship

Determine whether variables move in the same or opposite direction.

* Positive Relationship (+)
* Negative Relationship (-)
* No Relationship

#### 2. Strength of Relationship

Understand how strongly the variables are associated.

* Strong
* Moderate
* Weak

#### 3. Form of Relationship

* Linear Relationship
* Non-Linear Relationship

### Secondary Purpose

#### 1. Identify Outliers

Points that lie far away from the overall pattern.

#### 2. Identify Clusters

Groups of observations that naturally form distinct patterns.

#### 3. Detect Data Patterns

Reveal trends, gaps, and unusual structures in the data.

### Example Use Cases

* Advertising Spend vs Sales
* Experience vs Salary
* Study Hours vs Exam Score

### Disadvantage

The strength of a relationship observed in a scatter plot is often subjective and depends on visual interpretation.

Different analysts may interpret the same plot differently.

### Solution

Use statistical measures to quantify the relationship.

#### Covariance

Measures the direction of the relationship between two variables.

* Positive Covariance → Variables move together.
* Negative Covariance → Variables move in opposite directions.

Limitation:

* Magnitude is difficult to interpret.
* Depends on measurement units.

#### Correlation

Measures both direction and strength of the relationship.

##### Correlation Coefficient (r)

```text
-1 ≤ r ≤ +1
```

| r Value       | Interpretation                |
| ------------- | ----------------------------- |
| +1            | Perfect Positive Correlation  |
| +0.7 to +0.99 | Strong Positive Correlation   |
| +0.3 to +0.69 | Moderate Positive Correlation |
| 0             | No Correlation                |
| -0.3 to -0.69 | Moderate Negative Correlation |
| -0.7 to -0.99 | Strong Negative Correlation   |
| -1            | Perfect Negative Correlation  |

### Key Takeaway

Scatter Plots provide a visual understanding of:

* Direction of relationship
* Strength of relationship
* Linear or Non-linear patterns
* Outliers
* Clusters

Since visual assessment can be subjective, it is recommended to validate findings using Covariance and Correlation Coefficient (r).
