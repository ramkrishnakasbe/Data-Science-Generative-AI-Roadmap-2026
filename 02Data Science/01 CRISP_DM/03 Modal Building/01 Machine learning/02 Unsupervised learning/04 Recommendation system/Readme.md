# Recommendation Systems

# Overview

A **Recommendation System (Recommender System)** is a Machine Learning system that suggests relevant items to users based on their preferences, behavior, or similarities with other users/items.

Recommendation systems are one of the most successful applications of Machine Learning and Artificial Intelligence.

Examples include:

- Netflix → Movies & TV Shows
- Amazon → Products
- Spotify → Songs
- YouTube → Videos
- LinkedIn → Jobs & Connections
- Instagram → Posts & Reels

---

# Definition

A Recommendation System is a filtering system that predicts the items a user is most likely to like or interact with.

The goal is to provide **personalized recommendations** to improve user experience and increase engagement.

---

# Objectives

- Personalize user experience
- Increase customer satisfaction
- Improve product discovery
- Increase sales
- Increase user engagement
- Reduce search effort

---

# Characteristics

- Personalized recommendations
- Learns from user behavior
- Handles large datasets
- Improves customer retention
- Continuously updates recommendations

---

# Types of Recommendation Systems

```
Recommendation System
│
├── 1. Content-Based Filtering
├── 2. Collaborative Filtering
│      ├── User-Based
│      └── Item-Based
├── 3. Hybrid Recommendation
├── 4. Knowledge-Based
├── 5. Demographic-Based
└── 6. Popularity-Based
```

---

# 1. Content-Based Filtering

## Definition

Recommends items that are **similar to items the user has liked in the past**.

It uses the **features (content)** of the items.

Example

```
User likes

Action Movies

↓

Recommend

Marvel Movies

Mission Impossible

John Wick
```

---

## Working

```
User History

↓

Extract Item Features

↓

Find Similar Items

↓

Recommend Similar Items
```

---

## Advantages

- Personalized
- No need for other users
- Works for new users with history

---

## Disadvantages

- Limited diversity
- Requires item features
- Over-specialization

---

# 2. Collaborative Filtering

## Definition

Collaborative Filtering recommends items based on the preferences of **similar users** or **similar items**.

It assumes:

> Users with similar interests will like similar items.

---

## Types

### A. User-Based Collaborative Filtering

Find users with similar interests.

Example

```
Ram likes

Movie A

Movie B

Movie C

↓

Ravi likes

Movie A

Movie B

↓

Recommend

Movie C
```

---

### B. Item-Based Collaborative Filtering

Find items that are similar.

Example

```
Users buying

Laptop

↓

Also buy

Laptop Bag
Mouse
Keyboard
```

---

## Similarity Measures

- Cosine Similarity
- Pearson Correlation
- Euclidean Distance
- Jaccard Similarity

---

## Advantages

- Highly personalized
- No item features required
- Discovers hidden relationships

---

## Disadvantages

- Cold Start Problem
- Data Sparsity
- Scalability Issues

---

# 3. Hybrid Recommendation System

## Definition

Combines multiple recommendation techniques to improve accuracy.

Most modern systems use Hybrid models.

Example

Netflix combines

- Content-Based
- Collaborative Filtering
- User History
- Viewing Time
- Ratings

---

## Advantages

- Better accuracy
- Reduces limitations
- Handles cold start better

---

## Disadvantages

- Complex implementation
- High computational cost

---

# 4. Knowledge-Based Recommendation

Recommendations are generated using **business rules** and **domain knowledge**.

Example

```
House Recommendation

Budget

Location

Bedrooms

↓

Suggest Houses
```

Used when historical user data is limited.

---

# 5. Demographic-Based Recommendation

Recommendations are based on user demographics.

Example

- Age
- Gender
- Occupation
- Location

Example

```
Age

20-25

↓

Recommend

Gaming Products
```

---

# 6. Popularity-Based Recommendation

Recommends the most popular items.

Example

```
Trending Movies

Top Selling Products

Most Viewed Videos
```

Simple but not personalized.

---

# Recommendation Workflow

```
Collect User Data

↓

Preprocess Data

↓

Choose Recommendation Algorithm

↓

Train Model

↓

Generate Recommendations

↓

Evaluate

↓

Deploy
```

---

# User-Item Interaction Matrix

Recommendation systems often use a **User-Item Matrix**.

Example

| User | Movie A | Movie B | Movie C |
|------|---------|---------|---------|
| User1 | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | - |
| User2 | ⭐⭐⭐⭐ | - | ⭐⭐⭐⭐ |
| User3 | - | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ |

