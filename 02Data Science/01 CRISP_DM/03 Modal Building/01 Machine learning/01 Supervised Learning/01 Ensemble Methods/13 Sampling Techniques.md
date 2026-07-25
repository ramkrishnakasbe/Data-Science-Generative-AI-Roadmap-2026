# Sampling Techniques & Model Validation

> **Level:** Beginner → Advanced  
> **Prerequisites:** Basic Statistics, Machine Learning Fundamentals  
> **Goal:** Learn Probability Sampling, Non-Probability Sampling, Stratified Sampling, Systematic Sampling, Hold-Out Method, K-Fold Cross Validation, and LOOCV.

---

# Table of Contents

1. Introduction
2. What is Sampling?
3. Population vs Sample
4. Types of Sampling
5. Probability Sampling
6. Non-Probability Sampling
7. Stratified Sampling
8. Systematic Sampling
9. Hold-Out Method
10. Cross Validation
11. K-Fold Cross Validation
12. Stratified K-Fold Cross Validation
13. Leave-One-Out Cross Validation (LOOCV)
14. Comparison Table
15. Advantages & Disadvantages
16. Python Implementation
17. Interview Questions
18. Summary

---

# 1. Introduction

Sampling is the process of selecting a subset of observations from a population.

Instead of using the entire dataset, Machine Learning models often use a representative sample.

Sampling is important for

- Statistical Analysis
- Machine Learning
- Survey Analysis
- Model Validation
- Cross Validation

---

# 2. What is Sampling?

## Definition

Sampling is the process of selecting a subset of data from a larger population.

Example

```
Population

10,000 Customers

↓

Sample

1,000 Customers
```

The sample should represent the characteristics of the population.

---

# 3. Population vs Sample

| Population | Sample |
|------------|--------|
| Entire dataset | Subset of dataset |
| Large | Smaller |
| Expensive to analyze | Faster to analyze |
| Represents all observations | Represents selected observations |

---

# 4. Types of Sampling

Sampling techniques are broadly divided into

```
Sampling

│

├── Probability Sampling

│      ├── Simple Random Sampling
│      ├── Stratified Sampling
│      ├── Systematic Sampling

│

└── Non-Probability Sampling

       ├── Convenience Sampling
       ├── Judgment Sampling
       ├── Quota Sampling
       └── Snowball Sampling
```

---

# 5. Probability Sampling

## Definition

Every observation has a **known and non-zero probability** of being selected.

Selection is random.

Example

Population

```
A B C D E F G H
```

Random Sample

```
B D F H
```

---

## Types

### 1. Simple Random Sampling

Every observation has equal probability.

Example

```
Population

1 2 3 4 5 6

↓

Random Sample

2 5 6
```

---

### 2. Stratified Sampling

Population is divided into groups (strata).

Random samples are selected from each group.

Example

| Class | Count |
|------|------:|
| Positive | 900 |
| Negative | 100 |

10% Sample

| Class | Sample |
|------|------:|
| Positive | 90 |
| Negative | 10 |

Maintains class distribution.

---

### 3. Systematic Sampling

Select every **k-th observation** after choosing a random starting point.

Example

Population

```
1 2 3 4 5 6 7 8 9 10
```

Choose every 3rd sample

```
3

6

9
```

---

## Advantages

- Unbiased
- Representative
- Suitable for statistical inference

---

## Disadvantages

- May require complete population list
- Difficult for very large populations

---

# 6. Non-Probability Sampling

## Definition

Observations are selected without randomization.

Probability of selection is unknown.

---

## Types

### Convenience Sampling

Select easily available observations.

Example

Interviewing students in one classroom.

---

### Judgment Sampling

Researcher selects observations based on expertise.

---

### Quota Sampling

Select fixed numbers from each category.

Example

50 Males

50 Females

---

### Snowball Sampling

Existing participants recruit new participants.

Used in hidden populations.

Example

Drug users

Rare disease patients

---

## Advantages

- Fast
- Low cost
- Easy to implement

---

## Disadvantages

- High Bias
- Poor generalization
- Not representative

---

# 7. Stratified Sampling

## Definition

Population is divided into homogeneous groups.

Random samples are selected from each group.

Example

```
Population

↓

Male

Female

↓

Random Sampling

↓

Final Sample
```

---

## Why Stratified Sampling?

Useful for

- Imbalanced Classification
- Medical Data
- Fraud Detection

---

## Advantages

- Preserves class ratio
- Higher accuracy
- Lower sampling bias

---

# 8. Systematic Sampling

## Definition

Samples are selected at regular intervals.

Formula

```
k

=

Population Size

/

Sample Size
```

Example

Population

```
1000
```

Sample

```
100
```

```
k = 10
```

Choose

```
Every 10th Observation
```

---

## Advantages

- Simple
- Fast
- Uniform coverage

---

## Disadvantages

- Sensitive to hidden patterns
- Can introduce bias if data has periodic ordering

---

# 9. Hold-Out Method

Hold-Out is the simplest model validation technique.

Dataset

```
↓

Train Set

+

Test Set
```

Common Split

- 70 : 30
- 80 : 20
- 75 : 25

Example

