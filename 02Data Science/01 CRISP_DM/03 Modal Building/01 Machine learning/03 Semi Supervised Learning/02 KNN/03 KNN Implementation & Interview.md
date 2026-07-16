# 03 KNN Implementation & Interview.md

# 1. KNN Workflow

The complete workflow of implementing KNN is shown below.

```
Collect Dataset
        │
        ▼
Data Cleaning
        │
        ▼
Handle Missing Values
        │
        ▼
Feature Engineering
        │
        ▼
Feature Scaling
        │
        ▼
Train-Test Split
        │
        ▼
Choose K
        │
        ▼
Train KNN
        │
        ▼
Prediction
        │
        ▼
Model Evaluation
```

---

# 2. Import Libraries

```python
import numpy as np
import pandas as pd

from sklearn.model_selection import train_test_split

from sklearn.preprocessing import StandardScaler

from sklearn.neighbors import KNeighborsClassifier

from sklearn.metrics import accuracy_score
```

---

# 3. Loading Dataset

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

# 5. Feature Scaling

Feature scaling is **mandatory** for KNN because it is based on distance.

```python
scaler = StandardScaler()

X_train = scaler.fit_transform(X_train)

X_test = scaler.transform(X_test)
```

---

# 6. Training KNN Classifier

```python
knn = KNeighborsClassifier(

n_neighbors=5)

knn.fit(X_train, y_train)
```

---

# 7. Prediction

```python
prediction = knn.predict(X_test)
```

---

# 8. Accuracy

```python
accuracy = accuracy_score(

y_test,

prediction)

print(accuracy)
```

---

# 9. Complete Example

```python
from sklearn.datasets import load_iris

from sklearn.model_selection import train_test_split

from sklearn.preprocessing import StandardScaler

from sklearn.neighbors import KNeighborsClassifier

from sklearn.metrics import accuracy_score

iris = load_iris()

X = iris.data

y = iris.target

X_train, X_test, y_train, y_test = train_test_split(

X,
y,

test_size=0.2,

random_state=42)

scaler = StandardScaler()

X_train = scaler.fit_transform(X_train)

X_test = scaler.transform(X_test)

model = KNeighborsClassifier(

n_neighbors=5)

model.fit(X_train,y_train)

prediction = model.predict(X_test)

print(accuracy_score(y_test,prediction))
```

---

# 10. KNN for Regression

KNN also supports regression.

Instead of majority voting,

it computes the **average** of neighboring target values.

Python

```python
from sklearn.neighbors import KNeighborsRegressor

model = KNeighborsRegressor(

n_neighbors=5)

model.fit(X_train,y_train)

prediction = model.predict(X_test)
```

---

# 11. Hyperparameters

## n_neighbors

Number of nearest neighbors.

Default

```
5
```

---

## weights

```
uniform

distance
```

uniform

All neighbors contribute equally.

distance

Closer neighbors receive larger weights.

---

## metric

Distance metric.

Examples

```
euclidean

manhattan

minkowski

chebyshev
```

---

## algorithm

Neighbor searching algorithm.

```
auto

brute

kd_tree

ball_tree
```

---

## p

Used for Minkowski Distance.

```
p=1

↓

Manhattan

p=2

↓

Euclidean
```

---

# 12. Hyperparameter Tuning

Use Grid Search to find the optimal K.

```python
from sklearn.model_selection import GridSearchCV

param_grid = {

'n_neighbors':[3,5,7,9,11],

'weights':['uniform','distance']

}

grid = GridSearchCV(

KNeighborsClassifier(),

param_grid,

cv=5)

grid.fit(X_train,y_train)

print(grid.best_params_)
```

---

# 13. Cross Validation

Cross Validation helps estimate model performance on unseen data.

Example

```
K=3

↓

Accuracy

↓

K=5

↓

Accuracy

↓

K=7

↓

Accuracy

↓

Choose Highest Accuracy
```

Most commonly

```
5-Fold

10-Fold
```

---

# 14. Evaluation Metrics

## Accuracy

```
Accuracy

=

Correct Predictions

-------------------

Total Predictions
```

---

## Precision

```
TP

-----------

TP+FP
```

---

## Recall

```
TP

-----------

TP+FN
```

---

## F1 Score

```
2 × Precision × Recall

----------------------------

Precision + Recall
```

---

## Confusion Matrix

```
              Actual

          +          -

Pred +

         TP         FP

Pred -

         FN         TN
```

---

# 15. Choosing the Best K

Common approach

