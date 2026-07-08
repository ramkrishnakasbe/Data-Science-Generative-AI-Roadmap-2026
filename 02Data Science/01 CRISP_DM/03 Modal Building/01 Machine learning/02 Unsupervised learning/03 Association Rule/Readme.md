# Association Rule Learning / Market Basket Analysis

# Overview

Association Rule Learning is an **Unsupervised Machine Learning** technique used to discover interesting relationships, patterns, and associations between items in a large dataset.

One of its most common applications is **Market Basket Analysis (MBA)**, where retailers analyze customers' purchasing behavior to identify products that are frequently bought together.

Association Rule Learning helps businesses make data-driven decisions in areas such as product placement, recommendation systems, cross-selling, and promotional strategies.

---

# Definition

Association Rule Learning is a rule-based machine learning technique that identifies relationships between variables in large transactional datasets.

The discovered relationships are represented as **association rules** in the form:

```
If A is purchased,
then B is also likely to be purchased.

A → B
```

Example

```
Bread → Butter
```

This means customers who buy **Bread** are also likely to buy **Butter**.

---

# What is Market Basket Analysis?

Market Basket Analysis is the process of analyzing customer transactions to identify products that are frequently purchased together.

The goal is to understand customer buying behavior and generate actionable business insights.

Example

```
Transaction 1

Bread
Milk
Butter

---------------------

Transaction 2

Bread
Eggs

---------------------

Transaction 3

Milk
Butter

---------------------

Transaction 4

Bread
Milk
Butter
```

From these transactions, we may discover the rule:

```
Bread → Butter
```

---

# Objectives

- Discover hidden relationships
- Identify frequently purchased products
- Increase sales
- Improve product recommendations
- Optimize store layout
- Cross-selling
- Up-selling
- Customer behavior analysis

---

# Characteristics

- Unsupervised Learning
- Rule-Based Learning
- Works on Transactional Data
- No Target Variable
- Discovers Hidden Patterns
- Easy to Interpret
- Widely Used in Retail

---

# Basic Terminology

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
{Milk, Bread}

{Bread, Butter}

{Milk, Eggs, Butter}
```

---

## Transaction

A customer's purchase.

Example

```
Transaction 1

Milk

Bread

Butter
```

---

## Frequent Itemset

An itemset whose occurrence exceeds a minimum support threshold.

Example

```
Bread

Milk

Butter
```

appearing in many transactions.

---

## Association Rule

Represents a relationship between two itemsets.

```
A → B
```

Example

```
Milk → Bread
```

---

# Components of an Association Rule

```
A → B
```

Where

```
A

Antecedent

(If)
```

```
B

Consequent

(Then)
```

Example

```
Bread → Butter
```

Antecedent

```
Bread
```

Consequent

```
Butter
```

---

# Measures of Association Rules

The quality of an association rule is evaluated using:

- Support
- Confidence
- Lift

---

# 1. Support

Support measures **how frequently an itemset appears in the dataset**.

Formula

```
Support(A)

=

Transactions containing A

--------------------------

Total Transactions
```

Example

Suppose

```
10 Transactions

Bread appears in 6
```

Support

```
6/10

=

0.60

=

60%
```

Higher support means the item appears frequently.

---

# Support of a Rule

Formula

```
Support(A→B)

=

Transactions containing A and B

--------------------------------

Total Transactions
```

Example

```
Bread & Butter together

4 times

Total Transactions

10

Support

=

4/10

=

40%
```

---

# 2. Confidence

Confidence measures the probability of purchasing B after purchasing A.

Formula

```
Confidence(A→B)

=

Support(A∩B)

------------

Support(A)
```

Example

```
Bread appears

5 times

Bread & Butter

4 times
```

Confidence

```
4/5

=

80%
```

Interpretation

80% of customers buying Bread also purchased Butter.

---

# 3. Lift

Lift measures how much more likely two items occur together compared to random chance.

Formula

```
Lift

=

Confidence(A→B)

----------------

Support(B)
```

Interpretation

```
Lift = 1

No Association
```

```
Lift > 1

Positive Association
```

```
Lift < 1

Negative Association
```

Example

```
Lift = 2

Customers are twice as likely to purchase Butter with Bread.
```

---

# Example Calculation

Suppose

```
100 Transactions

Bread = 40

Butter = 50

Bread & Butter = 30
```

Support

```
30/100

=

30%
```

Confidence

```
30/40

=

75%
```

Lift

```
0.75

/

0.50

=

