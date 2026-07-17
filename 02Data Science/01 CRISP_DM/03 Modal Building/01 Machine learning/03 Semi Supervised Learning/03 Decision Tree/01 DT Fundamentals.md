# 01 Decision Tree Fundamentals.md

# 1. Introduction

## What is a Decision Tree?

A **Decision Tree** is a **Supervised Machine Learning algorithm** used for both **Classification** and **Regression** tasks.

It predicts the target variable by learning a series of **decision rules** from the training data. The data is recursively split into smaller subsets until a stopping condition is met.

A Decision Tree resembles an **upside-down tree**, where:

- The **root node** represents the entire dataset.
- Internal nodes represent decision rules.
- Leaf nodes represent the final prediction.

---

## Example

Suppose a bank wants to decide whether to approve a loan.

```
             Income > 50K?
               /      \
             Yes      No
             /          \
      Credit Score?     Reject
        /      \
      Good     Bad
      /          \
   Approve     Reject
```

Each question is a **decision rule**, and the final leaf gives the prediction.

---

# 2. Why Decision Tree?

Decision Trees are popular because they are:

- Easy to understand
- Easy to visualize
- Require little data preprocessing
- Handle both numerical and categorical data
- Perform both classification and regression

---

# 3. Characteristics

- Supervised Learning Algorithm
- Non-Parametric Model
- White-box Model (Highly Interpretable)
- Tree-based Algorithm
- Supports Classification & Regression
- Recursive Partitioning Algorithm

---

# 4. Decision Tree Terminology

## Root Node

The first node of the tree containing the entire dataset.

```
        Root
```

---

## Parent Node

A node that splits into one or more child nodes.

```
      Parent
      /    \
 Child1   Child2
```

---

## Child Node

Nodes created after a split.

```
Parent

↓

Child
```

---

## Internal Node

Any node that performs a decision but is not a leaf.

```
Age > 30 ?
```

---

## Leaf Node (Terminal Node)

The final node that contains the prediction.

```
Approved

Rejected
```

No further splitting occurs.

---

## Branch

The connection between two nodes.

```
Parent

│

Child
```

---

## Subtree

A smaller tree originating from an internal node.

```
      A
     / \
    B   C
       / \
      D   E
```

Node **C** and its descendants form a subtree.

---

## Depth

The number of edges from the root node to a given node.

Example

```
Root → Child → Leaf

Depth of Leaf = 2
```

---

## Height

The longest path from a node to its deepest leaf.

---

# 5. Types of Decision Trees

## Classification Tree

Used when the target variable is **categorical**.

Examples

- Spam / Not Spam
- Pass / Fail
- Fraud / Genuine

---

## Regression Tree

Used when the target variable is **continuous**.

Examples

- House Price
- Salary
- Temperature

---

# 6. How Does a Decision Tree Work?

The Decision Tree repeatedly splits the dataset into smaller subsets based on the feature that produces the **best split**.

Workflow

```
Entire Dataset

↓

Find Best Feature

↓

Split Dataset

↓

Repeat for Each Child

↓

Stopping Criteria

↓

Leaf Node
```

---

## Example

Dataset

| Age | Income | Loan |
|------|--------|------|
| 25 | Low | No |
| 35 | High | Yes |
| 40 | High | Yes |
| 28 | Low | No |

The algorithm may first split on **Income**, then on **Age**, until each leaf contains similar records.

---

# 7. Recursive Partitioning

Decision Trees use **Recursive Partitioning**, meaning the data is repeatedly divided into smaller subsets.

```
Dataset

↓

Split

↓

Split Again

↓

Split Again

↓

Leaf
```

The process continues until a stopping condition is met.

---

# 8. Decision Boundary

Decision Trees create **non-linear decision boundaries** by recursively partitioning the feature space.

Example

```
Feature 2

^

|

|------|------|

|      | Yes  |

|------|------|

| No   | Yes  |

+-----------------> Feature 1
```

Unlike Logistic Regression, Decision Trees can model complex boundaries.