```
Try

K=1

K=3

K=5

K=7

K=9

...

Choose Highest Validation Accuracy
```

---

# 16. KNN vs Logistic Regression

| KNN | Logistic Regression |
|------|---------------------|
| Lazy learner | Eager learner |
| Distance based | Probability based |
| Non-parametric | Parametric |
| No training | Training required |
| Slow prediction | Fast prediction |

---

# 17. KNN vs Decision Tree

| KNN | Decision Tree |
|------|---------------|
| Distance based | Rule based |
| Needs scaling | No scaling required |
| Lazy learner | Eager learner |
| Slow prediction | Fast prediction |

---

# 18. KNN vs Random Forest

| KNN | Random Forest |
|------|---------------|
| Single algorithm | Ensemble algorithm |
| Instance based | Tree based |
| Slow prediction | Faster prediction |
| High memory | Moderate memory |

---

# 19. KNN vs SVM

| KNN | SVM |
|------|-----|
| Distance based | Margin based |
| Lazy learner | Eager learner |
| Sensitive to scaling | Sensitive to scaling |
| Better for small datasets | Better for complex boundaries |

---

# 20. KNN vs Naive Bayes

| KNN | Naive Bayes |
|------|-------------|
| Distance based | Probability based |
| Lazy learner | Eager learner |
| Needs scaling | Usually no scaling |
| High prediction time | Fast prediction |
| High memory | Low memory |

---

# 21. Advantages

- Easy to understand
- Easy to implement
- No training phase
- Supports multiclass classification
- Supports regression
- Works well for small datasets
- Can learn complex decision boundaries

---

# 22. Disadvantages

- Slow prediction
- High memory requirement
- Sensitive to scaling
- Sensitive to irrelevant features
- Poor performance on high-dimensional data
- Computationally expensive for large datasets

---

# 23. Real-World Applications

## Recommendation Systems

```
Netflix

Amazon

Spotify
```

---

## Image Classification

Recognizing handwritten digits, objects, or faces.

---

## Face Recognition

Finding similar faces using nearest neighbors.

---

## Medical Diagnosis

Predicting diseases based on similar patient records.

---

## Fraud Detection

Identifying transactions similar to known fraudulent cases.

---

## Credit Risk Analysis

Predicting loan approval based on similar customers.

---

## Customer Segmentation

Grouping customers based on purchasing behavior.

---

## Anomaly Detection

Finding observations that are far from their nearest neighbors.

---

# 24. Common Interview Questions

### Why is KNN called a Lazy Learner?

Because it does not build a model during training. It stores the training data and performs computations only when making predictions.

---

### Why is feature scaling important in KNN?

KNN relies on distance calculations. Features with larger numerical values can dominate the distance, leading to biased predictions.

---

### Can KNN solve regression problems?

Yes. KNN Regression predicts the average (or weighted average) of the target values of the K nearest neighbors.

---

### Which distance metric is used most commonly?

**Euclidean Distance** is the default and most commonly used metric for numerical data.

---

### What happens if K = 1?

- High variance
- Sensitive to noise
- May overfit

---

### What happens if K is very large?

- High bias
- Underfitting
- Smoother decision boundary

---

### Does KNN require training?

No. KNN simply stores the training data and performs computations during prediction.

---

### Why is KNN slow?

For every new query, KNN computes distances to many or all training samples, making prediction computationally expensive.

---

### Can KNN handle multiclass classification?

Yes. KNN naturally supports binary and multiclass classification using majority voting.

---

### What are the limitations of KNN?

- High prediction time
- High memory usage
- Sensitive to scaling and irrelevant features
- Suffers from the curse of dimensionality

---

# 25. Best Practices

- Always scale numerical features.
- Use **Cross Validation** to select the best value of **K**.
- Remove irrelevant features before training.
- Use **Weighted KNN** when nearby neighbors should have more influence.
- Use **KD Tree** or **Ball Tree** to speed up neighbor searches on suitable datasets.
- Avoid KNN for extremely large or very high-dimensional datasets without optimization.

---

# 26. Summary

K-Nearest Neighbors (KNN) is a simple yet powerful supervised learning algorithm used for both classification and regression. It predicts outcomes based on the similarity of neighboring data points rather than learning an explicit model. Its performance depends heavily on choosing an appropriate **K**, selecting the right **distance metric**, and applying **feature scaling**. Although KNN is computationally expensive during prediction and suffers from the curse of dimensionality, it remains an excellent baseline algorithm and is widely used in recommendation systems, image recognition, medical diagnosis, and many other real-world applications.
