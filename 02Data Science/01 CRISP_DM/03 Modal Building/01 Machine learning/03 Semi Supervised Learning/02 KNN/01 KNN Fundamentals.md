# KNN Fundamentals

# 1. Introduction

## What is K-Nearest Neighbors (KNN)?

**K-Nearest Neighbors (KNN)** is a **Supervised Machine Learning algorithm** used for both **Classification** and **Regression** problems.

It predicts the output of a new data point by looking at the **K nearest training samples** based on a distance metric.

Unlike most machine learning algorithms, KNN **does not build a model during training**. Instead, it stores the training data and performs computations only during prediction.

Hence, it is called a **Lazy Learning Algorithm**.

---

## Example

Suppose we want to predict whether a new fruit is an **Apple** or an **Orange**.

Training Data

```
Apple     ● ● ●

Orange                ▲ ▲ ▲
```

New Fruit

```
Apple     ● ● ●
          ○

Orange                ▲ ▲ ▲
```

The new point (○) is closest to the Apple points.

Prediction

```
Apple
```

---

# 2. Why is it called K-Nearest Neighbors?

### K

Number of nearest neighbors considered.

Example

```
K = 3
```

Means

Look at the **3 nearest training samples**.

---

### Nearest

Nearest means **minimum distance** according to a chosen distance metric.

---

### Neighbors

Neighbor refers to nearby training observations.

---

# 3. Why is KNN called a Lazy Learner?

Most ML algorithms

```
Training
↓

Model

↓

Prediction
```

KNN

```
Training

↓

Store Dataset

↓

Prediction

↓

Compute Distances

↓

Return Result
```

No model is built during training.

Therefore,

KNN is called

- Lazy Learning
- Instance-Based Learning
- Memory-Based Learning

---

# 4. Characteristics of KNN

- Supervised Learning
- Non-parametric Algorithm
- Instance-based Learning
- Lazy Learning
- Simple to implement
- Supports Classification and Regression

---

# 5. Types of Problems Solved

## Classification

Output is categorical.

Examples

- Spam / Not Spam
- Disease / No Disease
- Cat / Dog

---

## Regression

Output is numerical.

Examples

- House Price
- Salary Prediction
- Temperature Prediction

---

# 6. Working of KNN

Suppose

```
K = 5
```

Prediction Steps

```
Step 1

Choose K

↓

Step 2

Compute distance from query point to every training sample

↓

Step 3

Sort distances

↓

Step 4

Select K nearest neighbors

↓

Step 5

Majority Voting (Classification)

OR

Average (Regression)

↓

Prediction
```

---

# 7. Choosing the Value of K

Choosing K is one of the most important decisions in KNN.

## Small K

Example

```
K = 1
```

Advantages

- Captures local patterns
- Flexible decision boundary

Disadvantages

- Sensitive to noise
- Overfitting

---

## Large K

Example

```
K = 25
```

Advantages

- Stable prediction
- Less sensitive to noise

Disadvantages

- Underfitting
- Ignores local patterns

---

### Rule of Thumb

```
K ≈ √N
```

Where

```
N = Number of training samples
```

Final K is usually selected using **Cross Validation**.

---

# 8. Majority Voting

Used for Classification.

Example

Nearest Neighbors

```
Apple

Apple

Orange

Apple

Orange
```

Votes

```
Apple = 3

Orange = 2
```

Prediction

```
Apple
```

---

# 9. Distance Metrics

KNN works by measuring similarity between data points.

Different metrics are used depending on the data type.

---

## Euclidean Distance

Most commonly used.

Formula

```
           ___________________________
d = √((x₂-x₁)² + (y₂-y₁)²)
```

Applications

- Numerical Data
- Continuous Variables

---

## Manhattan Distance

Also called

```
City Block Distance
```

Formula

```
d = |x₂-x₁| + |y₂-y₁|
```

Applications

- Grid-based movement
- Robust to outliers

---

## Minkowski Distance

