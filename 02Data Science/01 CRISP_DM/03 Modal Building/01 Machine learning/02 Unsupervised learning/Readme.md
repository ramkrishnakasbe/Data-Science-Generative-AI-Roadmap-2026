# Unsupervised Learning (Descriptive Learning)

# Overview

Unsupervised Learning is a type of Machine Learning in which the model learns patterns, structures, and relationships from **unlabeled data**. Unlike supervised learning, there is **no target (dependent) variable**. The objective is to discover hidden structures, similarities, clusters, or underlying patterns within the data.

It is also known as **Descriptive Learning** because it focuses on describing the data rather than making predictions.

---

# Learning Objectives

After completing this section, you should be able to:

- Understand the concept of Unsupervised Learning
- Differentiate between Supervised and Unsupervised Learning
- Perform clustering and dimensionality reduction
- Detect anomalies
- Discover association rules
- Apply recommender system techniques
- Evaluate clustering algorithms
- Select appropriate algorithms for different datasets

---

# Prerequisites

Before starting this section, you should be familiar with:

- Python
- Statistics
- Probability
- Linear Algebra
- Data Preprocessing
- Feature Scaling
- Exploratory Data Analysis (EDA)
- Distance Measures

---

# Topics Covered

## 1. Introduction

- What is Machine Learning?
- Types of Machine Learning
- What is Unsupervised Learning?
- Characteristics
- Advantages
- Disadvantages
- Applications

---

## 2. Distance Measures

- Euclidean Distance
- Manhattan Distance
- Minkowski Distance
- Cosine Distance
- Cosine Similarity
- Hamming Distance
- Mahalanobis Distance
- Jaccard Similarity

---

## 3. Clustering

### Partition Based Clustering

- K-Means Clustering
- K-Medoids (PAM)

### Hierarchical Clustering

- Agglomerative Clustering
- Divisive Clustering
- Dendrogram

### Density Based Clustering

- DBSCAN
- OPTICS

### Distribution Based Clustering

- Gaussian Mixture Model (GMM)
- Expectation Maximization (EM)

### Grid Based Clustering

- STING
- CLIQUE (Overview)

---

## 4. Cluster Validation

- Elbow Method
- Silhouette Score
- Davies-Bouldin Index
- Calinski-Harabasz Score
- Dunn Index (Overview)

---

## 5. Dimensionality Reduction

### Linear Techniques

- Principal Component Analysis (PCA)
- Singular Value Decomposition (SVD)

### Non-Linear Techniques

- t-SNE
- UMAP

---

## 6. Association Rule Mining

- Market Basket Analysis
- Support
- Confidence
- Lift
- Conviction
- Apriori Algorithm
- FP-Growth Algorithm
- ECLAT (Overview)

---

## 7. Anomaly Detection

- Statistical Methods
- Z-Score
- IQR Method
- Isolation Forest
- Local Outlier Factor (LOF)
- One-Class SVM

---

## 8. Recommender Systems

### Collaborative Filtering

- User-Based
- Item-Based

### Content-Based Filtering

### Hybrid Recommendation System

---

## 9. Topic Modeling (NLP)

- Latent Dirichlet Allocation (LDA)
- Latent Semantic Analysis (LSA)
- Non-negative Matrix Factorization (NMF)

---

## 10. Self-Organizing Maps (SOM)

- Concept
- Architecture
- Applications

---

## 11. Autoencoders

- Introduction
- Encoder
- Decoder
- Bottleneck Layer
- Applications

---

## 12. Cluster Interpretation

- Cluster Profiling
- Feature Importance
- Business Interpretation

---

## 13. Model Evaluation

### Internal Evaluation

- Silhouette Score
- Davies-Bouldin Index
- Calinski-Harabasz Score

### External Evaluation

- Adjusted Rand Index (ARI)
- Mutual Information
- Homogeneity
- Completeness

---

# Learning Flow

```text
Raw Data
      │
      ▼
Data Cleaning
      │
      ▼
Feature Engineering
      │
      ▼
Feature Scaling
      │
      ▼
Distance Calculation
      │
      ▼
Choose Algorithm
      │
      ▼
Model Training
      │
      ▼
Clusters / Patterns
      │
      ▼
Cluster Evaluation
      │
      ▼
Business Interpretation
```

---

# Types of Unsupervised Learning

| Type | Objective | Algorithms |
|-------|-----------|------------|
| Clustering | Group similar data | K-Means, DBSCAN, Hierarchical |
| Association | Discover relationships | Apriori, FP-Growth |
| Dimensionality Reduction | Reduce features | PCA, SVD, t-SNE, UMAP |
| Anomaly Detection | Detect unusual observations | Isolation Forest, LOF |
| Recommendation | Suggest similar items | Collaborative Filtering |

---

# Supervised vs Unsupervised Learning

| Supervised Learning | Unsupervised Learning |
|--------------------|-----------------------|
| Labeled Data | Unlabeled Data |
| Target Variable Available | No Target Variable |
| Prediction | Pattern Discovery |
| Regression & Classification | Clustering & Association |
| Accuracy Based Evaluation | Cluster Quality Evaluation |

---

# Popular Algorithms

| Algorithm | Category |
|------------|----------|
| K-Means | Clustering |
| Hierarchical Clustering | Clustering |
| DBSCAN | Density-Based Clustering |
| Gaussian Mixture Model | Probabilistic Clustering |
| PCA | Dimensionality Reduction |
| t-SNE | Visualization |
| UMAP | Dimensionality Reduction |
| Apriori | Association Rule Mining |
| Isolation Forest | Anomaly Detection |
| Autoencoder | Deep Unsupervised Learning |

---

# Real-World Applications

- Customer Segmentation
- Product Recommendation
- Fraud Detection
- Market Basket Analysis
- Image Compression
- Topic Discovery
- Document Clustering
- Social Network Analysis
- Medical Diagnosis
- Network Intrusion Detection
- Gene Expression Analysis
- Image Segmentation

---

# Folder Structure

```text
Unsupervised Learning/
│
├── README.md
│
├── 01 Introduction.md
├── 02 Distance Measures.md
├── 03 K-Means Clustering.md
├── 04 Hierarchical Clustering.md
├── 05 DBSCAN.md
├── 06 Gaussian Mixture Model.md
├── 07 Cluster Evaluation.md
├── 08 PCA.md
├── 09 t-SNE.md
├── 10 UMAP.md
├── 11 Association Rule Mining.md
├── 12 Apriori Algorithm.md
├── 13 FP-Growth.md
├── 14 Anomaly Detection.md
├── 15 Isolation Forest.md
├── 16 Local Outlier Factor.md
├── 17 Recommender Systems.md
├── 18 Topic Modeling.md
├── 19 Autoencoders.md
├── 20 Self Organizing Maps.md
├── 21 Cluster Interpretation.md
└── Cheat Sheet.md
```

---

# Summary

Unsupervised Learning (Descriptive Learning) enables machines to identify hidden structures, relationships, and patterns from **unlabeled data**. It includes **clustering**, **dimensionality reduction**, **association rule mining**, **anomaly detection**, **topic modeling**, and **recommendation systems**. These techniques are widely used for customer segmentation, fraud detection, market basket analysis, visualization, and exploratory data analysis. Mastering these algorithms is essential for both real-world machine learning applications and data science interviews.
