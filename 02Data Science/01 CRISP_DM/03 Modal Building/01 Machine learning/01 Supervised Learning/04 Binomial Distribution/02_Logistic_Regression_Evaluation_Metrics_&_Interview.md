# 02_Logistic_Regression_Evaluation_Metrics_&_Interview.md

# Confusion Matrix

A **Confusion Matrix** summarizes the performance of a classification model.

```
                    Predicted

                Positive   Negative

Actual Positive     TP         FN

Actual Negative     FP         TN
```

| Term | Meaning |
|------|---------|
| TP | True Positive (Correct Positive Prediction) |
| TN | True Negative (Correct Negative Prediction) |
| FP | False Positive (Type I Error) |
| FN | False Negative (Type II Error) |

---

# Types of Errors

## Type I Error (False Positive)

Actual class is Negative

Model predicts Positive

Example

```
Healthy Person

↓

Predicted as Diseased
```

Higher FP reduces **Precision**.

---

## Type II Error (False Negative)

Actual class is Positive

Model predicts Negative

Example

```
Cancer Patient

↓

Predicted Healthy
```

Higher FN reduces **Recall**.

---

# Accuracy

Measures the overall percentage of correct predictions.

Formula

```
Accuracy

=

(TP + TN)

/

(TP + TN + FP + FN)
```

Range

```
0 to 1

or

0% to 100%
```

Example

```
TP = 90

TN = 80

FP = 10

FN = 20

Accuracy

=

(90+80)

/

200

=

85%
```

### Advantages

- Easy to understand
- Useful for balanced datasets

### Limitations

Not reliable for **imbalanced datasets**.

Example

```
990 Negative

10 Positive
```

Predicting everything as Negative gives

```
99% Accuracy

But

0% Recall
```

---

# Precision

**Question**

> Out of all predicted positives, how many were actually positive?

Formula

```
Precision

=

TP

/

(TP + FP)
```

High Precision means

- Low False Positives
- High prediction quality

Applications

- Spam Detection
- Search Engines
- Recommendation Systems

---

# Recall (Sensitivity / True Positive Rate)

**Question**

> Out of all actual positives, how many did the model correctly identify?

Formula

```
Recall

=

TP

/

(TP + FN)
```

High Recall means

- Low False Negatives
- More actual positives detected

Applications

- Cancer Detection
- Fraud Detection
- Disease Diagnosis

---

# Sensitivity

Sensitivity and Recall are identical.

```
Sensitivity

=

Recall

=

TP

/

(TP + FN)
```

Higher Sensitivity

↓

Better detection of positive cases.

---

# Specificity (True Negative Rate)

**Question**

> Out of all actual negatives, how many were correctly classified?

Formula

```
Specificity

=

TN

/

(TN + FP)
```

High Specificity means

- Low False Positives
- Better identification of negative cases

Applications

- Medical Testing
- Security Systems
- Quality Inspection

---

# False Positive Rate (FPR)

Formula

```
FPR

=

FP

/

(FP + TN)
```

Relationship

```
Specificity

=

1 - FPR
```

Lower FPR is preferred.

---

# False Negative Rate (FNR)

Formula

```
FNR

=

FN

/

(FN + TP)
```

Relationship

```
Recall

=

1 - FNR
```

Lower FNR is preferred.

---

# Precision vs Recall

| Precision | Recall |
|------------|--------|
| Focuses on FP | Focuses on FN |
| Prediction Quality | Positive Detection |
| Spam Detection | Medical Diagnosis |
| High Precision → Low FP | High Recall → Low FN |

---

# Precision vs Specificity

| Precision | Specificity |
|------------|-------------|
| Uses Predicted Positives | Uses Actual Negatives |
| TP/(TP+FP) | TN/(TN+FP) |
| Prediction Reliability | Negative Class Detection |

---

# Recall vs Specificity

| Recall | Specificity |
|----------|-------------|
| Detect Positive Class | Detect Negative Class |
| TP/(TP+FN) | TN/(TN+FP) |
| Reduce FN | Reduce FP |

---

# F1 Score

F1 Score balances **Precision** and **Recall**.

Formula

```
F1

=

2 × Precision × Recall

/

(Precision + Recall)
```

Properties

- Harmonic Mean
- Penalizes imbalance
- Better than Accuracy for imbalanced datasets

Range

```
0 to 1
```

Higher is better.

---

# ROC Curve

ROC

↓

Receiver Operating Characteristic Curve

Plots

```
True Positive Rate

vs

False Positive Rate
```

Axes

```
Y-axis

↓

Recall

(TPR)
```

