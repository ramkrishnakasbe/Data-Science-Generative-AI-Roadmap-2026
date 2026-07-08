# Singular Value Decomposition (SVD)

# Overview

Singular Value Decomposition (SVD) is one of the most powerful **matrix decomposition** and **feature extraction** techniques in Machine Learning, Data Science, and Linear Algebra.

It decomposes a matrix into three simpler matrices, making it easier to analyze, compress, and extract meaningful information from high-dimensional data.

SVD is widely used in:

- Recommendation Systems (Netflix, Amazon)
- Image Compression
- Natural Language Processing (LSA)
- Face Recognition
- Data Compression
- Noise Reduction
- Dimensionality Reduction

---

# Definition

Singular Value Decomposition (SVD) is a matrix factorization technique that decomposes any matrix **A** into three matrices:

```
A = U Σ Vᵀ
```

Where:

- **U** → Left Singular Vectors
- **Σ (Sigma)** → Singular Values
- **Vᵀ** → Right Singular Vectors (Transpose)

Unlike PCA, SVD can be applied directly to any rectangular matrix.

---

# Why SVD?

Large datasets often contain:

- Redundant information
- Correlated features
- Noise
- High dimensionality

SVD helps by:

- Reducing dimensions
- Compressing data
- Removing noise
- Identifying hidden patterns
- Improving computational efficiency

---

# Characteristics

- Linear Algebra Technique
- Matrix Factorization Method
- Feature Extraction Technique
- Works for any matrix
- Can handle sparse matrices
- Basis of many recommendation systems
- Foundation for Latent Semantic Analysis (LSA)

---

# Matrix Decomposition

Instead of working with one large matrix,

```
A
```

SVD breaks it into

```
A = U Σ Vᵀ
```

This decomposition makes mathematical operations easier and reveals hidden relationships in the data.

---

# Components of SVD

```
          A

          ↓

    ┌───────────────┐
    │               │
    │   U Σ Vᵀ      │
    │               │
    └───────────────┘
```

---

# Matrix U (Left Singular Vectors)

Represents the relationships between observations (rows).

Properties:

- Orthogonal matrix
- Columns are orthonormal vectors
- Represents row space

Example

```
U

[ u₁ u₂ u₃ ]
```

---

# Sigma (Σ)

Sigma contains the **Singular Values**.

```
Σ

σ₁   0    0

0    σ₂   0

0     0   σ₃
```

Characteristics

- Diagonal matrix
- Singular values are non-negative
- Ordered from largest to smallest

```
σ₁ ≥ σ₂ ≥ σ₃
```

Larger singular values represent more important information.

---

# Matrix Vᵀ (Right Singular Vectors)

Represents the relationships between features (columns).

Properties

- Orthogonal matrix
- Columns are orthonormal
- Represents feature directions

---

# Understanding Singular Values

Singular values indicate how much information each component contains.

Example

```
σ₁ = 120

σ₂ = 40

σ₃ = 5
```

Interpretation

- First component contains most information.
- Third component contributes very little.

Therefore,

Small singular values can often be discarded.

---

# SVD Workflow

```
Original Matrix

↓

Matrix Decomposition

↓

U

Σ

Vᵀ

↓

Keep Top Singular Values

↓

Reduced Matrix
```

---

# Truncated SVD

Instead of using all singular values,

Keep only the largest **k** singular values.

Example

```
Original

σ₁

σ₂

σ₃

σ₄

σ₅
```

Keep

```
σ₁

σ₂
```

This significantly reduces dimensionality while preserving most information.

---

# Reduced SVD

Reduced SVD stores only the most important singular vectors.

Advantages

- Lower memory usage
- Faster computation
- Better scalability
- Efficient storage

---

# Mathematical Representation

For any matrix

```
A(m × n)
```

SVD decomposes it as

```
A = U Σ Vᵀ
```

Where

```
U

=

m × m

Σ

=

m × n

Vᵀ

=

n × n
```

For Reduced SVD

```
U

=

m × k

Σ

=

k × k

Vᵀ

=

k × n
```

---

# Example

Suppose

```
A

=

1 2

3 4

5 6
```

Applying SVD gives

```
A

=

U

×

Σ

×

Vᵀ
```

Instead of storing all information,

we may keep only

