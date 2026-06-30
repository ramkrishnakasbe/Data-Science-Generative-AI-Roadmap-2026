# 01. Introduction

# Overview

Unsupervised Learning is a type of Machine Learning in which the model learns from **unlabeled data**. Unlike supervised learning, there is **no target (dependent) variable** available during training.

The primary objective is to discover hidden patterns, structures, similarities, or relationships within the data without any prior knowledge of the expected output.

It is also known as **Descriptive Learning** because it focuses on describing and understanding the underlying structure of the dataset.

---

# What is Unsupervised Learning?

In Unsupervised Learning, the algorithm receives only the input features (X) and attempts to identify meaningful patterns on its own.

Unlike supervised learning, the model is **not provided with the correct answers (labels)** during training.

The output may include:

- Clusters
- Associations
- Hidden Patterns
- Lower-dimensional representations
- Anomalies

---

# Characteristics

- Works with unlabeled data
- No target (dependent) variable
- Learns hidden structures automatically
- Mainly used for Exploratory Data Analysis (EDA)
- Finds similarities among observations
- Discovers unknown patterns
- Sensitive to feature scaling and distance measures
- Often used before supervised learning

---

# Advantages

- No labeled data required
- Can discover hidden relationships
- Useful for exploratory analysis
- Identifies natural groupings in data
- Helps reduce dimensionality
- Detects anomalies and outliers
- Useful when labeling data is expensive

---

# Disadvantages

- Difficult to evaluate performance
- Results may be difficult to interpret
- Number of clusters may need to be chosen manually
- Different algorithms may produce different results
- Sensitive to noisy data and outliers
- Requires domain knowledge for interpretation

---

# Major Categories of Unsupervised Learning

## 1. Clustering

Groups similar observations into clusters.

### Algorithms

- K-Means Clustering
- K-Medoids (PAM)
- Hierarchical Clustering
  - Agglomerative Clustering
  - Divisive Clustering
- DBSCAN
- OPTICS
- Mean Shift
- Gaussian Mixture Model (GMM)
- Spectral Clustering
- Birch
- Affinity Propagation
- Fuzzy C-Means

---

## 2. Dimensionality Reduction

Reduces the number of features while preserving important information.

### Algorithms

- Principal Component Analysis (PCA)
- Kernel PCA
- Singular Value Decomposition (SVD)
- Factor Analysis
- Independent Component Analysis (ICA)
- t-SNE
- UMAP
- Linear Discriminant Analysis (LDA)*

> *LDA is generally a supervised technique but is often compared with dimensionality reduction methods.

---

## 3. Association Rule Mining

Discovers relationships between items.

### Algorithms

- Apriori
- FP-Growth
- ECLAT

---

## 4. Anomaly Detection

Detects unusual observations that differ significantly from the majority.

### Algorithms

- Isolation Forest
- Local Outlier Factor (LOF)
- One-Class SVM
- Elliptic Envelope

---

## 5. Topic Modeling

Discovers hidden topics from text documents.

### Algorithms

- Latent Dirichlet Allocation (LDA)
- Latent Semantic Analysis (LSA)
- Non-negative Matrix Factorization (NMF)

---

## 6. Recommendation Systems

Suggests products or content based on user behavior.

### Techniques

- Collaborative Filtering
- Content-Based Filtering
- Hybrid Recommendation System

---

## 7. Representation Learning

Learns efficient representations of data.

### Algorithms

- Autoencoders
- Variational Autoencoders (VAE)
- Self-Organizing Maps (SOM)

---

# Applications

- Customer Segmentation
- Market Basket Analysis
- Recommendation Systems
- Fraud Detection
- Anomaly Detection
- Image Segmentation
- Document Clustering
- Topic Discovery
- Social Network Analysis
- Healthcare Analytics
- Bioinformatics
- Data Compression

---

# Summary

Unsupervised Learning is used to explore **unlabeled datasets** and uncover hidden structures, relationships, and patterns. It forms the foundation for tasks such as **clustering**, **dimensionality reduction**, **association rule mining**, **anomaly detection**, **topic modeling**, and **recommendation systems**. These techniques are widely used for exploratory data analysis, customer segmentation, fraud detection, and knowledge discovery.
