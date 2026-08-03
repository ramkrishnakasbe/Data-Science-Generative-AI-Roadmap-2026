# Multinomial Logistic Regression (Softmax Regression)

> **Interview Level:** Beginner → Advanced
>
> **Goal:** Learn Multinomial Logistic Regression (Multiclass Logistic Regression), its mathematics, assumptions, evaluation metrics, implementation, and interview questions.

---

# What is Multinomial Logistic Regression?

Multinomial Logistic Regression (MLR) is an extension of **Binary Logistic Regression** used when the target variable has **more than two classes**.

Instead of predicting

```
Yes / No
```

it predicts

```
Class A

Class B

Class C

...

Class N
```

Examples

| Problem | Classes |
|----------|----------|
| Animal Classification | Dog, Cat, Horse |
| Digit Recognition | 0-9 |
| Iris Dataset | Setosa, Versicolor, Virginica |
| Sentiment Analysis | Positive, Neutral, Negative |
| Product Category | Electronics, Fashion, Grocery |

---

# Why Not Binary Logistic Regression?

Binary Logistic Regression can classify only

```
0

or

1
```

For problems having

```
3

4

5

...

N Classes
```

we use

```
Multinomial Logistic Regression
```

---

# Binary vs Multinomial Logistic Regression

| Binary Logistic Regression | Multinomial Logistic Regression |
|-----------------------------|--------------------------------|
| Two Classes | More than Two Classes |
| Sigmoid Function | Softmax Function |
| Single Probability | Probability for Every Class |
| One Decision Boundary | Multiple Decision Boundaries |

---

# Types of Logistic Regression

```
Logistic Regression

│

├── Binary Logistic Regression

├── Multinomial Logistic Regression

└── Ordinal Logistic Regression
```

---

# Mathematical Model

Linear Equation

For every class

```
Z₁ = β₀ + β₁X₁ + β₂X₂ + ...

Z₂ = β₀ + β₁X₁ + β₂X₂ + ...

...

Zn
```

Each class has its own coefficients.

---

# Softmax Function

Unlike Binary Logistic Regression,

Multinomial Logistic Regression uses the **Softmax Function**.

Formula

```
P(Class i)

=

e^(Zi)

/

Σ e^(Zj)
```

where

```
Zi

=

Linear Score

for class i
```

Properties

- Output lies between 0 and 1
- Sum of all probabilities equals 1
- Produces probability for every class

---

# Example

Suppose

```
Animal Classifier
```

Predicted probabilities

| Class | Probability |
|---------|------------|
| Dog | 0.15 |
| Cat | 0.70 |
| Horse | 0.15 |

Prediction

```
Cat
```

Highest probability wins.

---

# Decision Rule

```
Predicted Class

=

ArgMax

(Probability)
```

Example

```
Dog

0.20

Cat

0.72

Horse

0.08
```

Prediction

```
Cat
```

---

# Softmax vs Sigmoid

| Sigmoid | Softmax |
|----------|----------|
| Binary Classification | Multi-Class Classification |
| One Probability | Probability of Every Class |
| Independent Output | Probabilities Sum to 1 |

---

# Cost Function

Multinomial Logistic Regression uses

## Categorical Cross Entropy

Formula

```
Loss

=

−Σ

yi log(pi)
```

Lower Loss

↓

Better Model

---

# Optimization

Coefficients are estimated using

```
Maximum Likelihood Estimation

+

Gradient Descent
```

---

# Assumptions

- Target has more than two categories
- Classes are mutually exclusive
- Independent observations
- No severe multicollinearity
- Linear relationship between predictors and log-odds
- Large sample size
- No influential outliers

---

# Decision Boundary

Binary Logistic Regression

```
One Boundary
```

Multinomial Logistic Regression

```
Multiple Boundaries
```

Example

```
Dog

Cat

Horse

↓

Three Decision Regions
```

---

# One-vs-Rest (OvR)

Another way to solve multiclass classification.

Example

```
Dog vs Others

Cat vs Others

Horse vs Others
```

Three binary classifiers are trained.

Prediction

