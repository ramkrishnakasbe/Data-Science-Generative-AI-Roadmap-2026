# Binomial Distribution & Logistic Regression (Interview Notes)

## Why Logistic Regression?

Linear Regression predicts continuous values.

```
House Price → ₹50 Lakhs
Sales → 500 Units
```

For classification problems, the output should be a **probability (0–1)** instead of any real number.

Examples

- Spam / Not Spam
- Fraud / Genuine
- Disease / No Disease
- Customer Churn / No Churn

Linear Regression can predict values like:

```
-0.8
1.4
2.3
```

which are invalid probabilities.

Logistic Regression solves this problem.

---

# Binomial Distribution

Logistic Regression assumes the **target variable follows a Binomial Distribution**.

A Binomial Distribution models the number of successes in **n independent Bernoulli trials**.

Conditions

- Fixed number of trials (n)
- Two outcomes only
- Independent observations
- Constant probability (p)

Examples

| Problem | Success |
|----------|----------|
| Email | Spam |
| Customer | Churn |
| Patient | Disease |
| Loan | Default |
| Transaction | Fraud |

Notation

```
X ~ Binomial(n, p)
```

where

```
n = Number of trials
p = Probability of success
```

---

# Bernoulli Distribution

Special case of Binomial Distribution.

```
n = 1
```

Possible outcomes

```
0

or

1
```

Examples

```
Pass / Fail

Spam / Not Spam

Yes / No
```

Relationship

```
Bernoulli

↓

Multiple Independent Trials

↓

Binomial Distribution
```

---

# Why Binomial Distribution in Logistic Regression?

Suppose

```
Customer Churn

Yes = 1

No = 0
```

Instead of predicting

```
0

or

1
```

the model predicts

```
Probability of Churn
```

Example

```
0.82
```

Meaning

```
82% chance of churn
```

The actual target follows a Binomial Distribution.

---

# Probability

```
P(Y=1)

Probability of Success
```

```
P(Y=0)

Probability of Failure
```

Relationship

```
P(Y=0)

=

1-P(Y=1)
```

---

# Odds

Odds compare success against failure.

Formula

```
Odds

=

P

/

(1-P)
```

Example

```
P = 0.80

Odds

=

0.8

/

0.2

=

4
```

Meaning

Success is **4 times more likely** than failure.

---

# Log Odds (Logit)

Logistic Regression models **Log Odds**, not probability directly.

Formula

```
log(P/(1-P))
```

Also called

- Logit
- Log-Odds
- Logistic Function Input

Range

```
(-∞ , +∞)
```

---

# Logistic Regression Equation

Linear Equation

```
z

=

β₀

+

β₁X₁

+

β₂X₂

+

...

+

βₙXₙ
```

Convert linear output into probability using the Sigmoid Function.

---

# Sigmoid Function

Formula

```
P

=

1

/

(1+e⁻ᶻ)
```

where

```
z

=

β₀

+

β₁X₁

+

...
```

Range

```
0

to

1
```

Properties

- S-shaped curve
- Converts any real value into probability
- Smooth and differentiable
- Monotonic increasing

---

# Sigmoid Curve

```
Probability

1.0 |                 ****

0.8 |             ****

0.6 |         ****

0.5 |------***

0.4 |   **

0.2 | **

0.0 |*

      ----------------------------

          -∞      0      +∞
```

---

# Decision Boundary

Probability is converted into a class using a threshold.

Usually

```
Threshold = 0.5
```

Rule

```
P ≥ 0.5

↓

Class = 1
```

```
P < 0.5

↓

Class = 0
```

Threshold can be changed depending on business requirements.

Examples

Fraud Detection

```
0.90
```

Medical Diagnosis

```
0.30
```

---

# Cost Function

Unlike Linear Regression,

Logistic Regression **does not use MSE**.

Reason

- Non-convex optimization
- Multiple local minima
- Poor convergence

Instead it uses

## Binary Cross Entropy (Log Loss)

Formula

```
Cost

=

−[

y log(p)

+

(1-y)log(1-p)

]
```

