# Feature Engineering, Text Classification & Topic Modeling

# 1. Feature Engineering

## Definition

Feature Engineering is the process of creating, selecting, transforming, and extracting useful features (variables) from raw text data to improve the performance of Machine Learning models.

Since ML algorithms cannot understand raw text, feature engineering converts text into meaningful numerical representations.

---

## Feature Engineering Pipeline

```
Raw Text
    │
    ▼
Text Preprocessing
    │
    ▼
Tokenization
    │
    ▼
Text Representation
    │
    ▼
Feature Engineering
    │
    ├── Feature Selection
    ├── Feature Extraction
    ├── Vocabulary Building
    └── Dimensionality Reduction
    │
    ▼
Machine Learning Model
```

---

# 1.1 Feature Selection

## Definition

Feature Selection is the process of selecting the **most relevant features** while removing irrelevant or redundant features.

It improves model performance and reduces computational cost.

### Why Feature Selection?

- Reduces overfitting
- Improves accuracy
- Reduces training time
- Removes noisy features
- Simplifies the model

---

### Feature Selection Techniques

#### Filter Methods

Features are selected using statistical measures.

Examples

- Chi-Square Test
- Information Gain
- Mutual Information
- Correlation

---

#### Wrapper Methods

Features are selected by repeatedly training the model.

Examples

- Forward Selection
- Backward Elimination
- Recursive Feature Elimination (RFE)

---

#### Embedded Methods

Feature selection happens during model training.

Examples

- LASSO Regression
- Decision Tree
- Random Forest Feature Importance

---

# 1.2 Feature Extraction

## Definition

Feature Extraction transforms the original text into a new set of informative numerical features.

Unlike feature selection, it **creates new features** instead of selecting existing ones.

---

### Common Feature Extraction Techniques

- Bag of Words (BoW)
- TF-IDF
- Word2Vec
- GloVe
- FastText
- Doc2Vec
- BERT Embeddings

---

### Advantages

- Captures useful information
- Reduces noise
- Improves model performance
- Converts text into numerical vectors

---

# 1.3 Vocabulary Building

## Definition

Vocabulary Building is the process of creating a list of **unique words (tokens)** from the corpus.

Example

Documents

```
I love AI

AI is amazing

Machine Learning
```

Vocabulary

```
I
love
AI
is
amazing
Machine
Learning
```

Vocabulary Size = **7**

---

### Importance

- Used in Bag of Words
- Used in Count Vectorizer
- Used in TF-IDF
- Used for One-Hot Encoding

---

# 1.4 Dimensionality Reduction

## Definition

Text data usually contains thousands of features.

Dimensionality Reduction reduces the number of features while preserving the important information.

---

### Why?

- Faster training
- Less memory usage
- Removes noise
- Reduces overfitting
- Better visualization

---

### Common Techniques

- PCA (Principal Component Analysis)
- Truncated SVD
- LSA
- Autoencoders
- UMAP
- t-SNE (Visualization)

---

# Feature Selection vs Feature Extraction

| Feature Selection | Feature Extraction |
|-------------------|-------------------|
| Selects existing features | Creates new features |
| Removes irrelevant features | Combines information |
| Original features remain | Original features transformed |
| Faster | More computationally expensive |

---

# 2. Text Classification

## Definition

Text Classification is the process of assigning predefined categories or labels to text documents.

Input

```
Email
```

Output

```
Spam
```

---

## Text Classification Pipeline

```
Raw Text
      │
      ▼
Text Cleaning
      │
      ▼
Tokenization
      │
      ▼
Feature Extraction
      │
      ▼
Classification Model
      │
      ▼
Predicted Class
```

---

## Common Algorithms

Traditional ML

- Naive Bayes
- Logistic Regression
- SVM
- Decision Tree
- Random Forest
- XGBoost

Deep Learning

- CNN
- LSTM
- GRU
- BERT
- RoBERTa
- DistilBERT

---

# 2.1 Spam Detection

### Definition

Classifying emails or SMS messages as

- Spam
- Not Spam

Features Used

- TF-IDF
- Word Embeddings
- Sender Information
- Keywords

Applications

- Gmail
- Outlook
- SMS Filtering

---

# 2.2 Sentiment Analysis

### Definition

Determining the emotional tone of text.

Classes

- Positive
- Negative
- Neutral

Example

```
This movie is amazing.

↓

Positive
```

Applications

- Product Reviews
- Customer Feedback
- Twitter Analysis
- Brand Monitoring

---

# 2.3 Topic Classification

### Definition

Assigning documents to predefined topics.

Example

```
Stock Market rises

↓

Business
```

Possible Categories

- Sports
- Politics
- Business
- Entertainment
- Technology
- Health

---

# 2.4 Email Classification

Automatically categorizing emails.

Categories

