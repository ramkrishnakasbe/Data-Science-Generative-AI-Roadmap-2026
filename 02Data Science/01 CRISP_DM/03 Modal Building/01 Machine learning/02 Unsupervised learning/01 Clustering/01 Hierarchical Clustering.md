# Hierarchical Clustering

# Overview

Hierarchical Clustering is an **Unsupervised Machine Learning** algorithm that groups similar observations into clusters by creating a hierarchy of clusters. Unlike K-Means, it **does not require specifying the number of clusters (K) before training**.

The result is represented using a **Dendrogram**, a tree-like structure that illustrates how clusters are formed or divided at each stage.

Hierarchical clustering is widely used in:

- Customer Segmentation
- Gene Expression Analysis
- Document Clustering
- Image Segmentation
- Market Basket Analysis
- Social Network Analysis

---

# Definition

Hierarchical Clustering is a clustering technique that recursively merges or splits clusters based on similarity until a stopping criterion is reached.

Unlike partition-based clustering, it creates a **hierarchical relationship** among clusters rather than a flat partition.

---

# Intuition

Imagine organizing books in a library.

Initially, every book is separate.

```
Book1   Book2   Book3   Book4
```

You start grouping similar books together.

```
(Book1 Book2)

(Book3 Book4)
```

Finally,

```
((Book1 Book2) (Book3 Book4))
```

This gradual merging creates a hierarchy.

Hierarchical clustering follows the same principle.

---

# Characteristics

- Unsupervised Learning
- No target variable
- No need to specify K initially
- Produces a Dendrogram
- Uses distance measures
- Sensitive to feature scaling
- Computationally expensive for large datasets

---

# Terminology

## Cluster

A group of similar observations.

---

## Leaf Node

An individual data point before clustering begins.

---

## Internal Node

Represents the merging of two clusters.

---

## Root Node

Represents the final cluster containing all observations.

---

## Dendrogram

A tree-like diagram showing how clusters are merged or split.

---

# Types of Hierarchical Clustering

There are two approaches:

```
Hierarchical Clustering
        │
 ┌──────┴──────┐
 │             │
Agglomerative  Divisive
(Bottom-Up)    (Top-Down)
```

---

# 1. Agglomerative Clustering (Bottom-Up)

## Definition

Agglomerative clustering starts with each observation as an individual cluster. It repeatedly merges the two most similar clusters until all observations belong to a single cluster or another stopping criterion is reached.

This is the **most commonly used hierarchical clustering algorithm**.

---

## Working Principle

Step 1

Each observation starts as its own cluster.

```
A   B   C   D
```

Step 2

Find the closest pair.

```
A B

C

D
```

Step 3

Merge the next closest cluster.

```
AB

CD
```

Step 4

Merge all clusters.

```
ABCD
```

---

## Algorithm

1. Treat every observation as an individual cluster.
2. Compute the distance matrix.
3. Find the two nearest clusters.
4. Merge them.
5. Update the distance matrix.
6. Repeat until one cluster remains.

---

## Flowchart

```
Start

↓

Each Record = One Cluster

↓

Compute Distance Matrix

↓

Find Nearest Clusters

↓

Merge Them

↓

Update Distance Matrix

↓

One Cluster Left?

↓

Yes → Stop

No → Repeat
```

---

# Example

Suppose we have four observations.

```
A

B

C

D
```

Distance Matrix

| |A|B|C|D|
|--|--|--|--|--|
|A|0|2|7|9|
|B|2|0|8|10|
|C|7|8|0|3|
|D|9|10|3|0|

Smallest distance = **2**

Merge

```
(A,B)
```

Next smallest

```
(C,D)
```

Finally

```
((A,B),(C,D))
```

---

# Advantages

- Easy to understand
- No need to specify K
- Produces hierarchical structure
- Useful for visualization
- Works well on small datasets

---

# Disadvantages

- Computationally expensive
- Sensitive to noisy data
- Once merged, clusters cannot be separated
- Memory intensive

---

# 2. Divisive Clustering (Top-Down)

## Definition

Divisive clustering follows the opposite strategy.

Instead of merging clusters, it starts with **one large cluster** and recursively divides it into smaller clusters.

---

## Working Principle

Initially,

```
ABCD
```

Split

```
AB

CD
```

Split again

```
A

B

CD
```

Finally

```
A

B

C

D
```

---

## Algorithm

1. Place all observations into one cluster.
2. Find the least similar observations.
3. Split the cluster.
4. Repeat until each observation forms an individual cluster.

---

## Advantages

- Natural top-down hierarchy
- Useful when global structure is important

---

## Disadvantages

- Extremely expensive
- Rarely used in practice
- Difficult to determine optimal split

---

# Agglomerative vs Divisive

