# Text Mining

# 1. Introduction

## What is Text Mining?

Text Mining (also known as **Text Analytics**) is the process of extracting useful information, patterns, knowledge, and insights from **unstructured text data** using techniques from **Natural Language Processing (NLP)**, **Machine Learning**, **Statistics**, and **Linguistics**.

Unlike structured data (rows and columns), text data must first be cleaned and converted into a numerical format before machine learning algorithms can process it.

Examples of text data include:

- Emails
- Tweets
- News Articles
- Product Reviews
- Chat Messages
- Medical Records
- Legal Documents

---

## Why Text Mining?

Organizations generate huge amounts of text every day. Text mining helps convert this unstructured data into actionable insights.

Applications:

- Sentiment Analysis
- Spam Detection
- Document Classification
- Chatbots
- Recommendation Systems
- Search Engines
- Customer Feedback Analysis
- Fake News Detection

---

## Text Mining Pipeline

```
Raw Text

↓

Text Preprocessing

↓

Tokenization

↓

Stop Word Removal

↓

Stemming/Lemmatization

↓

Text Representation

↓

Feature Extraction

↓

Machine Learning / Deep Learning

↓

Prediction / Insights
```

---

# 2. Text Preprocessing

Text preprocessing improves text quality by removing unnecessary information before analysis.

---

## 2.1 Text Cleaning

Text cleaning removes unwanted information.

Example

```
Original

"Hello!!! Welcome to <b>OpenAI</b> 2025 :)"

↓

Cleaned

"hello welcome openai"
```

---

## 2.2 Lowercasing

Convert all characters to lowercase.

Example

```
Machine Learning

↓

machine learning
```

### Advantages

- Removes duplicate words due to case differences.
- Reduces vocabulary size.

---

## 2.3 Removing HTML Tags

Useful for web-scraped data.

Example

```
<p>Hello World</p>

↓

Hello World
```

Python

```python
from bs4 import BeautifulSoup

text = BeautifulSoup(html,"html.parser").get_text()
```

---

## 2.4 Removing Punctuation

Remove symbols such as

```
.,!?;:'"()[]{}
```

Example

```
Hello!!!

↓

Hello
```

---

## 2.5 Removing Numbers

Numbers may not contribute to meaning.

Example

```
iPhone 16

↓

iPhone
```

Keep numbers when they carry information (e.g., prices, years, ages).

---

## 2.6 Removing Special Characters

Remove characters like

```
@

#

$

%

^

*

_
```

Example

```
Python@2025

↓

Python
```

---

## 2.7 Removing Extra Spaces

Example

```
Machine      Learning

↓

Machine Learning
```

---

# 3. String Manipulation

---

## 3.1 Tokenization

### Definition

Tokenization is the process of breaking text into smaller units called **tokens**.

Sentence

```
Machine Learning is awesome
```

Tokens

```
["Machine",
 "Learning",
 "is",
 "awesome"]
```

Types

- Word Tokenization
- Sentence Tokenization
- Character Tokenization

Python

```python
from nltk.tokenize import word_tokenize

word_tokenize(text)
```

---

## 3.2 Stop Word Removal

### Definition

Stop words are common words that carry little meaning.

Examples

```
is

the

are

of

and

to
```

Sentence

```
Machine Learning is the future
```

After removal

```
Machine Learning future
```

Advantages

- Reduces noise
- Improves efficiency

---

## 3.3 Stemming

### Definition

Stemming removes suffixes to obtain the root form.

Examples

| Original | Stem |
|-----------|------|
| Playing | Play |
| Connected | Connect |
| Studies | Studi |
| Running | Run |

Algorithms

- Porter Stemmer
- Snowball Stemmer
- Lancaster Stemmer

Pros

- Fast
- Simple

Cons

- Root words may not be valid English words.

---

## 3.4 Lemmatization

### Definition

Lemmatization converts words to their dictionary (base) form using vocabulary and grammar.

Examples

| Original | Lemma |
|-----------|-------|
| Better | Good |
| Running | Run |
| Studies | Study |
| Went | Go |

Advantages

- More accurate than stemming.
- Produces meaningful words.

Disadvantages

- Slower than stemming.

---

## Stemming vs Lemmatization

| Stemming | Lemmatization |
|-----------|---------------|
| Rule-based | Dictionary-based |
| Faster | Slower |
| May create invalid words | Produces valid words |
| Less accurate | More accurate |

---

## 3.5 N-Grams

### Definition

N-Grams are sequences of **N consecutive words**.

Example

Sentence

```
I love Machine Learning
```

### Unigram (1-word)

```
I

Love

Machine

Learning
```

