# Text Mining Terminology

This document contains the most common terminology used in **Text Mining**, **Natural Language Processing (NLP)**, and **Large Language Models (LLMs)**. These terms are frequently asked in Data Science, NLP, and AI interviews.

---

# 1. Corpus

### Definition

A **Corpus** (plural: Corpora) is a collection of text documents used for text mining, NLP, and machine learning tasks.

### Examples

- Collection of News Articles
- Wikipedia Articles
- Customer Reviews
- Emails
- Tweets

---

# 2. Document

### Definition

A **Document** is a single unit of text within a corpus.

### Example

Corpus

```
Document 1 → Movie Review

Document 2 → Product Review

Document 3 → News Article
```

---

# 3. Sentence

### Definition

A sentence is a sequence of words expressing a complete thought.

Example

```
Machine Learning is amazing.
```

---

# 4. Token

### Definition

A **Token** is the smallest unit obtained after tokenization.

Example

Sentence

```
I love Machine Learning
```

Tokens

```
I

Love

Machine

Learning
```

---

# 5. Tokenization

### Definition

Tokenization is the process of breaking text into smaller units called **tokens**.

Types

- Word Tokenization
- Sentence Tokenization
- Character Tokenization

---

# 6. Lexicon

### Definition

A **Lexicon** is a dictionary or vocabulary containing words along with their meanings, sentiment scores, or linguistic information.

Applications

- Sentiment Analysis
- Spell Checking
- POS Tagging
- Named Entity Recognition

---

# 7. Vocabulary

### Definition

Vocabulary is the set of **unique words** present in a corpus.

Example

Sentence

```
Machine Learning is Machine Learning
```

Vocabulary

```
Machine

Learning

is
```

Vocabulary Size = **3**

---

# 8. Term

### Definition

A **Term** is any word or phrase considered important for analysis.

Example

```
Artificial Intelligence

Machine Learning

Deep Learning
```

---

# 9. Stop Words

### Definition

Commonly occurring words that usually do not contribute much meaning.

Examples

```
is

the

of

to

an

and
```

---

# 10. N-Gram

### Definition

An N-Gram is a sequence of **N consecutive words**.

Example

Sentence

```
I love Machine Learning
```

Unigram

```
I

Love

Machine

Learning
```

Bigram

```
I Love

Love Machine

Machine Learning
```

Trigram

```
I Love Machine

Love Machine Learning
```

---

# 11. Stemming

### Definition

Stemming removes prefixes or suffixes to obtain the root form of a word.

Example

```
Running

↓

Run

Connected

↓

Connect
```

---

# 12. Lemmatization

### Definition

Lemmatization converts a word into its **dictionary (base) form** using grammar and vocabulary.

Example

```
Better

↓

Good

Running

↓

Run
```

---

# 13. Morphology

### Definition

Morphology is the study of the internal structure and formation of words.

Example

```
Unhappiness

↓

Un + Happy + ness
```

---

# 14. Morpheme

### Definition

A **Morpheme** is the smallest meaningful unit of language.

Examples

```
un

happy

ness
```

Word

```
Unhappiness

=

Un + Happy + ness
```

Types

- Free Morpheme
- Bound Morpheme

---

# 15. Phoneme

### Definition

A **Phoneme** is the smallest unit of sound that can distinguish one word from another.

Examples

```
Bat

Cat
```

Only one sound changes.

---

# 16. Grapheme

### Definition

A **Grapheme** is the smallest written unit of a language (letters or characters).

Examples

```
A

B

C

क

你
```

---

# 17. Character

### Definition

A character is an individual letter, digit, punctuation mark, or symbol.

Example

```
M

L

1

@
```

---

# 18. Word Embedding

### Definition

A dense numerical vector representing the semantic meaning of a word.

Example

```
King

↓

[0.12, 0.45, -0.33, ...]
```

---

# 19. Document Embedding

### Definition

A numerical vector representing an entire document.

Popular Methods

- Doc2Vec
- Sentence Transformers
- BERT Embeddings

---

# 20. Vectorization

### Definition

Vectorization is the process of converting text into numerical vectors so machine learning algorithms can process it.

Methods

- Bag of Words
- TF-IDF
- Word2Vec
- CountVectorizer
- HashingVectorizer

---

# 21. Document Vectorization

### Definition

Converting an entire document into a numerical feature vector.

Applications

- Document Classification
- Recommendation Systems
- Similarity Search

---

# 22. Bag of Words (BoW)

### Definition

Represents text using the frequency of words while ignoring grammar and word order.

---

# 23. TF-IDF

### Definition

A weighting technique that measures the importance of a word in a document relative to the entire corpus.

