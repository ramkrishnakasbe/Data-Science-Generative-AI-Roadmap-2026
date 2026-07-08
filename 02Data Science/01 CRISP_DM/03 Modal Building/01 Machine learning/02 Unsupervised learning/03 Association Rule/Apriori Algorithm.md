# Apriori Algorithm

# Overview

The **Apriori Algorithm** is one of the most popular algorithms used in **Association Rule Learning** and **Market Basket Analysis (MBA)**. It is used to identify **frequent itemsets** from a transactional database and generate **association rules**.

The algorithm works on the principle that:

> **"If an itemset is frequent, then all of its subsets must also be frequent."**

This is known as the **Apriori Principle** or **Downward Closure Property**.

---

# Definition

Apriori is an iterative algorithm that discovers **frequent itemsets** by repeatedly generating larger itemsets from smaller frequent itemsets and eliminating those that do not satisfy the **minimum support threshold**.

Once the frequent itemsets are found, association rules are generated using **confidence** and **lift**.

---

# Why Apriori?

Suppose a supermarket has millions of transactions.

```
T1 : Bread, Milk, Butter

T2 : Bread, Eggs

T3 : Milk, Butter

T4 : Bread, Milk

T5 : Bread, Butter
```

The supermarket wants answers like:

- Which products are bought together?
- Which products should be placed together?
- Which products should be recommended?

Apriori helps answer these questions.

---

# Characteristics

- Unsupervised Learning
- Rule-Based Algorithm
- Works on Transaction Data
- Uses Frequent Itemsets
- Requires Minimum Support
- Generates Association Rules
- Breadth-First Search (BFS) Approach

---

# Important Terminology

## Item

A single product.

Example

```
Milk

Bread

Butter
```

---

## Itemset

A collection of one or more items.

Example

```
{Bread}

{Milk, Bread}

{Milk, Bread, Butter}
```

---

## Frequent Itemset

An itemset whose support is greater than or equal to the **Minimum Support**.

---

## Candidate Itemset

Possible itemsets generated during each iteration before checking their support.

---

## Minimum Support

The minimum frequency required for an itemset to be considered frequent.

Example

```
Minimum Support = 40%
```

Any itemset with support less than 40% is discarded.

---

# Apriori Principle (Downward Closure Property)

The Apriori algorithm is based on the following principle:

> **If an itemset is frequent, then all of its subsets must also be frequent.**

Conversely,

> **If an itemset is infrequent, then all of its supersets will also be infrequent.**

Example

```
{Bread, Butter} is Frequent

↓

Bread is Frequent

Butter is Frequent
```

If

```
{Bread, Butter}

is NOT Frequent
```

Then

```
{Bread, Butter, Milk}

cannot be Frequent.
```

This property allows Apriori to **prune** many unnecessary candidate itemsets.

---

# Working of Apriori Algorithm

Suppose we have the following transactions:

| Transaction | Items |
|-------------|-------|
| T1 | Bread, Milk |
| T2 | Bread, Butter |
| T3 | Bread, Milk, Butter |
| T4 | Milk, Butter |
| T5 | Bread, Milk |

Minimum Support = **40%**

Total Transactions = **5**

---

# Step 1: Generate Frequent 1-Itemsets (L1)

Count the occurrence of each item.

| Item | Count | Support |
|------|------:|--------:|
| Bread | 4 | 80% |
| Milk | 4 | 80% |
| Butter | 3 | 60% |

All satisfy the minimum support.

```
L1

Bread

Milk

Butter
```

---

# Step 2: Generate Candidate 2-Itemsets (C2)

Combine the frequent 1-itemsets.

```
Bread, Milk

Bread, Butter

Milk, Butter
```

---

# Step 3: Calculate Support

| Itemset | Count | Support |
|---------|------:|--------:|
| Bread, Milk | 3 | 60% |
| Bread, Butter | 2 | 40% |
| Milk, Butter | 2 | 40% |

All satisfy minimum support.

```
L2

Bread, Milk

Bread, Butter

Milk, Butter
```

---

# Step 4: Generate Candidate 3-Itemsets (C3)

Join the frequent 2-itemsets.

```
Bread

Milk

Butter

↓

Bread, Milk, Butter
```

---

# Step 5: Calculate Support

```
Bread, Milk, Butter
```

Appears only in

```
T3
```

Support

