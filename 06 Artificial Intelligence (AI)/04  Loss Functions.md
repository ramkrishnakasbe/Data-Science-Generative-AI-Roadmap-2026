# 4. Loss Functions

## 1. What is a Loss Function?

A **loss function** measures how different the model's prediction is from the actual target.

```text
Input
  ↓
Neural Network
  ↓
Prediction (ŷ)
  ↓
Loss Function ← Actual Target (y)
  ↓
Loss
```

The objective of training is to minimize the loss.

```text
Lower Loss → Better Fit to Training Data
```

---

# 2. Loss Function vs Cost Function vs Objective Function

These terms are often used interchangeably, but they can have slightly different meanings.

### Loss Function

Measures error for an individual sample.

```text
L(y, ŷ)
```

### Cost Function

Usually represents average loss over the dataset or batch.

```text
J = (1/n) Σ L(yᵢ, ŷᵢ)
```

### Objective Function

The quantity being optimized. It may include regularization.

```text
Objective = Data Loss + Regularization
```

---

# 3. Why Do We Need a Loss Function?

A neural network needs a numerical signal indicating how good or bad its predictions are.

Example:

```text
Actual = 100
Prediction = 90
```

The loss function converts the error into a number.

```text
Loss = Error Measure
```

The optimizer then tries to minimize this value.

---

# 4. Complete Training Flow

```text
Training Data
      ↓
Forward Propagation
      ↓
Prediction
      ↓
Loss Function
      ↓
Loss
      ↓
Backpropagation
      ↓
Gradients
      ↓
Optimizer
      ↓
Weight Update
      ↓
Repeat
```

---

# 5. Loss Function Categories

```text
Loss Functions
│
├── Regression
│   ├── MSE
│   ├── MAE
│   ├── RMSE
│   └── Huber Loss
│
├── Classification
│   ├── Binary Cross Entropy
│   ├── Categorical Cross Entropy
│   ├── Sparse Categorical Cross Entropy
│   └── Hinge Loss
│
├── Imbalanced Classification
│   └── Focal Loss
│
└── Specialized
    ├── KL Divergence
    ├── Contrastive Loss
    └── Triplet Loss
```

---

# 6. Regression Loss Functions

Regression predicts continuous values.

Examples:

```text
House Price
Sales
Temperature
Demand
Revenue
```

Common losses:

```text
MSE
MAE
RMSE
Huber Loss
```

---

# 7. Mean Squared Error — MSE

MSE measures the average squared difference between actual and predicted values.

Formula:

```text
MSE = (1/n) Σᵢ (yᵢ - ŷᵢ)²
```

Where:

* `y` = actual value
* `ŷ` = predicted value
* `n` = number of observations

---

# 8. MSE Example

Actual:

```text
[10, 20, 30]
```

Predicted:

```text
[12, 18, 33]
```

Errors:

```text
[-2, 2, -3]
```

Squared errors:

```text
[4, 4, 9]
```

MSE:

```text
MSE = (4 + 4 + 9) / 3
```

```text
MSE = 17 / 3
```

```text
MSE ≈ 5.67
```

---

# 9. Properties of MSE

MSE:

* Is always non-negative
* Penalizes large errors strongly
* Is differentiable
* Is sensitive to outliers

Because the error is squared:

```text
Error = 2
Squared Error = 4
```

```text
Error = 10
Squared Error = 100
```

Therefore, large errors receive disproportionately high penalties.

---

# 10. MSE Derivative

For a single prediction:

```text
L = (y - ŷ)²
```

Derivative with respect to prediction:

```text
∂L/∂ŷ = 2(ŷ - y)
```

This gradient is used during backpropagation.

---

# 11. Advantages of MSE

* Simple
* Differentiable
* Strongly penalizes large errors
* Common for regression
* Works well with gradient-based optimization

---

# 12. Disadvantages of MSE