| Feature | Agglomerative | Divisive |
|----------|---------------|----------|
| Approach | Bottom-Up | Top-Down |
| Initial State | n clusters | 1 cluster |
| Process | Merge | Split |
| Popularity | Very High | Low |
| Complexity | High | Very High |

---

# Distance Matrix

Hierarchical clustering depends on a distance matrix.

Example

| |A|B|C|
|--|--|--|--|
|A|0|2|5|
|B|2|0|3|
|C|5|3|0|

The algorithm repeatedly updates this matrix after every merge.

---

# Linkage Methods

Linkage determines how the distance between clusters is calculated.

## 1. Single Linkage

Uses the minimum distance.

```
Distance

=

Minimum Pairwise Distance
```

Advantages

- Detects irregular clusters

Disadvantages

- Chaining effect

---

## 2. Complete Linkage

Uses the maximum distance.

```
Distance

=

Maximum Pairwise Distance
```

Advantages

- Produces compact clusters

Disadvantages

- Sensitive to outliers

---

## 3. Average Linkage

Uses the average distance between all observations.

Advantages

- Balanced clusters
- Less sensitive than complete linkage

---

## 4. Centroid Linkage

Uses the distance between cluster centroids.

Best suited for numerical datasets.

---

## 5. Ward's Linkage

Merges clusters that result in the smallest increase in within-cluster variance.

Advantages

- Compact clusters
- Frequently used with Euclidean distance

Disadvantages

- Assumes spherical clusters

---

# Dendrogram

A dendrogram is a tree representation of hierarchical clustering.

Example

```
           ───────────────
          |              |
      ────              ────
     |   |             |   |
     A   B             C   D
```

The height at which two branches merge represents the distance between the clusters.

To determine the number of clusters, draw a horizontal cut across the dendrogram.

```
           ───────────────
          |              |
      ────              ────
     |   |             |   |
     A   B             C   D

--------------- Cut Here ---------------

Clusters

(A,B)

(C,D)
```

---

# Time Complexity

| Operation | Complexity |
|-----------|------------|
| Distance Matrix | O(n²) |
| Agglomerative Clustering | O(n² log n) to O(n³) |
| Memory | O(n²) |

---

# Python Example

```python
from sklearn.cluster import AgglomerativeClustering

model = AgglomerativeClustering(
    n_clusters=3,
    linkage='ward'
)

labels = model.fit_predict(X)
```

---

# Plotting a Dendrogram

```python
from scipy.cluster.hierarchy import linkage
from scipy.cluster.hierarchy import dendrogram
import matplotlib.pyplot as plt

Z = linkage(X, method='ward')

plt.figure(figsize=(10,5))
dendrogram(Z)
plt.show()
```

---

# Applications

## Customer Segmentation

Group customers based on purchasing behavior.

---

## Document Clustering

Cluster similar articles.

---

## Image Segmentation

Group similar pixels.

---

## Healthcare

Group patients with similar symptoms.

---

## Bioinformatics

Cluster genes based on expression patterns.

---

## Fraud Detection

Identify suspicious transaction groups.

---

# When to Use Hierarchical Clustering

Use when:

- Dataset is small to medium
- Number of clusters is unknown
- Hierarchical relationships are important
- Visualization through a dendrogram is required

Avoid when:

- Dataset is very large
- Fast clustering is required
- Memory is limited

---

# Hierarchical Clustering vs K-Means

| Feature | Hierarchical | K-Means |
|----------|--------------|---------|
| Need K | No | Yes |
| Output | Dendrogram | K Clusters |
| Speed | Slow | Fast |
| Large Datasets | Poor | Excellent |
| Cluster Shape | Flexible | Mostly Spherical |
| Reassignment | No | Yes |

---

# Interview Questions

### 1. What is Hierarchical Clustering?

A clustering algorithm that builds a hierarchy of clusters using either a bottom-up (Agglomerative) or top-down (Divisive) approach.

---

### 2. Why is a Dendrogram used?

To visualize how clusters are merged or divided and to help determine the appropriate number of clusters.

---

### 3. Which is more commonly used: Agglomerative or Divisive?

Agglomerative Clustering.

---

### 4. What are the common linkage methods?

- Single Linkage
- Complete Linkage
- Average Linkage
- Centroid Linkage
- Ward's Linkage

---

### 5. Can Hierarchical Clustering handle large datasets?

Generally no, because it has high computational and memory requirements.

---

# Summary

Hierarchical Clustering is a powerful unsupervised learning technique that builds a hierarchy of clusters instead of creating a fixed partition. It consists of two approaches: **Agglomerative (Bottom-Up)** and **Divisive (Top-Down)**. Cluster formation depends on the chosen **linkage method**, and the results are visualized using a **Dendrogram**. It is especially useful when the number of clusters is unknown and when understanding hierarchical relationships in the data is important, although its computational cost makes it less suitable for very large datasets.