- Promotions
- Social
- Primary
- Updates
- Spam

Applications

- Gmail
- Outlook
- Yahoo Mail

---

# 2.5 News Classification

Automatically assigning news articles into categories.

Example

```
India wins World Cup

↓

Sports
```

Categories

- Sports
- Politics
- Technology
- Finance
- Entertainment
- Health

---

# Evaluation Metrics

- Accuracy
- Precision
- Recall
- F1 Score
- ROC-AUC
- Confusion Matrix

---

# 3. Topic Modeling

## Definition

Topic Modeling is an **unsupervised learning technique** that automatically discovers hidden topics from a collection of documents.

Unlike text classification, topic labels are **not predefined**.

---

## Topic Modeling Workflow

```
Documents
      │
      ▼
Preprocessing
      │
      ▼
Vectorization
      │
      ▼
Topic Modeling Algorithm
      │
      ▼
Hidden Topics
```

---

# Why Topic Modeling?

- Discover hidden themes
- Organize documents
- Document clustering
- Recommendation systems
- Trend analysis

---

# 3.1 Latent Semantic Analysis (LSA)

## Definition

LSA is a dimensionality reduction technique that discovers hidden relationships between words and documents using **Singular Value Decomposition (SVD).**

Pipeline

```
Documents
      │
      ▼
TF-IDF Matrix
      │
      ▼
SVD
      │
      ▼
Latent Topics
```

Advantages

- Fast
- Easy to implement
- Removes noise

Limitations

- Assumes linear relationships
- Topics may be difficult to interpret

---

# 3.2 Probabilistic Latent Semantic Analysis (PLSA)

## Definition

PLSA is a probabilistic model that represents each document as a mixture of topics and each topic as a probability distribution over words.

Instead of using matrix decomposition, PLSA models the probability of words appearing in documents.

Advantages

- Better topic modeling than LSA
- Probabilistic interpretation

Limitations

- Overfitting
- Doesn't generalize well to unseen documents

---

# 3.3 Latent Dirichlet Allocation (LDA)

## Definition

LDA is the most popular probabilistic topic modeling algorithm.

It assumes

- A document contains multiple topics.
- Each topic contains multiple words.

Example

Document

```
Football Match

↓

Sports (80%)

Politics (20%)
```

Pipeline

```
Documents
      │
      ▼
Bag of Words / TF-IDF
      │
      ▼
LDA
      │
      ▼
Topic Distribution
```

Advantages

- Highly interpretable
- Handles large document collections
- Most widely used topic model

Applications

- News Analysis
- Research Papers
- Social Media
- Customer Reviews

---

# 3.4 Non-negative Matrix Factorization (NMF)

## Definition

NMF decomposes a document-term matrix into two non-negative matrices.

```
Document-Term Matrix

=

Document-Topic Matrix

×

Topic-Word Matrix
```

Unlike SVD,

all values remain positive, making topics easier to interpret.

Advantages

- Easy to interpret
- Fast
- Good for sparse text data

Applications

- Topic Modeling
- Recommendation Systems
- Document Clustering

---

# Comparison of Topic Modeling Algorithms

| Algorithm | Technique | Supervised | Advantages | Limitations |
|------------|-----------|------------|------------|-------------|
| LSA | SVD | No | Fast, simple | Less interpretable |
| PLSA | Probabilistic | No | Better topic representation | Overfitting |
| LDA | Bayesian Probabilistic | No | Most popular, interpretable | Slower |
| NMF | Matrix Factorization | No | Easy to interpret | Requires choosing number of topics |

---

# Applications

- Document Organization
- News Categorization
- Search Engines
- Recommendation Systems
- Customer Feedback Analysis
- Social Media Analytics
- Scientific Literature Analysis
- Healthcare Documents
- Legal Documents

---

# Interview Questions

1. What is Feature Engineering?
2. Difference between Feature Selection and Feature Extraction?
3. Why is Vocabulary Building important?
4. What is Dimensionality Reduction in NLP?
5. What is Text Classification?
6. Explain Spam Detection and Sentiment Analysis.
7. Difference between Text Classification and Topic Modeling?
8. What is LSA?
9. Explain PLSA.
10. Why is LDA the most popular Topic Modeling algorithm?
11. Difference between LDA and NMF?
12. Which Topic Modeling algorithm is commonly used in industry?

---

# Summary

Feature Engineering transforms raw text into meaningful numerical representations through feature selection, feature extraction, vocabulary building, and dimensionality reduction. Text Classification is a supervised learning task that assigns predefined labels (e.g., spam, sentiment, news category) to documents. Topic Modeling is an unsupervised learning approach that discovers hidden themes in text using algorithms such as **LSA**, **PLSA**, **LDA**, and **NMF**, making it valuable for organizing, summarizing, and analyzing large collections of documents.
