# 02. Clustering

# Overview

Clustering is an **Unsupervised Machine Learning** technique used to group similar data points into clusters based on their characteristics or similarity. The goal is to ensure that data points within the same cluster are more similar to each other than to those in other clusters.

Unlike supervised learning, clustering does **not require labeled data**. It automatically identifies hidden patterns and structures within the dataset.

---

# Definition

**Clustering** is the process of partitioning a dataset into multiple groups (clusters) such that:

- Objects within the same cluster are highly similar.
- Objects belonging to different clusters are highly dissimilar.

---

# Why Clustering?

Clustering helps to:

- Discover hidden patterns
- Segment data into meaningful groups
- Understand customer behavior
- Detect anomalies
- Simplify large datasets
- Support decision making
- Improve data visualization

---

# Example

Suppose a shopping mall has customer information:

| Customer | Age | Annual Income | Spending Score |
|----------|----:|--------------:|---------------:|
| A | 22 | 25K | 80 |
| B | 24 | 27K | 78 |
| C | 45 | 90K | 20 |
| D | 47 | 95K | 18 |

Clustering may automatically group them into:

**Cluster 1**
- Young customers
- Low income
- High spending

**Cluster 2**
- Older customers
- High income
- Low spending

This helps businesses create targeted marketing campaigns.

---

# Characteristics of Clustering

- Unsupervised learning technique
- Works with unlabeled data
- Groups similar observations
- Based on similarity or distance
- No predefined output labels
- Useful for exploratory data analysis
- Sensitive to feature scaling
- Different algorithms produce different clusters

---

# Terminologies

## Cluster

A collection of similar data points.

Example:

```
Cluster 1

Apple
Orange
Banana
```

---

## Centroid

The center point of a cluster.

Used mainly in:

- K-Means Clustering

---

## Distance Measure

Measures similarity between observations.

Common distance measures:

- Euclidean Distance
- Manhattan Distance
- Minkowski Distance
- Cosine Distance
- Cosine Similarity
- Hamming Distance
- Mahalanobis Distance

---

## Similarity

Higher similarity indicates that observations belong to the same cluster.

---

# Types of Clustering

There are several clustering approaches depending on how clusters are formed.

---

# 1. Partition-Based Clustering

The dataset is divided into **K predefined clusters**.

### Characteristics

- Fast
- Simple
- Suitable for large datasets

### Algorithms

- K-Means
- K-Medoids (PAM)

---

# 2. Hierarchical Clustering

Creates a hierarchy of clusters represented by a **Dendrogram**.

### Types

- Agglomerative (Bottom-Up)
- Divisive (Top-Down)

### Algorithms

- Agglomerative Clustering
- Divisive Clustering

---

# 3. Density-Based Clustering

Clusters are formed based on regions with high data density.

### Characteristics

- Detects arbitrary-shaped clusters
- Handles noise and outliers well

### Algorithms

- DBSCAN
- OPTICS

---

# 4. Distribution-Based Clustering

Assumes that data follows a probability distribution.

### Algorithms

- Gaussian Mixture Model (GMM)
- Expectation Maximization (EM)

---

# 5. Grid-Based Clustering

Divides the data space into grids before clustering.

### Characteristics

- Very fast
- Suitable for very large datasets

### Algorithms

- STING
- CLIQUE

---

# 6. Fuzzy Clustering

A data point can belong to multiple clusters with different membership values.

### Algorithm

- Fuzzy C-Means

---

# Common Clustering Algorithms

| Algorithm | Type |
|-----------|------|
| K-Means | Partition-Based |
| K-Medoids | Partition-Based |
| Hierarchical Clustering | Hierarchical |
| DBSCAN | Density-Based |
| OPTICS | Density-Based |
| Gaussian Mixture Model | Distribution-Based |
| Mean Shift | Density-Based |
| Birch | Hierarchical |
| Spectral Clustering | Graph-Based |
| Affinity Propagation | Message Passing |
| Fuzzy C-Means | Fuzzy Clustering |

---

# Choosing the Right Clustering Algorithm

| Situation | Recommended Algorithm |
|-----------|----------------------|
| Large dataset | K-Means |
| Unknown cluster shape | DBSCAN |
| Hierarchical relationships | Hierarchical Clustering |
| Soft clustering | Fuzzy C-Means |
| Probabilistic clustering | Gaussian Mixture Model |
| Presence of outliers | DBSCAN |
| Unknown number of clusters | DBSCAN, Hierarchical |

---

# Advantages of Clustering

- No labeled data required
- Discovers hidden patterns
- Simple to understand
- Helps customer segmentation
- Detects anomalies
- Useful for recommendation systems
- Supports exploratory data analysis

---

# Disadvantages of Clustering

- Difficult to determine the optimal number of clusters
- Sensitive to feature scaling
- Results depend on the chosen algorithm
- Sensitive to noisy data
- Interpretation may require domain knowledge

---

# Applications of Clustering

## Customer Segmentation

Group customers based on purchasing behavior.

---

## Market Segmentation

Identify customer groups for targeted marketing.

---

## Recommendation Systems

Recommend products based on similar users.

---

## Image Segmentation

Separate different regions in an image.

---

## Document Clustering

Group similar articles or research papers.

---

## Social Network Analysis

Identify communities within social networks.

---

## Bioinformatics

Cluster genes or proteins with similar characteristics.

---

## Healthcare

Group patients with similar symptoms or diseases.

---

## Fraud Detection

Identify unusual transaction patterns.

---

## Anomaly Detection

Detect abnormal observations that differ significantly from the majority.

---

# Clustering Workflow

```text
Raw Data
     │
     ▼
Data Cleaning
     │
     ▼
Feature Scaling
     │
     ▼
Choose Distance Measure
     │
     ▼
Choose Clustering Algorithm
     │
     ▼
Train Model
     │
     ▼
Generate Clusters
     │
     ▼
Evaluate Clusters
     │
     ▼
Interpret Results
```

---

# Cluster Evaluation Methods

Common methods used to evaluate clustering performance:

- Elbow Method
- Silhouette Score
- Davies-Bouldin Index
- Calinski-Harabasz Index
- Dunn Index

*(These topics will be covered separately.)*

---

# Summary

Clustering is one of the most important techniques in **Unsupervised Learning** used to group similar observations without predefined labels. It is widely applied in customer segmentation, recommendation systems, fraud detection, image segmentation, healthcare, and market basket analysis. Various clustering approaches—such as **Partition-Based**, **Hierarchical**, **Density-Based**, **Distribution-Based**, **Grid-Based**, and **Fuzzy Clustering**—are available, and the choice depends on the nature of the dataset and the problem being solved.
