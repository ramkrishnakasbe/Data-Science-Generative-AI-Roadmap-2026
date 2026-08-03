# Logistic Regression Fundamentals

## What is Logistic Regression?

Logistic Regression is a **Supervised Machine Learning Classification Algorithm** used to predict the probability of a categorical outcome.

It is primarily used for:

- Binary Classification
- Multi-class Classification (OvR, Softmax)
- Probability Estimation

Examples

- Spam / Not Spam
- Fraud / Genuine
- Disease / No Disease
- Customer Churn
- Loan Default

Although called **Regression**, it is actually a **Classification Algorithm** because it predicts class probabilities.

---

# Why Not Linear Regression?

Linear Regression predicts continuous values.

Example

```
Predicted Probability

1.42

-0.35
```

These are invalid probabilities.

A probability must always lie between

```
0 and 1
```

Logistic Regression converts the linear output into probability using the **Sigmoid Function**.

---

# Binomial Distribution

Logistic Regression assumes the dependent variable follows a **Binomial Distribution**.

Conditions

- Two outcomes
- Independent observations
- Constant probability
- Fixed number of trials

Notation

```
X ~ Binomial(n,p)
```

where

```
n = Number of Trials

p = Probability of Success
```

---

# Bernoulli Distribution

Special case of Binomial Distribution

```
n = 1
```

Possible values

```
0

1
```

Examples

- Pass / Fail
- Fraud / Genuine
- Churn / No Churn

---

# Relationship

```
Bernoulli Trial

↓

Repeated n Times

↓

Binomial Distribution

↓

Logistic Regression
```

---

# Probability

```
P(Y=1)
```

Probability of Success

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
P=0.80

Odds=4
```

Meaning

Success is four times more likely.

---

# Log Odds (Logit)

Formula

```
log(P/(1-P))
```

Range

```
(-∞,+∞)
```

Linear Regression predicts Log Odds.

---

# Logistic Regression Equation

```
Z

=

β₀

+

β₁X₁

+

β₂X₂

...

+

βₙXₙ
```

---

# Sigmoid Function

```
P

=

1

/

(1+e⁻ᶻ)
```

Range

```
0

to

1
```

Properties

- S-shaped curve
- Differentiable
- Monotonic
- Converts any value into probability

---

# Decision Boundary

Usually

```
0.5
```

Rule

```
Probability ≥ 0.5

↓

Class 1
```

```
Probability <0.5

↓

Class 0
```

Threshold depends on business requirements.

---

# Cost Function

Logistic Regression does NOT use MSE.

Instead it uses

## Binary Cross Entropy

```
Cost

=

−[

ylog(p)

+

(1-y)log(1-p)

]
```

Lower Loss

↓

Better Model

---

# Maximum Likelihood Estimation (MLE)

Goal

Find coefficients that maximize the probability of observing the actual labels.

Workflow

```
Initialize Coefficients

↓

Predict Probability

↓

Calculate Log Loss

↓

Update Coefficients

↓

Repeat
```

---

# Gradient Descent

Updates coefficients.

```
β

=

β

-

α×Gradient
```

where

```
α

=

Learning Rate
```

---

# Coefficient Interpretation

Positive coefficient

↓

Higher probability

Negative coefficient

↓

Lower probability

---

# Odds Ratio

```
Odds Ratio

=

e^β
```

Interpretation

| Odds Ratio | Meaning |
|------------|----------|
| >1 | Positive Effect |
| <1 | Negative Effect |
| =1 | No Effect |

---

# Assumptions

- Binary Target
- Independent Observations
- No Severe Multicollinearity
- Linear Relationship between Predictors and Log Odds
- Large Dataset
- No Extreme Outliers

---

# Advantages

- Fast
- Simple
- Interpretable
- Gives Probabilities
- Works well for Binary Classification

---

# Limitations

- Linear Decision Boundary
- Sensitive to Multicollinearity
- Cannot model highly non-linear relationships
- Sensitive to Outliers

---

# Quick Revision

| Topic | Key Point |
|---------|-----------|
| Target | Binary |
| Distribution | Binomial |
| Function | Sigmoid |
| Output | Probability |
| Cost Function | Binary Cross Entropy |
| Optimization | Gradient Descent |
| Estimation | Maximum Likelihood |
| Interpretation | Odds Ratio |
