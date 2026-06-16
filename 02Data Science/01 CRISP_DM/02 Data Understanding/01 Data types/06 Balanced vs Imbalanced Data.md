# Balanced vs Imbalanced Data

# 1. Data Classification

```text
Classification Dataset
│
├── 1. Balanced Data
│
└── 2. Imbalanced Data
     │
     └── 2.1 Rare Event Data
```

---

# Why This Topic is Important?

Most real-world Machine Learning classification problems are imbalanced.

Examples:

- Fraud Detection
- Disease Prediction
- Credit Default Prediction
- Equipment Failure Prediction
- Network Intrusion Detection

Understanding class distribution is essential before building any classification model.

---

# 1. Balanced Data

## Definition

A dataset is called Balanced when all target classes have approximately equal observations.

---

## Example

Loan Approval Dataset

| Class | Count |
|---------|---------|
| Approved | 500 |
| Rejected | 500 |

Total Records = 1000

---

## Visualization

```text
Approved  ██████████ 500

Rejected  ██████████ 500
```

---

## Characteristics

- Classes are evenly distributed.
- Model learns all classes properly.
- Accuracy can be trusted.
- Easier model training.

---

## Real-World Example

Employee Attrition Dataset

| Attrition | Count |
|------------|--------|
| Yes | 1000 |
| No | 1000 |

Balanced distribution.

---

# 2. Imbalanced Data

## Definition

A dataset is called Imbalanced when one class has significantly more observations than another.

---

## Example

Fraud Detection Dataset

| Class | Count |
|---------|---------|
| Fraud | 100 |
| Non-Fraud | 10000 |

---

## Visualization

```text
Fraud       █

Non-Fraud   ███████████████████████████
```

---

## Characteristics

- One class dominates.
- Minority class becomes difficult to learn.
- Accuracy becomes misleading.
- Special handling required.

---

# 2.1 Rare Event Data

## Definition

Rare Event Data is an extreme form of imbalanced data where the target event occurs very infrequently.

---

## Examples

### Banking

Fraud Transactions

```text
Fraud = 0.2%

Non-Fraud = 99.8%
```

---

### Healthcare

Cancer Detection

```text
Cancer Cases = 1%

Normal Cases = 99%
```

---

### Manufacturing

Machine Failure Prediction

```text
Failure = 0.5%

Normal = 99.5%
```

---

# Why Imbalanced Data is a Problem?

Suppose:

| Class | Count |
|---------|---------|
| Fraud | 100 |
| Non-Fraud | 10000 |

Total Records = 10100

---

Model Prediction:

```text
Predict EVERYTHING as Non-Fraud
```

Result:

```text
Correct Predictions = 10000
```

Accuracy:

```text
10000 / 10100

= 99%
```

---

### Problem

99% Accuracy looks amazing.

But:

```text
Fraud Detection = 0%
```

The model completely fails.

---

# Accuracy Trap

## Dataset

| Class | Count |
|---------|---------|
| Positive | 50 |
| Negative | 950 |

---

Model predicts:

```text
Everything = Negative
```

---

Confusion Matrix

| Actual / Predicted | Positive | Negative |
|-------------------|-----------|-----------|
| Positive | 0 | 50 |
| Negative | 0 | 950 |

Accuracy:

```text
950 / 1000

= 95%
```

Yet the model is useless.

---

# Metrics for Imbalanced Data

Instead of Accuracy, use:

## Precision

Measures prediction quality.

```text
Among predicted positives,
how many are actually positive?
```

---

## Recall

Measures detection ability.

```text
Among actual positives,
how many were detected?
```

---

## F1 Score

Balance between Precision and Recall.

---

## ROC-AUC

Measures overall classification capability.

---

## PR-AUC

Often preferred for highly imbalanced datasets.

---

# Methods to Handle Imbalanced Data

# 1. Oversampling

Increase minority class records.

---

Original Data

| Fraud | Non-Fraud |
|---------|---------|
| 100 | 10000 |

---

After Oversampling

