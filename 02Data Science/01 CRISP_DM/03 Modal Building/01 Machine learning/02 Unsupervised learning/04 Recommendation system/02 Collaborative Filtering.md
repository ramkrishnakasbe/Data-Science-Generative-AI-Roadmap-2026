# Collaborative Filtering

# Overview

Collaborative Filtering (CF) is one of the most widely used recommendation techniques in Machine Learning. It recommends items based on the behavior and preferences of similar users or similar items.

Unlike **Content-Based Filtering**, Collaborative Filtering does **not require item features**. Instead, it relies on user interactions such as ratings, purchases, clicks, or watch history.

It is the backbone of recommendation systems used by Netflix, Amazon, Spotify, YouTube, and many e-commerce platforms.

---

# Definition

Collaborative Filtering is a recommendation technique that predicts a user's preferences based on the preferences of other users with similar tastes or based on items that have similar interaction patterns.

**Key Idea:**

> Users with similar interests tend to like similar items.

---

# Characteristics

- Unsupervised Learning
- Uses user-item interactions
- Does not require item metadata
- Learns from collective user behavior
- Highly personalized recommendations
- Improves with more user data

---

# Real-Life Example

Suppose:

| User | Movies Liked |
|------|--------------|
| Ram | Avengers, Iron Man, Thor |
| Ravi | Avengers, Iron Man |
| Priya | Titanic, Notebook |

Ram and Ravi have similar interests.

Since Ram liked **Thor** and Ravi hasn't watched it,

the system recommends **Thor** to Ravi.

---

# Collaborative Filtering Workflow

```text
Collect User Data

↓

Create User-Item Matrix

↓

Calculate Similarity

↓

Find Nearest Users/Items

↓

Predict Ratings

↓

Recommend Top-N Items
```

---

# Types of Collaborative Filtering

```text
Collaborative Filtering

│

├── Memory-Based Filtering
│      ├── User-Based CF
│      └── Item-Based CF
│
└── Model-Based Filtering
       ├── Matrix Factorization
       ├── SVD
       ├── ALS
       └── Deep Learning Models
```

---

# 1. User-Based Collaborative Filtering

## Definition

User-Based Collaborative Filtering recommends items based on **similar users**.

If two users have similar preferences, the system recommends items liked by one user to the other.

---

## Working

```text
Find Similar Users

↓

Collect Their Favorite Items

↓

Recommend Unseen Items
```

---

## Example

| User | Movies |
|------|---------|
| Ram | A B C |
| Ravi | A B |
| Amit | D E |

Ram and Ravi are similar.

Since Ram watched **Movie C**, recommend it to Ravi.

---

# User Similarity

User similarity is calculated using:

- Cosine Similarity
- Pearson Correlation
- Euclidean Distance
- Jaccard Similarity

---

# User-Item Matrix

| User | Movie A | Movie B | Movie C | Movie D |
|------|:-------:|:-------:|:-------:|:-------:|
| Ram | 5 | 4 | 5 | ? |
| Ravi | 5 | 4 | ? | 3 |
| Priya | 2 | 1 | 2 | 5 |

Rows represent users.

Columns represent items.

Values represent ratings.

---

# Steps in User-Based CF

1. Build User-Item Matrix.
2. Compute similarity between users.
3. Select Top-K similar users.
4. Predict missing ratings.
5. Recommend highest-rated unseen items.

---

# Rating Prediction

Predicted rating for User **u** on Item **i**:

```text
Predicted Rating

=

Weighted Average of Ratings

from Similar Users
```

Mathematically:

```text
Pred(u,i)

=

Σ(Similarity × Rating)

----------------------------

Σ Similarity
```

---

# Advantages

- Personalized recommendations
- Simple implementation
- No need for item features

---

# Disadvantages

- Cold Start Problem
- Sparse data
- Slow with many users
- Scalability issues

---

# 2. Item-Based Collaborative Filtering

## Definition

Instead of finding similar users, Item-Based CF finds **similar items**.

If users frequently buy two products together, they are considered similar.

---

## Working

```text
Find Similar Items

↓

Recommend Similar Items
```

---

## Example

Suppose many users purchase:

```text
Laptop

↓

Mouse

↓

Keyboard

↓

Laptop Bag
```

A customer purchasing a Laptop may be recommended:

- Mouse
- Keyboard
- Laptop Bag

---

# Item Similarity

Similarity is calculated using:

- Cosine Similarity
- Pearson Correlation
- Adjusted Cosine Similarity

---

# Steps in Item-Based CF

1. Build User-Item Matrix.
2. Calculate similarity between items.
3. Find Top-K similar items.
4. Predict missing ratings.
5. Recommend similar items.

---

# User-Based vs Item-Based CF

| Feature | User-Based | Item-Based |
|---------|------------|------------|
| Finds Similar | Users | Items |
| Scalability | Lower | Better |
| Stability | Changes frequently | More stable |
| Recommendation | Based on similar users | Based on similar items |

---

# Similarity Measures

## 1. Cosine Similarity