* Sensitive to outliers
* Squared units make interpretation less intuitive

Example:

```text
Target Unit = Rupees
MSE Unit = Rupees²
```

---

# 13. Mean Absolute Error — MAE

MAE measures the average absolute error.

Formula:

```text
MAE = (1/n) Σᵢ |yᵢ - ŷᵢ|
```

---

# 14. MAE Example

Actual:

```text
[10, 20, 30]
```

Predicted:

```text
[12, 18, 33]
```

Absolute errors:

```text
[2, 2, 3]
```

MAE:

```text
MAE = (2 + 2 + 3) / 3
```

```text
MAE = 7 / 3
```

```text
MAE ≈ 2.33
```

---

# 15. MSE vs MAE

| Feature             | MSE            | MAE                        |
| ------------------- | -------------- | -------------------------- |
| Error               | Squared        | Absolute                   |
| Outlier Sensitivity | High           | Lower                      |
| Differentiability   | Smooth         | Not differentiable at zero |
| Large Errors        | Strong penalty | Linear penalty             |
| Units               | Squared units  | Original units             |

---

# 16. Why MAE Is More Robust to Outliers

Suppose errors are:

```text
[1, 2, 3, 20]
```

MAE:

```text
MAE = 26 / 4 = 6.5
```

MSE:

```text
MSE = (1 + 4 + 9 + 400) / 4
```

```text
MSE = 103.5
```

The large error has a much stronger effect on MSE.

---

# 17. RMSE

RMSE stands for:

**Root Mean Squared Error**

Formula:

```text
RMSE = √[(1/n) Σᵢ (yᵢ - ŷᵢ)²]
```

It is simply the square root of MSE.

---

# 18. Why Use RMSE?

RMSE has the same units as the target.

If:

```text
Target = Sales Units
```

then:

```text
RMSE = Sales Units
```

This makes interpretation easier than MSE.

---

# 19. MSE vs RMSE

```text
MSE
 ↓
Square Root
 ↓
RMSE
```

MSE is often convenient as an optimization loss.

RMSE is frequently useful as an evaluation metric.

---

# 20. Huber Loss

Huber Loss combines properties of MSE and MAE.

For error:

```text
e = y - ŷ
```

Huber Loss:

```text
Lδ(e) =
    1/2 e²                 if |e| ≤ δ
    δ(|e| - 1/2δ)          if |e| > δ
```

Where `δ` controls the transition between quadratic and linear behavior.

---

# 21. Huber Loss Behavior

For small errors:

```text
Huber ≈ MSE
```

For large errors:

```text
Huber ≈ MAE
```

Conceptually:

```text
Small Error
    ↓
Quadratic Penalty

Large Error
    ↓
Linear Penalty
```

---

# 22. Why Huber Loss Is Useful

Huber Loss is useful when:

```text
Need Smooth Optimization
        +
Some Robustness to Outliers
```

It is less sensitive to extreme errors than MSE while remaining differentiable.

---

# 23. Regression Loss Comparison

| Loss  | Outlier Sensitivity |     Smooth | Typical Use              |
| ----- | ------------------: | ---------: | ------------------------ |
| MSE   |                High |        Yes | Standard regression      |
| MAE   |                 Low | No at zero | Robust regression        |
| RMSE  |                High |        Yes | Evaluation               |
| Huber |              Medium |        Yes | Robust + stable training |

---

# 24. Classification Loss

Classification predicts classes.

Examples:

```text
Spam / Not Spam
Fraud / Not Fraud
Cat / Dog
Low / Medium / High
```

Common losses:

```text
Binary Cross Entropy
Categorical Cross Entropy
Sparse Categorical Cross Entropy
Focal Loss
Hinge Loss
```

---

# 25. Binary Cross Entropy — BCE

BCE is commonly used for binary classification.

For a single observation:

```text
L = -[y log(p) + (1-y)log(1-p)]
```

Where:

