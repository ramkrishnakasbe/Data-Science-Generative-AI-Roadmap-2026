# Ordinal Logistic Regression (Proportional Odds Model)

> **Interview Level:** Beginner → Advanced
>
> **Goal:** Learn Ordinal Logistic Regression, its mathematical intuition, assumptions, evaluation metrics, implementation, and interview questions.

---

# What is Ordinal Logistic Regression?

Ordinal Logistic Regression (OLR) is a **Supervised Machine Learning Classification Algorithm** used when the **target variable has ordered (ranked) categories**.

Unlike Multinomial Logistic Regression, the classes have a **natural order**.

Examples

| Problem | Classes |
|----------|----------|
| Customer Satisfaction | Poor, Average, Good, Excellent |
| Education Level | High School, Bachelor's, Master's, PhD |
| Movie Rating | 1⭐, 2⭐, 3⭐, 4⭐, 5⭐ |
| Disease Severity | Mild, Moderate, Severe |
| Credit Rating | Low, Medium, High |

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

# Why Not Multinomial Logistic Regression?

Multinomial Logistic Regression treats every class as **independent**.

Example

```
Poor

Average

Good

Excellent
```

It ignores that

```
Poor < Average < Good < Excellent
```

Ordinal Logistic Regression preserves this ordering.

---

# Ordinal vs Multinomial

| Ordinal Logistic Regression | Multinomial Logistic Regression |
|------------------------------|--------------------------------|
| Ordered Classes | Unordered Classes |
| Uses Class Ranking | No Ranking |
| Predicts Ordered Categories | Predicts Independent Classes |
| More Efficient for Ordered Data | Better for Nominal Data |

---

# Examples of Ordinal Problems

Customer Feedback

```
Very Dissatisfied

↓

Dissatisfied

↓

Neutral

↓

Satisfied

↓

Very Satisfied
```

Loan Risk

```
Low

↓

Medium

↓

High
```

Pain Level

```
None

↓

Mild

↓

Moderate

↓

Severe
```

---

# Mathematical Idea

Instead of predicting each class separately,

Ordinal Logistic Regression predicts

```
Cumulative Probability
```

Example

```
P(Y ≤ Poor)

P(Y ≤ Average)

P(Y ≤ Good)
```

The remaining probability belongs to the highest category.

---

# Cumulative Logit Model

Also called

```
Proportional Odds Model
```

Formula

```
log(

P(Y≤j)

/

P(Y>j)

)

=

αj

-

βX
```

Where

```
αj

=

Threshold (Cut Point)

β

=

Regression Coefficients

X

=

Predictor Variables
```

Each category has a different threshold (**α**) but shares the same coefficients (**β**).

---

# Why "Proportional Odds"?

The relationship between predictors and the log-odds is assumed to be **constant across all category thresholds**.

Example

```
Poor | Average | Good | Excellent
```

The effect of **Age**, **Income**, or **Experience** is assumed to be the same across every split.

This is called the **Proportional Odds Assumption**.

---

# Thresholds (Cut Points)

For four ordered classes

```
Poor

Average

Good

Excellent
```

Model estimates

```
Threshold 1

Poor | Others

Threshold 2

Poor, Average | Others

Threshold 3

Poor, Average, Good | Excellent
```

---

# Prediction

The model computes cumulative probabilities and converts them into probabilities for each class.

Example

| Class | Probability |
|--------|------------|
| Poor | 0.05 |
| Average | 0.15 |
| Good | 0.60 |
| Excellent | 0.20 |

Prediction

```
Good
```

(Highest probability)

---

# Decision Rule

```
Highest Probability

↓

Predicted Class
```

---

# Cost Function

Ordinal Logistic Regression uses

```
Maximum Likelihood Estimation (MLE)
```

The likelihood is optimized by minimizing the **Negative Log-Likelihood (Log Loss)**.

---

# Optimization

```
Initialize Parameters

↓

Calculate Probabilities

↓

Compute Log-Likelihood

↓

Gradient-Based Optimization

↓

Update Parameters

↓

Repeat Until Convergence
```

---

# Assumptions

- Dependent variable is ordinal.
- Categories are mutually exclusive.
- Independent observations.
- No severe multicollinearity.
- Linear relationship between predictors and log-odds.
- **Proportional Odds Assumption** holds.
- No influential outliers.
- Adequate sample size.

---

# Checking Proportional Odds Assumption

Common statistical tests

- Brant Test
- Likelihood Ratio Test
- Score Test
- Wald Test

