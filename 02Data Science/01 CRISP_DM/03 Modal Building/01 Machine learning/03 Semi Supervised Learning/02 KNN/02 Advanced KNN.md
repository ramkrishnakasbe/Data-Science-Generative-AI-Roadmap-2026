# 02 Advanced KNN.md

# 1. Introduction

Although KNN is simple to understand, its performance depends heavily on several important concepts such as **feature scaling**, **distance computation**, **choice of K**, **search algorithms**, and **hyperparameter tuning**.

This chapter covers the advanced concepts that make KNN practical for real-world applications.

---

# 2. Weighted KNN

## Definition

In standard KNN, all K neighbors contribute equally to the prediction.

In **Weighted KNN**, closer neighbors are given **higher importance**, while farther neighbors contribute less.

---

## Why Weighted KNN?

Consider

```
K = 5

Neighbor     Distance

A            0.2

A            0.3

B            3.5

B            4.1

B            4.5
```

Standard KNN

```
A = 2 votes

B = 3 votes

Prediction = B
```

This prediction is misleading because A points are much closer.

Weighted KNN gives more weight to nearby points.

Prediction becomes

```
A
```

---

## Common Weight Function

```
Weight = 1 / Distance
```

or

```
Weight = 1 / Distance²
```

Smaller distance

↓

Higher weight

---

## Advantages

- Better accuracy
- Reduces influence of distant neighbors
- Handles class overlap better

---

# 3. Feature Scaling

## Why Feature Scaling?

KNN uses **distance calculations**.

Features with larger values dominate the distance.

Example

| Feature | Value |
|----------|-------|
| Age | 25 |
| Salary | 800000 |

Salary dominates Euclidean distance.

---

## Without Scaling

```
Age      25

Salary   800000
```

Salary contributes much more.

Prediction becomes biased.

---

## With Scaling

```
Age      0.42

Salary   0.37
```

Both contribute equally.

---

## Common Scaling Techniques

### Standardization

```
z = (x-μ)/σ
```

Mean = 0

Standard Deviation = 1

---

### Min-Max Scaling

```
(x-min)/(max-min)
```

Range

```
0 to 1
```

---

### Robust Scaling

Uses

- Median
- IQR

Suitable for outliers.

---

# 4. Choosing Optimal K

Choosing K is one of the most important hyperparameters.

---

## Small K

Advantages

- Flexible
- Captures local patterns

Disadvantages

- Overfitting
- Sensitive to noise

---

## Large K

Advantages

- Stable
- Less noise

Disadvantages

- Underfitting
- Smooth decision boundary

---

## Rule of Thumb

```
K ≈ √N
```

Where

```
N = Number of Training Samples
```

---

## Best Method

Use **Cross Validation**.

---

# 5. Cross Validation

Cross Validation helps find the best K.

Example

```
K

↓

1

3

5

7

9

11

↓

Choose Highest Validation Accuracy
```

Most commonly

```
K-Fold Cross Validation
```

---

# 6. KNN for Regression

KNN is also used for regression.

Difference

Classification

↓

Majority Vote

Regression

↓

Average of K neighbors

Example

Nearest House Prices

```
40

42

45

43

44
```

Prediction

```
(40+42+45+43+44)/5

=

42.8
```

---

# 7. Time Complexity

Suppose

```
N

Training Samples

D

Features
```

Training

```
O(1)
```

Prediction

```
O(N × D)
```

Sorting

```
O(N log N)
```

Overall

```
O(ND)
```

---

# 8. Space Complexity

Entire training data must be stored.

```
Memory

=

O(N × D)
```

Large datasets require large memory.

---

# 9. Brute Force Search

Simplest implementation.

```
Query Point

↓

Distance with Every Point

↓

Sort

↓

Nearest Neighbor
```

Advantages

- Simple
- Accurate

Disadvantages

- Slow

---

# 10. KD Tree

## Definition

KD Tree (**K-Dimensional Tree**) is a binary tree used to speed up nearest-neighbor searches.

Instead of checking every point, the search space is divided into regions.

```
                Root
               /    \
          Left      Right
         /             \
     Region1         Region2
```

---

## Advantages

- Faster searching
- Efficient for low-dimensional data

---

## Limitations

