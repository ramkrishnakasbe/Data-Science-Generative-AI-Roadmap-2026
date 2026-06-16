# CRISP-DM (Cross-Industry Standard Process for Data Mining)

## What is CRISP-DM?

CRISP-DM (Cross-Industry Standard Process for Data Mining) is the most widely used framework for executing Data Science and Machine Learning projects.

It provides a structured approach to solving business problems using data.

The framework was developed to ensure that Data Science projects focus on business goals rather than just building models.

---

# Why CRISP-DM?

Without a framework:

```text
Business Problem
      ↓
Random Analysis
      ↓
Random Model
      ↓
Poor Results
```

With CRISP-DM:

```text
Business Problem
      ↓
Business Understanding
      ↓
Data Understanding
      ↓
Data Preparation
      ↓
Model Building
      ↓
Evaluation
      ↓
Deployment
```

---

# CRISP-DM Lifecycle

```text
CRISP-DM
│
├── 1. Business Understanding
│
├── 2. Data Understanding
│
├── 3. Data Preparation
│
├── 4. Modeling
│
├── 5. Evaluation
│
└── 6. Deployment
```

---

# 1. Business Understanding

## Objective

Understand the business problem before touching any data.

The most important phase of the entire project.

---

## Questions to Ask

### What problem are we solving?

Examples:

* Predict customer churn
* Detect fraud transactions
* Forecast sales
* Recommend products

---

### Why is it important?

Example:

A telecom company loses customers every month.

Business wants to identify customers likely to leave.

---

### What is the success criteria?

Examples:

* Reduce churn by 15%
* Increase sales by 20%
* Improve fraud detection accuracy

---

## Deliverables

* Business Problem Statement
* Project Objectives
* Success Metrics
* Constraints
* Stakeholder Requirements

---

# Example

### Business Problem

Netflix wants to reduce subscriber cancellations.

### Goal

Predict customers likely to cancel their subscription.

### Success Metric

Reduce churn by 10%.

---

# 2. Data Understanding

## Objective

Collect and understand available data.

---

## Activities

### Data Collection

Sources:

* Databases
* APIs
* Excel Files
* Cloud Storage
* Data Warehouses

---

### Data Exploration

Understand:

* Number of rows
* Number of columns
* Data types
* Missing values
* Outliers

---

### Exploratory Data Analysis (EDA)

Examples:

* Distribution Analysis
* Correlation Analysis
* Trend Analysis

---

## Questions

* Do we have enough data?
* Is data relevant?
* Is data reliable?
* What patterns exist?

---

## Deliverables

* Data Dictionary
* Data Quality Report
* EDA Report

---

# Example

Customer Churn Dataset

Features:

```text
Customer_ID
Age
Salary
Tenure
Contract_Type
Monthly_Charges
Churn
```

Explore:

* Missing values
* Churn percentage
* Average tenure

---

# 3. Data Preparation

## Objective

Convert raw data into model-ready data.

This phase usually consumes 60%–80% of project effort.

---

## Activities

### Data Cleaning

Handle:

* Missing values
* Duplicate records
* Invalid records

---

### Outlier Treatment

Methods:

* IQR Method
* Z-Score Method

---

### Feature Engineering

Create new features.

Example:

```text
Customer Age = 30

Joining Year = 2018

Current Year = 2025

Years_With_Company = 7
```

---

### Encoding

Convert categories to numbers.

Methods:

* Label Encoding
* One-Hot Encoding

---

### Scaling

Methods:

* Standardization
* Normalization

---

### Data Splitting

```text
Training Data = 80%

Testing Data = 20%
```

---

## Deliverables

* Clean Dataset
* Feature Set
* Training Dataset
* Testing Dataset

---

# 4. Modeling

## Objective

Build Machine Learning models.

---

## Activities

Choose appropriate algorithms.

---

### Supervised Learning

#### Regression

Examples:

* Linear Regression
* Random Forest Regressor

Used for:

```text
Predict Salary
Predict Sales
Predict Revenue
```

