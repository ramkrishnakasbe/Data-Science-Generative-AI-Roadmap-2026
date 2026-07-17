# 02 Splitting Criteria.md

# 1. Introduction

The most important step in building a Decision Tree is deciding **where to split the data**.

A good split should create **pure child nodes**, meaning each child node contains observations that mostly belong to a single class.

Different Decision Tree algorithms use different **splitting criteria** to measure the quality of a split.

Common splitting criteria are:

- Entropy
- Information Gain
- Gini Index
- Gain Ratio
- Misclassification Error
- Variance Reduction (Regression)
- Mean Squared Error (MSE)
- Mean Absolute Error (MAE)

---

# 2. What is Node Impurity?

A node is called **Pure** if all records belong to the same class.

Example

```
Yes
Yes
Yes
Yes
```

Pure Node

---

A node is **Impure** if it contains multiple classes.

Example

```
Yes
No
Yes
No
```

Impure Node

The goal of a Decision Tree is to **reduce impurity after every split**.

---

# 3. Entropy

## Definition

Entropy measures the **uncertainty**, **randomness**, or **impurity** in a dataset.

It comes from **Information Theory** introduced by **Claude Shannon**.

Decision Tree algorithms such as **ID3** and **C4.5** use Entropy to evaluate candidate splits.

---

## Formula

```
Entropy(S)

=

- Σ Pi log₂(Pi)
```

Where

- Pi = Probability of class *i*
- S = Dataset

---

## Properties

### Pure Node

```
Yes

Yes

Yes

Yes
```

Entropy

```
0
```

---

### Equal Classes

```
Yes

No

Yes

No
```

Entropy

```
1
```

(Maximum uncertainty for binary classification)

---

## Range

Binary Classification

```
0 ≤ Entropy ≤ 1
```

Multi-class

```
0 ≤ Entropy ≤ log₂(C)
```

where

```
C = Number of classes
```

---

## Numerical Example

Dataset

| Class | Count |
|--------|------:|
| Yes | 6 |
| No | 4 |

Probability

```
P(Yes)=6/10=0.6

P(No)=4/10=0.4
```

Entropy

```
= -(0.6 log₂0.6)

-(0.4 log₂0.4)

≈ 0.971
```

---

## Interpretation

| Entropy | Meaning |
|----------|---------|
| 0 | Pure Node |
| Close to 0 | Less uncertainty |
| 1 | Maximum impurity |

---

# 4. Information Gain

## Definition

Information Gain measures **how much impurity decreases after splitting**.

The feature with the **highest Information Gain** is selected for splitting.

---

## Formula

```
Information Gain

=

Entropy(Parent)

-

Weighted Entropy(Children)
```

or

```
IG

=

Entropy(S)

-

Σ

(|Sv| / |S|)

×

Entropy(Sv)
```

---

## Interpretation

Higher Information Gain

↓

Better Split

---

## Numerical Example

Parent Entropy

```
0.97
```

Children Entropy

```
0.20

0.30
```

Weighted Entropy

```
0.26
```

Information Gain

```
0.97

-

0.26

=

0.71
```

The feature producing **0.71** would be preferred over another feature producing **0.40**.

---

## Advantages

- Easy to understand
- Finds informative splits
- Widely used in ID3

---

## Limitations

Information Gain is **biased toward features with many unique values**.

Example

```
Employee ID

1001

1002

1003

...
```

Splitting on ID creates many pure nodes but does not generalize well.

This limitation is addressed using **Gain Ratio (C4.5)**.

---

# 5. Gini Index

## Definition

The Gini Index measures the probability of **incorrect classification** if a sample is randomly labeled according to the class distribution.

It is the default criterion used in **CART (Classification and Regression Trees).**

---

## Formula

```
Gini

=

1

-

Σ Pi²
```

---

## Range

Binary Classification

```
0 ≤ Gini ≤ 0.5
```

---

## Properties

### Pure Node

```
Yes

Yes

Yes
```

Gini

```
0
```

---

### Equal Classes

```
Yes

No
```

Gini

```
0.5
```

---

## Numerical Example

Dataset

| Class | Count |
|--------|------:|
| Yes | 6 |
| No | 4 |

```
P(Yes)=0.6

P(No)=0.4
```

```
Gini

=

1

-

(0.6²+0.4²)

=

1

-

(0.36+0.16)

=

0.48
```

---

## Advantages

- Faster than Entropy
- Simpler computation
- Preferred in CART
- Works well on large datasets

---

# 6. Entropy vs Gini