If the assumption fails

- Partial Proportional Odds Model
- Generalized Ordered Logit Model

may be preferred.

---

# Interpretation of Coefficients

Positive Coefficient

↓

Higher probability of belonging to **higher ordered categories**.

Negative Coefficient

↓

Higher probability of belonging to **lower ordered categories**.

Odds Ratio

```
Odds Ratio

=

e^β
```

Interpretation

| Odds Ratio | Meaning |
|------------|---------|
| >1 | Higher odds of moving to a higher category |
| <1 | Higher odds of remaining in a lower category |
| =1 | No Effect |

---

# Evaluation Metrics

## Confusion Matrix

Shows predicted vs actual classes.

---

## Accuracy

```
Correct Predictions

/

Total Predictions
```

---

## Precision

Computed for each class.

Average

- Macro
- Micro
- Weighted

---

## Recall

Measures correctly identified instances for each class.

---

## F1 Score

Balances Precision and Recall.

Useful for imbalanced ordinal datasets.

---

## Cohen's Kappa

Measures agreement beyond chance.

Higher value indicates better agreement.

---

## Mean Absolute Error (Ordinal Distance)

Sometimes used because prediction errors have **order**.

Example

Predicting

```
Excellent

instead of

Good
```

is less severe than predicting

```
Excellent

instead of

Poor
```

---

# Advantages

- Uses natural ordering.
- More informative than Multinomial Logistic Regression.
- Produces interpretable coefficients.
- Efficient with ordered categories.
- Predicts probabilities.

---

# Limitations

- Requires proportional odds assumption.
- Linear decision boundary.
- Sensitive to multicollinearity.
- Less suitable for highly non-linear relationships.

---

# Applications

- Customer Satisfaction Analysis
- Credit Rating
- Employee Performance Rating
- Product Reviews
- Risk Assessment
- Education Level Prediction
- Disease Severity Classification
- Survey Analysis

---

# Python Implementation

Scikit-learn does **not** directly support Ordinal Logistic Regression.

Using `statsmodels`

```python
from statsmodels.miscmodels.ordinal_model import OrderedModel

model = OrderedModel(
    y,
    X,
    distr="logit"
)

result = model.fit()

prediction = result.predict(X_test)
```

Alternative libraries

- mord
- statsmodels

---

# Binary vs Multinomial vs Ordinal

| Binary | Multinomial | Ordinal |
|---------|-------------|----------|
| Two Classes | Multiple Unordered Classes | Multiple Ordered Classes |
| Sigmoid | Softmax | Cumulative Logit |
| Yes / No | Cat / Dog / Horse | Poor / Average / Good |

---

# Ordinal vs Multinomial

| Ordinal | Multinomial |
|----------|-------------|
| Ordered Labels | Unordered Labels |
| Uses Thresholds | Separate Class Probabilities |
| Proportional Odds | Softmax |
| Better for Rankings | Better for Nominal Classes |

---

# Interview Questions

## Beginner

1. What is Ordinal Logistic Regression?
2. Difference between Binary, Multinomial, and Ordinal Logistic Regression.
3. Give real-world examples of ordinal data.
4. What are ordered categories?
5. Why can't Multinomial Logistic Regression be used efficiently for ordinal data?

---

## Intermediate

1. Explain the Proportional Odds Model.
2. What is the Cumulative Logit Model?
3. What are Thresholds (Cut Points)?
4. Explain cumulative probabilities.
5. How do you interpret coefficients?

---

## Advanced

1. What is the Proportional Odds Assumption?
2. How do you test the Proportional Odds Assumption?
3. What happens if the assumption is violated?
4. Explain the mathematics of the cumulative logit equation.
5. Compare Ordinal Logistic Regression with Decision Trees and Gradient Boosting.

---

# Quick Revision

| Topic | Key Point |
|---------|-----------|
| Problem Type | Ordered Multi-Class Classification |
| Classes | ≥ 3 Ordered Categories |
| Examples | Ratings, Satisfaction, Severity |
| Model | Proportional Odds Model |
| Equation | Cumulative Logit |
| Estimation | Maximum Likelihood Estimation (MLE) |
| Optimization | Gradient-Based Optimization |
| Key Assumption | Proportional Odds Assumption |
| Output | Probability of Each Ordered Class |
| Evaluation | Accuracy, Precision, Recall, F1, Cohen's Kappa |
| Python | `statsmodels.OrderedModel()` |
| Best For | Ordered Classification Problems |