---

#### Classification

Examples:

* Logistic Regression
* Decision Tree
* Random Forest
* XGBoost

Used for:

```text
Fraud Detection
Customer Churn
Disease Prediction
```

---

### Unsupervised Learning

Examples:

* K-Means Clustering
* Hierarchical Clustering

Used for:

```text
Customer Segmentation
Market Basket Analysis
```

---

## Deliverables

* Trained Models
* Hyperparameter Results
* Performance Metrics

---

# Example

Build:

```text
Logistic Regression
Random Forest
XGBoost
```

Compare performance and choose the best model.

---

# 5. Evaluation

## Objective

Determine whether the model solves the business problem.

---

## Technical Evaluation

### Classification Metrics

* Accuracy
* Precision
* Recall
* F1 Score
* ROC-AUC

---

### Regression Metrics

* MAE
* MSE
* RMSE
* R² Score

---

## Business Evaluation

Ask:

### Does the model achieve business goals?

Example:

Business wanted:

```text
Reduce churn by 10%
```

Model predicts churn accurately enough to achieve this goal.

---

## Deliverables

* Evaluation Report
* Model Comparison Report
* Business Validation Report

---

# Example

| Model               | Accuracy |
| ------------------- | -------- |
| Logistic Regression | 82%      |
| Random Forest       | 89%      |
| XGBoost             | 91%      |

Best Model:

```text
XGBoost
```

---

# 6. Deployment

## Objective

Make the model available for real-world usage.

---

## Deployment Methods

### Batch Deployment

Example:

Generate predictions once per day.

---

### Real-Time Deployment

Example:

Fraud detection during payment processing.

---

### Cloud Deployment

Platforms:

* AWS
* Azure
* GCP

---

### API Deployment

Tools:

* Flask
* FastAPI
* Django

---

## Monitoring

Track:

* Model Accuracy
* Data Drift
* Concept Drift
* Prediction Quality

---

## Deliverables

* Production Model
* APIs
* Monitoring Dashboard
* Documentation

---

# Example

Customer enters details.

```text
Customer Data
      ↓
API
      ↓
ML Model
      ↓
Churn Prediction
      ↓
Business Action
```

---

# Complete CRISP-DM Flow

```text
Business Problem
        ↓
Business Understanding
        ↓
Data Understanding
        ↓
Data Preparation
        ↓
Model Building
        ↓
Evaluation
        ↓
Deployment
        ↓
Monitoring
```

---

# Real-World Example: Customer Churn Project

## Business Understanding

Predict customers likely to leave.

---

## Data Understanding

Collect customer transaction and subscription data.

---

## Data Preparation

Clean missing values and create features.

---

## Modeling

Train Logistic Regression and XGBoost.

---

## Evaluation

Select best-performing model.

---

## Deployment

Deploy as REST API.

---

# Benefits of CRISP-DM

✅ Business-focused

✅ Industry Standard

✅ Structured Workflow

✅ Reduces Project Failure

✅ Improves Communication

✅ Reusable Framework

✅ Works Across Industries

---

# Interview Questions

## What is CRISP-DM?

A standard framework for executing Data Science and Machine Learning projects.

---

## How many phases are there in CRISP-DM?

6 Phases:

1. Business Understanding
2. Data Understanding
3. Data Preparation
4. Modeling
5. Evaluation
6. Deployment

---

## Which phase consumes the most time?

Data Preparation

Typically 60–80% of project effort.

---

## Which is the most important phase?

Business Understanding

A wrong business objective can make the entire project fail.

---

## Why is Evaluation important?

To ensure the model solves the business problem and not just achieve good technical metrics.

---

# Key Takeaways

✅ CRISP-DM is the industry-standard Data Science lifecycle

✅ Always start with the business problem

✅ Data Preparation is the most time-consuming phase

✅ Evaluation must consider both technical and business metrics

✅ Deployment and monitoring are essential for production success

✅ Every successful Data Science project follows a structured process similar to CRISP-DM