```
1 / 5

=

20%
```

Minimum support required

```
40%
```

Hence,

```
Discard
```

No further itemsets can be generated.

---

# Final Frequent Itemsets

```
L1

Bread

Milk

Butter

----------------

L2

Bread, Milk

Bread, Butter

Milk, Butter
```

---

# Rule Generation

From the frequent itemsets, association rules are generated.

Example

```
Bread → Milk

Milk → Bread

Bread → Butter

Butter → Bread
```

These rules are evaluated using:

- Support
- Confidence
- Lift

---

# Flowchart

```text
Start

↓

Read Transactions

↓

Generate Candidate 1-Itemsets

↓

Calculate Support

↓

Remove Infrequent Itemsets

↓

Generate Larger Candidate Itemsets

↓

Calculate Support

↓

Prune Infrequent Itemsets

↓

Repeat Until No New Frequent Itemsets

↓

Generate Association Rules

↓

Calculate Confidence & Lift

↓

End
```

---

# Candidate Generation

Apriori generates larger itemsets by joining smaller frequent itemsets.

Example

```
L2

AB

AC

BC

↓

Candidate

ABC
```

---

# Pruning

After candidate generation,

remove all candidates whose subsets are not frequent.

Example

Suppose

```
ABC
```

If

```
BC

is NOT Frequent
```

Then

```
ABC

cannot be Frequent.
```

This significantly reduces the search space.

---

# Advantages

- Easy to understand
- Simple implementation
- Finds hidden purchasing patterns
- Suitable for market basket analysis
- Produces interpretable rules

---

# Disadvantages

- Generates many candidate itemsets
- Multiple database scans
- Slow for very large datasets
- High memory usage
- Less efficient than FP-Growth

---

# Time Complexity

Worst Case

```
O(2ⁿ)
```

where **n** is the number of unique items.

The search space grows exponentially as the number of items increases.

---

# Python Implementation

```python
from mlxtend.frequent_patterns import apriori
from mlxtend.frequent_patterns import association_rules

# Find frequent itemsets
frequent_itemsets = apriori(
    df,
    min_support=0.4,
    use_colnames=True
)

print(frequent_itemsets)
```

Generate association rules:

```python
rules = association_rules(
    frequent_itemsets,
    metric="confidence",
    min_threshold=0.6
)

print(rules[['antecedents',
             'consequents',
             'support',
             'confidence',
             'lift']])
```

---

# Apriori vs FP-Growth

| Feature | Apriori | FP-Growth |
|---------|----------|-----------|
| Candidate Generation | Yes | No |
| Database Scans | Multiple | Two |
| Speed | Slower | Faster |
| Memory Usage | Higher | Lower |
| Large Dataset | Less Efficient | More Efficient |
| Complexity | Simpler | More Complex |

---

# Applications

- Market Basket Analysis
- Product Recommendation
- Cross Selling
- Shelf Placement
- Website Clickstream Analysis
- Medical Diagnosis
- Fraud Detection
- Customer Behavior Analysis

---

# Interview Questions

## 1. What is the Apriori Algorithm?

Apriori is a rule-based algorithm used to discover frequent itemsets and generate association rules from transactional data.

---

## 2. What is the Apriori Principle?

If an itemset is frequent, all of its subsets must also be frequent. If an itemset is infrequent, none of its supersets can be frequent.

---

## 3. Why is pruning used in Apriori?

Pruning removes candidate itemsets that cannot possibly be frequent, reducing computation time and memory usage.

---

## 4. Why is Apriori slow?

It generates a large number of candidate itemsets and requires multiple scans of the transaction database.

---

## 5. What is the difference between Apriori and FP-Growth?

Apriori generates candidate itemsets and scans the database multiple times, whereas FP-Growth builds an FP-Tree, avoids candidate generation, and is generally much faster on large datasets.

---

# Summary

The **Apriori Algorithm** is a foundational algorithm for **Association Rule Learning** and **Market Basket Analysis**. It discovers **frequent itemsets** using the **Apriori Principle**, generates larger itemsets iteratively, prunes infrequent candidates, and finally produces association rules evaluated using **Support**, **Confidence**, and **Lift**. Although simple and interpretable, it becomes computationally expensive for large datasets due to repeated database scans and candidate generation, making algorithms like **FP-Growth** more suitable for large-scale applications.