### Bigram (2-word)

```
I Love

Love Machine

Machine Learning
```

### Trigram (3-word)

```
I Love Machine

Love Machine Learning
```

Applications

- Auto-complete
- Language Modeling
- Machine Translation
- Search Engines

---

# 4. Text Representation

Machine learning models cannot understand text directly. Text representation converts text into numerical vectors.

---

## 4.1 Bag of Words (BoW)

### Definition

BoW represents a document by counting the frequency of each word.

Example

Documents

```
D1

I love AI

D2

I love Python
```

Vocabulary

```
I

Love

AI

Python
```

Vector Representation

| Document | I | Love | AI | Python |
|-----------|:-:|:-:|:-:|:-:|
| D1 |1|1|1|0|
| D2 |1|1|0|1|

Advantages

- Simple
- Easy to implement

Disadvantages

- Ignores word order
- High-dimensional sparse vectors

---
# Document-Term Matrix (DTM) & Term-Document Matrix (TDM)

Before applying Machine Learning algorithms, text documents are converted into a matrix representation. The two most common representations are:

- Document-Term Matrix (DTM)
- Term-Document Matrix (TDM)

---

# 1. Document-Term Matrix (DTM)

## Definition

A **Document-Term Matrix (DTM)** is a matrix where:

- **Rows represent documents**
- **Columns represent unique terms (words)**
- Each cell contains the frequency or weight of a term in a document.

It is the most commonly used representation in text mining.

---

## Example

Documents

```
D1 : I love AI

D2 : AI loves Python

D3 : I love Python
```

Vocabulary

```
I
Love
AI
Loves
Python
```

### Document-Term Matrix

| Document | I | Love | AI | Loves | Python |
|-----------|:-:|:-:|:-:|:-:|:-:|
| D1 |1|1|1|0|0|
| D2 |0|0|1|1|1|
| D3 |1|1|0|0|1|

---

### Characteristics

- Rows = Documents
- Columns = Terms
- Widely used in Machine Learning
- Input to BoW and TF-IDF
- Usually sparse

---

# 2. Term-Document Matrix (TDM)

## Definition

A **Term-Document Matrix (TDM)** is simply the transpose of a Document-Term Matrix.

Here,

- **Rows represent terms**
- **Columns represent documents**

---

## Example

| Term | D1 | D2 | D3 |
|------|:-:|:-:|:-:|
| I |1|0|1|
| Love |1|0|1|
| AI |1|1|0|
| Loves |0|1|0|
| Python |0|1|1|

---

### Characteristics

- Rows = Terms
- Columns = Documents
- Useful for word analysis
- Commonly used in information retrieval and topic modeling

---

# DTM vs TDM

| Feature | DTM | TDM |
|----------|-----|-----|
| Rows | Documents | Terms |
| Columns | Terms | Documents |
| Most Common | ✅ Yes | Less Common |
| ML Algorithms | ✅ Used | Rarely Used |
| TF-IDF | ✅ Yes | Yes |
| BoW | ✅ Yes | Yes |

---

# Relationship

```
           DTM

        Terms →
      ┌───────────────┐
Docs ↓│ D1 D2 D3 ...  │
      └───────────────┘

Transpose (T)

↓

           TDM

        Docs →
      ┌───────────────┐
Terms↓│ D1 D2 D3 ...  │
      └───────────────┘
```

Mathematically,

```
TDM = (DTM)ᵀ
```

---

# Applications

- Bag of Words (BoW)
- TF-IDF
- Topic Modeling (LSA, LDA, NMF)
- Text Classification
- Information Retrieval
- Document Clustering
- Recommendation Systems

---

# Interview Questions

### What is a Document-Term Matrix?

A matrix where rows represent documents, columns represent terms, and values indicate the frequency or weight of each term in each document.

---

### What is a Term-Document Matrix?

A matrix where rows represent terms and columns represent documents. It is the transpose of a Document-Term Matrix.

---

### Which one is commonly used in Machine Learning?

**Document-Term Matrix (DTM)** is the most commonly used representation for machine learning and NLP tasks.

---

### Is TF-IDF calculated on DTM or TDM?

Typically, **TF-IDF is computed on a Document-Term Matrix (DTM)**, where each row is a document and each column is a term.
#### TF-IDF (Term Frequency–Inverse Document Frequency)

### Definition

**TF-IDF** is a statistical technique used to measure the importance of a word in a document relative to a collection of documents (corpus).

- Words that appear **frequently in a document** receive a higher score.
- Words that appear **frequently across all documents** (e.g., *the*, *is*, *and*) receive a lower score.

---

### Formula

