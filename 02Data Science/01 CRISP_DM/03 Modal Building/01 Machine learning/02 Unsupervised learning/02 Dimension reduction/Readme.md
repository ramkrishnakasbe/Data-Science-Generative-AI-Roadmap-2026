# Dimension Reduction

# Overview

Dimension Reduction is a data preprocessing technique used to reduce the number of input features (dimensions) in a dataset while preserving as much useful information as possible.

It helps simplify complex datasets, reduce computational cost, remove redundant information, and improve model performance.

Dimension Reduction is widely used in:

- Machine Learning
- Deep Learning
- Data Visualization
- Image Processing
- Natural Language Processing
- Recommendation Systems

---

# Definition

Dimension Reduction is the process of transforming a high-dimensional dataset into a lower-dimensional dataset while retaining the important characteristics and patterns of the original data.

---

# Why Do We Need Dimension Reduction?

As the number of features increases, several challenges arise:

- Increased computational complexity
- Longer training time
- Higher memory consumption
- Overfitting
- Multicollinearity
- Curse of Dimensionality
- Difficult visualization
- Noisy and redundant features

Dimension Reduction helps overcome these challenges.

---

# Curse of Dimensionality

As the number of dimensions increases:

- Data becomes sparse.
- Distance calculations become less meaningful.
- Machine learning models require more data.
- Computational complexity increases.

Example

```
1 Dimension

--------

2 Dimensions

□□□□

3 Dimensions

Cube

100 Dimensions

Mostly Empty Space
```

---

# Objectives

- Reduce number of features
- Remove redundant information
- Remove correlated variables
- Improve model performance
- Faster training
- Better visualization
- Reduce overfitting

---

# Types of Dimension Reduction

There are two main approaches.

```
Dimension Reduction
        │
 ┌──────┴────────┐
 │               │
Feature       Feature
Selection     Extraction
```

---

# 1. Feature Selection

Feature Selection removes unnecessary features while keeping the original features unchanged.

No new features are created.

Example

Original Features

```
Age

Salary

Height

Weight

City
```

Selected Features

```
Age

Salary

Weight
```

---

## Advantages

- Easy to interpret
- Original features remain
- Faster training
- Reduced complexity

---

## Common Feature Selection Methods

### Filter Methods

Select features using statistical tests.

Examples

- Correlation
- Chi-Square Test
- ANOVA
- Information Gain
- Variance Threshold

---

### Wrapper Methods

Evaluate different feature subsets using machine learning models.

Examples

- Forward Selection
- Backward Elimination
- Recursive Feature Elimination (RFE)

---

### Embedded Methods

Feature selection occurs during model training.

Examples

- LASSO Regression
- Ridge Regression
- Decision Tree Feature Importance
- Random Forest Feature Importance

---

# 2. Feature Extraction

Feature Extraction creates new features by combining existing features.

Original features are transformed into a new feature space.

Example

```
100 Features

↓

20 New Features
```

---

## Advantages

- Removes redundancy
- Captures maximum information
- Handles correlated variables
- Better visualization

---

## Disadvantages

- New features are difficult to interpret.
- Original features are lost.

---

# Popular Dimension Reduction Techniques

## Principal Component Analysis (PCA)

Most widely used linear dimension reduction technique.

PCA transforms correlated variables into a smaller set of uncorrelated variables called **Principal Components**.

Characteristics

- Linear Technique
- Unsupervised
- Maximizes variance
- Removes multicollinearity
- Uses Eigenvalues and Eigenvectors

Applications

- Data Compression
- Face Recognition
- Image Processing
- Visualization

---

## Linear Discriminant Analysis (LDA)

LDA is a supervised dimension reduction technique.

Objective

Maximize class separation.

Applications

- Classification
- Face Recognition
- Medical Diagnosis

---

## Singular Value Decomposition (SVD)

Matrix decomposition technique.

Widely used in:

- Recommendation Systems
- NLP
- Text Mining
- Image Compression

---

## t-SNE (t-Distributed Stochastic Neighbor Embedding)

Non-linear dimension reduction algorithm.

Used primarily for visualization.

Characteristics

- Preserves local structure
- Excellent for high-dimensional visualization
- Computationally expensive

Applications

- Data Visualization
- Deep Learning Embeddings
- Gene Expression Analysis

