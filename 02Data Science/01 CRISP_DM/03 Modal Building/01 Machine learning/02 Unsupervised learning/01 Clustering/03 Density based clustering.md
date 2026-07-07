# Density-Based Clustering (DBSCAN)

# Overview

DBSCAN (Density-Based Spatial Clustering of Applications with Noise) is a popular **density-based unsupervised machine learning algorithm** used to discover clusters of arbitrary shapes while automatically identifying outliers (noise).

Unlike K-Means, DBSCAN **does not require specifying the number of clusters (K)** beforehand. Instead, it groups together points that are densely packed and marks points in low-density regions as outliers.

DBSCAN is particularly effective for datasets containing noise or clusters with irregular shapes.

---

# Definition

DBSCAN groups data points into clusters based on the density of neighboring points.

A cluster is formed when a region contains a sufficient number of nearby observations within a specified distance.

---

# Characteristics

- Unsupervised Learning
- Density-Based Clustering
- No need to specify K
- Can detect outliers
- Finds clusters of arbitrary shape
- Works well with noisy datasets
- Uses neighborhood density instead of centroids

---

# Why DBSCAN?

K-Means has several limitations:

- Requires predefined K
- Sensitive to outliers
- Assumes spherical clusters
- Poor performance on irregular-shaped clusters

DBSCAN overcomes many of these limitations by using **density** rather than distance to a centroid.

---

# Basic Terminology

## Density

Density refers to the number of neighboring points within a specified radius.

Higher density indicates that points are likely to belong to the same cluster.

---

# Important Parameters

DBSCAN requires only two parameters:

## 1. Epsilon (ε or eps)

The maximum radius around a point to search for neighboring points.

```
        ε Radius

        ○ ○
     ○   ●   ○
        ○ ○
```

All points inside this radius are considered neighbors.

---

## 2. MinPts (Minimum Points)

The minimum number of neighboring points required to form a dense region.

Example

```
MinPts = 5
```

If a point has at least 5 neighbors inside ε, it becomes a Core Point.

---

# Types of Points

DBSCAN classifies every observation into one of three categories.

```
          DBSCAN
             │
    ┌────────┼────────┐
    │        │        │
 Core     Border    Noise
 Point     Point     Point
```

---

# 1. Core Point

A point having at least **MinPts neighbors** within ε distance.

Example

```
○ ○ ○

○ ● ○

○ ○ ○
```

The center point has many nearby observations.

Hence,

```
Core Point
```

---

# 2. Border Point

A point that has fewer than MinPts neighbors but lies inside the ε neighborhood of a Core Point.

Example

```
Core ● ● ●

          ○
```

The circle belongs to the cluster but cannot create its own cluster.

---

# 3. Noise Point (Outlier)

A point that is neither a Core Point nor a Border Point.

Example

```
Cluster

● ● ● ●

               ○
```

The isolated point is considered noise.

---

# Working of DBSCAN

Suppose

```
ε = 2

MinPts = 4
```

### Step 1

Select an unvisited point.

---

### Step 2

Find all neighboring points within ε distance.

---

### Step 3

If neighbors ≥ MinPts

Create a new cluster.

Otherwise

Mark the point as noise temporarily.

---

### Step 4

Expand the cluster by checking all neighboring Core Points.

---

### Step 5

Continue until all reachable points are assigned.

---

### Step 6

Repeat for remaining unvisited points.

---

# Flowchart

```
Start

↓

Select an Unvisited Point

↓

Find ε Neighbors

↓

Neighbors ≥ MinPts ?

↓

Yes

↓

Create Cluster

↓

Expand Cluster

↓

Repeat

↓

No

↓

Mark as Noise

↓

Continue

↓

Stop
```

---

# Example

Dataset

```
● ● ● ●

● ● ●

                ● ● ●

               ● ●

                       ○
```

Cluster 1

```
● ● ● ●

● ● ●
```

Cluster 2

```
● ● ●

● ●
```

Noise

```
○
```

DBSCAN automatically identifies two clusters and one outlier.

