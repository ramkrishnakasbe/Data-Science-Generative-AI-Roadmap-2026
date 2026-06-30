# Distance Measures

# Overview

Distance Measures are mathematical techniques used to quantify how similar or dissimilar two objects are. They form the foundation of many Machine Learning algorithms, especially **Unsupervised Learning**, where grouping similar observations is the primary objective.

Distance measures are widely used in:

- Clustering
- Classification (KNN)
- Recommendation Systems
- Anomaly Detection
- Information Retrieval
- Computer Vision
- Natural Language Processing

---

# What is Distance?

Distance is a numerical value that represents the dissimilarity between two observations.

- Smaller Distance → More Similar
- Larger Distance → Less Similar

Example

```
Person A : Age = 25

Person B : Age = 26

Distance = Small
```

```
Person A : Age = 25

Person B : Age = 70

Distance = Large
```

---

# Similarity vs Distance

| Similarity | Distance |
|------------|----------|
| Measures likeness | Measures dissimilarity |
| Larger value = More similar | Smaller value = More similar |
| Maximum indicates identical objects | Zero indicates identical objects |
| Example: Cosine Similarity | Example: Euclidean Distance |

---

# Why are Distance Measures Important?

Distance measures help us to:

- Group similar observations
- Identify nearest neighbors
- Detect outliers
- Build recommendation systems
- Measure similarity between documents
- Perform clustering
- Reduce dimensionality

---

# Properties of a Distance Metric

A valid distance metric should satisfy the following properties.

---

## 1. Non-Negativity

Distance can never be negative.

```
d(A,B) ≥ 0
```

Example

```
Distance = 5 ✔

Distance = -2 ✘
```

---

## 2. Identity of Indiscernibles

Distance between identical objects is zero.

```
d(A,A)=0
```

Example

```
Age = 25

Age = 25

Distance = 0
```

---

## 3. Symmetry

Distance remains the same irrespective of direction.

```
d(A,B)=d(B,A)
```

Example

```
Mumbai → Pune

=

Pune → Mumbai
```

---

## 4. Triangle Inequality

The shortest path between two points is the direct path.

```
d(A,C)

≤

d(A,B)+d(B,C)
```

---

# Types of Distance Calculation

Distance can be calculated between:

1. Record to Record
2. Group to Record
3. Group to Group

---

# 1. Record to Record Distance

Measures the distance between two individual observations.

Example

| Customer | Age | Salary |
|----------|-----|---------|
| A | 25 | 30000 |
| B | 30 | 35000 |

Distance

```
A ↔ B
```

### Common Methods

- Euclidean Distance
- Manhattan Distance
- Minkowski Distance
- Chebyshev Distance
- Cosine Distance
- Cosine Similarity
- Hamming Distance
- Mahalanobis Distance

Applications

- KNN
- K-Means
- DBSCAN

---

# 2. Group to Record Distance

Measures the distance between a cluster (group) and a new observation.

Example

```
Cluster

•

•

•

        New Record
              •

Distance

Cluster ↔ Record
```

### Methods

- Centroid Distance
- Medoid Distance
- Average Distance
- Nearest Neighbor
- Farthest Neighbor

Applications

- K-Means
- K-Medoids
- Cluster Assignment

---

# 3. Group to Group Distance

Measures the distance between two clusters.

Example

```
Cluster A

•••

        ↔

Cluster B

••••
```

### Methods

- Single Linkage
- Complete Linkage
- Average Linkage
- Centroid Linkage
- Ward's Method

Applications

- Hierarchical Clustering

---

# Choosing Distance Based on Data Type

Different data types require different distance measures.

```
Data Type
     │
     ├── Numerical
     ├── Categorical
     └── Mixed
```

---

# Distance Measures for Numerical Data

Numerical data contains continuous values.

Example

```
Age

Salary

Height

Weight
```

## Common Distance Measures

### Euclidean Distance

Most commonly used.

Measures straight-line distance.

Best for

- Continuous variables
- K-Means
- PCA

---

### Squared Euclidean Distance

Similar to Euclidean but squares the final distance.

Used in optimization.

---

### Manhattan Distance

Also called City Block Distance.

Measures horizontal and vertical movement.

Best for

- Grid-based movement
- High-dimensional data

---

### Minkowski Distance