---

# 9. Stopping Criteria

A Decision Tree stops growing when one or more conditions are met.

Common stopping criteria:

- All samples belong to the same class.
- Maximum tree depth is reached.
- Minimum samples required for splitting are not available.
- Minimum samples in a leaf node are reached.
- No further improvement in impurity.
- All features have been used.

---

# 10. Overfitting

## Definition

Overfitting occurs when the tree becomes too complex and memorizes the training data.

Characteristics

- Very high training accuracy
- Poor test accuracy
- Deep tree
- Many leaf nodes

Example

```
Training Accuracy

100%

Testing Accuracy

70%
```

---

# 11. Underfitting

Underfitting occurs when the tree is too simple.

Characteristics

- Low training accuracy
- Low testing accuracy
- Very shallow tree

---

# 12. Preventing Overfitting

Methods

- Limit maximum depth
- Increase minimum samples per split
- Increase minimum samples per leaf
- Pruning
- Cross Validation
- Feature Selection

---

# 13. Advantages

- Easy to understand and explain
- Easy to visualize
- Works with numerical and categorical data
- No feature scaling required
- Handles missing values (algorithm-dependent)
- Captures non-linear relationships
- Performs feature selection automatically
- Robust to outliers

---

# 14. Disadvantages

- Can easily overfit
- High variance
- Sensitive to small changes in data
- Biased toward features with many categories (e.g., ID3)
- May produce unstable trees
- Lower accuracy than ensemble methods like Random Forest or XGBoost

---

# 15. Applications

- Loan Approval
- Credit Risk Analysis
- Medical Diagnosis
- Fraud Detection
- Customer Churn Prediction
- Employee Attrition
- Disease Prediction
- Marketing Campaign Analysis
- Insurance Claim Prediction

---

# 16. Time Complexity

Let:

- **N** = Number of samples
- **M** = Number of features

Training

```
O(M × N log N)
```

Prediction

```
O(Tree Depth)
```

Balanced trees provide faster predictions.

---

# 17. Space Complexity

Depends on the number of nodes.

Approximate

```
O(N)
```

---

# 18. Decision Tree vs Linear Models

| Decision Tree | Logistic Regression |
|---------------|---------------------|
| Non-linear | Linear |
| No scaling required | Scaling may help |
| Easy to interpret | Moderate interpretation |
| Handles feature interactions naturally | Requires feature engineering |

---

# 19. Common Interview Questions

### What is a Decision Tree?

A supervised learning algorithm that recursively splits data into smaller subsets to make predictions.

---

### Is a Decision Tree Parametric?

No. It is a **Non-Parametric** model because it makes no assumptions about the data distribution.

---

### Can Decision Trees perform regression?

Yes. They support both **classification** and **regression**.

---

### Why are Decision Trees easy to interpret?

Each prediction follows a clear sequence of decision rules from the root node to a leaf node.

---

### What is Recursive Partitioning?

The process of repeatedly splitting the dataset into smaller subsets until a stopping criterion is reached.

---

### What causes overfitting in Decision Trees?

- Excessive tree depth
- Too many leaf nodes
- Memorizing training data
- Lack of pruning

---

### How can overfitting be reduced?

- Pre-pruning
- Post-pruning
- Limiting tree depth
- Increasing minimum samples per leaf
- Cross Validation

---

### Does a Decision Tree require feature scaling?

No. Decision Trees split data based on feature values rather than distance, so scaling is generally unnecessary.

---

# 20. Summary

- Decision Trees are **supervised, non-parametric, tree-based algorithms** used for classification and regression.
- They work by recursively splitting the dataset using the best feature at each step.
- They are highly interpretable and require little preprocessing.
- Their biggest challenge is **overfitting**, which can be controlled using pruning and hyperparameter tuning.
- Decision Trees form the foundation of powerful ensemble algorithms such as **Random Forest**, **Gradient Boosting**, **XGBoost**, **LightGBM**, and **CatBoost**.
