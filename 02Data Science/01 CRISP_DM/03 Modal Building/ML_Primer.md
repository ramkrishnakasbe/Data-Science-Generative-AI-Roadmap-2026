# Machine Learning Primer

# Overview

Machine Learning (ML) is a branch of Artificial Intelligence (AI) that enables computers to learn patterns from data and make predictions or decisions without being explicitly programmed.

Instead of writing rules manually, machine learning algorithms learn from historical data and improve their performance over time.

---

# Artificial Intelligence vs Machine Learning vs Deep Learning

| Artificial Intelligence | Machine Learning | Deep Learning |
|-------------------------|------------------|---------------|
| Makes machines intelligent | Learns patterns from data | Uses deep neural networks to learn complex patterns |
| Broadest field | Subset of AI | Subset of ML |

---

# Types of Machine Learning

## 1. Supervised Learning

- Uses labeled data
- Predicts target variable
- Includes Regression and Classification

**Examples**

- House Price Prediction
- Spam Detection
- Disease Prediction

---

## 2. Unsupervised Learning (Descriptive Learning)

- Uses unlabeled data
- Finds hidden patterns
- Includes Clustering and Association

**Examples**

- Customer Segmentation
- Market Basket Analysis
- Topic Modeling

---

## 3. Semi-Supervised Learning

- Uses both labeled and unlabeled data
- Helpful when labeling data is expensive

**Examples**

- Medical Imaging
- Speech Recognition

---

## 4. Self-Supervised Learning

- Creates labels automatically from data
- Mainly used in Deep Learning

**Examples**

- GPT
- BERT
- Computer Vision Models

---

## 5. Reinforcement Learning

- Learns through rewards and penalties
- Agent interacts with environment

**Examples**

- Robotics
- Self-driving Cars
- Game Playing

---

## 6. Forecasting / Time Series

- Predicts future values using historical observations

**Examples**

- Stock Price Prediction
- Weather Forecasting
- Sales Forecasting

---

# Machine Learning Workflow

```text
Business Problem
      │
      ▼
Data Collection
      │
      ▼
Data Preprocessing
      │
      ▼
Exploratory Data Analysis
      │
      ▼
Feature Engineering
      │
      ▼
Feature Scaling
      │
      ▼
Split Dataset
      │
      ▼
Model Training
      │
      ▼
Validation
      │
      ▼
Hyperparameter Tuning
      │
      ▼
Testing
      │
      ▼
Deployment
```

---

# Dataset Components

Every supervised learning dataset contains:

## Features (Independent Variables)

Represented by **X**

Example

| Age | Salary | Experience |
|-----|---------|------------|

These are the input variables.

---

## Target Variable (Dependent Variable)

Represented by **Y**

Example

| Purchased |
|------------|
| Yes |
| No |

This is the output the model tries to predict.

---

# Parameters vs Hyperparameters

## Parameters

- Learned automatically by the model
- Updated during training

**Examples**

- Weights
- Bias
- Regression Coefficients

---

## Hyperparameters

- Set before training
- Control model behavior

**Examples**

- Learning Rate
- Number of Neighbors
- Tree Depth
- Number of Trees
- Epochs

---

# Dataset Splitting

The dataset is divided into three parts.

## Training Set

Purpose:

- Build the model
- Learn patterns from data

Typical Size:

- 70%
- 80%

---

## Validation Set

Purpose:

- Tune hyperparameters
- Compare different models

---

## Testing Set

Purpose:

- Evaluate final model
- Measure performance on unseen data

Testing data should never be used during training.

---

# Hyperparameter Tuning

Used to find the best hyperparameter values for a model.

Common Techniques

- Grid Search
- Random Search
- Bayesian Optimization

---

# Grid Search

- Tests every possible combination
- Finds the best parameters
- Computationally expensive

---

# Random Search

- Tests random combinations
- Faster than Grid Search
- Suitable for large parameter spaces

---

# Cross Validation

Cross Validation evaluates a model using multiple train-test splits.

Common Methods

- K-Fold Cross Validation
- Stratified K-Fold
- Leave-One-Out (LOOCV)

---

# Generalization

Generalization is the ability of a model to perform well on unseen data.

A good model should perform well on both training and testing datasets.

---

# Generalization Error

Testing error is also called **Generalization Error**.

Generalization Error consists of:

- Bias Error
- Variance Error
- Irreducible Error

---

# Bias

- Error caused by overly simple assumptions
- High bias leads to Underfitting

Characteristics

- High Training Error
- High Testing Error

---

# Variance

- Error caused by excessive model complexity
- Model memorizes training data

Characteristics

- Low Training Error
- High Testing Error

---

# Irreducible Error

- Error caused by noise in the data
- Cannot be eliminated completely

Examples

- Measurement errors
- Human errors
- Random noise

---

# Bias-Variance Tradeoff

A good model balances:

- Low Bias
- Low Variance

The goal is to achieve good generalization.

---

# Comparing Training Error and Testing Error

## Right Fit

Training Error → Low

Testing Error → Low

Training and testing errors are close to each other.

---

## Overfitting (High Variance)

Training Error → Low

Testing Error → High

Model memorizes training data instead of learning patterns.

### Common Solutions

- Regularization
- More Training Data
- Feature Selection
- Cross Validation
- Early Stopping
- Pruning

---

## Underfitting (High Bias)

Training Error → High

Testing Error → High

Model is too simple to capture the underlying patterns.

### Common Solutions

- Increase Model Complexity
- Better Feature Engineering
- Add More Features
- Reduce Regularization
- Train Longer

---

# Regularization

Regularization helps prevent Overfitting.

Common Types

- L1 Regularization (Lasso)
- L2 Regularization (Ridge)
- Elastic Net

---

# Model Evaluation

## Regression Metrics

- MAE
- MSE
- RMSE
- R² Score
- Adjusted R²

---

## Classification Metrics

- Accuracy
- Precision
- Recall
- F1 Score
- ROC Curve
- AUC
- Confusion Matrix

---

# Complete Machine Learning Pipeline

```text
Business Problem
      │
      ▼
Collect Data
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
Feature Scaling
      │
      ▼
Split Data
      │
      ▼
Training
      │
      ▼
Validation
      │
      ▼
Hyperparameter Tuning
      │
      ▼
Testing
      │
      ▼
Model Evaluation
      │
      ▼
Deployment
      │
      ▼
Monitoring
```

---

# Real-World Applications

- House Price Prediction
- Customer Churn Prediction
- Fraud Detection
- Recommendation Systems
- Disease Prediction
- Spam Detection
- Sentiment Analysis
- Stock Price Forecasting

---

# Summary

Machine Learning is a subset of Artificial Intelligence that enables systems to learn from data. A typical ML workflow includes data preprocessing, feature engineering, dataset splitting, model training, validation, hyperparameter tuning, testing, and deployment. Understanding concepts such as bias, variance, generalization, overfitting, underfitting, and regularization is essential for building accurate and reliable machine learning models.
