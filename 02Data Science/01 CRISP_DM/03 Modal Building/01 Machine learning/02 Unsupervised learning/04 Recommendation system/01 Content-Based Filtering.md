# Content-Based Filtering

# Overview

Content-Based Filtering (CBF) is one of the most widely used recommendation techniques in Machine Learning. It recommends items to a user based on the **features (content)** of items that the user has previously liked or interacted with.

Unlike Collaborative Filtering, it **does not depend on other users**. Instead, it builds a profile of each user based on their interests and recommends similar items.

---

# Definition

Content-Based Filtering is a recommendation technique that recommends items **similar to those a user has liked in the past** by comparing item features.

It answers the question:

> **"If the user liked this item before, what other items have similar characteristics?"**

---

# Real-Life Examples

### Netflix

If you frequently watch:

- Action Movies
- Sci-Fi Movies
- Marvel Movies

Netflix recommends:

- Avengers
- Iron Man
- Captain America
- Mission Impossible

---

### Spotify

If you listen to:

- Rock Music

Spotify recommends more Rock songs.

---

### Amazon

If you purchase:

- Python Programming Books

Amazon recommends:

- Machine Learning Books
- Data Science Books
- AI Books

---

# Characteristics

- Personalized recommendations
- Uses item features
- Independent of other users
- Requires item metadata
- Easy to interpret
- Suitable for new items

---

# Working Principle

```
User History

↓

Identify Liked Items

↓

Extract Item Features

↓

Create User Profile

↓

Compare with Other Items

↓

Recommend Most Similar Items
```

---

# Example

Suppose a user watches the following movies:

| Movie | Genre |
|-------|--------|
| Iron Man | Action, Sci-Fi |
| Avengers | Action, Sci-Fi |
| Captain America | Action |

The user profile becomes:

```
Action ⭐⭐⭐⭐⭐

Sci-Fi ⭐⭐⭐⭐

Comedy ⭐

Romance ⭐
```

Now suppose another movie has features:

```
Mission Impossible

Genre

Action

Thriller
```

Since it matches the user's interest, it is recommended.

---

# Components of Content-Based Filtering

```
Content-Based Filtering

│

├── User Profile

├── Item Profile

├── Feature Extraction

├── Similarity Calculation

└── Recommendation
```

---

# 1. User Profile

A user profile represents the interests and preferences of a user.

It is created from:

- Ratings
- Purchases
- Search History
- Watch History
- Click History
- Likes

Example

```
User

Likes

Action

Sci-Fi

Adventure
```

---

# 2. Item Profile

Each item is represented using its features.

Example

Movie

```
Title

Avengers
```

Features

```
Genre

Action

Sci-Fi

Adventure

Marvel
```

Book

```
Author

Publication

Category

Language
```

Product

```
Brand

Price

Category

Color
```

---

# 3. Feature Extraction

Feature extraction converts item attributes into numerical vectors.

Example

| Movie | Action | Comedy | Romance | Sci-Fi |
|--------|:------:|:-------:|:--------:|:-------:|
| Iron Man |1|0|0|1|
| Avengers |1|0|0|1|
| Titanic |0|0|1|0|

These vectors are used to calculate similarity.

---

# Feature Representation Techniques

### Numerical Features

```
Age

Salary

Price
```

---

### Categorical Features

```
Genre

Language

Country
```

Usually converted using

- One-Hot Encoding
- Label Encoding

---

### Text Features

Used in:

- Movies
- News
- Books
- Articles

Common methods:

- Bag of Words (BoW)
- TF-IDF
- Word Embeddings (Word2Vec, GloVe, BERT)

---

# Similarity Measures

After representing items as vectors, similarity is calculated.

Most popular methods:

- Cosine Similarity ⭐
- Euclidean Distance
- Jaccard Similarity
- Pearson Correlation

---

# Cosine Similarity

## Definition

Cosine Similarity measures the cosine of the angle between two vectors.

It measures **direction**, not magnitude.

---

## Formula

