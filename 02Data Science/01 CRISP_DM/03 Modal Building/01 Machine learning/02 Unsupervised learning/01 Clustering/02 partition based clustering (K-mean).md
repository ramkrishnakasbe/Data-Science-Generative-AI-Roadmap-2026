# Partition Based Clustering (K-Means)

# Overview

Partition-Based Clustering is one of the most popular clustering techniques in Unsupervised Machine Learning. It divides a dataset into **K disjoint (non-overlapping) clusters**, where each data point belongs to exactly one cluster.

The objective is to group similar observations together while ensuring that observations in different clusters are as dissimilar as possible.

The most widely used Partition-Based Clustering algorithm is **K-Means Clustering**.

---

# Characteristics

- Unsupervised Learning
- Distance-based algorithm
- Requires specifying the number of clusters (K)
- Each observation belongs to only one cluster
- Works best for numerical data
- Suitable for large datasets
- Sensitive to feature scaling and outliers

---

# Types of Partition-Based Clustering

Common partition-based algorithms include:

- K-Means ⭐⭐⭐⭐⭐
- K-Medoids (PAM)
- CLARA
- CLARANS
- Fuzzy C-Means

Among these, **K-Means** is the most popular and widely used algorithm.

---

# What is K-Means Clustering?

K-Means is an iterative clustering algorithm that partitions the dataset into **K clusters** by minimizing the distance between data points and their assigned cluster centroid.

The algorithm continuously updates the cluster centers until no significant changes occur.

---

# Objective

The objective of K-Means is to minimize the **Within Cluster Sum of Squares (WCSS)**, also known as **Inertia**.

It tries to make:

- Points within the same cluster as close as possible.
- Different clusters as far apart as possible.

---

# Terminologies

## Cluster

A collection of similar observations.

Example

```
Cluster 1

A B C D
```

---

## Centroid

The center point of a cluster.

It is calculated as the **mean of all observations** belonging to that cluster.

```
Cluster

● ● ● ●

     X

X = Centroid
```

---

## Distance

Distance measures how similar or dissimilar two observations are.

Common distance measures:

- Euclidean Distance
- Manhattan Distance
- Minkowski Distance

K-Means primarily uses **Euclidean Distance**.

---

# Euclidean Distance

The Euclidean Distance is the straight-line distance between two points.

Formula

```
d = √[(x₂-x₁)² + (y₂-y₁)²]
```

Example

```
Point A = (2,3)

Point B = (5,7)

Distance

= √[(5-2)²+(7-3)²]

= √25

= 5
```

---

# How K-Means Works

Suppose

```
K = 3
```

### Step 1

Select the number of clusters (K).

```
K = 3
```

---

### Step 2

Randomly initialize K centroids.

```
●

      ●

            ●
```

---

### Step 3

Assign every data point to its nearest centroid.

```
Cluster 1

● ● ●

Cluster 2

● ●

Cluster 3

● ● ● ●
```

---

### Step 4

Calculate the new centroid of each cluster.

The centroid is simply the average of all observations.

---

### Step 5

Reassign all observations based on the updated centroids.

---

### Step 6

Repeat Steps 4 and 5 until centroids no longer move or a stopping criterion is met.

---

# Flowchart

```
Start

↓

Choose K

↓

Initialize Centroids

↓

Assign Points

↓

Calculate New Centroids

↓

Centroids Changed?

↓

Yes → Repeat

↓

No

↓

Stop
```

---

# Mathematical Objective (WCSS)

K-Means minimizes the **Within Cluster Sum of Squares (WCSS)**.

```
WCSS = Σ Distance²(Point, Centroid)
```

Lower WCSS indicates tighter, more compact clusters.

---

# Manual Example

Dataset

| Point | X | Y |
|------|---|---|
| A | 1 | 1 |
| B | 2 | 2 |
| C | 8 | 8 |
| D | 9 | 9 |

Choose

```
K = 2
```

Initial Centroids

```
C1 = A

C2 = C
```

### First Assignment

Cluster 1

```
A

B
```

Cluster 2

```
C

D
```

### New Centroids

Cluster 1

```
((1+2)/2 , (1+2)/2)

=

(1.5 ,1.5)
```

Cluster 2

```
((8+9)/2 , (8+9)/2)

=

(8.5 ,8.5)
```

Since assignments remain unchanged, the algorithm converges.

---

# Stopping Criteria

The algorithm stops when:

- Centroids no longer change.
- Cluster assignments remain the same.
- Maximum iterations are reached.
- Improvement in WCSS becomes negligible.

---

# Choosing the Optimal K