* `y` = actual class, 0 or 1
* `p` = predicted probability of class 1

---

# 26. BCE Example

Actual:

```text
y = 1
```

Prediction:

```text
p = 0.9
```

Loss:

```text
L = -log(0.9)
```

This produces a small loss.

If:

```text
p = 0.1
```

then:

```text
L = -log(0.1)
```

This produces a much larger loss.

Therefore:

```text
Correct + Confident → Small Loss
Wrong + Confident → Large Loss
```

---

# 27. Why BCE Works Well

BCE strongly penalizes confident incorrect predictions.

Example:

```text
Actual = 1
```

Prediction:

```text
0.99 → Very Small Loss
0.80 → Small Loss
0.50 → Moderate Loss
0.10 → Large Loss
0.01 → Very Large Loss
```

---

# 28. Binary Classification Architecture

Typical neural network:

```text
Input
 ↓
Dense
 ↓
ReLU / GELU
 ↓
Dense
 ↓
Sigmoid
 ↓
Probability
 ↓
Binary Cross Entropy
```

---

# 29. BCE and Sigmoid

Common combination:

```text
Output Activation → Sigmoid
Loss → Binary Cross Entropy
```

Conceptually:

```text
Logit
 ↓
Sigmoid
 ↓
Probability
 ↓
BCE
```

In practical frameworks, a combined **BCE-with-logits** loss is often preferred because it is numerically more stable.

---

# 30. BCE with Logits

Instead of explicitly performing:

```text
Logit
 ↓
Sigmoid
 ↓
BCE
```

a framework can directly use:

```text
Binary Cross Entropy with Logits
```

The sigmoid operation is incorporated into the loss calculation.

Advantages:

* Better numerical stability
* Avoids some overflow/underflow issues
* Common practical implementation

---

# 31. Multi-Class Classification

Suppose there are three mutually exclusive classes:

```text
Cat
Dog
Horse
```

Output:

```text
[0.7, 0.2, 0.1]
```

The probabilities sum to:

```text
1.0
```

Softmax is commonly used to produce this distribution.

---

# 32. Categorical Cross Entropy

Categorical Cross Entropy is used when the target is represented as a one-hot vector.

Formula:

```text
L = -Σᵢ yᵢ log(pᵢ)
```

Example target:

```text
[1, 0, 0]
```

Prediction:

```text
[0.7, 0.2, 0.1]
```

Loss:

```text
L = -log(0.7)
```

---

# 33. Sparse Categorical Cross Entropy

Sparse Categorical Cross Entropy is used when the target is represented by a class index rather than a one-hot vector.

Example:

```text
Class 0
```

instead of:

```text
[1, 0, 0]
```

Both can represent the same class.

---

# 34. Categorical vs Sparse Categorical Cross Entropy

| Feature           | Categorical CE | Sparse Categorical CE |
| ----------------- | -------------- | --------------------- |
| Target            | One-hot        | Integer class label   |
| Example           | `[0,1,0]`      | `1`                   |
| Number of Classes | Known          | Known                 |
| Typical Use       | One-hot labels | Integer labels        |

---

# 35. Multi-Class Architecture

```text
Input
 ↓
Dense
 ↓
ReLU / GELU
 ↓
Dense
 ↓
Softmax
 ↓
Class Probabilities
 ↓
Cross Entropy
```

---

# 36. Cross Entropy Intuition

Cross entropy measures how well predicted probabilities match the actual class distribution.

For a one-hot target:

```text
Actual:
[1, 0, 0]
```

Good prediction:

```text
[0.95, 0.03, 0.02]
```

Low loss.

Bad prediction:

```text
[0.05, 0.90, 0.05]
```

High loss.

---

# 37. Why Cross Entropy Instead of MSE for Classification?

MSE can be used in some classification settings, but cross entropy is usually preferred.

Reasons:

