# 02 Types of Naive Bayes.md

# Introduction

Naive Bayes is not a single algorithm. Depending on the type of input data, different variants of Naive Bayes are used.

The major types are:

1. Gaussian Naive Bayes
2. Multinomial Naive Bayes
3. Bernoulli Naive Bayes
4. Complement Naive Bayes

The difference lies in how they calculate the **Likelihood P(X|C)**.

---

# Choosing the Correct Naive Bayes

| Data Type | Algorithm |
|------------|-----------|
| Continuous Numerical Data | Gaussian NB |
| Word Counts | Multinomial NB |
| Binary Features (0/1) | Bernoulli NB |
| Imbalanced Text Dataset | Complement NB |

---

# 1. Gaussian Naive Bayes

## Definition

Gaussian Naive Bayes assumes that numerical features follow a **Normal (Gaussian) Distribution**.

Suitable for

- Height
- Weight
- Age
- Temperature
- Salary
- Continuous Variables

---

## Gaussian Distribution

```
            *
          *   *
        *       *
      *           *
----*---------------*-----
```

Bell-shaped curve

---

## Assumption

Each feature follows

```
X ~ N(μ,σ²)
```

where

- μ = Mean
- σ = Standard Deviation

---

## Probability Density Function

```
                 1
P(x)= --------------------------
      √(2πσ²)

      × e^(-(x-μ)² / 2σ²)
```

The algorithm computes this probability for every feature.

---

## Example

Predict whether a patient has diabetes.

Features

- Age
- BMI
- Blood Pressure

Since all are numerical,

Use

```
Gaussian Naive Bayes
```

---

## Advantages

- Works well with numerical data
- Fast
- Easy implementation

---

## Limitations

- Assumes normal distribution
- Sensitive to outliers

---

# 2. Multinomial Naive Bayes

## Definition

Used when features represent **counts or frequencies**.

Mostly used in

- NLP
- Text Classification
- Spam Detection

---

## Example

Sentence

```
I love AI
```

Vocabulary

```
I

Love

AI

Python
```

Vector

```
[1 1 1 0]
```

If

```
AI AI AI Python
```

Vector

```
[0 0 3 1]
```

Counts matter.

---

## Formula

Likelihood

```
P(Word|Class)

=

Word Count

--------------

Total Words
```

---

## Applications

- Spam Detection
- Email Classification
- News Classification
- Document Classification

---

## Advantages

- Excellent for text data
- Fast
- High accuracy

---

## Limitations

Cannot handle continuous numerical features directly.

---

# 3. Bernoulli Naive Bayes

## Definition

Bernoulli NB works on **binary features**.

Each feature is

```
0

or

1
```

Meaning

Word Present?

Yes → 1

No → 0

---

## Example

Vocabulary

```
AI

Python

Data
```

Document

```
AI Python
```

Vector

```
[1 1 0]
```

Word frequency is ignored.

Only presence matters.

---

## Applications

- Email Classification
- Binary Text Features
- Document Classification

---

## Advantages

- Simple
- Works well for binary data

---

## Disadvantages

Ignores word frequency.

---

# Bernoulli vs Multinomial

Sentence

```
AI AI AI Python
```

Bernoulli

```
AI = 1

Python =1
```

Multinomial

```
AI =3

Python =1
```

Multinomial preserves frequency.

---

# 4. Complement Naive Bayes

## Why was it introduced?

Multinomial NB performs poorly on **imbalanced datasets**.

Complement Naive Bayes improves performance.

---

## Idea

Instead of learning from

```
Current Class
```

It learns from

```
All Other Classes
```

Hence the name

```
Complement
```

---

## Applications

- Highly Imbalanced Text Classification
- News Articles
- Large Vocabulary Problems

---

## Advantages

- Better for imbalanced datasets
- Better accuracy than Multinomial NB in some cases

---

# Laplace Smoothing

## Zero Frequency Problem

Suppose

Training Data

```
Spam

Lottery

Offer

Prize
```

Test Email

```
Scholarship
```

Since

```
Scholarship
```

never appeared,

Probability becomes

```
0
```

Entire prediction becomes zero.

---

## Solution

Add 1 to every count.

Formula

```
P(word|class)

=

Count(word)+1

---------------------------

Total Words + Vocabulary Size
```

This is called

- Laplace Smoothing
- Add-One Smoothing

---

## Example

Without smoothing

```
Lottery

Probability

3/10
```

Scholarship

```
0/10
```

With smoothing

```
Scholarship

1/(10+V)
```

Now probability is never zero.

---

# Log Probability

## Why use Log?

Suppose

```
0.0001

×

0.0002

×

0.0003

×

0.0005
```

Product becomes

```
0.000000000003
```

Very small values cause **Numerical Underflow**.

Instead

Take logarithm.

```
log(a×b×c)

=

log(a)

+

log(b)

+

log(c)
```

Now multiplication becomes addition.

Advantages

- Faster
- Stable
- Avoids underflow

---

# Comparison

| Feature | Gaussian | Multinomial | Bernoulli | Complement |
|----------|-----------|-------------|------------|-------------|
| Continuous Data | ✅ | ❌ | ❌ | ❌ |
| Word Counts | ❌ | ✅ | ❌ | ✅ |
| Binary Features | ❌ | ❌ | ✅ | ❌ |
| Imbalanced Dataset | ❌ | Average | Average | ✅ |
| Spam Detection | ❌ | ✅ | ✅ | ✅ |
| Numerical Data | ✅ | ❌ | ❌ | ❌ |

---

# Which Naive Bayes Should You Use?

| Problem | Recommended Algorithm |
|----------|----------------------|
| Height, Weight | Gaussian NB |
| Sentiment Analysis | Multinomial NB |
| Spam Detection | Multinomial NB |
| Binary Features | Bernoulli NB |
| Imbalanced Text Data | Complement NB |

---

# Advantages

- Very fast
- Easy to train
- Works well on high-dimensional data
- Excellent for NLP
- Low memory usage

---

# Disadvantages

- Independence assumption
- Sensitive to correlated features
- Gaussian assumes normal distribution
- Bernoulli ignores frequency

---

# Interview Questions

### Which Naive Bayes is used for numerical data?

**Gaussian Naive Bayes**

---

### Which Naive Bayes is best for text classification?

**Multinomial Naive Bayes**

---

### Which Naive Bayes works with binary features?

**Bernoulli Naive Bayes**

---

### Which Naive Bayes handles imbalanced datasets better?

**Complement Naive Bayes**

---

### What is Laplace Smoothing?

A technique that prevents zero probabilities by adding **1** to every feature count.

---

### Why use Log Probability?

To avoid numerical underflow and convert multiplication into addition.

---

# Summary

- **Gaussian NB** → Continuous numerical features.
- **Multinomial NB** → Count-based features (most common for NLP).
- **Bernoulli NB** → Binary (0/1) features.
- **Complement NB** → Imbalanced text datasets.
- **Laplace Smoothing** solves the zero-frequency problem.
- **Log Probability** improves numerical stability during probability calculations.
