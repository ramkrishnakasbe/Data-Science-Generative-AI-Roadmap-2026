# 10. String Manipulation (Text Preprocessing in NLP)

# Overview

String Manipulation (Text Preprocessing) is the process of cleaning, transforming, and preparing textual data before applying Natural Language Processing (NLP) or Machine Learning algorithms.

Computers cannot understand raw text directly. Therefore, text must be converted into a structured format that models can process efficiently.

---

# Why String Manipulation is Important?

Text preprocessing helps to:

- Remove unwanted words and symbols
- Reduce text complexity
- Improve model accuracy
- Reduce dimensionality
- Improve training speed
- Standardize textual data

---

# Text Preprocessing Pipeline

```
Raw Text
    │
    ▼
Tokenization
    │
    ▼
Lower Case Conversion
    │
    ▼
Remove Punctuation
    │
    ▼
Remove Stop Words
    │
    ▼
Stemming / Lemmatization
    │
    ▼
Word Embedding
    │
    ▼
Machine Learning Model
```

---

# 1. Tokenization

## Definition

Tokenization is the process of breaking text into smaller units called **tokens**.

A token may be:

- Word
- Sentence
- Character
- Sub-word

It is usually the first step in NLP.

---

## Types of Tokenization

### A. Word Tokenization

Splits a sentence into words.

Example

```
Sentence:

"I love Data Science"

↓

["I", "love", "Data", "Science"]
```

---

### B. Sentence Tokenization

Splits a paragraph into sentences.

Example

```
"I love NLP. It is interesting."

↓

Sentence 1
Sentence 2
```

---

### C. Character Tokenization

Splits text into individual characters.

Example

```
Hello

↓

H
e
l
l
o
```

---

## Python Example

```python
from nltk.tokenize import word_tokenize

text = "I love Data Science"

tokens = word_tokenize(text)

print(tokens)
```

---

## Advantages

- First step of NLP
- Converts text into processable units
- Preserves word order

---

## Applications

- Chatbots
- Translation
- Text Classification
- Search Engines

---

# 2. Stemming

## Definition

Stemming reduces a word to its root form by removing prefixes or suffixes.

The resulting word may **not be a valid English word**.

---

## Example

| Original | Stem |
|----------|------|
| Playing | Play |
| Played | Play |
| Player | Player |
| Studies | Studi |
| Running | Run |

Notice:

```
Studies

↓

Studi ❌
```

Not a valid English word.

---

## Popular Stemmers

- Porter Stemmer
- Snowball Stemmer
- Lancaster Stemmer

---

## Python Example

```python
from nltk.stem import PorterStemmer

ps = PorterStemmer()

print(ps.stem("playing"))
print(ps.stem("studies"))
```

---

## Advantages

- Fast
- Simple
- Reduces vocabulary size

---

## Disadvantages

- Produces incorrect words
- Lower accuracy than lemmatization

---

# 3. Lemmatization

## Definition

Lemmatization converts words into their **dictionary (lemma) form** using vocabulary and grammar.

Unlike stemming, the output is always a meaningful word.

---

## Example

| Original | Lemma |
|----------|-------|
| Playing | Play |
| Better | Good |
| Studies | Study |
| Running | Run |
| Children | Child |

---

## Python Example

```python
from nltk.stem import WordNetLemmatizer

lemmatizer = WordNetLemmatizer()

print(lemmatizer.lemmatize("studies"))
```

---

## Advantages

- Produces meaningful words
- More accurate
- Preferred in NLP projects

---

## Disadvantages

- Slower than stemming
- Requires dictionary lookup

---

# Stemming vs Lemmatization

| Feature | Stemming | Lemmatization |
|----------|-----------|---------------|
| Dictionary Used | No | Yes |
| Speed | Fast | Slower |
| Accuracy | Lower | Higher |
| Output | May not be a word | Valid word |
| Example | Studies → Studi | Studies → Study |

---

# 4. Stop Word Removal

## Definition

Stop words are commonly occurring words that carry very little meaning.

Examples include:

```
is
am
are
the
a
an
of
to
for
in
on
```

These words are removed to reduce unnecessary information.

---

## Example

Original Sentence

```
I am learning Data Science in Python
```

After Removing Stop Words

```
learning Data Science Python
```

---

## Python Example

```python
from nltk.corpus import stopwords

stop_words = set(stopwords.words("english"))

words = ["I","am","learning","Data","Science"]

filtered = [w for w in words if w.lower() not in stop_words]

print(filtered)
```

---

## Advantages