```
Cos(A,B)

=

A · B

----------------

||A|| ||B||
```

where:

- A · B = Dot Product
- ||A|| = Magnitude of A
- ||B|| = Magnitude of B

---

## Range

```
-1  to  1
```

For most recommendation systems (non-negative vectors):

```
0 to 1
```

---

## Interpretation

| Cosine Similarity | Meaning |
|------------------:|---------|
| 1 | Exactly Similar |
| 0.8 | Highly Similar |
| 0.5 | Moderately Similar |
| 0 | No Similarity |

---

## Example

Movie A

```
[1,1,0,1]
```

Movie B

```
[1,1,0,0]
```

Cosine similarity

```
≈0.82
```

Hence,

Recommend Movie B.

---

# Euclidean Distance

Measures the straight-line distance between two vectors.

Formula

```
√Σ(x−y)²
```

Smaller distance indicates greater similarity.

---

# Jaccard Similarity

Used mainly for binary data.

Formula

```
Intersection

-------------

Union
```

Example

```
User A

Action

Comedy

Sci-Fi

User B

Action

Sci-Fi
```

Jaccard Similarity

```
2/3

=

0.67
```

---

# Recommendation Workflow

```
User History

↓

Build User Profile

↓

Extract Item Features

↓

Convert to Feature Vectors

↓

Calculate Similarity

↓

Rank Items

↓

Recommend Top-N Items
```

---

# Example Workflow

```
User watches

Iron Man

↓

Action

Sci-Fi

↓

Find Movies

↓

Avengers

Captain America

Mission Impossible

↓

Recommend
```

---

# Python Example

## Using TF-IDF + Cosine Similarity

```python
from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.metrics.pairwise import cosine_similarity

movies = [
    "Action Sci-Fi Marvel",
    "Action Adventure",
    "Romance Drama"
]

tfidf = TfidfVectorizer()

matrix = tfidf.fit_transform(movies)

similarity = cosine_similarity(matrix)

print(similarity)
```

---

# Advantages

- Personalized recommendations
- Easy to understand
- No dependency on other users
- Works well with new items
- Fast recommendation generation
- Preserves user privacy

---

# Disadvantages

- Requires detailed item features
- Over-specialization (recommends only similar items)
- Difficult to recommend diverse content
- Limited discovery of new interests
- New users (without history) face the **User Cold Start** problem

---

# Content-Based Filtering vs Collaborative Filtering

| Content-Based | Collaborative |
|---------------|---------------|
| Uses item features | Uses user behavior |
| No need for other users | Requires many users |
| Works for new items | Suffers from item cold start |
| Personalized | Community-driven |
| Limited diversity | Better diversity |

---

# Applications

- Netflix Movie Recommendation
- Spotify Music Recommendation
- Amazon Product Recommendation
- News Article Recommendation
- Job Recommendation
- Book Recommendation
- E-Learning Course Recommendation
- Restaurant Recommendation

---

# Interview Questions

## 1. What is Content-Based Filtering?

A recommendation technique that suggests items similar to those a user has previously liked based on item features.

---

## 2. What information is required?

- User history
- Item features (metadata)

---

## 3. Which similarity measure is most commonly used?

**Cosine Similarity** is the most widely used similarity measure for content-based recommendation systems.

---

## 4. What is the biggest limitation?

**Over-specialization**, where users continue to receive recommendations that are very similar to their past preferences, limiting discovery of new content.

---

## 5. Does Content-Based Filtering require data from other users?

**No.** It relies only on the user's own interactions and the features of the items.

---

# Summary

Content-Based Filtering is a recommendation technique that recommends items similar to those a user has liked in the past by analyzing **item features**. It builds a **user profile** from historical interactions, represents items as feature vectors, and uses similarity measures such as **Cosine Similarity**, **Euclidean Distance**, or **Jaccard Similarity** to identify and recommend the most relevant items. It is simple, interpretable, and effective when rich item metadata is available, making it widely used in movie, music, news, and product recommendation systems.
