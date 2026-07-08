# Principal Component Analysis (PCA)

# Overview

Principal Component Analysis (PCA) is one of the most popular **Feature Extraction** and **Dimensionality Reduction** techniques in Machine Learning. It transforms a dataset with many correlated variables into a smaller set of **uncorrelated variables** called **Principal Components (PCs)** while preserving as much information (variance) as possible.

PCA is an **Unsupervised Learning** algorithm because it does not use the target variable during computation.

---

# Definition

Principal Component Analysis (PCA) is a statistical technique that converts a high-dimensional dataset into a lower-dimensional dataset by creating new variables (Principal Components) that capture the maximum variance in the data.

Instead of removing features, PCA creates **new features** that are linear combinations of the original features.

---

# Why PCA?

As the number of features increases:

- Training time increases.
- Memory usage increases.
- Models become more complex.
- Visualization becomes difficult.
- Multicollinearity increases.
- Overfitting may occur.
- Curse of dimensionality affects performance.

PCA helps solve these problems by reducing the number of dimensions while retaining most of the useful information.

---

# Objectives of PCA

- Reduce dimensionality.
- Preserve maximum information.
- Remove multicollinearity.
- Reduce noise.
- Improve computational efficiency.
- Improve visualization.
- Reduce overfitting.

---

# Characteristics

- Unsupervised Learning
- Linear Transformation Technique
- Feature Extraction Method
- Creates new features
- Maximizes variance
- Removes feature correlation
- Sensitive to feature scaling

---

# Intuition

Imagine you have customer data with:

- Age
- Salary
- Annual Spending

These variables may be highly correlated.

Instead of using all three features separately, PCA creates new variables (Principal Components) that summarize the information with fewer dimensions.

Example:

```
Original Features

Age
Salary
Spending

↓

PCA

↓

PC1
PC2
```

Most of the information from the three original features can often be represented using just two principal components.

---

# Curse of Dimensionality

As dimensions increase:

- Data becomes sparse.
- Distance calculations become less meaningful.
- More training samples are required.
- Models become computationally expensive.

Example:

```
1D → Line

2D → Square

3D → Cube

100D → Huge Sparse Space
```

PCA helps reduce the number of dimensions and mitigates this problem.

---

# Key Concepts

Before understanding PCA, you should know:

- Variance
- Covariance
- Covariance Matrix
- Eigenvalues
- Eigenvectors

---

# Variance

Variance measures how much a feature varies from its mean.

High variance means:

- Data is spread out.
- Contains more information.

Low variance means:

- Data is concentrated.
- Less information.

Formula

```
Variance = Σ(x − μ)² / n
```

Example

```
Data A

5 5 5 5 5

Variance = 0

---------------------

Data B

2 4 6 8 10

Variance = High
```

---

# Covariance

Covariance measures how two variables change together.

Positive Covariance

```
Age ↑

Salary ↑
```

Negative Covariance

```
Temperature ↑

Jacket Sales ↓
```

Zero Covariance

No relationship exists between variables.

Formula

```
Cov(X,Y)

=

Σ[(Xi-μx)(Yi-μy)] / (n-1)
```

---

# Covariance Matrix

For multiple variables, covariance values are organized into a matrix.

Example

```
          Age  Salary  Spending

Age         x

Salary

Spending
```

The diagonal contains variances, while the off-diagonal elements represent covariance between features.

PCA computes principal components from this covariance matrix.

---

# Feature Scaling

Feature scaling is essential before applying PCA because features with larger scales dominate the variance.

Example

```
Age

20-60

Salary

20,000-2,000,000
```

Salary has much larger values and would dominate the principal components.

Common scaling methods:

- StandardScaler ⭐ Recommended
- MinMaxScaler
- RobustScaler

Python

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()

X_scaled = scaler.fit_transform(X)
```

---

# Principal Components

Principal Components are new variables formed as linear combinations of the original features.

Properties:

- Uncorrelated with each other.
- Ordered by variance.
- PC1 captures the highest variance.
- PC2 captures the second-highest variance.
- PC3 captures the third-highest variance, and so on.

```
Original Features

X1
X2
X3

↓

PCA

↓

PC1
PC2
PC3
```

---

# Eigenvalues and Eigenvectors

PCA uses the covariance matrix to compute:

## Eigenvectors

- Represent the **direction** of maximum variance.
- Define the axes (Principal Components).

## Eigenvalues

- Represent the **amount of variance** captured along each eigenvector.
- Larger eigenvalues indicate more important principal components.

Example:

| Principal Component | Eigenvalue |
|---------------------|-----------:|
| PC1 | 8.2 |
| PC2 | 2.1 |
| PC3 | 0.4 |

Here, **PC1** explains the most variance and is the most informative.

---

# PCA Workflow

```
Original Dataset