* Better probabilistic interpretation
* Stronger gradients for incorrect confident predictions
* Well matched to classification likelihood
* Works naturally with sigmoid/softmax outputs
* Commonly provides better optimization behavior

---

# 38. Negative Log-Likelihood

Cross entropy is closely related to **Negative Log-Likelihood (NLL)**.

For a correct class probability:

```text
p = probability assigned to true class
```

NLL:

```text
L = -log(p)
```

Therefore:

```text
High probability for true class
        ↓
Low Loss
```

```text
Low probability for true class
        ↓
High Loss
```

---

# 39. Maximum Likelihood Connection

Classification with cross entropy can be understood through maximum likelihood.

Goal:

```text
Maximize Likelihood
```

Equivalent optimization:

```text
Minimize Negative Log-Likelihood
```

Therefore:

```text
Maximum Likelihood
        ↓
Negative Log
        ↓
Cross Entropy Loss
```

This is an important interview concept.

---

# 40. Focal Loss

Focal Loss is designed to address class imbalance and focus training more strongly on difficult examples.

Binary form:

```text
FL(pₜ) = -αₜ(1-pₜ)^γ log(pₜ)
```

Where:

* `pₜ` = probability assigned to the true class
* `αₜ` = class weighting factor
* `γ` = focusing parameter

---

# 41. Focal Loss Intuition

For an easy example:

```text
pₜ ≈ 1
```

Then:

```text
(1-pₜ)^γ ≈ 0
```

So its contribution is reduced.

For a difficult example:

```text
pₜ = low
```

Its contribution remains larger.

Therefore:

```text
Focal Loss
      ↓
Down-weight Easy Examples
      ↓
Focus on Hard Examples
```

---

# 42. Focal Loss Applications

Commonly associated with:

```text
Object Detection
Highly Imbalanced Classification
Rare-Event Detection
```

---

# 43. Class Weighted Loss

Another approach to class imbalance is assigning different weights to classes.

Example:

```text
Class 0 → Weight = 1
Class 1 → Weight = 5
```

Misclassifying the minority class contributes more to the loss.

---

# 44. Focal Loss vs Class Weighting

| Feature                  | Class Weighting | Focal Loss |
| ------------------------ | --------------- | ---------- |
| Handles Class Imbalance  | Yes             | Yes        |
| Focuses on Hard Examples | Limited         | Yes        |
| Easy Example Reduction   | No              | Yes        |
| Complexity               | Lower           | Higher     |

---

# 45. Hinge Loss

Hinge Loss is associated with Support Vector Machines and margin-based classification.

For binary labels `y ∈ {-1, +1}`:

```text
L = max(0, 1 - yŷ)
```

It encourages predictions to have a margin from the decision boundary.

Hinge loss is less common than cross entropy for modern neural-network classifiers.

---

# 46. KL Divergence

KL Divergence measures how one probability distribution differs from another.

Formula:

```text
D_KL(P || Q) = Σᵢ P(i) log(P(i) / Q(i))
```

Where:

* `P` = reference distribution
* `Q` = predicted/approximating distribution

---

# 47. KL Divergence Properties

Important:

```text
D_KL(P || Q) ≥ 0
```

under standard assumptions.

However:

```text
D_KL(P || Q) ≠ D_KL(Q || P)
```

Therefore, KL Divergence is **not symmetric**.

---

# 48. KL Divergence Applications

Used in:

* Variational Autoencoders
* Knowledge Distillation
* Distribution Matching
* Probabilistic Modeling

---

# 49. Contrastive Loss

Contrastive Loss is used to learn useful representations by comparing pairs.

Goal:

```text
Similar Pair
    ↓
Bring Embeddings Closer

Dissimilar Pair
    ↓
Push Embeddings Apart
```

Common applications:

* Face recognition
* Similarity learning
* Representation learning

---

# 50. Triplet Loss

Triplet Loss uses:

```text
Anchor
Positive
Negative
```

