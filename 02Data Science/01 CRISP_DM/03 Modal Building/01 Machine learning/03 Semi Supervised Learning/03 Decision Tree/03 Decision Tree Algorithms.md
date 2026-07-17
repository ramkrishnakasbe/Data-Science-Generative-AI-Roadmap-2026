# 03 Decision Tree Algorithms.md

# 1. Introduction

Several Decision Tree algorithms have been developed over time. Each algorithm differs in the way it selects the best split, handles missing values, supports continuous attributes, and performs pruning.

The most popular algorithms are:

- ID3
- C4.5
- C5.0
- CART
- CHAID

---

# 2. ID3 (Iterative Dichotomiser 3)

## Introduction

ID3 was developed by **Ross Quinlan** in **1986**.

It is one of the earliest Decision Tree algorithms and is designed **only for classification problems**.

---

## Splitting Criterion

ID3 uses

```
Information Gain
```

to choose the best feature.

Feature with highest Information Gain is selected.

---

## Working

```
Training Dataset

↓

Calculate Entropy

↓

Calculate Information Gain

↓

Choose Best Feature

↓

Split Dataset

↓

Repeat Recursively

↓

Leaf Node
```

---

## Stopping Conditions

- All records belong to same class
- No features remain
- Dataset becomes empty

---

## Advantages

- Simple
- Easy implementation
- Easy interpretation

---

## Disadvantages

- Supports only categorical attributes
- No pruning
- Overfitting
- Biased toward attributes with many values
- Cannot handle missing values

---

# 3. C4.5 Algorithm

## Introduction

C4.5 is an improved version of ID3 developed by **Ross Quinlan**.

It solves many limitations of ID3.

---

## Improvements over ID3

- Supports continuous attributes
- Handles missing values
- Uses Gain Ratio
- Supports pruning
- Better accuracy

---

## Splitting Criterion

Instead of Information Gain,

C4.5 uses

```
Gain Ratio
```

---

## Working

```
Dataset

↓

Entropy

↓

Gain Ratio

↓

Best Feature

↓

Split

↓

Pruning

↓

Final Tree
```

---

## Advantages

- Handles numerical data
- Handles missing values
- Less overfitting
- Better than ID3

---

## Disadvantages

- More computationally expensive
- Slightly slower than ID3

---

# 4. C5.0 Algorithm

## Introduction

C5.0 is the commercial successor of C4.5.

It is faster and produces smaller trees.

---

## Improvements

- Faster training
- Lower memory usage
- Better pruning
- Supports boosting
- Better accuracy
- Handles large datasets

---

## Applications

- Banking
- Medical diagnosis
- Fraud detection
- Credit scoring

---

# 5. CART (Classification and Regression Trees)

## Introduction

CART was proposed by

```
Breiman

Friedman

Olshen

Stone
```

Unlike ID3 and C4.5,

CART supports both

- Classification
- Regression

---

## Splitting Criterion

Classification

```
Gini Index
```

Regression

```
Variance Reduction

or

Mean Squared Error
```

---

## Binary Splits

CART always creates

```
Two Child Nodes
```

Example

```
Income > 50K ?

      Yes

      No
```

---

## Working

```
Dataset

↓

Gini Index

↓

Best Split

↓

Binary Tree

↓

Repeat

↓

Leaf
```

---

## Advantages

- Supports regression
- Fast
- Binary tree
- Easy implementation
- Works with numerical features

---

## Disadvantages

- Can overfit
- Sensitive to data changes

---

# 6. CHAID

## Full Form

```
Chi-square Automatic Interaction Detection
```

---

## Introduction

CHAID uses

```
Chi-Square Test
```

to determine the best split.

Mostly used in

- Marketing
- Customer Segmentation
- Survey Analysis

---

## Characteristics

- Multi-way split
- Categorical variables
- Statistical significance based

---

## Advantages

- Easy interpretation
- Handles categorical data
- Fast

---

## Limitations

- Not suitable for regression
- Less popular than CART

---

# 7. Binary Split vs Multi-way Split

## Binary Split

Only two child nodes.

Example

```
Age > 30

↓

Yes

No
```

Algorithms

- CART

---

## Multi-way Split

Multiple child nodes.

Example

```
Color

↓

Red

Blue

Green

Black
```

Algorithms

- ID3
- C4.5
- CHAID

---# Greedy Algorithm in Decision Trees

## What is a Greedy Algorithm?

A **Greedy Algorithm** makes the **best possible decision at the current step** without considering future consequences.

Decision Trees are built using a greedy approach because, at every node, the algorithm selects the feature that produces the **best split** according to the chosen impurity measure.

```
Dataset
    │
    ▼
Evaluate All Features
    │
    ▼
Choose Best Split
    │
    ▼
Split Data
    │
    ▼
Repeat on Child Nodes
```

Once a split is made, **it is never reconsidered or changed**.

---

## Why is Decision Tree called Greedy?

Suppose we have three candidate features.

| Feature | Information Gain |
|---------|------------------:|
| Age | 0.18 |
| Income | 0.42 |
| Education | 0.25 |

The Decision Tree immediately selects **Income** because it has the **highest Information Gain**.

It **does not check** whether choosing another feature first could produce a better overall tree later.

This is called a **Greedy Choice**.

---

## Advantages

- Fast
- Easy to implement
- Efficient for large datasets

---

## Disadvantages

- Does not guarantee the globally optimal tree
- May produce a locally optimal solution
- Sensitive to noisy data

---

# Attribute Selection Measure (ASM)

## Definition

An **Attribute Selection Measure** is a criterion used to determine **which feature should be selected for splitting** at each node of the Decision Tree.