```
X-axis

↓

False Positive Rate

(FPR)
```

Ideal ROC Curve stays close to the **Top Left Corner**.

---

# AUC

AUC

↓

Area Under ROC Curve

Measures overall classifier performance.

Range

| AUC | Interpretation |
|------|---------------|
| 1.0 | Perfect |
| 0.90–0.99 | Excellent |
| 0.80–0.89 | Good |
| 0.70–0.79 | Fair |
| 0.60–0.69 | Poor |
| 0.50 | Random Guess |

Higher AUC indicates better class separation.

---

# ROC vs AUC

| ROC | AUC |
|------|-----|
| Curve | Numerical Score |
| Visual Comparison | Single Performance Metric |
| Threshold Independent | Threshold Independent |

---

# Precision-Recall Curve

Plots

```
Precision

vs

Recall
```

Best used when

- Dataset is imbalanced
- Positive class is rare

Examples

- Fraud Detection
- Disease Detection
- Intrusion Detection

---

# ROC vs Precision-Recall Curve

| ROC Curve | PR Curve |
|------------|----------|
| Balanced Dataset | Imbalanced Dataset |
| Uses TPR & FPR | Uses Precision & Recall |
| Overall Performance | Positive Class Performance |

---

# Threshold Tuning

Default Threshold

```
0.5
```

Lower Threshold

- Higher Recall
- Lower Precision
- More Positive Predictions

Higher Threshold

- Higher Precision
- Lower Recall
- Fewer Positive Predictions

Business requirements determine the threshold.

---

# Metric Selection Guide

| Business Problem | Best Metric |
|------------------|-------------|
| Balanced Dataset | Accuracy |
| Spam Detection | Precision |
| Disease Detection | Recall |
| Cancer Detection | Recall |
| Loan Approval | Precision |
| Fraud Detection | Precision + Recall |
| Highly Imbalanced Dataset | F1 Score |
| Model Comparison | ROC-AUC |
| Rare Positive Events | Precision-Recall Curve |

---

# Important Relationships

```
Recall

=

Sensitivity

=

True Positive Rate
```

```
Specificity

=

True Negative Rate
```

```
Specificity

=

1 - FPR
```

```
Recall

=

1 - FNR
```

---

# Interview Questions

## Beginner

1. What is a Confusion Matrix?
2. Explain TP, TN, FP and FN.
3. What is Accuracy?
4. Why is Accuracy misleading for imbalanced datasets?
5. What is Precision?
6. What is Recall?
7. What is Sensitivity?
8. What is Specificity?
9. Difference between Recall and Sensitivity.
10. Difference between Precision and Accuracy.

---

## Intermediate

1. Precision vs Recall.
2. Precision vs Specificity.
3. Recall vs Specificity.
4. What is F1 Score?
5. Why is F1 Score the Harmonic Mean?
6. Explain False Positive Rate.
7. Explain False Negative Rate.
8. What is Threshold Tuning?
9. Explain ROC Curve.
10. Explain AUC.

---

## Advanced

1. Why is ROC threshold independent?
2. Why is Precision-Recall Curve preferred for imbalanced datasets?
3. When is ROC misleading?
4. Which metric would you use for fraud detection and why?
5. Which metric is more important for cancer detection?
6. How would you reduce False Positives?
7. How would you reduce False Negatives?
8. How do you select an optimal threshold?
9. What happens to Precision and Recall when the threshold changes?
10. Compare ROC-AUC with F1 Score.

---

# Quick Revision

| Metric | Formula | Best When |
|---------|---------|-----------|
| Accuracy | (TP+TN)/(TP+TN+FP+FN) | Balanced Data |
| Precision | TP/(TP+FP) | False Positives are costly |
| Recall (Sensitivity) | TP/(TP+FN) | False Negatives are costly |
| Specificity | TN/(TN+FP) | Correctly identify Negatives |
| FPR | FP/(FP+TN) | Lower is Better |
| FNR | FN/(FN+TP) | Lower is Better |
| F1 Score | 2PR/(P+R) | Imbalanced Data |
| ROC | TPR vs FPR | Model Comparison |
| AUC | Area Under ROC | Overall Classifier Performance |
| PR Curve | Precision vs Recall | Rare Positive Class |

# Interview Tip

**Remember this mapping:**

- **Precision → FP**
- **Recall/Sensitivity → FN**
- **Specificity → TN**
- **ROC → TPR vs FPR**
- **AUC → Overall ranking ability**
- **F1 Score → Balance of Precision & Recall**
- **PR Curve → Best for imbalanced datasets**