Measures the cosine of the angle between two vectors.

Formula

```text
Cos(A,B)

=

A·B

--------------

||A|| ||B||
```

Range

```text
0 to 1
```

Higher value means greater similarity.

---

## 2. Pearson Correlation

Measures linear correlation between two users or items.

Formula

```text
Correlation

=

Cov(X,Y)

--------------

σxσy
```

Range

```text
-1 to +1
```

---

## 3. Euclidean Distance

Measures straight-line distance.

Formula

```text
√Σ(x−y)²
```

Smaller distance indicates higher similarity.

---

## 4. Jaccard Similarity

Suitable for binary interactions.

Formula

```text
Intersection

--------------

Union
```

---

# Memory-Based Collaborative Filtering

Uses the entire User-Item Matrix directly.

Examples:

- User-Based CF
- Item-Based CF

Advantages:

- Easy to implement
- Easy to explain

Disadvantages:

- Slow on large datasets
- Scalability problems

---

# Model-Based Collaborative Filtering

Instead of comparing users directly,

a Machine Learning model is trained.

Popular methods:

- Matrix Factorization
- Singular Value Decomposition (SVD)
- Alternating Least Squares (ALS)
- Neural Collaborative Filtering (NCF)

Advantages:

- Faster predictions
- Better scalability
- Higher accuracy

---

# Matrix Factorization

The User-Item Matrix is decomposed into two lower-dimensional matrices.

```text
User Matrix

×

Item Matrix

↓

Predicted Ratings
```

Matrix Factorization discovers hidden (latent) factors that explain user preferences.

Popular techniques:

- SVD
- Truncated SVD
- ALS

---

# Cold Start Problem

Occurs when there is insufficient data.

### User Cold Start

New user with no history.

### Item Cold Start

New item with no ratings.

### System Cold Start

New platform with little data.

---

# Data Sparsity

Most users rate only a few items.

Result:

- Sparse User-Item Matrix
- Difficult similarity calculation

Solutions:

- Matrix Factorization
- Hybrid Recommendation
- Implicit Feedback

---

# Scalability Problem

As users and items grow,

similarity calculations become expensive.

Solutions:

- Item-Based CF
- SVD
- ALS
- Approximate Nearest Neighbor Search

---

# Python Example (Surprise Library)

```python
from surprise import Dataset
from surprise import SVD

# Load sample dataset
data = Dataset.load_builtin("ml-100k")

# Build trainset
trainset = data.build_full_trainset()

# Train SVD model
model = SVD()
model.fit(trainset)
```

Predict rating

```python
prediction = model.predict(uid=1, iid=10)

print(prediction.est)
```

---

# Advantages

- Highly personalized
- Discovers hidden preferences
- No need for item features
- Learns automatically
- Widely used in industry

---

# Disadvantages

- Cold Start Problem
- Data Sparsity
- Scalability issues
- Computationally expensive
- Requires a large amount of interaction data

---

# Applications

- Netflix Movie Recommendations
- Amazon Product Recommendations
- Spotify Music Suggestions
- YouTube Video Recommendations
- LinkedIn Job Recommendations
- Facebook Friend Suggestions
- E-commerce Cross-Selling

---

# Collaborative Filtering vs Content-Based Filtering

| Feature | Collaborative Filtering | Content-Based Filtering |
|----------|-------------------------|-------------------------|
| Uses | User interactions | Item features |
| Item metadata required | No | Yes |
| Personalized | Yes | Yes |
| Recommends new interests | Yes | Limited |
| Suffers from cold start | Yes | Mainly user cold start |
| Diversity | High | Lower |

---

# Interview Questions

## 1. What is Collaborative Filtering?

A recommendation technique that predicts user preferences based on the behavior of similar users or similar items.

---

## 2. What are the two main types?

- User-Based Collaborative Filtering
- Item-Based Collaborative Filtering

---

## 3. What is the difference between Memory-Based and Model-Based CF?

- **Memory-Based CF** uses the user-item matrix directly and computes similarities at recommendation time.
- **Model-Based CF** trains a machine learning model (e.g., SVD, ALS) to learn latent patterns and make predictions.

---

## 4. What is the Cold Start Problem?

The difficulty of making recommendations for new users, new items, or a new system due to insufficient interaction data.

---

## 5. Why is SVD used in Collaborative Filtering?

SVD performs **matrix factorization**, discovering latent factors that capture hidden relationships between users and items. This improves recommendation accuracy and handles sparse datasets more effectively.

---

# Summary

Collaborative Filtering is a recommendation technique that predicts user preferences based on the collective behavior of users. It can be implemented as **User-Based**, **Item-Based**, or **Model-Based** approaches. Similarity measures such as **Cosine Similarity**, **Pearson Correlation**, and **Euclidean Distance** are used to identify similar users or items, while advanced methods like **SVD** and **ALS** leverage matrix factorization to improve scalability and accuracy. Despite challenges such as **cold start** and **data sparsity**, Collaborative Filtering remains one of the most widely adopted recommendation techniques in modern applications.
