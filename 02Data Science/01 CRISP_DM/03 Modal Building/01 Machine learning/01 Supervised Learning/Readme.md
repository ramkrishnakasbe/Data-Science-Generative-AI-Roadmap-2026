# Supervised Learning

# Overview

Supervised Learning is a type of Machine Learning in which the model learns from labeled data. Each training example contains both the input features (X) and the correct output (Y). The objective is to learn a mapping function from inputs to outputs so that the model can accurately predict the target variable for unseen data.

---

# Learning Objectives

After completing this section, you should be able to:

- Understand supervised learning concepts
- Differentiate regression and classification
- Build regression and classification models
- Select appropriate algorithms
- Evaluate model performance
- Handle overfitting and underfitting
- Perform hyperparameter tuning
- Apply feature selection techniques
- Interpret machine learning models

---

# Prerequisites

Before starting this section, you should be familiar with:

- Python
- Statistics
- Probability
- Linear Algebra
- Data Preprocessing
- Feature Scaling
- Exploratory Data Analysis (EDA)

---

# Topics Covered

## 1. Introduction

- What is Machine Learning?
- Types of Machine Learning
- What is Supervised Learning?
- Components of Supervised Learning
- Training vs Testing
- Features and Target Variable
- Learning Process

---

## 2. Regression Algorithms

- Linear Regression
- Multiple Linear Regression
- Polynomial Regression

---

## 3. Classification Algorithms

- Logistic Regression
- K-Nearest Neighbors (KNN)
- Naive Bayes
- Decision Tree
- Random Forest
- Support Vector Machine (SVM)

---

## 4. Ensemble Learning

- Voting
- Bagging
- Boosting
- Random Forest
- AdaBoost
- Gradient Boosting
- XGBoost
- LightGBM
- CatBoost

---

## 5. Model Evaluation

### Regression Metrics

- MAE
- MSE
- RMSE
- R² Score
- Adjusted R²

### Classification Metrics

- Accuracy
- Precision
- Recall
- Specificity
- F1 Score
- ROC Curve
- AUC
- Confusion Matrix

---

## 6. Cross Validation

- Train-Test Split
- K-Fold
- Stratified K-Fold
- Leave-One-Out (LOOCV)

---

## 7. Hyperparameter Tuning

- Grid Search
- Random Search
- Bayesian Optimization (Overview)

---

## 8. Bias-Variance Tradeoff

- Bias
- Variance
- Underfitting
- Overfitting

---

## 9. Regularization

- Ridge Regression (L2)
- Lasso Regression (L1)
- Elastic Net

---

## 10. Feature Selection

- Filter Methods
- Wrapper Methods
- Embedded Methods

---

## 11. Class Imbalance

- SMOTE
- Random Oversampling
- Random Undersampling
- Class Weights

---

## 12. Probability & Threshold

- Probability Prediction
- Threshold Selection
- ROC Threshold
- Precision-Recall Tradeoff

---

## 13. Model Explainability

- Feature Importance
- Permutation Importance
- SHAP
- LIME

---

# Learning Flow

```
Supervised Learning
        │
        ▼
Problem Definition
        │
        ▼
Data Collection
        │
        ▼
Data Cleaning
        │
        ▼
EDA
        │
        ▼
Feature Engineering
        │
        ▼
Train-Test Split
        │
        ▼
Choose Algorithm
        │
        ▼
Train Model
        │
        ▼
Prediction
        │
        ▼
Model Evaluation
        │
        ▼
Hyperparameter Tuning
        │
        ▼
Final Model
```

---

# Regression vs Classification

| Regression | Classification |
|------------|---------------|
| Predicts continuous values | Predicts categorical values |
| Example: House Price | Example: Spam Detection |
| Output: Numeric | Output: Class Label |

---

# Popular Algorithms

| Algorithm | Type |
|------------|------|
| Linear Regression | Regression |
| Logistic Regression | Classification |
| KNN | Both |
| Decision Tree | Both |
| Random Forest | Both |
| SVM | Both |
| Naive Bayes | Classification |
| XGBoost | Both |

---

# Real-World Applications

- House Price Prediction
- Credit Risk Analysis
- Customer Churn Prediction
- Disease Prediction
- Fraud Detection
- Email Spam Detection
- Sentiment Analysis
- Sales Forecasting
- Loan Approval
- Recommendation Systems

---

# Summary

Supervised Learning is one of the most widely used machine learning paradigms, where models learn from labeled data to predict outcomes. It consists of regression and classification algorithms, supported by preprocessing, model evaluation, validation, tuning, and explainability techniques. Mastering these topics forms the foundation of practical machine learning and is essential for data science interviews.