Generalized form of Euclidean and Manhattan Distance.

Special Cases

```
p = 1

↓

Manhattan
```

```
p = 2

↓

Euclidean
```

---

### Chebyshev Distance

Maximum absolute difference between two dimensions.

Useful in board games and grid navigation.

---

### Mahalanobis Distance

Accounts for correlation between variables.

Useful for:

- Multivariate Outlier Detection
- Anomaly Detection

---

### Cosine Distance

Measures the angle between vectors.

Common in:

- NLP
- Text Mining
- Recommendation Systems

---

### Pearson Correlation Distance

Measures linear relationship between variables.

Common in:

- Recommendation Systems
- Time Series

---

# Distance Measures for Categorical Data

Categorical data contains labels instead of numbers.

Example

```
Gender

Color

Country

Department
```

---

## Hamming Distance

Counts the number of mismatched positions.

Best for

- Binary Data
- Strings

---

## Jaccard Distance

Measures dissimilarity between two sets.

Used for

- Market Basket Analysis
- Text Mining

---

## Dice Similarity

Measures overlap between two sets.

Similar to Jaccard but gives more weight to common elements.

---

## Simple Matching Coefficient (SMC)

Measures similarity considering both matches and mismatches.

---

## Overlap Coefficient

Measures overlap between two sets.

Useful for sparse datasets.

---

# Distance Measures for Mixed Data

Mixed data contains both numerical and categorical variables.

Example

| Age | Salary | Gender | City |
|-----|--------|--------|------|
| 25 | 35000 | Male | Pune |

---

## Why Can't Euclidean Distance Be Used?

Euclidean Distance only works correctly for numerical variables.

Categorical values cannot be directly subtracted.

---

## Gower Distance

Most popular distance measure for mixed datasets.

Supports

- Numerical Data
- Categorical Data
- Binary Data
- Ordinal Data

Widely used in customer segmentation.

---

## HEOM

(Heterogeneous Euclidean-Overlap Metric)

Supports both

- Numerical
- Categorical

---

## HVDM

(Heterogeneous Value Difference Metric)

Improved version of HEOM.

Handles mixed variables more effectively.

---

# Distance Measures Summary

| Data Type | Distance Measures |
|------------|------------------|
| Numerical | Euclidean, Manhattan, Minkowski, Chebyshev, Mahalanobis, Cosine, Pearson |
| Categorical | Hamming, Jaccard, Dice, SMC, Overlap |
| Mixed | Gower, HEOM, HVDM |

---

# Comparison of Popular Distance Measures

| Distance Measure | Data Type | Best Used In |
|------------------|-----------|--------------|
| Euclidean | Numerical | K-Means |
| Manhattan | Numerical | High-dimensional data |
| Minkowski | Numerical | Generalized distance |
| Chebyshev | Numerical | Grid movement |
| Mahalanobis | Numerical | Outlier Detection |
| Cosine | Numerical/Text | NLP |
| Hamming | Categorical | Binary Data |
| Jaccard | Categorical | Set Similarity |
| Dice | Categorical | Text Mining |
| Gower | Mixed | Customer Segmentation |

---

# Applications of Distance Measures

- K-Nearest Neighbors (KNN)
- K-Means Clustering
- Hierarchical Clustering
- DBSCAN
- Recommendation Systems
- Fraud Detection
- Image Recognition
- Natural Language Processing
- Market Basket Analysis
- Customer Segmentation

---

# Which Distance Measure Should You Choose?

| Scenario | Recommended Distance |
|-----------|----------------------|
| Continuous numerical data | Euclidean |
| High-dimensional numerical data | Manhattan |
| Correlated numerical features | Mahalanobis |
| Text documents | Cosine Similarity |
| Binary variables | Hamming |
| Set comparison | Jaccard |
| Mixed numerical & categorical data | Gower |
| Hierarchical clustering | Single, Complete, Average, Ward Linkage |

---

# Summary

Distance Measures are fundamental to many Machine Learning algorithms, especially clustering and nearest-neighbor methods. The choice of distance measure depends on the **type of data (numerical, categorical, or mixed)** and the **problem being solved**. Understanding distance properties, record-to-record, group-to-record, and group-to-group distances helps in selecting the most appropriate algorithm and producing meaningful clusters and similarity analyses.