```
σ₁

σ₂
```

and discard smaller singular values.

This reduces storage while maintaining most of the important structure.

---

# SVD vs PCA

Although closely related, they are not identical.

| PCA | SVD |
|------|-----|
| Feature Extraction | Matrix Factorization |
| Uses Covariance Matrix | Uses Original Matrix |
| Eigenvalues & Eigenvectors | Singular Values & Singular Vectors |
| Requires Feature Scaling | Often works directly on data |
| Mainly for Dimensionality Reduction | Used for Decomposition & Dimensionality Reduction |

---

# SVD vs Eigen Decomposition

| Eigen Decomposition | SVD |
|---------------------|-----|
| Only Square Matrix | Any Matrix |
| Uses Eigenvalues | Uses Singular Values |
| May produce complex values | Always real, non-negative singular values |
| Limited applications | Broad applications |

---

# Advantages

- Works on any matrix
- Excellent for sparse data
- Reduces dimensionality
- Removes redundancy
- Noise reduction
- Efficient data compression
- Improves computational performance

---

# Disadvantages

- Computationally expensive for very large matrices
- Difficult mathematical interpretation
- Information loss if too many components are removed
- Less interpretable than original features

---

# Applications

## Recommendation Systems

Netflix

Amazon

Spotify

MovieLens

Predict user preferences using latent factors.

---

## Natural Language Processing

Latent Semantic Analysis (LSA)

Document similarity

Topic modeling

Semantic search

---

## Image Compression

Compress images by keeping only the largest singular values.

Benefits

- Smaller file size
- Minimal quality loss

---

## Face Recognition

Represent faces using fewer dimensions while preserving key facial features.

---

## Noise Reduction

Remove small singular values that mainly represent noise.

---

## Data Compression

Store only important singular values and vectors to reduce memory requirements.

---

# Python Implementation (NumPy)

```python
import numpy as np

A = np.array([
    [1,2],
    [3,4],
    [5,6]
])

U, S, VT = np.linalg.svd(A)

print(U)
print(S)
print(VT)
```

---

# Python Implementation (Scikit-learn)

```python
from sklearn.decomposition import TruncatedSVD

svd = TruncatedSVD(n_components=2)

X_reduced = svd.fit_transform(X)

print(X_reduced.shape)
```

---

# Important Parameters

| Parameter | Description |
|-----------|-------------|
| n_components | Number of singular vectors to retain |
| algorithm | SVD computation algorithm |
| random_state | Reproducibility |

---

# Choosing Number of Components

Common approaches

- Explained Variance
- Cumulative Variance
- Domain Knowledge
- Cross Validation

Typically,

retain enough components to explain

```
90%

95%

99%
```

of the variance.

---

# Time Complexity

For matrix

```
m × n
```

Time Complexity

```
O(mn²)

or

O(n³)

depending on implementation
```

---

# Interview Questions

## 1. What is SVD?

SVD is a matrix decomposition technique that decomposes a matrix into **U, Σ, and Vᵀ**.

---

## 2. What are Singular Values?

Singular values represent the importance (amount of information) captured by each latent component.

---

## 3. Why is SVD preferred over Eigen Decomposition?

Because SVD works for **any matrix**, whereas Eigen Decomposition requires a square matrix.

---

## 4. Where is SVD used?

- Recommendation Systems
- NLP
- Image Compression
- Face Recognition
- Feature Extraction
- Noise Reduction

---

## 5. What is Truncated SVD?

A dimensionality reduction technique that keeps only the largest singular values and their corresponding vectors.

---

## 6. What is the difference between PCA and SVD?

PCA performs dimensionality reduction using the covariance matrix and eigen decomposition, whereas SVD directly factorizes the original data matrix into **U**, **Σ**, and **Vᵀ**. PCA can be efficiently implemented using SVD.

---

# Summary

Singular Value Decomposition (SVD) is a powerful matrix factorization technique that decomposes a matrix into **U**, **Σ**, and **Vᵀ**. It is widely used for **dimensionality reduction**, **feature extraction**, **data compression**, **noise reduction**, and **recommendation systems**. By retaining only the largest singular values, SVD efficiently represents high-dimensional data while preserving most of its important information, making it a fundamental tool in Machine Learning, Data Science, and Artificial Intelligence.