The goal is to choose the attribute that produces the **purest child nodes**.

```
Dataset

↓

Evaluate Every Feature

↓

Compute ASM

↓

Choose Best Feature

↓

Split Dataset
```

---

## Common Attribute Selection Measures

| Measure | Used In |
|----------|---------|
| Information Gain | ID3 |
| Gain Ratio | C4.5, C5.0 |
| Gini Index | CART |
| Chi-Square | CHAID |
| Variance Reduction | Regression Tree |

---

## Desired Properties of a Good ASM

A good Attribute Selection Measure should:

- Maximize class purity
- Minimize impurity
- Produce meaningful splits
- Avoid overfitting
- Handle different types of data effectively

---

# Information Gain Attribute Selection

Information Gain is one of the most popular **Attribute Selection Measures**.

It measures **how much uncertainty decreases after splitting** on an attribute.

## Formula

```
Information Gain

=

Entropy(Parent)

−

Weighted Entropy(Children)
```

or

```
IG(S,A)

=

Entropy(S)

−

Σ

(|Sv| / |S|)

×

Entropy(Sv)
```

Where:

- **S** = Dataset
- **A** = Attribute
- **Sv** = Subset after split

---

## Working

```
Calculate Entropy

↓

Calculate Information Gain
for every attribute

↓

Choose attribute with
Highest Information Gain

↓

Split Dataset
```

---

## Example

| Attribute | Information Gain |
|-----------|------------------:|
| Age | 0.23 |
| Income | 0.54 |
| Education | 0.18 |

Selected Attribute

```
Income
```

because it has the **highest Information Gain**.

---

## Advantages

- Simple to understand
- Produces informative splits
- Reduces uncertainty
- Works well for classification problems

---

## Limitations

- Biased toward attributes with many distinct values
- May overfit on high-cardinality features

This drawback is addressed by **Gain Ratio**, which is used in **C4.5** and **C5.0**.


# 8. Classification Tree vs Regression Tree

| Classification Tree | Regression Tree |
|---------------------|-----------------|
| Predict Class | Predict Number |
| Gini | Variance Reduction |
| Entropy | MSE |
| Information Gain | MAE |

---

# 9. Comparison of Algorithms

| Feature | ID3 | C4.5 | C5.0 | CART | CHAID |
|---------|-----|------|------|------|-------|
| Classification | ✅ | ✅ | ✅ | ✅ | ✅ |
| Regression | ❌ | ❌ | ❌ | ✅ | ❌ |
| Continuous Features | ❌ | ✅ | ✅ | ✅ | Limited |
| Missing Values | ❌ | ✅ | ✅ | Limited | Limited |
| Pruning | ❌ | ✅ | ✅ | ✅ | ❌ |
| Split Criterion | Information Gain | Gain Ratio | Gain Ratio | Gini/MSE | Chi-Square |
| Binary Split | ❌ | ❌ | ❌ | ✅ | ❌ |
| Multi-way Split | ✅ | ✅ | ✅ | ❌ | ✅ |

---

# 10. Pruning

Pruning removes unnecessary branches from a Decision Tree.

Purpose

- Reduce overfitting
- Improve generalization
- Simplify tree

Types

### Pre-Pruning

Stop tree growth early.

Methods

- max_depth
- min_samples_split
- min_samples_leaf

---

### Post-Pruning

Grow full tree first.

Then remove weak branches.

Produces better generalization.

---

# 11. Feature Importance

Decision Trees naturally rank features.

Features that reduce impurity the most receive the highest importance.

Example

```
Income

Importance = 0.45

Age

Importance = 0.32

Education

Importance = 0.18

Gender

Importance = 0.05
```

---

# 12. Advantages of Decision Tree Algorithms

- Easy to interpret
- No feature scaling
- Handles nonlinear relationships
- Works with mixed data
- Supports feature importance
- Fast prediction

---

# 13. Limitations

- Overfitting
- High variance
- Unstable
- Greedy algorithm
- Lower accuracy than ensemble methods

---

# 14. Which Algorithm Should You Use?

| Problem | Recommended Algorithm |
|----------|----------------------|
| Basic Classification | ID3 |
| Mixed Data | C4.5 |
| Large Dataset | C5.0 |
| Regression | CART |
| Business Analytics | CHAID |

---

# 15. Interview Questions

### Which algorithm uses Information Gain?

**ID3**

---

### Which algorithm uses Gain Ratio?

**C4.5** and **C5.0**

---

### Which algorithm uses Gini Index?

**CART**

---

### Which algorithm supports regression?

**CART**

---

### Which algorithm always creates binary splits?

**CART**

---

### Which algorithm handles continuous features?

**C4.5**, **C5.0**, and **CART**

---

### Why is C4.5 better than ID3?

- Handles continuous attributes
- Uses Gain Ratio
- Supports pruning
- Handles missing values
- Less prone to overfitting

---

### Which Decision Tree algorithm is most commonly implemented in Scikit-learn?

**CART (Classification and Regression Trees)**

---

# 16. Summary

- **ID3** is the foundational Decision Tree algorithm and uses **Information Gain** but supports only categorical data.
- **C4.5** improves upon ID3 by introducing **Gain Ratio**, handling continuous features, missing values, and pruning.
- **C5.0** is a faster and more memory-efficient commercial enhancement of C4.5.
- **CART** is the most widely used algorithm in practice, supporting both **classification** and **regression** with **binary splits** using **Gini Index** or **MSE**.
- **CHAID** is a statistical Decision Tree algorithm based on the **Chi-Square test**, commonly used in business analytics and customer segmentation.
- Understanding the differences between these algorithms is a favorite topic in machine learning interviews.