↓

Handle Missing Values

↓

Feature Scaling

↓

Compute Covariance Matrix

↓

Calculate Eigenvalues & Eigenvectors

↓

Sort Eigenvalues (Descending)

↓

Select Top k Components

↓

Transform Original Data

↓

Reduced Dataset
```

---

# PCA Algorithm

1. Collect the dataset.
2. Handle missing values.
3. Standardize the features.
4. Compute the covariance matrix.
5. Calculate eigenvalues and eigenvectors.
6. Sort eigenvalues in descending order.
7. Select the top **k** principal components.
8. Project the original data onto the selected components.
9. Obtain the reduced dataset.

---

# Choosing the Number of Components

Common approaches:

## Explained Variance Ratio

Indicates how much variance each principal component explains.

Example

| PC | Explained Variance |
|----|-------------------:|
| PC1 | 60% |
| PC2 | 25% |
| PC3 | 10% |
| PC4 | 5% |

Using PC1 and PC2 retains **85%** of the total variance.

---

## Scree Plot

A Scree Plot displays eigenvalues against principal components.

```
Variance

|

|\
| \
|  \
|   \______

+------------------>

 PC1 PC2 PC3 PC4
```

The "elbow" in the plot often indicates the optimal number of components.

---

# Advantages

- Reduces dimensionality.
- Faster model training.
- Removes multicollinearity.
- Reduces noise.
- Improves visualization.
- Helps mitigate overfitting.
- Retains most of the important information.

---

# Disadvantages

- Loss of interpretability (new features are combinations of original ones).
- Some information is lost.
- Assumes linear relationships.
- Sensitive to feature scaling.
- Principal components may not have intuitive meanings.

---

# Applications

- Image Compression
- Face Recognition
- Recommendation Systems
- Gene Expression Analysis
- Finance
- Medical Data Analysis
- Data Visualization
- Fraud Detection
- Natural Language Processing

---

# Python Implementation (Scikit-learn)

```python
from sklearn.preprocessing import StandardScaler
from sklearn.decomposition import PCA

# Standardize data
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)

# Apply PCA
pca = PCA(n_components=2)

X_pca = pca.fit_transform(X_scaled)

print(X_pca.shape)
```

---

# Explained Variance in Python

```python
print(pca.explained_variance_ratio_)
```

Example Output

```
[0.72, 0.18]
```

This means:

- PC1 explains 72% of the variance.
- PC2 explains 18% of the variance.

Together, they retain **90%** of the dataset's information.

---

# PCA vs Feature Selection

| PCA | Feature Selection |
|------|-------------------|
| Creates new features | Keeps original features |
| Reduces dimensionality | Removes less useful features |
| Harder to interpret | Easier to interpret |
| Removes multicollinearity | May not remove multicollinearity |

---

# PCA vs LDA

| PCA | LDA |
|------|-----|
| Unsupervised | Supervised |
| Maximizes variance | Maximizes class separation |
| Does not use target variable | Uses target variable |
| Used for feature extraction | Used for feature extraction + classification |

---

# Interview Questions

## 1. What is PCA?

PCA is an unsupervised dimensionality reduction technique that transforms correlated features into a smaller set of uncorrelated principal components while preserving maximum variance.

---

## 2. Why is feature scaling important before PCA?

Because PCA is based on variance. Features with larger scales dominate the principal components if data is not standardized.

---

## 3. What are Principal Components?

Principal Components are new orthogonal features formed as linear combinations of the original features.

---

## 4. What is the difference between Eigenvalues and Eigenvectors?

- **Eigenvectors** determine the direction of the principal components.
- **Eigenvalues** indicate the amount of variance captured by each principal component.

---

## 5. Is PCA supervised or unsupervised?

PCA is an **Unsupervised Learning** algorithm because it does not use the target variable.

---

## 6. What is Explained Variance?

Explained Variance is the proportion of the dataset's total variance captured by each principal component.

---

## 7. What are the limitations of PCA?

- Information loss
- Reduced interpretability
- Assumes linear relationships
- Sensitive to scaling

---

# Summary

Principal Component Analysis (PCA) is one of the most widely used feature extraction techniques for reducing the dimensionality of high-dimensional datasets. It creates **orthogonal principal components** that capture the maximum variance while minimizing information loss. PCA improves computational efficiency, reduces multicollinearity, and enhances visualization, making it an essential preprocessing technique in Machine Learning, Data Science, and Artificial Intelligence.
