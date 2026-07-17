# 04 Decision Tree Implementation & Interview.md

# 1. Introduction

After understanding the theory behind Decision Trees, the next step is learning how to implement, tune, visualize, and evaluate them.

Scikit-learn implements the **CART (Classification and Regression Trees)** algorithm.

---

# 2. Import Libraries

```python
import pandas as pd
import numpy as np

from sklearn.model_selection import train_test_split

from sklearn.tree import DecisionTreeClassifier
from sklearn.tree import DecisionTreeRegressor

from sklearn.metrics import accuracy_score
```

---

# 3. Load Dataset

```python
df = pd.read_csv("data.csv")

X = df.drop("Target", axis=1)

y = df["Target"]
```

---

# 4. Train-Test Split

```python
X_train, X_test, y_train, y_test = train_test_split(

X,
y,

test_size=0.2,
random_state=42)
```

---

# 5. Train Decision Tree Classifier

```python
model = DecisionTreeClassifier()

model.fit(X_train,y_train)
```

---

# 6. Prediction

```python
prediction = model.predict(X_test)
```

---

# 7. Accuracy

```python
accuracy = accuracy_score(

y_test,

prediction)

print(accuracy)
```

---

# 8. Decision Tree Regression

```python
model = DecisionTreeRegressor()

model.fit(X_train,y_train)

prediction = model.predict(X_test)
```

---

# 9. Important Hyperparameters

## criterion

Determines the splitting criterion.

Classification

```
gini

entropy

log_loss
```

Regression

```
squared_error

friedman_mse

absolute_error
```

---

## splitter

```
best

random
```

---

## max_depth

Maximum depth of the tree.

Example

```python
DecisionTreeClassifier(max_depth=5)
```

Purpose

- Reduce overfitting
- Smaller tree

---

## min_samples_split

Minimum samples required to split a node.

Example

```python
min_samples_split=10
```

---

## min_samples_leaf

Minimum samples allowed in a leaf.

Example

```python
min_samples_leaf=5
```

---

## max_leaf_nodes

Maximum leaf nodes.

Helps prevent overfitting.

---

## max_features

Number of features considered while splitting.

Options

```
sqrt

log2

None
```

---

## random_state

Makes results reproducible.

---

## ccp_alpha

Used for **Cost Complexity Pruning**.

Larger value

↓

Smaller Tree

---

# 10. Pre-Pruning (Early Stopping)

Pre-pruning stops tree growth before it becomes too complex.

Methods

- max_depth
- min_samples_leaf
- min_samples_split
- max_leaf_nodes
- min_impurity_decrease

Advantages

- Faster
- Prevents overfitting
- Smaller tree

Disadvantages

- May stop too early
- Can underfit

---

# 11. Post-Pruning

Tree is grown completely first.

Weak branches are then removed.

```
Full Tree

↓

Remove Weak Branches

↓

Simplified Tree
```

Advantages

- Better generalization
- Better accuracy
- Less overfitting

---

# 12. Cost Complexity Pruning (CCP)

Scikit-learn uses **Cost Complexity Pruning**.

Formula

```
Cost

=

Error

+

α × Number of Leaves
```

Where

```
α

=

Complexity Parameter
```

Large α

↓

Smaller Tree

Small α

↓

Larger Tree

Python

```python
DecisionTreeClassifier(

ccp_alpha=0.01)
```

---

# 13. Feature Importance

Decision Trees automatically rank features according to their contribution.

```python
model.feature_importances_
```

Example

```
Income      0.42

Age         0.31

Education   0.18

Gender      0.09
```

Higher value

↓

More Important Feature

---

# 14. Visualizing Decision Tree

```python
from sklearn.tree import plot_tree

plot_tree(model)
```

or

```python
from sklearn.tree import export_graphviz
```

Visualization helps explain the model.

---

# 15. Model Evaluation

## Classification

- Accuracy
- Precision
- Recall
- F1 Score
- ROC-AUC
- Confusion Matrix

---

## Regression

- MAE
- MSE
- RMSE
- R² Score

---

# 16. Decision Tree vs Logistic Regression

| Decision Tree | Logistic Regression |
|---------------|---------------------|
| Non-linear | Linear |
| No Scaling | Scaling Preferred |
| Tree Rules | Mathematical Equation |
| Easy Interpretation | Moderate |