```
TF-IDF = TF × IDF
```

Where,

**Term Frequency (TF)**

Measures how often a term appears in a document.

```
TF = (Number of times a term appears in a document)
     ------------------------------------------------
       Total number of terms in the document
```

**Inverse Document Frequency (IDF)**

Measures how unique or rare a term is across the corpus.

```
IDF = log(Total Number of Documents
          -------------------------
          Number of Documents containing the term)
```

---

### Example

Documents

```
D1 : I love AI

D2 : I love Python

D3 : AI is amazing
```

- **"love"** appears in multiple documents → Lower IDF
- **"Python"** appears in only one document → Higher IDF

Therefore,

```
TF-IDF(Python) > TF-IDF(love)
```

---

### Advantages

- Gives more importance to unique words.
- Reduces the impact of common words.
- Improves text classification and information retrieval.
- Simple and computationally efficient.

---

### Limitations

- Ignores word order and context.
- Produces sparse vectors.
- Cannot capture semantic meaning (unlike Word2Vec or BERT).

---

### Applications

- Search Engines
- Text Classification
- Information Retrieval
- Document Ranking
- Keyword Extraction
- Recommendation Systems
## 4.3 One-Hot Encoding

Each word is represented as a binary vector.

Vocabulary

```
AI

ML

Python
```

Encoding

```
AI

[1 0 0]

ML

[0 1 0]

Python

[0 0 1]
```

Limitations

- Sparse vectors
- No semantic relationship

---

## 4.4 Count Vectorizer

CountVectorizer converts text into a matrix of word counts.

Example

```
I love AI

↓

[1 1 1]
```

Python

```python
from sklearn.feature_extraction.text import CountVectorizer

vectorizer = CountVectorizer()
X = vectorizer.fit_transform(corpus)
```

---

## 4.5 Hashing Vectorizer

Uses a hash function to map words into a fixed-size feature space.

Advantages

- Memory efficient
- Fast
- Suitable for large datasets

Disadvantages

- Hash collisions may occur.

---

# 5. Word Embeddings

Traditional methods treat words as independent. Word embeddings represent words as dense vectors where similar words have similar meanings.

---

## 5.1 Word2Vec

Developed by Google.

Learns word meanings from surrounding context.

Architectures

- CBOW (Continuous Bag of Words)
- Skip-Gram

Example

```
King

↓

[0.21, -0.44, 0.78, ...]
```

Advantages

- Captures semantic similarity.
- Dense vector representation.

---

## 5.2 GloVe (Global Vectors)

Developed by Stanford University.

Combines:

- Global word co-occurrence
- Local context

Advantages

- Better captures global statistics.
- Widely used in NLP.

---

## 5.3 FastText

Developed by Facebook.

Unlike Word2Vec, FastText learns embeddings for **subwords (character n-grams)**.

Advantages

- Handles rare words.
- Works well with misspellings.
- Supports multiple languages.

---

## 5.4 Doc2Vec

Extension of Word2Vec for representing **entire documents** instead of individual words.

Applications

- Document Classification
- Document Retrieval
- Recommendation Systems

---

## 5.5 BERT Embeddings

BERT (Bidirectional Encoder Representations from Transformers) generates **context-aware embeddings**.

Example

```
"I went to the bank to deposit money."

"I sat on the river bank."
```

The word **"bank"** receives different embeddings because BERT considers the surrounding context.

Advantages

- Context-aware
- State-of-the-art performance
- Handles polysemy (multiple meanings)

Applications

- Question Answering
- Named Entity Recognition
- Sentiment Analysis
- Search Engines
- Chatbots
- Large Language Models (LLMs)

---

# Interview Questions

1. What is Text Mining?
2. Explain the Text Mining pipeline.
3. Why is text preprocessing necessary?
4. Difference between Stemming and Lemmatization?
5. What are Stop Words?
6. What are N-grams?
7. Explain Bag of Words.
8. Difference between BoW and TF-IDF?
9. What is CountVectorizer?
10. What is HashingVectorizer?
11. What are Word Embeddings?
12. Difference between Word2Vec, GloVe, FastText, and BERT?
13. Why are embeddings better than One-Hot Encoding?
14. What are contextual embeddings?

---

# Summary

Text Mining is the process of extracting valuable information from unstructured text. A typical workflow involves preprocessing text, tokenization, stop-word removal, stemming or lemmatization, converting text into numerical representations (BoW, TF-IDF, CountVectorizer, HashingVectorizer), and using dense word embeddings (Word2Vec, GloVe, FastText, Doc2Vec, or BERT) to build machine learning or deep learning models for NLP applications.