- Reduces dimensionality
- Faster model training
- Removes unnecessary words

---

## Disadvantages

Sometimes stop words carry important meaning.

Example

```
I do NOT like this movie
```

Removing

```
NOT
```

changes the meaning completely.

---

# 5. Word Embedding

## Definition

Word Embedding converts words into dense numerical vectors while preserving their semantic meaning.

Words with similar meanings have similar vector representations.

Unlike One-Hot Encoding, word embeddings capture relationships between words.

---

## Why Word Embeddings?

One-Hot Encoding treats all words as independent.

Example:

```
King

Queen

Man

Woman
```

All are equally distant.

Word Embeddings learn semantic relationships.

Example:

```
King - Man + Woman ≈ Queen
```

---

## Types of Word Embeddings

### A. Word2Vec

Developed by Google.

Techniques:

- CBOW (Continuous Bag of Words)
- Skip-Gram

---

### B. GloVe

Developed by Stanford.

Uses global word co-occurrence statistics.

---

### C. FastText

Developed by Facebook.

Represents words using character n-grams.

Handles unknown words better.

---

### D. Contextual Embeddings

Modern transformer-based embeddings.

Examples:

- BERT
- RoBERTa
- GPT Embeddings

These generate different vectors depending on context.

---

## Applications

- Sentiment Analysis
- Machine Translation
- Chatbots
- Recommendation Systems
- Question Answering

---

# 6. Document Similarity

## Definition

Document Similarity measures how similar two documents are.

It is widely used in:

- Search engines
- Recommendation systems
- Duplicate document detection
- Plagiarism detection

---

## Common Similarity Measures

### Cosine Similarity

Most widely used method.

Measures the angle between two vectors.

Range

```
-1 to 1
```

Usually for text:

```
0 → Completely different

1 → Exactly same
```

---

### Euclidean Distance

Measures straight-line distance.

Smaller distance indicates higher similarity.

---

### Jaccard Similarity

Measures overlap between two sets.

Formula

```
Intersection / Union
```

Useful for comparing sets of words.

---

## Python Example

```python
from sklearn.metrics.pairwise import cosine_similarity
```

---

# Applications

- Search Engines
- Resume Matching
- Recommendation Systems
- Duplicate Detection

---

# 7. Topic Modeling

## Definition

Topic Modeling is an unsupervised learning technique used to automatically discover hidden topics in a collection of documents.

Instead of manually assigning topics, the algorithm identifies groups of related words.

---

## Example

Documents

```
Football
Cricket
Player
Match
Goal
```

↓

Topic

```
Sports
```

---

Another document

```
Bank
Money
Loan
Finance
```

↓

Topic

```
Finance
```

---

## Popular Topic Modeling Algorithms

### 1. LDA (Latent Dirichlet Allocation)

Most widely used.

Each document contains multiple topics.

Each topic contains multiple words.

---

### 2. LSA (Latent Semantic Analysis)

Uses matrix decomposition (SVD).

Finds hidden semantic relationships.

---

### 3. NMF (Non-negative Matrix Factorization)

Matrix factorization technique.

Works well for sparse text data.

---

## Applications

- News categorization
- Customer feedback analysis
- Research paper organization
- Social media analysis
- Document clustering

---

# Complete NLP Preprocessing Flow

```
Raw Text
      │
      ▼
Tokenization
      │
      ▼
Lower Case
      │
      ▼
Remove Punctuation
      │
      ▼
Remove Stop Words
      │
      ▼
Stemming / Lemmatization
      │
      ▼
Word Embedding
      │
      ▼
Feature Extraction
      │
      ▼
Machine Learning Model
```

---

# Comparison of Techniques

| Technique | Purpose | Output |
|-----------|---------|--------|
| Tokenization | Split text | Tokens |
| Stemming | Remove suffixes | Root word (may be invalid) |
| Lemmatization | Dictionary root | Valid word |
| Stop Word Removal | Remove common words | Important words |
| Word Embedding | Convert words into vectors | Dense vectors |
| Document Similarity | Compare documents | Similarity score |
| Topic Modeling | Discover hidden topics | Topics |

---

# Summary

String Manipulation (Text Preprocessing) is a fundamental step in Natural Language Processing (NLP). It prepares raw text for machine learning by cleaning, simplifying, and converting it into numerical representations. Common techniques include **Tokenization**, **Stemming**, **Lemmatization**, **Stop Word Removal**, **Word Embedding**, **Document Similarity**, and **Topic Modeling**. Proper text preprocessing improves model performance, reduces computational complexity, and enables algorithms to understand human language more effectively.