---

## UMAP (Uniform Manifold Approximation and Projection)

Modern alternative to t-SNE.

Advantages

- Faster
- Better scalability
- Preserves both local and global structure

Applications

- Visualization
- Clustering
- NLP
- Image Embeddings

---

# PCA Workflow

```
Original Dataset

↓

Feature Scaling

↓

Covariance Matrix

↓

Eigenvalues

↓

Eigenvectors

↓

Principal Components

↓

Reduced Dataset
```

---

# Choosing the Number of Components

Common approaches:

- Explained Variance Ratio
- Cumulative Explained Variance
- Scree Plot
- Domain Knowledge

Typically,

```
95%

or

99%

Explained Variance
```

is retained.

---

# Advantages

- Reduces computation time
- Removes redundant features
- Reduces overfitting
- Improves visualization
- Removes multicollinearity
- Simplifies models

---

# Disadvantages

- Information loss
- Reduced interpretability
- PCA assumes linear relationships
- Some algorithms are computationally expensive

---

# Applications

- Customer Segmentation
- Image Compression
- Face Recognition
- Medical Imaging
- Text Mining
- Recommendation Systems
- Fraud Detection
- Genomics
- Speech Recognition

---

# Python Example (PCA)

```python
from sklearn.decomposition import PCA

pca = PCA(n_components=2)

X_pca = pca.fit_transform(X)
```

---

# Python Example (LDA)

```python
from sklearn.discriminant_analysis import LinearDiscriminantAnalysis

lda = LinearDiscriminantAnalysis(n_components=2)

X_lda = lda.fit_transform(X, y)
```

---

# Python Example (t-SNE)

```python
from sklearn.manifold import TSNE

tsne = TSNE(n_components=2)

X_tsne = tsne.fit_transform(X)
```

---

# Python Example (UMAP)

```python
import umap

reducer = umap.UMAP()

X_umap = reducer.fit_transform(X)
```

---

# Comparison of Dimension Reduction Techniques

| Technique | Type | Supervised | Linear | Primary Use |
|------------|------|------------|--------|-------------|
| PCA | Feature Extraction | No | Yes | Variance Maximization |
| LDA | Feature Extraction | Yes | Yes | Classification |
| SVD | Feature Extraction | No | Yes | Matrix Decomposition |
| t-SNE | Feature Extraction | No | No | Visualization |
| UMAP | Feature Extraction | No | No | Visualization & Clustering |

---

# Feature Selection vs Feature Extraction

| Feature Selection | Feature Extraction |
|-------------------|--------------------|
| Removes features | Creates new features |
| Original features remain | Original features transformed |
| Easy to interpret | Harder to interpret |
| Faster | More computationally intensive |
| No information transformation | Information is compressed |

---

# Interview Questions

## 1. What is Dimension Reduction?

Dimension Reduction is the process of reducing the number of features while preserving as much useful information as possible.

---

## 2. Why is Dimension Reduction required?

- Reduce computational cost
- Remove redundancy
- Reduce overfitting
- Improve visualization
- Handle curse of dimensionality

---

## 3. What is the difference between Feature Selection and Feature Extraction?

Feature Selection removes unnecessary features, whereas Feature Extraction creates new features by combining existing ones.

---

## 4. Is PCA supervised or unsupervised?

PCA is an **unsupervised** dimension reduction technique.

---

## 5. Why is PCA sensitive to feature scaling?

PCA is based on variance, so features with larger scales dominate the principal components if scaling is not applied.

---

## 6. What is the difference between PCA and LDA?

| PCA | LDA |
|------|-----|
| Unsupervised | Supervised |
| Maximizes variance | Maximizes class separation |
| Does not use target variable | Uses target variable |

---

## 7. Which technique is best for visualization?

- PCA (basic visualization)
- t-SNE
- UMAP

---

# Summary

Dimension Reduction is an essential preprocessing technique that simplifies high-dimensional datasets by reducing the number of features while preserving important information. It can be achieved through **Feature Selection**, which removes irrelevant features, or **Feature Extraction**, which creates new features from existing ones. Popular techniques such as **PCA**, **LDA**, **SVD**, **t-SNE**, and **UMAP** are widely used for improving model performance, reducing computational complexity, visualizing data, and overcoming the curse of dimensionality.