Rows → Users

Columns → Items

Values → Ratings or Interactions

---

# Similarity Measures

## 1. Cosine Similarity

Measures the cosine angle between two vectors.

Range

```
0 to 1
```

Higher value = More Similar

---

## 2. Pearson Correlation

Measures linear relationship between ratings.

Range

```
-1 to +1
```

---

## 3. Euclidean Distance

Measures straight-line distance.

Smaller distance = More Similar

---

## 4. Jaccard Similarity

Used for binary interactions.

Example

```
Purchased

Not Purchased
```

---

# Matrix Factorization

One of the most popular recommendation techniques.

Uses

- SVD
- Truncated SVD
- Alternating Least Squares (ALS)

It decomposes the user-item matrix into latent factors.

```
User Matrix

×

Item Matrix

↓

Predicted Ratings
```

---

# Cold Start Problem

Occurs when there is insufficient data.

Types

## User Cold Start

New user with no history.

---

## Item Cold Start

New item with no ratings.

---

## System Cold Start

New platform with no users or items.

---

# Data Sparsity

Most users rate only a small fraction of available items.

This creates a sparse user-item matrix.

---

# Evaluation Metrics

## Rating Prediction

- RMSE
- MAE
- MSE

---

## Ranking Metrics

- Precision@K
- Recall@K
- MAP
- NDCG
- Hit Rate

---

# Python Example (Content-Based)

```python
from sklearn.metrics.pairwise import cosine_similarity

similarity = cosine_similarity(item_features)
```

---

# Python Example (Collaborative Filtering using Surprise)

```python
from surprise import SVD
from surprise import Dataset

data = Dataset.load_builtin('ml-100k')

model = SVD()

trainset = data.build_full_trainset()

model.fit(trainset)
```

---

# Python Example (Matrix Factorization)

```python
from sklearn.decomposition import TruncatedSVD

svd = TruncatedSVD(n_components=50)

latent_matrix = svd.fit_transform(user_item_matrix)
```

---

# Advantages

- Personalized recommendations
- Increased customer engagement
- Improved sales
- Better customer experience
- Better product discovery
- Increased user retention

---

# Disadvantages

- Cold Start Problem
- Data Sparsity
- Scalability
- Privacy concerns
- Popularity bias
- Computationally expensive

---

# Real-World Applications

- Netflix (Movies)
- Amazon (Products)
- Spotify (Music)
- YouTube (Videos)
- LinkedIn (Jobs)
- Instagram (Content)
- Facebook (Friends)
- Flipkart (Products)
- Swiggy (Food)
- Zomato (Restaurants)

---

# Interview Questions

## 1. What is a Recommendation System?

A machine learning system that predicts and suggests relevant items to users based on their preferences or behavior.

---

## 2. What are the main types of Recommendation Systems?

- Content-Based Filtering
- Collaborative Filtering
- Hybrid Recommendation
- Knowledge-Based
- Demographic-Based
- Popularity-Based

---

## 3. What is Collaborative Filtering?

A recommendation technique that recommends items based on similar users or similar items.

---

## 4. What is the Cold Start Problem?

It occurs when there is insufficient data about new users or new items, making recommendations difficult.

---

## 5. Why is SVD used in Recommendation Systems?

SVD performs **matrix factorization** to discover hidden (latent) relationships between users and items, enabling prediction of missing ratings and improving recommendation accuracy.

---

## 6. What is Data Sparsity?

A situation where most entries in the user-item matrix are missing because users interact with only a small subset of available items.

---

# Recommendation System Comparison

| Type | Uses | Advantages | Disadvantages |
|------|------|------------|---------------|
| Content-Based | Item Features | Personalized | Limited diversity |
| User-Based CF | Similar Users | Good personalization | Cold start |
| Item-Based CF | Similar Items | Stable recommendations | Sparse data |
| Hybrid | Combination | Best accuracy | Complex |
| Knowledge-Based | Rules | Works without history | Domain expertise needed |
| Popularity-Based | Trending items | Simple | Not personalized |

---

# Summary

A **Recommendation System** is a machine learning application that predicts and suggests relevant items to users. The most common approaches are **Content-Based Filtering**, **Collaborative Filtering (User-Based and Item-Based)**, and **Hybrid Recommendation Systems**. Advanced systems often use **Matrix Factorization (SVD/ALS)** and similarity measures such as **Cosine Similarity** or **Pearson Correlation**. Recommendation systems power modern platforms like Netflix, Amazon, Spotify, YouTube, and LinkedIn by delivering personalized user experiences.