Lower Log Loss

↓

Better Model

---

# Maximum Likelihood Estimation (MLE)

Logistic Regression estimates coefficients using **Maximum Likelihood Estimation**, not Ordinary Least Squares.

Goal

Choose coefficients that maximize the probability of observing the actual labels.

Workflow

```
Initialize Coefficients

↓

Calculate Probability

↓

Compute Log Loss

↓

Gradient Descent

↓

Update Coefficients

↓

Repeat Until Convergence
```

---

# Gradient Descent

Updates coefficients to minimize Log Loss.

Update Rule

```
β

=

β

-

α

×

Gradient
```

where

```
α

=

Learning Rate
```

---

# Interpretation of Coefficients

Each coefficient represents the change in **Log Odds** for a one-unit increase in the predictor, keeping other variables constant.

Positive Coefficient

```
Probability increases
```

Negative Coefficient

```
Probability decreases
```

Exponentiating a coefficient gives the **Odds Ratio**.

---

# Odds Ratio

Formula

```
Odds Ratio

=

e^β
```

Interpretation

| Odds Ratio | Meaning |
|------------|---------|
| >1 | Odds Increase |
| <1 | Odds Decrease |
| =1 | No Effect |

Example

```
β = 0.69

Odds Ratio

≈ 2
```

A one-unit increase in the feature doubles the odds of the positive class.

---

# Assumptions

- Binary dependent variable
- Independent observations
- No severe multicollinearity
- Linear relationship between predictors and log-odds
- Large sample size
- Limited influence of extreme outliers

---

# Evaluation Metrics

Do **not** rely only on accuracy.

Confusion Matrix

```
                Predicted

              0        1

Actual 0      TN       FP

Actual 1      FN       TP
```

Important Metrics

```
Accuracy

=

(TP+TN)

/

Total
```

```
Precision

=

TP

/

(TP+FP)
```

```
Recall

=

TP

/

(TP+FN)
```

```
F1 Score

=

2PR

/

(P+R)
```

```
Specificity

=

TN

/

(TN+FP)
```

```
ROC-AUC
```

Higher AUC indicates better class separation.

---

# Advantages

- Simple and interpretable
- Fast training
- Produces probabilities
- Works well for binary classification
- Easy to deploy
- Robust baseline model

---

# Limitations

- Linear decision boundary
- Sensitive to multicollinearity
- Cannot model complex non-linear relationships without feature engineering
- Requires sufficient data
- Performance degrades with many irrelevant features

---

# Interview Questions

1. Why can't Linear Regression be used for classification?
2. Why is Logistic Regression called a regression algorithm despite solving classification problems?
3. Why does Logistic Regression use the Sigmoid Function?
4. Explain Bernoulli and Binomial Distribution.
5. Why does Logistic Regression use Binomial Distribution?
6. Difference between probability, odds, and log-odds.
7. Why is MSE not used in Logistic Regression?
8. What is Log Loss?
9. Why is Maximum Likelihood Estimation used?
10. Explain Odds Ratio.
11. How do you interpret logistic regression coefficients?
12. Why can the decision threshold be changed?
13. When is Logistic Regression preferred over Decision Trees?
14. What assumptions does Logistic Regression make?
15. Which evaluation metrics are most important for an imbalanced dataset?

---

# Quick Revision

| Topic | Key Point |
|--------|-----------|
| Target Distribution | Binomial |
| Single Trial | Bernoulli |
| Output | Probability (0–1) |
| Function | Sigmoid |
| Equation | Logit = β₀ + β₁X₁ + ... |
| Estimation | Maximum Likelihood Estimation (MLE) |
| Optimization | Gradient Descent |
| Cost Function | Binary Cross Entropy (Log Loss) |
| Threshold | Usually 0.5 |
| Coefficient Interpretation | Change in Log Odds |
| `e^β` | Odds Ratio |
| Evaluation | Precision, Recall, F1, ROC-AUC, Confusion Matrix |
| Best For | Binary Classification |