Performance decreases in high dimensions.

---

# 11. Ball Tree

Instead of rectangles (KD Tree),

Ball Tree divides data into **hyperspheres (balls)**.

```
      (Ball)

   ***********
 *             *
*     Data      *
 *             *
   ***********
```

Advantages

- Better than KD Tree for higher dimensions.

---

# KD Tree vs Ball Tree

| KD Tree | Ball Tree |
|-----------|-----------|
| Hyper-rectangles | Hyperspheres |
| Better for low dimensions | Better for high dimensions |
| Faster in 2D/3D | Better beyond 20 dimensions |

---

# 12. Approximate Nearest Neighbor (ANN)

Searching every point is expensive.

ANN finds

```
Almost Nearest Neighbor
```

instead of

```
Exact Nearest Neighbor
```

Advantages

- Very fast
- Used in recommendation systems
- Used in image retrieval
- Used in vector databases

Libraries

- FAISS
- Annoy
- HNSW
- ScaNN

---

# 13. Handling Missing Values

Missing values cannot be used directly.

Methods

- Mean Imputation
- Median Imputation
- Mode Imputation
- KNN Imputation

---

# 14. Handling Categorical Features

Distance metrics like Euclidean are not suitable.

Possible approaches

- One-Hot Encoding
- Label Encoding
- Hamming Distance
- Gower Distance (mixed data)

---

# 15. Handling Outliers

KNN is sensitive to outliers.

Example

```
● ● ● ● ●

                     X
```

The outlier may become a neighbor.

Solutions

- Remove Outliers
- Robust Scaling
- Increase K
- Weighted KNN

---

# 16. Bias-Variance Tradeoff

Small K

```
Low Bias

High Variance
```

Large K

```
High Bias

Low Variance
```

Goal

Choose K that balances both.

---

# 17. Hyperparameters

| Hyperparameter | Description |
|---------------|-------------|
| n_neighbors | Number of neighbors |
| metric | Distance metric |
| weights | Uniform or Distance |
| algorithm | auto, kd_tree, ball_tree, brute |
| leaf_size | Tree search optimization |
| p | Minkowski parameter |

---

# 18. Choosing Distance Metric

| Data Type | Recommended Distance |
|------------|---------------------|
| Numerical | Euclidean |
| Numerical + Outliers | Manhattan |
| Binary | Hamming |
| Text | Cosine Similarity |
| Mixed | Gower Distance |

---

# 19. Advantages

- Easy to understand
- No training phase
- Supports multiclass classification
- Supports regression
- Easy to update
- Flexible decision boundaries

---

# 20. Disadvantages

- Slow prediction
- High memory usage
- Sensitive to scaling
- Sensitive to irrelevant features
- Suffers from curse of dimensionality
- Computationally expensive on large datasets

---

# 21. Interview Questions

### Why is Feature Scaling important in KNN?

Because KNN uses distance calculations, features with larger scales dominate the distance.

---

### Which scaling method is preferred?

- StandardScaler
- MinMaxScaler

depending on the dataset.

---

### Why use Weighted KNN?

Closer neighbors are usually more informative than distant neighbors.

---

### Why is KD Tree faster?

Because it avoids comparing the query point with every training sample.

---

### Difference between KD Tree and Ball Tree?

KD Tree partitions data using hyperplanes (rectangular regions), whereas Ball Tree partitions data using hyperspheres. Ball Trees generally perform better in higher-dimensional spaces.

---

### Can KNN handle regression?

Yes. It predicts the average (or weighted average) of the target values of the K nearest neighbors.

---

### Why is KNN slow?

During prediction, KNN computes distances from the query point to many or all training samples.

---

### How do you choose the best value of K?

Using **K-Fold Cross Validation** or Grid Search.

---

# 22. Summary

- **Weighted KNN** improves prediction by giving more importance to nearby neighbors.
- **Feature Scaling** is essential because KNN is distance-based.
- **Cross Validation** is the preferred method for selecting the optimal **K**.
- **KD Tree** and **Ball Tree** speed up nearest-neighbor searches.
- **KNN Regression** predicts the average of neighboring target values.
- KNN performs well on small to medium datasets but becomes computationally expensive for very large or high-dimensional datasets.