1.5
```

Interpretation

Customers buying Bread are **1.5 times more likely** to buy Butter.

---

# Popular Algorithms

## 1. Apriori Algorithm ⭐⭐⭐⭐⭐

Most popular algorithm.

Working Principle

```
Generate Candidate Itemsets

↓

Calculate Support

↓

Remove Infrequent Itemsets

↓

Generate Larger Itemsets

↓

Generate Association Rules
```

Advantages

- Easy to understand
- Accurate
- Widely used

Disadvantages

- Slow on large datasets
- Generates many candidate itemsets

---

## 2. FP-Growth Algorithm

FP-Growth uses an FP-Tree instead of candidate generation.

Advantages

- Faster than Apriori
- Handles large datasets
- Less memory consumption

Disadvantages

- More complex implementation

---

## 3. ECLAT Algorithm

Uses a vertical data format instead of horizontal transactions.

Advantages

- Fast support counting
- Efficient for dense datasets

---

# Apriori Algorithm

## Step 1

Find frequent 1-itemsets.

```
Milk

Bread

Butter
```

---

## Step 2

Generate candidate 2-itemsets.

```
Milk Bread

Milk Butter

Bread Butter
```

---

## Step 3

Calculate support.

---

## Step 4

Remove infrequent itemsets.

---

## Step 5

Generate 3-itemsets.

---

## Step 6

Generate association rules.

---

# Python Implementation

```python
from mlxtend.frequent_patterns import apriori
from mlxtend.frequent_patterns import association_rules

frequent_items = apriori(df,
                         min_support=0.2,
                         use_colnames=True)

rules = association_rules(
            frequent_items,
            metric="confidence",
            min_threshold=0.6)

print(rules)
```

---

# Important Parameters

| Parameter | Description |
|------------|------------|
| min_support | Minimum support threshold |
| min_confidence | Minimum confidence |
| metric | confidence, lift, leverage, conviction |
| use_colnames | Show item names instead of indices |

---

# Advantages

- Easy to understand
- Finds hidden patterns
- Improves recommendations
- Supports cross-selling
- Business-friendly
- Actionable insights

---

# Disadvantages

- Slow for very large datasets
- Requires parameter tuning
- May generate too many rules
- Not suitable for continuous data directly

---

# Applications

## Retail

Market Basket Analysis

---

## E-Commerce

Amazon product recommendations

---

## Banking

Credit card usage analysis

---

## Healthcare

Disease co-occurrence

Medicine recommendation

---

## Telecommunications

Service bundling

---

## Web Analytics

Website click pattern analysis

---

## Recommendation Systems

Netflix

Amazon

Flipkart

---

## Fraud Detection

Identify unusual purchasing patterns.

---

# Association Rule vs Classification

| Association Rule | Classification |
|------------------|----------------|
| Unsupervised | Supervised |
| No Target Variable | Requires Target Variable |
| Finds Relationships | Predicts Labels |
| Rule Based | Prediction Based |

---

# Interview Questions

## 1. What is Association Rule Learning?

Association Rule Learning is an unsupervised machine learning technique used to discover relationships between items in transactional data.

---

## 2. What is Market Basket Analysis?

A business application of association rule learning used to identify products that are frequently purchased together.

---

## 3. What are the three important measures?

- Support
- Confidence
- Lift

---

## 4. Which algorithm is most commonly used?

Apriori Algorithm.

---

## 5. Which algorithm is faster than Apriori?

FP-Growth Algorithm.

---

## 6. What does Lift > 1 indicate?

A positive association between two items.

---

## 7. What is the difference between Support and Confidence?

| Support | Confidence |
|----------|------------|
| Frequency of an itemset in all transactions | Probability of purchasing B when A is purchased |

---

## 8. What is the difference between Apriori and FP-Growth?

| Apriori | FP-Growth |
|----------|-----------|
| Candidate generation | FP-Tree |
| Slower | Faster |
| Higher memory usage | Lower memory usage |
| Simpler | More efficient |

---

# Summary

Association Rule Learning is an unsupervised learning technique used to discover relationships between items in transactional datasets. Its most common application is **Market Basket Analysis**, which helps businesses understand customer purchasing behavior. The quality of association rules is measured using **Support**, **Confidence**, and **Lift**, while algorithms such as **Apriori**, **FP-Growth**, and **ECLAT** are used to identify frequent itemsets and generate meaningful association rules. These techniques are widely used in retail, e-commerce, healthcare, banking, and recommendation systems.