---

# 24. Named Entity (Entity)

### Definition

A real-world object identified within text.

Examples

- Person
- Organization
- Location
- Date
- Money

Sentence

```
Google was founded in California.
```

Entities

```
Google

California
```

---

# 25. Named Entity Recognition (NER)

### Definition

The process of automatically identifying named entities from text.

---

# 26. Part-of-Speech (POS) Tagging

### Definition

Assigning grammatical labels to words.

Examples

```
Noun

Verb

Adjective

Adverb

Pronoun
```

---

# 27. Parsing

### Definition

Analyzing the grammatical structure of a sentence.

---

# 28. Chunking

### Definition

Grouping words into meaningful phrases.

Example

```
Natural Language Processing

↓

Noun Phrase
```

---

# 29. Parsing Tree (Syntax Tree)

### Definition

A tree representation showing the grammatical structure of a sentence.

---

# 30. Semantic Analysis

### Definition

Understanding the meaning of text rather than just its grammar.

---

# 31. Syntactic Analysis

### Definition

Analyzing sentence structure according to grammar rules.

---

# 32. Pragmatics

### Definition

Understanding language based on context and real-world knowledge.

Example

```
It's cold here.
```

Meaning may imply:

```
Please close the window.
```

---

# 33. Ambiguity

### Definition

When a word or sentence has multiple meanings.

Example

```
Bank
```

Could mean

- River Bank
- Financial Bank

---

# 34. Homonym

### Definition

Words with the **same spelling and pronunciation** but different meanings.

Examples

```
Bat

Animal

Cricket Bat
```

---

# 35. Homophone

### Definition

Words that sound the same but have different spellings and meanings.

Examples

```
Sea

See

Flower

Flour
```

---

# 36. Homograph

### Definition

Words with the **same spelling** but different meanings (sometimes different pronunciation).

Examples

```
Lead (Metal)

Lead (To Guide)

Bow (Ribbon)

Bow (To Bend)
```

---

# 37. Polysemy

### Definition

A single word having multiple related meanings.

Example

```
Head

Head of a person

Head of a company
```

---

# 38. Synonym

### Definition

Different words having similar meanings.

Examples

```
Big

Large

Huge
```

---

# 39. Antonym

### Definition

Words with opposite meanings.

Examples

```
Hot

Cold
```

---

# 40. Context

### Definition

The surrounding words that help determine the meaning of a word.

Example

```
River Bank

Bank Account
```

---

# 41. Language Model (LM)

### Definition

A model that predicts the probability of the next word or sequence of words in text.

Examples

- GPT
- BERT
- LLaMA
- Gemini

---

# 42. Transformer

### Definition

A deep learning architecture based on the **Attention Mechanism**, designed to process sequences efficiently and capture long-range dependencies.

---

# 43. Attention Mechanism

### Definition

A technique that enables a model to focus on the most relevant words in a sentence while processing text.

---

# 44. Embedding Space

### Definition

A high-dimensional vector space where semantically similar words are located close to each other.

---

# 45. Similarity

### Definition

A measure of how alike two pieces of text or vectors are.

Common Measures

- Cosine Similarity
- Jaccard Similarity
- Euclidean Distance
- Manhattan Distance

---

# Quick Revision Table

| Term | Definition |
|------|------------|
| Corpus | Collection of documents |
| Document | Single text file or article |
| Token | Smallest text unit after tokenization |
| Tokenization | Splitting text into tokens |
| Lexicon | Dictionary of words and meanings |
| Vocabulary | Unique words in a corpus |
| Stop Words | Frequently occurring words with little meaning |
| N-Gram | Sequence of N consecutive words |
| Stemming | Reduces words to root form using rules |
| Lemmatization | Converts words to dictionary form |
| Morpheme | Smallest meaningful unit of a word |
| Phoneme | Smallest unit of sound |
| Grapheme | Smallest written unit (letter/character) |
| Vectorization | Converting text into numerical vectors |
| Word Embedding | Dense vector representation of a word |
| Document Embedding | Dense vector representation of a document |
| BoW | Frequency-based text representation |
| TF-IDF | Importance-weighted text representation |
| Homonym | Same spelling & pronunciation, different meanings |
| Homophone | Same pronunciation, different spelling |
| Homograph | Same spelling, different meanings/pronunciation |
| Polysemy | One word with multiple related meanings |
| NER | Identifying named entities in text |
| POS Tagging | Assigning grammatical labels to words |
| Transformer | Attention-based deep learning architecture |
| Attention | Focus mechanism for important words |
| Embedding Space | Vector space where similar words are close together |