Goal:

```text
Distance(Anchor, Positive)
<
Distance(Anchor, Negative)
```

with a margin.

A common formulation:

```text
L = max(0, d(a,p) - d(a,n) + α)
```

Where:

* `a` = anchor
* `p` = positive
* `n` = negative
* `α` = margin

---

# 51. Contrastive vs Triplet Loss

| Feature               | Contrastive         | Triplet                      |
| --------------------- | ------------------- | ---------------------------- |
| Input                 | Pair                | Triplet                      |
| Positive Relationship | Yes                 | Yes                          |
| Negative Relationship | Yes                 | Yes                          |
| Main Goal             | Similarity learning | Relative ranking             |
| Example               | Similar / Different | Anchor / Positive / Negative |

---

# 52. Loss Function and Output Activation

A very important interview relationship:

| Problem                         | Output Activation | Typical Loss                     |
| ------------------------------- | ----------------- | -------------------------------- |
| Regression                      | Linear            | MSE / MAE / Huber                |
| Binary Classification           | Sigmoid           | Binary Cross Entropy             |
| Multi-Class                     | Softmax           | Categorical Cross Entropy        |
| Multi-Class with integer labels | Softmax           | Sparse Categorical Cross Entropy |
| Multi-Label                     | Sigmoid           | Binary Cross Entropy             |
| Imbalanced Detection            | Sigmoid/Softmax   | Focal Loss                       |

---

# 53. Multi-Label Classification

Suppose an image can contain:

```text
Cat = 1
Dog = 1
Car = 0
```

Output:

```text
[0.90, 0.80, 0.10]
```

Use:

```text
Sigmoid
+
Binary Cross Entropy
```

Do not use softmax because classes are not mutually exclusive.

---

# 54. Multi-Class vs Multi-Label

### Multi-Class

Exactly one class is correct.

```text
Cat OR Dog OR Horse
```

Use:

```text
Softmax + Cross Entropy
```

### Multi-Label

Multiple classes can be correct.

```text
Cat AND Dog
```

Use:

```text
Sigmoid + Binary Cross Entropy
```

This distinction is frequently asked in interviews.

---

# 55. Loss Landscape

The loss function creates a landscape over model parameters.

```text
Loss
 ↑
 |        /\
 |       /  \
 |   ___/    \____
 |__/              \__
 +------------------------→ Parameters
```

Training attempts to move toward regions of lower loss.

Gradient-based optimizers use the local gradient to determine update direction.

---

# 56. Convex vs Non-Convex Loss

Many deep neural networks produce highly non-convex optimization problems.

```text
Convex
   ↓
One Global Minimum Structure
```

Deep neural networks:

```text
Non-Convex
   ↓
Complex Optimization Landscape
```

Possible features:

* Local minima
* Saddle points
* Flat regions
* Steep regions

Modern optimizers are designed to navigate these landscapes effectively.

---

# 57. Loss vs Evaluation Metric

Loss function and evaluation metric do not have to be the same.

Example:

```text
Training Loss → Binary Cross Entropy
Evaluation → Precision, Recall, F1, ROC-AUC
```

For regression:

```text
Training Loss → MSE
Evaluation → MAE / RMSE / MAPE
```

The loss is chosen primarily to enable effective learning; metrics are selected to measure business/task performance.

---

# 58. Loss Function and Business Objective

The mathematically convenient loss may not perfectly represent the business objective.

Example:

Fraud detection:

```text
False Negative
    ↓
Very Expensive
```

You may use:

```text
Weighted Loss
```

or another strategy to give greater importance to minority/fraud examples.

Therefore:

```text
Technical Objective
       ≠
Always Business Objective
```

---

# 59. Regularization in Objective Function

Regularization can be added to the loss.

### L2 Regularization

```text
Objective = Loss + λΣw²
```

### L1 Regularization

```text
Objective = Loss + λΣ|w|
```