```
1000 Records

↓

800 Train

200 Test
```

---

## Advantages

- Fast
- Easy
- Suitable for large datasets

---

## Disadvantages

- Performance depends on one split
- Higher variance

---

# 10. Cross Validation

Cross Validation repeatedly trains and evaluates the model using different subsets.

Purpose

- Better model evaluation
- Hyperparameter tuning
- Reduce evaluation bias

---

# 11. K-Fold Cross Validation

Dataset is divided into **K equal folds**.

Example

```
Dataset

↓

Fold1

Fold2

Fold3

Fold4

Fold5
```

Iteration 1

```
Train

F2 F3 F4 F5

Test

F1
```

Iteration 2

```
Train

F1 F3 F4 F5

Test

F2
```

Continue until every fold becomes the validation set exactly once.

Final Performance

```
Average of all K scores
```

---

## Common Values

- K = 5
- K = 10

---

## Advantages

- Better estimate
- Uses all data
- Less variance than Hold-Out

---

## Disadvantages

- Slower
- More computationally expensive

---

# 12. Stratified K-Fold Cross Validation

Normal K-Fold may create folds with unequal class distributions.

Stratified K-Fold preserves the class ratio in every fold.

Example

Original Dataset

```
90%

10%
```

Every Fold

```
90%

10%
```

Best choice for

- Classification
- Imbalanced datasets

---

# 13. Leave-One-Out Cross Validation (LOOCV)

LOOCV is an extreme version of K-Fold.

```
K = Number of Samples
```

Example

5 Samples

Iteration 1

```
Train

2 3 4 5

Test

1
```

Iteration 2

```
Train

1 3 4 5

Test

2
```

Repeat until every sample has been used once for testing.

---

## Advantages

- Maximum training data
- Very low bias

---

## Disadvantages

- Extremely slow
- High computational cost
- Not suitable for large datasets

---

# 14. Comparison Table

| Technique | Random | Preserves Class Ratio | Speed | Best Use |
|------------|--------|----------------------|-------|----------|
| Hold-Out | Yes | No | Fast | Large Dataset |
| K-Fold CV | Yes | No | Medium | General ML |
| Stratified K-Fold | Yes | Yes | Medium | Classification |
| LOOCV | Yes | Yes | Very Slow | Small Dataset |

---

# 15. Advantages & Disadvantages

## Hold-Out

### Advantages

- Fast
- Simple
- Easy implementation

### Disadvantages

- High variance
- Depends on one split

---

## K-Fold

### Advantages

- Better evaluation
- Uses all data
- Stable performance estimate

### Disadvantages

- More computation

---

## LOOCV

### Advantages

- Maximum training data
- Low bias

### Disadvantages

- Very slow
- Computationally expensive

---

# 16. Python Implementation

## Hold-Out

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X,
    y,
    test_size=0.2,
    random_state=42
)
```

---

## K-Fold

```python
from sklearn.model_selection import KFold

kf = KFold(
    n_splits=5,
    shuffle=True,
    random_state=42
)
```

---

## Stratified K-Fold

```python
from sklearn.model_selection import StratifiedKFold

skf = StratifiedKFold(
    n_splits=5,
    shuffle=True,
    random_state=42
)
```

---

## LOOCV

```python
from sklearn.model_selection import LeaveOneOut

loo = LeaveOneOut()
```

---

# 17. Interview Questions

## Beginner

1. What is Sampling?
2. Difference between Population and Sample?
3. What is Probability Sampling?
4. What is Non-Probability Sampling?
5. What is Stratified Sampling?

---

## Intermediate

1. Difference between Random and Stratified Sampling?
2. Explain Systematic Sampling.
3. Why is Stratified Sampling used in classification?
4. What is Hold-Out Validation?
5. Difference between Hold-Out and Cross Validation?

---

## Advanced

1. Explain K-Fold Cross Validation.
2. What is Stratified K-Fold?
3. Difference between LOOCV and K-Fold?
4. When should LOOCV be preferred?
5. Which validation method is best for imbalanced datasets?

---

# 18. Summary

- **Sampling** is selecting a subset of observations from a population.
- **Probability Sampling** gives every observation a known chance of selection.
- **Non-Probability Sampling** selects observations without randomization.
- **Stratified Sampling** preserves class distribution and is ideal for imbalanced datasets.
- **Systematic Sampling** selects every k-th observation after a random start.
- **Hold-Out Method** is the simplest validation technique using a single train-test split.
- **K-Fold Cross Validation** provides a more reliable estimate by averaging performance across multiple folds.
- **Stratified K-Fold** maintains class proportions in each fold.
- **LOOCV** uses one sample for testing and the remaining samples for training in each iteration.

---

# Key Takeaways

- **Probability Sampling → Random Selection**
- **Non-Probability Sampling → Non-Random Selection**
- **Stratified Sampling → Preserves Class Distribution**
- **Systematic Sampling → Every k-th Observation**
- **Hold-Out → Single Train-Test Split**
- **K-Fold CV → Multiple Train-Test Splits**
- **Stratified K-Fold → Best for Classification**
- **LOOCV → K = Number of Samples**
- **Cross Validation provides a more reliable estimate than a single Hold-Out split**
