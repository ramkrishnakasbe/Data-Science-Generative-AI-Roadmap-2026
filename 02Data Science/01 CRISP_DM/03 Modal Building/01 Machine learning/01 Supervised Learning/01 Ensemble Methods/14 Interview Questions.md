# Ensemble Learning - Interview Questions & Coding Questions

> **Level:** Beginner → Advanced
> **Purpose:** Data Science / Machine Learning Interview Preparation
> **Topics Covered:** Bagging, Boosting, Random Forest, Extra Trees, AdaBoost, Gradient Boosting, XGBoost, Voting, Stacking, Sampling, Cross Validation

---

# Table of Contents

1. Theory Interview Questions
2. Scenario-Based Questions
3. Coding Questions
4. Machine Learning Implementation Questions
5. SQL + Ensemble Questions
6. Python Interview Questions
7. Advanced Interview Questions
8. Frequently Asked Company Questions

---

# 1. Beginner Interview Questions

### Ensemble Learning

1. What is Ensemble Learning?
2. Why do we use Ensemble Models?
3. What are Weak Learners?
4. What are Strong Learners?
5. Explain Bias and Variance.
6. Difference between Bagging and Boosting.
7. What are the different Ensemble Techniques?
8. What is Bootstrap Sampling?
9. What is Out-of-Bag (OOB) Error?
10. What is Voting?
11. What is Stacking?
12. What is Blending?
13. Why does Ensemble Learning improve accuracy?
14. What are homogeneous and heterogeneous ensembles?
15. Explain majority voting.

---

# 2. Bagging Questions

1. What is Bagging?
2. Explain Bootstrap Aggregation.
3. Why is Bootstrap Sampling used?
4. How many trees are created in Bagging?
5. Can the same sample appear multiple times?
6. Explain OOB Score.
7. How is final prediction calculated?
8. Bagging for Classification vs Regression.
9. Advantages of Bagging.
10. Limitations of Bagging.

---

# 3. Random Forest Questions

1. What is Random Forest?
2. Why is it called Random Forest?
3. Difference between Decision Tree and Random Forest.
4. Why are random features selected?
5. What is Feature Importance?
6. Explain Gini Importance.
7. Explain OOB Score.
8. How does Random Forest prevent overfitting?
9. Explain max_features.
10. Explain n_estimators.
11. Why are Decision Trees unpruned in Random Forest?
12. Random Forest vs Extra Trees.
13. Random Forest vs XGBoost.
14. Random Forest for Classification vs Regression.

---

# 4. Extra Trees Questions

1. What is Extra Trees?
2. Difference between Extra Trees and Random Forest.
3. Why are random thresholds used?
4. Which algorithm trains faster?
5. Which algorithm has lower variance?
6. When should Extra Trees be preferred?

---

# 5. AdaBoost Questions

1. What is AdaBoost?
2. Why is it called Adaptive Boosting?
3. What is a weak learner?
4. Why are Decision Stumps used?
5. Explain sample weights.
6. Explain learner weights.
7. How are misclassified samples handled?
8. What is weighted voting?
9. AdaBoost vs Gradient Boosting.
10. Limitations of AdaBoost.

---

# 6. Gradient Boosting Questions

1. What is Gradient Boosting?
2. Explain residual errors.
3. Why are residuals predicted?
4. Explain loss function.
5. Why is Gradient Descent used?
6. What is shrinkage?
7. Explain learning rate.
8. What is n_estimators?
9. Gradient Boosting vs AdaBoost.
10. Gradient Boosting vs XGBoost.

---

# 7. XGBoost Questions

1. What is XGBoost?
2. Why is XGBoost faster?
3. What is Regularization?
4. Explain Gamma.
5. Explain Alpha and Lambda.
6. How does XGBoost handle missing values?
7. What is tree pruning?
8. What is Early Stopping?
9. Explain Feature Importance.
10. XGBoost vs Random Forest.
11. XGBoost vs LightGBM.
12. When should you use XGBoost?

---

# 8. Voting Questions

1. What is Voting Classifier?
2. Difference between Hard Voting and Soft Voting.
3. Which voting is more accurate?
4. Explain probability averaging.
5. Explain weighted voting.
6. Voting vs Bagging.
7. Voting vs Stacking.

---

# 9. Stacking Questions

1. What is Stacking?
2. What is a Meta Learner?
3. What are Base Learners?
4. Why is Cross Validation required?
5. Explain Out-of-Fold Predictions.
6. Can XGBoost be a Meta Learner?
7. Advantages of Stacking.
8. Stacking vs Voting.

---

# 10. Sampling Questions

1. What is Sampling?
2. Probability vs Non-Probability Sampling.
3. Explain Bootstrap Sampling.
4. Explain Stratified Sampling.
5. Explain Systematic Sampling.
6. Sampling with Replacement.
7. Sampling without Replacement.
8. Hold-Out Method vs K-Fold.
9. LOOCV vs K-Fold.
10. Why Stratified K-Fold?

---

# 11. Scenario-Based Questions

### Scenario 1

Your Random Forest is overfitting.

How will you reduce overfitting?

---

### Scenario 2

Dataset contains

```
98%

2%
```

class distribution.

Which sampling method will you use?

---

### Scenario 3

Your XGBoost model gives

```
99%

Training Accuracy

75%

Testing Accuracy
```

What is happening?

---

### Scenario 4

Why is Soft Voting usually better than Hard Voting?

---

### Scenario 5