| Feature | Entropy | Gini |
|---------|---------|-------|
| Formula | Logarithmic | Squared Probability |
| Speed | Slower | Faster |
| Used By | ID3, C4.5 | CART |
| Range | 0–1 | 0–0.5 |
| Computation | More complex | Simpler |

---

# 7. Gain Ratio

## Why Gain Ratio?

Information Gain prefers features with many unique values.

Gain Ratio removes this bias.

Used in

```
C4.5
```

---

## Formula

```
Gain Ratio

=

Information Gain

-------------------

Split Information
```

Split Information

```
=

- Σ Pi log₂Pi
```

---

## Advantages

- Removes bias toward high-cardinality features
- Produces balanced trees
- Better than Information Gain in many cases

---

# 8. Misclassification Error

## Definition

Measures the probability of assigning the wrong class.

Formula

```
Misclassification

=

1

-

Max(Pi)
```

---

Example

```
Yes = 80%

No = 20%
```

```
Error

=

1

-

0.8

=

0.2
```

---

## Properties

- Simple
- Less sensitive than Entropy
- Rarely used for splitting
- Often used for pruning

---

# 9. Regression Tree Splitting

Classification Trees use impurity measures.

Regression Trees use **prediction error**.

Common criteria

- Variance Reduction
- Mean Squared Error (MSE)
- Mean Absolute Error (MAE)

---

# 10. Variance Reduction

## Definition

Variance measures how spread out the target values are.

A good split should **reduce variance**.

Formula

```
Variance

=

Σ(x-μ)²

---------

N
```

Best split

↓

Maximum reduction in variance.

---

# 11. Mean Squared Error (MSE)

Used in regression trees.

Formula

```
MSE

=

Σ(y-ŷ)²

---------

N
```

Where

- y = Actual value
- ŷ = Predicted value

Lower MSE

↓

Better split

---

# 12. Mean Absolute Error (MAE)

Formula

```
MAE

=

Σ|y-ŷ|

---------

N
```

Properties

- Easy to interpret
- Less sensitive to outliers than MSE

---

# 13. How Does a Decision Tree Choose the Best Split?

```
For Every Feature

↓

Generate Candidate Splits

↓

Compute Entropy / Gini / MSE

↓

Calculate Impurity Reduction

↓

Select Best Split

↓

Repeat Recursively
```

---

# 14. Summary Comparison

| Criterion | Classification | Regression | Algorithm |
|-----------|---------------|-----------|-----------|
| Entropy | ✅ | ❌ | ID3, C4.5 |
| Information Gain | ✅ | ❌ | ID3 |
| Gain Ratio | ✅ | ❌ | C4.5 |
| Gini Index | ✅ | ❌ | CART |
| Misclassification Error | ✅ | ❌ | Mainly Pruning |
| Variance Reduction | ❌ | ✅ | Regression Tree |
| MSE | ❌ | ✅ | CART Regression |
| MAE | ❌ | ✅ | Regression Trees |

---

# 15. Interview Questions

### Why do Decision Trees use splitting criteria?

To find the feature and threshold that produce the **purest child nodes**.

---

### Which algorithm uses Entropy?

**ID3** and **C4.5**

---

### Which algorithm uses Gini Index?

**CART (Classification and Regression Trees)**

---

### Which is faster: Entropy or Gini?

**Gini Index**, because it avoids logarithmic calculations.

---

### Why is Information Gain biased?

It prefers features with many unique values, even if they are not useful for prediction.

---

### How does Gain Ratio solve this problem?

It normalizes Information Gain using **Split Information**, reducing the bias toward high-cardinality features.

---

### Which impurity measure is used for regression trees?

Regression trees use **Variance Reduction**, **MSE**, or **MAE** instead of Entropy or Gini.

---

### Can Entropy and Gini produce different trees?

Yes. Although they often choose similar splits, different impurity measures can lead to different tree structures.

---

# 16. Summary

- A Decision Tree grows by selecting the **best split** at each node.
- **Entropy** measures uncertainty, while **Information Gain** measures the reduction in uncertainty after a split.
- **Gini Index** is computationally faster and is used by the **CART** algorithm.
- **Gain Ratio** improves Information Gain by removing its bias toward features with many unique values.
- For regression problems, Decision Trees rely on **Variance Reduction**, **MSE**, or **MAE** instead of classification impurity measures.
- Understanding these splitting criteria is essential because they form the foundation of all Decision Tree algorithms and are among the most frequently asked topics in machine learning interviews.