Generalization of Euclidean and Manhattan.

Formula

```
             p
d = (Σ |xi-yi| )
      1/p
```

Special Cases

```
p = 1 → Manhattan

p = 2 → Euclidean
```

---

## Chebyshev Distance

Measures the maximum absolute difference.

Formula

```
max(|xi-yi|)
```

Applications

- Chess movement
- Warehouse optimization

---

## Hamming Distance

Used for categorical or binary data.

Measures number of positions where values differ.

Example

```
101100

111000
```

Different positions = 3

Distance = 3

---

## Cosine Similarity

Measures angle between two vectors.

Formula

```
A·B

-----------------

||A|| ||B||
```

Range

```
-1 to 1
```

Applications

- NLP
- Text Mining
- Recommendation Systems

---

# 10. Choosing Distance Metric

| Data Type | Distance |
|------------|----------|
| Numerical | Euclidean |
| Numerical with Outliers | Manhattan |
| Binary | Hamming |
| Text Data | Cosine Similarity |
| Mixed | Gower Distance (commonly used) |

---

# 11. Decision Boundary

Decision Boundary separates different classes.

### Small K

```
Complex Boundary

Overfitting
```

### Large K

```
Smooth Boundary

Underfitting
```

---

# 12. Curse of Dimensionality

As the number of features increases,

```
Distance between points becomes almost equal.
```

Therefore,

Nearest neighbors become difficult to identify.

Problems

- Lower accuracy
- Increased computation
- Sparse data
- Distance loses meaning

Solutions

- Feature Selection
- PCA
- LDA
- Feature Extraction
- Remove irrelevant features

---

# 13. Advantages

- Simple to understand
- No training phase
- Works for classification and regression
- Handles multiclass classification
- Easy to update with new data
- No assumptions about data distribution

---

# 14. Disadvantages

- Slow prediction
- High memory usage
- Sensitive to feature scaling
- Sensitive to irrelevant features
- Suffers from curse of dimensionality
- Poor performance on very large datasets

---

# 15. Applications

- Recommendation Systems
- Image Recognition
- Face Recognition
- Handwriting Recognition
- Medical Diagnosis
- Fraud Detection
- Customer Segmentation
- Document Classification
- Credit Risk Analysis

---

# 16. Complexity

Training

```
O(1)
```

(Only stores data)

Prediction

```
O(n × d)
```

Where

- n = Number of samples
- d = Number of features

Memory

```
O(n × d)
```

---

# 17. Interview Questions

### Why is KNN called a Lazy Learner?

Because it does not build a model during training. It stores the training data and performs computations only during prediction.

---

### Is KNN Parametric or Non-Parametric?

**Non-Parametric**, because it makes no assumptions about the underlying data distribution.

---

### Can KNN perform Regression?

Yes. In regression, KNN predicts the output by taking the **average (or weighted average)** of the K nearest neighbors.

---

### Why is Feature Scaling important in KNN?

KNN relies on distance calculations. Features with larger scales can dominate the distance, so scaling ensures all features contribute fairly.

---

### What happens when K = 1?

- Very sensitive to noise
- High variance
- Can overfit the training data

---

### What happens when K is very large?

- Smoother decision boundary
- Less sensitive to noise
- Higher bias
- Can underfit

---

### What is the Curse of Dimensionality?

As the number of features increases, distances between points become less meaningful, making it difficult for KNN to identify true nearest neighbors.

---

# 18. Summary

- KNN is a **supervised, non-parametric, instance-based learning algorithm**.
- It predicts using the **K nearest neighbors** based on a chosen **distance metric**.
- It supports both **classification** and **regression**.
- Common distance metrics include **Euclidean, Manhattan, Minkowski, Chebyshev, Hamming, and Cosine Similarity**.
- Choosing the right **K value**, applying **feature scaling**, and addressing the **curse of dimensionality** are critical for good performance.
- KNN is simple, intuitive, and widely used as a strong baseline algorithm in machine learning.