| Fraud | Non-Fraud |
|---------|---------|
| 10000 | 10000 |

---

### Advantages

- Preserves information.
- Easy implementation.

### Disadvantages

- Risk of overfitting.

---

# 2. Undersampling

Reduce majority class records.

---

Original Data

| Fraud | Non-Fraud |
|---------|---------|
| 100 | 10000 |

---

After Undersampling

| Fraud | Non-Fraud |
|---------|---------|
| 100 | 100 |

---

### Advantages

- Faster training.

### Disadvantages

- Loss of information.

---

# 3. SMOTE

## Synthetic Minority Oversampling Technique

Generates synthetic minority samples instead of duplicating existing records.

---

Example

Original Fraud Samples

```text
100
```

SMOTE Creates

```text
100 → 5000
```

using synthetic records.

---

### Advantages

- Reduces overfitting.
- Widely used.

### Interview Point

SMOTE is one of the most commonly asked interview topics in Machine Learning.

---

# 4. Class Weights

Assign higher penalty to minority class errors.

Example:

```python
class_weight='balanced'
```

in Scikit-Learn.

---

# 5. Ensemble Methods

Examples:

- Random Forest
- XGBoost
- LightGBM
- Balanced Random Forest

Often perform better on imbalanced datasets.

---

# Real-World Applications

## Fraud Detection

```text
Fraud = Minority
```

---

## Medical Diagnosis

```text
Disease = Minority
```

---

## Cyber Security

```text
Attack = Minority
```

---

## Credit Risk

```text
Default = Minority
```

---

## Predictive Maintenance

```text
Machine Failure = Minority
```

---

# Balanced vs Imbalanced Data

| Feature | Balanced | Imbalanced |
|----------|----------|------------|
| Class Distribution | Equal | Unequal |
| Accuracy Reliable | Yes | No |
| Special Treatment Needed | No | Yes |
| Real-World Occurrence | Rare | Very Common |
| Example | Employee Attrition | Fraud Detection |

---

# Interview Questions & Answers

## Q1. What is Balanced Data?

### Answer

A dataset where all target classes have approximately equal observations.

---

## Q2. What is Imbalanced Data?

### Answer

A dataset where one class significantly outnumbers another class.

---

## Q3. Why is Accuracy misleading for Imbalanced Data?

### Answer

A model can predict only the majority class and still achieve very high accuracy.

---

## Q4. What is Rare Event Data?

### Answer

A dataset where the target event occurs very infrequently.

Examples:

- Fraud
- Cancer
- Machine Failure

---

## Q5. What is SMOTE?

### Answer

Synthetic Minority Oversampling Technique used to generate synthetic minority class records.

---

## Q6. What is Oversampling?

### Answer

Increasing minority class observations to balance the dataset.

---

## Q7. What is Undersampling?

### Answer

Reducing majority class observations to balance the dataset.

---

## Q8. Which metrics should be used for Imbalanced Data?

### Answer

- Precision
- Recall
- F1 Score
- ROC-AUC
- PR-AUC

---

## Q9. Give examples of Imbalanced Data problems.

### Answer

- Fraud Detection
- Disease Prediction
- Credit Default Prediction
- Machine Failure Prediction

---

## Q10. Which is better: Accuracy or F1 Score for Imbalanced Data?

### Answer

F1 Score is generally preferred because it considers both Precision and Recall.

---

# Summary

```text
Balanced Data
│
├── Equal Class Distribution
├── Accuracy Reliable
└── Easier Training

Imbalanced Data
│
├── Unequal Class Distribution
├── Accuracy Misleading
├── Rare Events
├── SMOTE
├── Oversampling
├── Undersampling
└── Precision / Recall / F1
```

---

# Key Takeaways

- Most real-world classification problems are imbalanced.
- Accuracy alone should never be trusted on imbalanced datasets.
- Precision, Recall, and F1 Score are critical evaluation metrics.
- SMOTE is a popular technique for handling imbalanced data.
- Fraud Detection, Disease Prediction, and Credit Risk are classic imbalanced data problems.