When would you prefer Bagging over Boosting?

---

### Scenario 6

Which algorithm would you choose for

- Credit Card Fraud
- Customer Churn
- House Price Prediction
- Image Classification

Why?

---

# 12. Coding Questions (Python)

## Easy

### Question 1

Implement Bagging Classifier.

---

### Question 2

Train Random Forest on Iris Dataset.

---

### Question 3

Calculate Feature Importance.

---

### Question 4

Perform Bootstrap Sampling manually.

---

### Question 5

Split data using Stratified Sampling.

---

# Intermediate Coding Questions

### Question 6

Implement Hard Voting.

---

### Question 7

Implement Soft Voting.

---

### Question 8

Implement Stacking Classifier.

---

### Question 9

Implement AdaBoost.

---

### Question 10

Implement Gradient Boosting.

---

### Question 11

Train XGBoost on Titanic Dataset.

---

### Question 12

Perform Hyperparameter Tuning using GridSearchCV.

---

### Question 13

Perform RandomizedSearchCV on Random Forest.

---

### Question 14

Calculate OOB Score.

---

### Question 15

Plot Feature Importance.

---

# Advanced Coding Questions

### Question 16

Build a complete Fraud Detection Pipeline using XGBoost.

---

### Question 17

Compare

- Decision Tree
- Random Forest
- XGBoost

using Cross Validation.

---

### Question 18

Implement K-Fold Cross Validation manually.

---

### Question 19

Implement Bootstrap Sampling without sklearn.

---

### Question 20

Build a Stacking Model using

- Random Forest
- XGBoost
- SVM

Meta Learner

```
Logistic Regression
```

---

# 13. Machine Learning Practical Questions

1. How do you tune Random Forest?
2. How do you tune XGBoost?
3. Which evaluation metric would you choose?
4. How do you deal with Imbalanced Data?
5. How do you prevent overfitting?
6. How do you improve recall?
7. Explain Precision vs Recall.
8. Explain ROC-AUC.
9. What is Feature Importance?
10. How do you select important features?

---

# 14. SQL + Machine Learning Questions

1. Find duplicate records.
2. Handle missing values using SQL.
3. Calculate class distribution.
4. Find Top-N customers.
5. Rolling Average.
6. Moving Average.
7. Window Functions.
8. Dense Rank vs Rank.
9. CTE Interview Questions.
10. Joins for ML datasets.

---

# 15. Python Questions

1. Difference between list and tuple.
2. Lambda Function.
3. Map vs Filter.
4. Decorators.
5. Generators.
6. Iterators.
7. Exception Handling.
8. NumPy vs List.
9. Pandas merge().
10. GroupBy operations.

---

# 16. Advanced Interview Questions

1. Explain Bias-Variance Tradeoff.
2. Why does Bagging reduce variance?
3. Why does Boosting reduce bias?
4. Explain OOB Error mathematically.
5. Why does XGBoost use Regularization?
6. Explain Gradient Descent in Gradient Boosting.
7. Explain Residual Learning.
8. Explain Feature Importance calculation.
9. Explain SHAP Values.
10. Difference between Explainability and Interpretability.

---

# 17. Frequently Asked Company Questions

### TCS

- Random Forest
- Bagging
- Bootstrap Sampling
- Feature Importance

---

### Accenture

- XGBoost
- Hyperparameter Tuning
- Cross Validation
- ROC-AUC

---

### Deloitte

- Ensemble Learning
- Random Forest
- Business Case Studies

---

### Cognizant

- Bagging vs Boosting
- Voting
- Gradient Boosting

---

### Infosys

- Decision Trees
- Random Forest
- AdaBoost
- Sampling

---

### Walmart

- XGBoost
- Feature Engineering
- Model Evaluation
- Ensemble Learning

---

### Amazon

- XGBoost
- Explainability
- SHAP Values
- Bias-Variance Tradeoff
- Hyperparameter Optimization

---

### Microsoft

- Ensemble Architecture
- Cross Validation
- Stacking
- Model Deployment

---

# Quick Revision Checklist

- ✅ Ensemble Learning
- ✅ Bagging
- ✅ Boosting
- ✅ Random Forest
- ✅ Extra Trees
- ✅ AdaBoost
- ✅ Gradient Boosting
- ✅ XGBoost
- ✅ Voting
- ✅ Stacking
- ✅ Bootstrap Sampling
- ✅ Stratified Sampling
- ✅ Hold-Out Method
- ✅ K-Fold Cross Validation
- ✅ LOOCV
- ✅ Hyperparameter Tuning
- ✅ Feature Importance
- ✅ OOB Score
- ✅ Bias-Variance Tradeoff
- ✅ Model Evaluation Metrics
- ✅ Python Implementation
- ✅ Practical Coding Questions

---

# Interview Preparation Tips

- Focus on **concepts first**, then learn **Python implementations** using `scikit-learn` and `xgboost`.
- Be ready to explain **why** you choose one ensemble method over another in a business scenario.
- Practice coding ensemble models on datasets such as **Titanic**, **Iris**, **Wine Quality**, **House Prices**, and **Credit Card Fraud**.
- Revise hyperparameters (`n_estimators`, `max_depth`, `learning_rate`, `subsample`, `colsample_bytree`, etc.) and understand how they affect model performance.
- Interviewers often ask for **comparisons** (Bagging vs Boosting, Random Forest vs XGBoost, Voting vs Stacking) along with practical use cases, so prepare those thoroughly.