Where:

```text
λ = Regularization Strength
```

The optimizer minimizes the complete objective.

---

# 60. Loss Function and Outliers

If the dataset contains significant outliers:

```text
MSE
 ↓
Strong Outlier Influence
```

Possible alternatives:

```text
MAE
Huber Loss
```

Decision:

```text
Need Strong Penalty for Large Errors?
        ↓
       MSE

Need Robustness?
        ↓
       MAE

Need Both Smoothness + Robustness?
        ↓
       Huber
```

---

# 61. Loss Function Selection Strategy

```text
What is the Problem?
        │
 ┌──────┴─────────┐
 ↓                ↓
Regression     Classification
 ↓                ↓
MSE/MAE/Huber   What type?
                 │
          ┌──────┴──────────┐
          ↓                 ↓
       Binary          Multi-Class
          ↓                 ↓
        BCE           Cross Entropy
```

For imbalanced classification:

```text
Class Weighting
or
Focal Loss
```

may be considered.

---

# 62. Practical PyTorch Examples

### MSE

```python
import torch.nn as nn

loss_fn = nn.MSELoss()
```

### MAE

```python
loss_fn = nn.L1Loss()
```

### Huber

```python
loss_fn = nn.HuberLoss()
```

### Binary Cross Entropy with Logits

```python
loss_fn = nn.BCEWithLogitsLoss()
```

### Multi-Class Cross Entropy

```python
loss_fn = nn.CrossEntropyLoss()
```

Important:

For `CrossEntropyLoss`, raw logits are normally passed directly. Do not apply softmax manually before the loss.

---

# 63. Common PyTorch Mistake

Incorrect:

```python
logits = model(x)
probs = torch.softmax(logits, dim=1)
loss = nn.CrossEntropyLoss()(probs, y)
```

Preferred:

```python
logits = model(x)
loss = nn.CrossEntropyLoss()(logits, y)
```

`CrossEntropyLoss` internally combines the relevant log-softmax and negative log-likelihood operations.

---

# 64. TensorFlow/Keras Example

### Regression

```python
model.compile(
    optimizer="adam",
    loss="mse"
)
```

### Binary Classification

```python
model.compile(
    optimizer="adam",
    loss="binary_crossentropy"
)
```

### Multi-Class Classification

```python
model.compile(
    optimizer="adam",
    loss="categorical_crossentropy"
)
```

For integer class labels:

```python
loss="sparse_categorical_crossentropy"
```

---

# 65. Common Interview Questions

## Basic

1. What is a loss function?
2. Why do neural networks need a loss function?
3. Difference between loss and cost?
4. Difference between loss and evaluation metric?
5. What is an objective function?

## Regression

6. What is MSE?
7. Why does MSE penalize outliers?
8. What is MAE?
9. MSE vs MAE?
10. What is RMSE?
11. Why is RMSE easier to interpret than MSE?
12. What is Huber Loss?
13. When would you use Huber instead of MSE?

## Classification

14. What is Binary Cross Entropy?
15. Why is BCE used for binary classification?
16. What is categorical cross entropy?
17. Categorical vs sparse categorical cross entropy?
18. Why use cross entropy instead of MSE for classification?
19. What is negative log-likelihood?
20. What is the relationship between cross entropy and maximum likelihood?

## Imbalanced Data

21. What is Focal Loss?
22. Why is Focal Loss useful?
23. Class weighting vs Focal Loss?
24. How would you design a loss for highly imbalanced fraud detection?

## Advanced

25. What is KL Divergence?
26. Is KL Divergence symmetric?
27. What is Contrastive Loss?
28. What is Triplet Loss?
29. What is the purpose of a margin in Triplet Loss?
30. How does regularization modify the objective function?

---

# 66. Scenario-Based Interview Questions

### Q1. You are predicting house prices. Which loss would you choose?

Possible starting choices:

```text
MSE
MAE
Huber
```