---

# 17. Decision Tree vs KNN

| Decision Tree | KNN |
|---------------|-----|
| Tree Based | Distance Based |
| No Scaling | Scaling Required |
| Fast Prediction | Slow Prediction |
| Low Memory | High Memory |

---

# 18. Decision Tree vs Random Forest

| Decision Tree | Random Forest |
|---------------|---------------|
| Single Tree | Multiple Trees |
| Faster Training | Slower Training |
| More Overfitting | Less Overfitting |
| Lower Accuracy | Higher Accuracy |

---

# 19. Decision Tree vs SVM

| Decision Tree | SVM |
|---------------|-----|
| Rule Based | Margin Based |
| Easy Interpretation | Difficult Interpretation |
| Fast Prediction | Moderate Prediction |

---

# 20. Advantages

- Easy to understand
- Easy visualization
- No feature scaling
- Handles numerical & categorical data
- Feature importance available
- Non-linear decision boundaries
- Fast prediction

---

# 21. Disadvantages

- Overfitting
- High variance
- Unstable
- Greedy algorithm
- Lower accuracy than ensemble methods

---

# 22. Real-World Applications

- Loan Approval
- Fraud Detection
- Medical Diagnosis
- Credit Scoring
- Customer Churn Prediction
- Employee Attrition
- Marketing Analytics
- Insurance Risk Analysis
- Sales Prediction

---

# 23. Complete Example

```python
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
from sklearn.tree import DecisionTreeClassifier
from sklearn.metrics import accuracy_score

iris = load_iris()

X = iris.data

y = iris.target

X_train,X_test,y_train,y_test = train_test_split(

X,
y,

test_size=0.2,

random_state=42)

model = DecisionTreeClassifier(

criterion="gini",

max_depth=4,

random_state=42)

model.fit(X_train,y_train)

prediction = model.predict(X_test)

print("Accuracy :",accuracy_score(y_test,prediction))
```

---

# 24. Common Interview Questions

### Which Decision Tree algorithm does Scikit-learn use?

**CART (Classification and Regression Trees).**

---

### Does Decision Tree require Feature Scaling?

No.

Decision Trees split based on feature values, not distances.

---

### Why do Decision Trees overfit?

Because they keep splitting until every training sample is classified correctly, creating a very deep tree.

---

### How can overfitting be reduced?

- Pre-pruning
- Post-pruning
- Cost Complexity Pruning
- Limiting max_depth
- Increasing min_samples_leaf
- Cross Validation

---

### What is Cost Complexity Pruning?

A pruning technique that balances tree complexity and prediction error using the parameter **ccp_alpha**.

---

### Which hyperparameter controls tree depth?

```
max_depth
```

---

### Which hyperparameter controls minimum samples in a leaf?

```
min_samples_leaf
```

---

### What is Feature Importance?

A score indicating how much each feature contributes to reducing impurity in the Decision Tree.

---

### What are the assumptions of Decision Tree?

Decision Trees make **very few assumptions** about the underlying data. They are considered **non-parametric models** and can handle linear and non-linear relationships.

---

### Why is Decision Tree considered a White Box Model?

Because every prediction can be traced through a sequence of understandable decision rules from the root node to a leaf node.

---

# 25. Best Practices

- Use **Gini Index** for faster training (default in Scikit-learn).
- Use **Entropy** when maximizing information gain is preferred.
- Limit **max_depth** to reduce overfitting.
- Tune **min_samples_split** and **min_samples_leaf**.
- Apply **Cost Complexity Pruning** for better generalization.
- Evaluate the model using **Cross Validation**.
- Use **Random Forest** or **Gradient Boosting** if a single Decision Tree underperforms.

---

# 26. Summary

- Scikit-learn implements the **CART** algorithm for Decision Trees.
- Decision Trees are simple to train, interpret, and visualize.
- Proper tuning of **max_depth**, **min_samples_split**, **min_samples_leaf**, and **ccp_alpha** is essential to prevent overfitting.
- Feature importance and visualization make Decision Trees highly interpretable.
- Decision Trees form the foundation of advanced ensemble algorithms such as **Random Forest**, **AdaBoost**, **Gradient Boosting**, **XGBoost**, **LightGBM**, and **CatBoost**, making them one of the most important topics for Data Science and Machine Learning interviews.