---

# Choosing Parameters

## Choosing ε

Too Small

```
Many small clusters

Lots of noise
```

Too Large

```
Clusters merge

Poor clustering
```

---

## Choosing MinPts

General guideline

```
MinPts

≥ Number of Features + 1
```

Common choices

```
4

5

10
```

---

# Distance Measure

DBSCAN usually uses

- Euclidean Distance
- Manhattan Distance
- Minkowski Distance

Euclidean Distance is the default in most implementations.

---

# Advantages

- No need to specify K
- Detects outliers automatically
- Handles arbitrary-shaped clusters
- Works well for noisy datasets
- Robust against outliers
- Suitable for spatial datasets

---

# Disadvantages

- Difficult to choose ε
- Sensitive to parameter selection
- Struggles with varying cluster densities
- Performance decreases in high-dimensional data

---

# Time Complexity

Without indexing

```
O(n²)
```

With KD-Tree or Ball Tree

```
O(n log n)
```

Space Complexity

```
O(n)
```

---

# Python Implementation

```python
from sklearn.cluster import DBSCAN

dbscan = DBSCAN(
    eps=0.5,
    min_samples=5
)

labels = dbscan.fit_predict(X)

print(labels)
```

---

# Important Parameters

| Parameter | Description |
|-----------|-------------|
| eps | Neighborhood radius |
| min_samples | Minimum neighbors required |
| metric | Distance metric |
| algorithm | Neighbor search algorithm |

---

# Applications

- Customer Segmentation
- Fraud Detection
- GPS Data Analysis
- Image Segmentation
- Anomaly Detection
- Disease Outbreak Detection
- Social Network Analysis
- Geographic Information Systems (GIS)
- Recommendation Systems

---

# DBSCAN vs K-Means

| Feature | DBSCAN | K-Means |
|----------|---------|----------|
| Need K | No | Yes |
| Outlier Detection | Yes | No |
| Cluster Shape | Arbitrary | Spherical |
| Uses Centroid | No | Yes |
| Sensitive to Outliers | No | Yes |
| Handles Noise | Excellent | Poor |

---

# DBSCAN vs Hierarchical Clustering

| Feature | DBSCAN | Hierarchical |
|----------|---------|-------------|
| Need K | No | No |
| Detect Outliers | Yes | No |
| Dendrogram | No | Yes |
| Large Dataset | Better | Slower |
| Cluster Shape | Arbitrary | Flexible |

---

# Limitations

DBSCAN performs poorly when:

- Cluster densities vary significantly.
- Dataset is very high-dimensional.
- ε is difficult to determine.
- Features are not properly scaled.

---

# Interview Questions

## 1. What is DBSCAN?

DBSCAN is a density-based clustering algorithm that groups points based on the density of neighboring observations while identifying outliers as noise.

---

## 2. What are the two important parameters?

- Epsilon (ε)
- MinPts (min_samples)

---

## 3. What is a Core Point?

A point having at least MinPts neighboring points within ε distance.

---

## 4. What is a Border Point?

A point that belongs to a cluster but does not have enough neighbors to become a Core Point.

---

## 5. What is a Noise Point?

A point that does not belong to any cluster because it is not density reachable from any Core Point.

---

## 6. Why is DBSCAN better than K-Means?

- No need to specify K
- Detects outliers
- Handles irregular-shaped clusters
- More robust to noise

---

## 7. What is the biggest drawback of DBSCAN?

Selecting an appropriate ε value is challenging, and DBSCAN struggles when clusters have different densities.

---

# Summary

DBSCAN is one of the most powerful density-based clustering algorithms. It groups observations based on **density connectivity** rather than centroids, making it ideal for datasets containing **noise**, **outliers**, and **irregularly shaped clusters**. It requires only two parameters—**ε (epsilon)** and **MinPts**—and automatically discovers the number of clusters. While it performs exceptionally well on spatial and noisy data, its effectiveness depends on choosing appropriate parameter values and may decrease for high-dimensional or varying-density datasets.