If large errors should be heavily penalized:

```text
MSE
```

If outliers are a concern:

```text
MAE / Huber
```

---

### Q2. Fraud occurs in only 1% of transactions. Which loss strategy could you use?

Possible approaches:

```text
Class-Weighted BCE
Focal Loss
```

Also evaluate with appropriate metrics such as:

```text
Precision
Recall
F1
PR-AUC
```

Accuracy alone can be misleading.

---

### Q3. You have three mutually exclusive classes. Which loss?

```text
Softmax
+
Categorical Cross Entropy
```

or, with integer class labels:

```text
Softmax-style multiclass logits
+
Sparse Categorical Cross Entropy
```

---

### Q4. An image can contain multiple objects simultaneously. Which output/loss combination?

```text
Sigmoid
+
Binary Cross Entropy
```

because each label is treated independently.

---

### Q5. Your regression dataset contains extreme outliers. What would you try?

```text
Huber Loss
```

is a strong candidate because it behaves quadratically for small errors and linearly for large errors.

---

# 67. Most Important Loss Functions to Remember

```text
Regression
│
├── MSE
├── MAE
├── RMSE
└── Huber
```

```text
Classification
│
├── Binary Cross Entropy
├── Categorical Cross Entropy
├── Sparse Categorical Cross Entropy
└── Focal Loss
```

```text
Representation Learning
│
├── Contrastive Loss
└── Triplet Loss
```

```text
Probabilistic / Generative
│
└── KL Divergence
```

---

# 68. Quick Revision

### Regression

```text
Continuous Target
      ↓
MSE / MAE / Huber
```

### Binary Classification

```text
Sigmoid
   +
Binary Cross Entropy
```

### Multi-Class

```text
Softmax
   +
Cross Entropy
```

### Multi-Label

```text
Sigmoid
   +
Binary Cross Entropy
```

### Imbalanced Classification

```text
Weighted Loss
or
Focal Loss
```

### Similarity Learning

```text
Contrastive / Triplet Loss
```

---

# 69. Key Formulas

### MSE

```text
MSE = (1/n) Σᵢ (yᵢ - ŷᵢ)²
```

### MAE

```text
MAE = (1/n) Σᵢ |yᵢ - ŷᵢ|
```

### RMSE

```text
RMSE = √[(1/n) Σᵢ (yᵢ - ŷᵢ)²]
```

### Binary Cross Entropy

```text
L = -[y log(p) + (1-y)log(1-p)]
```

### Categorical Cross Entropy

```text
L = -Σᵢ yᵢ log(pᵢ)
```

### Huber Loss

```text
Lδ(e) =
    1/2 e²                 if |e| ≤ δ
    δ(|e| - 1/2δ)          if |e| > δ
```

### Focal Loss

```text
FL(pₜ) = -αₜ(1-pₜ)^γ log(pₜ)
```

### KL Divergence

```text
D_KL(P || Q) = Σᵢ P(i) log(P(i) / Q(i))
```

### Triplet Loss

```text
L = max(0, d(a,p) - d(a,n) + α)
```

---

# 70. Interview Mental Model

```text
                    LOSS FUNCTION
                         │
             ┌───────────┴───────────┐
             ↓                       ↓
        Regression              Classification
             │                       │
      ┌──────┼──────┐          ┌─────┴─────┐
      ↓      ↓      ↓          ↓           ↓
     MSE    MAE   Huber       Binary      Multi-Class
                               ↓             ↓
                              BCE       Cross Entropy
```

Remember the core relationship:

```text
Prediction
    ↓
Loss
    ↓
Gradient
    ↓
Backpropagation
    ↓
Optimizer
    ↓
Parameter Update
```

The most important interview skill is to explain **why a particular loss function is appropriate for a problem, how it behaves mathematically, how it handles outliers or class imbalance, and how it interacts with the output activation and optimizer**.