Highest probability wins.

---

# Multinomial vs One-vs-Rest

| Multinomial | One-vs-Rest |
|--------------|------------|
| One Model | Multiple Binary Models |
| Uses Softmax | Uses Sigmoid |
| Classes compete together | Independent classifiers |
| Better calibrated probabilities | Simpler implementation |

---

# Advantages

- Simple
- Fast
- Interpretable
- Predicts probabilities
- Handles multiclass problems directly
- Easy deployment

---

# Limitations

- Linear decision boundary
- Sensitive to multicollinearity
- Requires feature engineering for complex data
- Doesn't perform well on highly non-linear problems

---

# Evaluation Metrics

## Confusion Matrix

Used to compare predicted and actual classes.

---

## Accuracy

```
Correct Predictions

/

Total Predictions
```

---

## Precision

Calculated for every class.

Can be averaged using

- Macro Average
- Micro Average
- Weighted Average

---

## Recall

Measures correctly identified instances of each class.

---

## F1 Score

Balances Precision and Recall.

Very useful for imbalanced multiclass datasets.

---

## ROC-AUC

ROC can be extended using

```
One-vs-Rest

or

One-vs-One
```

Average AUC is reported.

---

# Macro, Micro and Weighted Average

## Macro Average

Simple average of all classes.

Treats every class equally.

---

## Micro Average

Computes metrics globally.

Useful for class imbalance.

---

## Weighted Average

Weighted by class frequency.

Most commonly reported in Scikit-Learn.

---

# Applications

- Image Classification
- Handwritten Digit Recognition
- Disease Classification
- Customer Segmentation
- NLP Classification
- Document Classification
- Product Categorization
- Emotion Detection

---

# Python Implementation

```python
from sklearn.linear_model import LogisticRegression

model = LogisticRegression(

multi_class='multinomial',

solver='lbfgs'

)

model.fit(X_train,y_train)

prediction = model.predict(X_test)

probability = model.predict_proba(X_test)
```

---

# Important Parameters

```python
multi_class='multinomial'
```

```
solver='lbfgs'
```

Common Solvers

- lbfgs
- newton-cg
- saga
- sag

---

# Binary vs Multinomial vs Ordinal

| Binary | Multinomial | Ordinal |
|---------|-------------|----------|
| Two Classes | Multiple Classes | Ordered Classes |
| Sigmoid | Softmax | Cumulative Logit |
| Yes/No | Cat/Dog/Horse | Low/Medium/High |

---

# Interview Questions

## Beginner

1. What is Multinomial Logistic Regression?
2. Difference between Binary and Multinomial Logistic Regression.
3. Why do we use the Softmax Function?
4. What is the output of Softmax?
5. What is the difference between Sigmoid and Softmax?
6. Explain ArgMax.
7. Why do probabilities sum to 1?

---

## Intermediate

1. Explain Categorical Cross Entropy.
2. Difference between One-vs-Rest and Multinomial Logistic Regression.
3. Explain Macro, Micro and Weighted Average.
4. Which solver is used for Multinomial Logistic Regression?
5. How are coefficients estimated?

---

## Advanced

1. Why is Softmax preferred over Sigmoid for multiclass classification?
2. Explain Maximum Likelihood Estimation in Multiclass Logistic Regression.
3. Why is Cross Entropy preferred over MSE?
4. Explain Decision Boundaries in Multiclass Classification.
5. Compare Multinomial Logistic Regression with Decision Trees and Naive Bayes.

---

# Quick Revision

| Topic | Key Point |
|---------|-----------|
| Problem Type | Multi-Class Classification |
| Classes | ≥ 3 |
| Function | Softmax |
| Cost Function | Categorical Cross Entropy |
| Optimization | MLE + Gradient Descent |
| Prediction | ArgMax Probability |
| Output | Probability of Every Class |
| Evaluation | Accuracy, Precision, Recall, F1, ROC-AUC |
| Alternative | One-vs-Rest (OvR) |
| Best For | Linearly Separable Multi-Class Problems |
| Python | `LogisticRegression(multi_class="multinomial")` |
```