Selecting the correct value of **K** is one of the biggest challenges in K-Means.

### 1. Elbow Method

The Elbow Method plots:

```
K

vs

WCSS
```

As K increases:

- WCSS decreases.
- After a certain point, the improvement becomes very small.

The "elbow point" is chosen as the optimal K.

---

### 2. Silhouette Score

Measures how well each observation fits within its assigned cluster.

Range

```
-1  to  +1
```

Interpretation

- +1 → Excellent clustering
- 0 → Overlapping clusters
- -1 → Incorrect clustering

Higher score is better.

---

# Initialization Methods

## Random Initialization

Centroids are selected randomly.

Problem:

Different runs may produce different results.

---

## K-Means++

An improved initialization technique.

Advantages

- Better initial centroids
- Faster convergence
- More stable clusters

Most libraries use **K-Means++** by default.

---

# Assumptions

K-Means assumes:

- Clusters are spherical.
- Clusters have similar sizes.
- Features are numerical.
- Distance measure is meaningful.
- Data is properly scaled.

---

# Importance of Feature Scaling

Since K-Means uses Euclidean Distance, features with larger values dominate the clustering.

Example

```
Salary

0-100000

Age

20-60
```

Salary will dominate unless scaling is applied.

Recommended scaling methods:

- StandardScaler
- MinMaxScaler
- RobustScaler

---

# Advantages

- Simple and easy to understand.
- Fast and efficient.
- Works well on large datasets.
- Easy to implement.
- Produces compact clusters.
- Scalable to millions of records.

---

# Disadvantages

- Need to specify K beforehand.
- Sensitive to outliers.
- Sensitive to initialization.
- Works only with numerical data.
- Assumes spherical clusters.
- Different initial centroids may produce different results.

---

# Time Complexity

For

- n = observations
- k = clusters
- i = iterations

Time Complexity

```
O(n × k × i)
```

Space Complexity

```
O(n)
```

---

# Python Implementation

```python
from sklearn.cluster import KMeans

kmeans = KMeans(
    n_clusters=3,
    init="k-means++",
    random_state=42
)

labels = kmeans.fit_predict(X)

print(labels)
```

---

# Important Parameters

| Parameter | Description |
|-----------|-------------|
| n_clusters | Number of clusters |
| init | Initialization method |
| random_state | Reproducibility |
| max_iter | Maximum iterations |
| n_init | Number of initializations |

---

# Applications

- Customer Segmentation
- Market Basket Analysis
- Image Compression
- Image Segmentation
- Recommendation Systems
- Document Clustering
- Fraud Detection
- Social Network Analysis
- Medical Data Analysis
- Sales Segmentation

---

# K-Means vs Hierarchical Clustering

| Feature | K-Means | Hierarchical |
|----------|----------|-------------|
| Need K | Yes | No |
| Speed | Fast | Slow |
| Large Dataset | Excellent | Poor |
| Output | K Clusters | Dendrogram |
| Outlier Handling | Poor | Poor |
| Cluster Shape | Spherical | Flexible |

---

# Limitations

K-Means struggles when:

- Clusters have irregular shapes.
- Dataset contains many outliers.
- Clusters have different densities.
- Categorical features are present.
- Number of clusters is unknown.

For such datasets, algorithms like **DBSCAN** or **Hierarchical Clustering** may perform better.

---

# Interview Questions

### 1. What is K-Means Clustering?

An unsupervised partition-based algorithm that divides data into K clusters by minimizing the within-cluster variance.

---

### 2. Why is feature scaling important in K-Means?

Because K-Means relies on Euclidean Distance, features with larger scales can dominate the clustering process.

---

### 3. What is WCSS?

Within Cluster Sum of Squares (Inertia), the sum of squared distances between each point and its assigned centroid. K-Means minimizes this value.

---

### 4. How do you choose the optimal K?

Common methods include:
- Elbow Method
- Silhouette Score
- Domain Knowledge

---

### 5. Why is K-Means sensitive to outliers?

Outliers can significantly shift the centroid because centroids are calculated using the mean.

---

### 6. What is K-Means++?

An improved centroid initialization technique that selects initial centroids more strategically, leading to better convergence and more stable results.

---

# Summary

K-Means is the most widely used partition-based clustering algorithm. It partitions data into **K clusters** by assigning each observation to the nearest centroid and iteratively updating the centroids until convergence. It is fast, scalable, and effective for numerical data with compact, spherical clusters. However, it requires specifying the number of clusters in advance, is sensitive to outliers and feature scaling, and may not perform well on irregularly shaped or varying-density clusters.
