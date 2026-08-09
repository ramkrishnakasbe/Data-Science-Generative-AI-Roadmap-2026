# 06_Regularization_and_Normalization.md

# Regularization and Normalization

Regularization and normalization are important techniques used to make deep learning models **more stable, generalizable, and easier to train**.

```text
Regularization
→ Controls Overfitting

Normalization
→ Stabilizes and Improves Training
```

---

# 1. Overfitting

Overfitting occurs when a model learns the training data too closely but performs poorly on unseen data.

```text
Training Performance → Very Good
Validation Performance → Poor
```

Typical pattern:

```text
Loss
 ↑
 | Training Loss
 | \
 |  \
 |   \________
 |
 | Validation Loss
 |       \____
 |            \__
 |              /
 |             /
 +--------------------→ Epochs
                 ↑
             Overfitting
```

Common causes:

* Model is too complex
* Limited training data
* Too many parameters
* Noisy training data
* Insufficient regularization
* Excessive training

---

# 2. Underfitting

Underfitting occurs when the model is unable to learn the underlying patterns.

```text
Training Performance → Poor
Validation Performance → Poor
```

Possible causes:

* Model too simple
* Insufficient training
* Excessive regularization
* Poor features
* Learning rate problems

---

# 3. Bias-Variance Tradeoff

A useful way to understand model complexity:

```text
High Bias
    ↓
Underfitting

High Variance
    ↓
Overfitting
```

Conceptually:

```text
Model Complexity
       →
Bias     ↓
Variance ↑
```

The goal is to find a model with good generalization.

---

# 4. Regularization

Regularization adds constraints or penalties to discourage overly complex models.

```text
Original Objective
       +
Regularization
       ↓
Better Generalization
```

Common techniques:

```text
L1 Regularization
L2 Regularization
Dropout
Early Stopping
Data Augmentation
Weight Decay
Label Smoothing
```

---

# 5. L1 Regularization

L1 regularization adds the absolute value of weights to the objective.

```text
L_total = L_data + λΣ|w|
```

Where:

* `L_data` = original loss
* `λ` = regularization strength
* `w` = model parameters

L1 tends to encourage some weights to become exactly zero.

---

# 6. L1 Regularization Effect

Conceptually:

```text
Many Parameters
      ↓
L1 Penalty
      ↓
Some Weights → 0
```

This can produce sparse models.

Advantages:

* Encourages sparsity
* Can perform implicit feature selection
* Useful when many parameters may be unnecessary

---

# 7. L2 Regularization

L2 regularization penalizes the squared magnitude of weights.

```text
L_total = L_data + λΣw²
```

It encourages weights to remain relatively small.

```text
Large Weights
     ↓
L2 Penalty
     ↓
Smaller Weights
```

L2 is widely used in deep learning.

---

# 8. L1 vs L2

| Feature               | L1          | L2             |   |      |
| --------------------- | ----------- | -------------- | - | ---- |
| Penalty               | `           | w              | ` | `w²` |
| Sparsity              | Strong      | Usually weaker |   |      |
| Can make weights zero | Yes         | Usually no     |   |      |
| Feature Selection     | Can help    | Less direct    |   |      |
| Deep Learning Usage   | Less common | Very common    |   |      |

---

# 9. Elastic Net

Elastic Net combines L1 and L2 regularization.

```text
L_total = L_data
        + λ₁Σ|w|
        + λ₂Σw²
```

It combines:

```text
L1 → Sparsity
L2 → Weight Shrinkage
```

Elastic Net is more common in traditional machine learning than in modern deep neural networks.

---

# 10. Weight Decay

Weight decay gradually pushes parameters toward smaller values.

Conceptually:

```text
Weight
  ↓
Decay
  ↓
Smaller Weight
```

A simplified update:

```text
w_new = w_old - η × gradient - ηλw_old
```

Weight decay is closely related to L2 regularization for standard SGD, but the distinction becomes important with adaptive optimizers.

---

# 11. L2 Regularization vs Weight Decay

For standard SGD, L2 regularization and weight decay can produce equivalent updates under common formulations.

With adaptive optimizers such as Adam, directly adding an L2 penalty to the loss is not necessarily equivalent to decoupled weight decay.

This is why **AdamW** is important.

```text
Adam + L2 Penalty
        ≠
AdamW
```

in general.

---

# 12. Dropout

Dropout randomly disables a portion of neurons during training.

Example:

```text
Before Dropout:

● ● ● ● ●
 \|/|\|/
  ● ● ●


After Dropout:

● ✕ ● ✕ ●
 \ |   |
  ●   ●
```

The dropped neurons do not participate in that training step.

---

# 13. Why Dropout Works

Dropout prevents the network from relying too heavily on specific neurons.

It encourages distributed representations.

Conceptually:

```text
Without Dropout
→ Strong Dependency Between Neurons

With Dropout
→ More Robust Representations
```

---

# 14. Dropout Probability

If:

```text
p = 0.5
```

approximately 50% of the eligible activations are dropped during training.

Common values depend on the architecture.

Typical examples:

```text
0.1
0.2
0.3
0.5
```

Higher dropout is not automatically better.

---

# 15. Training vs Inference with Dropout

Dropout is normally active during training:

```text
Training
→ Dropout ON
```

During inference:

```text
Inference
→ Dropout OFF
```

Modern frameworks generally handle the corresponding scaling automatically.

PyTorch:

```python
model.train()
```

activates training behavior.

```python
model.eval()
```

switches to evaluation behavior.

---

# 16. Dropout vs L2

| Feature         | Dropout                     | L2                                 |
| --------------- | --------------------------- | ---------------------------------- |
| Main Idea       | Randomly remove activations | Penalize large weights             |
| Training Effect | Adds stochasticity          | Shrinks weights                    |
| Inference       | Disabled                    | Remains part of learned parameters |
| Common Usage    | Deep Networks               | Very common                        |

Both can be used together, but excessive regularization can cause underfitting.

---

# 17. Early Stopping

Early stopping prevents unnecessary training after validation performance stops improving.

```text
Training
   ↓
Validation Improves
   ↓
Validation Plateaus
   ↓
Validation Worsens
   ↓
Stop
```

The best model checkpoint is often restored.

---

# 18. Data Augmentation

Data augmentation creates modified versions of existing training examples.

For images:

```text
Original Image
     ↓
Rotation
Flip
Crop
Resize
Color Modification
     ↓
Additional Training Examples
```

For text:

```text
Synonym Replacement
Back Translation
Paraphrasing
Token-Level Augmentation
```

For audio:

```text
Time Shifting
Noise Injection
Pitch Modification
Time Stretching
```

Augmentation can improve generalization without collecting entirely new data.

---

# 19. Label Smoothing

Instead of using completely hard labels:

```text
Cat = 1
Dog = 0
```

label smoothing assigns slightly softer targets.

For example:

```text
Cat = 0.9
Dog = 0.1
```

The exact values depend on the smoothing configuration.

Benefits can include:

* Reduced overconfidence
* Better generalization
* More stable classification

---

# 20. Normalization

Normalization techniques transform activations or inputs into a more suitable numerical range or distribution.

Main techniques used in deep learning:

```text
Batch Normalization
Layer Normalization
Instance Normalization
Group Normalization
RMSNorm
```

---

# 21. Why Normalization Helps

Deep neural networks can become difficult to optimize when activation distributions or scales vary significantly.

Normalization can help:

```text
Stable Activations
      ↓
More Stable Gradients
      ↓
Easier Optimization
```

Normalization is not simply about forcing every value into `[0, 1]`.

---

# 22. Batch Normalization

Batch Normalization normalizes activations using statistics calculated from a mini-batch.

For an activation `x`:

```text
μ_B = Batch Mean
σ²_B = Batch Variance
```

Normalize:

```text
x̂ = (x - μ_B) / √(σ²_B + ε)
```

Then learnable parameters are applied:

```text
y = γx̂ + β
```

Where:

* `γ` = learnable scale
* `β` = learnable shift

---

# 23. Batch Normalization Intuition

```text
Raw Activations
      ↓
Calculate Batch Statistics
      ↓
Normalize
      ↓
Scale + Shift
      ↓
Next Layer
```

The model still controls the final distribution through `γ` and `β`.

---

# 24. Batch Normalization During Training

During training, BatchNorm uses statistics from the current mini-batch.

```text
Training
→ Current Batch Mean/Variance
```

It also maintains running statistics for inference.

---

# 25. Batch Normalization During Inference

During inference, the model normally uses stored running statistics rather than statistics from the current batch.

```text
Training
→ Batch Statistics

Inference
→ Running Statistics
```

This is one reason `train()` and `eval()` modes matter in frameworks such as PyTorch.

---

# 26. BatchNorm Advantages

* Can stabilize training
* Often allows larger learning rates
* Can improve optimization
* Can provide some regularization effect
* Very effective in many CNN architectures

---

# 27. BatchNorm Limitations

BatchNorm can become problematic when:

* Batch size is very small
* Batch statistics are noisy
* Data distribution varies significantly
* Architecture is not well suited to batch-based statistics

This is one reason alternative normalization methods are important.

---

# 28. Layer Normalization

Layer Normalization normalizes across features within an individual sample.

Conceptually:

```text
Sample
 ↓
Features
 ↓
Calculate Mean/Variance Across Features
 ↓
Normalize
```

Unlike BatchNorm:

```text
BatchNorm
→ Depends on Batch Statistics

LayerNorm
→ Operates Independently Per Sample
```

---

# 29. LayerNorm Formula

For features in a layer:

```text
μ = Mean(features)
```

```text
σ² = Variance(features)
```

Normalize:

```text
x̂ = (x - μ) / √(σ² + ε)
```

Then:

```text
y = γx̂ + β
```

---

# 30. Why LayerNorm Is Important

LayerNorm is widely used in:

```text
Transformers
LLMs
RNN-related architectures
```

It is particularly useful when batch-dependent statistics are undesirable.

---

# 31. BatchNorm vs LayerNorm

| Feature              | BatchNorm                       | LayerNorm          |
| -------------------- | ------------------------------- | ------------------ |
| Statistics           | Across batch-related dimensions | Within each sample |
| Depends on Batch     | Yes                             | No                 |
| Small Batch Friendly | Less reliable                   | Better             |
| Transformers         | Less common                     | Very common        |
| CNNs                 | Very common                     | Less dominant      |

---

# 32. Instance Normalization

Instance Normalization normalizes each individual sample and channel separately.

It is particularly associated with:

```text
Image Generation
Style Transfer
Computer Vision
```

Conceptually:

```text
Image
 ↓
Each Channel
 ↓
Normalize Independently
```

---

# 33. Group Normalization

Group Normalization divides channels into groups and normalizes within each group.

```text
Channels
 ↓
Group 1
Group 2
Group 3
...
 ↓
Normalize Each Group
```

It can work well with small batch sizes.

---

# 34. GroupNorm vs BatchNorm

| Feature          | BatchNorm          | GroupNorm           |
| ---------------- | ------------------ | ------------------- |
| Batch Dependency | Yes                | No                  |
| Small Batch      | Can be problematic | Works well          |
| CNNs             | Very common        | Useful alternative  |
| Statistics       | Batch-based        | Group/channel-based |

---

# 35. RMSNorm

RMSNorm simplifies LayerNorm by using the root mean square rather than explicitly centering activations around their mean.

RMS value:

```text
RMS(x) = √(1/n Σx_i² + ε)
```

Normalization:

```text
x̂_i = x_i / RMS(x)
```

Then a learnable scale can be applied.

RMSNorm is widely relevant in modern Transformer architectures.

---

# 36. LayerNorm vs RMSNorm

| Feature                  | LayerNorm | RMSNorm              |
| ------------------------ | --------- | -------------------- |
| Mean Subtraction         | Yes       | No                   |
| Variance Calculation     | Yes       | No explicit variance |
| RMS Scaling              | No        | Yes                  |
| Computational Complexity | Higher    | Simpler              |
| Modern LLM Usage         | Common    | Very common          |

---

# 37. Normalization vs Standardization

These terms are sometimes used loosely, but they are not always identical.

### Standardization

Usually refers to:

```text
z = (x - μ) / σ
```

giving approximately:

```text
Mean ≈ 0
Std ≈ 1
```

### Normalization

Can refer broadly to transforming data or activations into a controlled scale or distribution.

Always clarify the specific technique being discussed.

---

# 38. Input Normalization

Input features should often be scaled appropriately before training.

For standardization:

```text
x_scaled = (x - μ) / σ
```

For min-max scaling:

```text
x_scaled = (x - x_min) / (x_max - x_min)
```

For image models, inputs are often normalized according to the preprocessing expected by the model.

---

# 39. Data Normalization vs BatchNorm

These are different concepts.

```text
Data Normalization
→ Applied to Input Data

BatchNorm
→ Applied to Internal Activations
```

Example:

```text
Raw Data
 ↓
Input Preprocessing
 ↓
Neural Network
 ↓
BatchNorm
 ↓
Activation
```

---

# 40. Pre-Norm vs Post-Norm

Important for Transformer architectures.

### Post-Norm

Conceptually:

```text
x
 ↓
Attention
 ↓
Residual
 ↓
LayerNorm
```

### Pre-Norm

Conceptually:

```text
x
 ↓
LayerNorm
 ↓
Attention
 ↓
Residual
```

Modern Transformer architectures commonly use Pre-LN or related normalization designs because they can improve optimization stability in deep networks.

---

# 41. Regularization vs Normalization

| Aspect             | Regularization         | Normalization                  |
| ------------------ | ---------------------- | ------------------------------ |
| Main Goal          | Improve Generalization | Stabilize Training             |
| Overfitting        | Directly targets it    | May indirectly help            |
| Examples           | Dropout, L1, L2        | BatchNorm, LayerNorm           |
| Parameter Control  | Often yes              | Usually transforms activations |
| Training Stability | Can help               | Major objective                |

They solve different problems but can be used together.

---

# 42. Regularization Stack

A practical deep learning model may use:

```text
Data Augmentation
       ↓
Weight Decay
       ↓
Dropout
       ↓
Early Stopping
```

Not every model needs every technique.

Too much regularization can cause:

```text
Underfitting
```

---

# 43. Normalization Stack

Depending on architecture:

```text
CNN
→ BatchNorm / GroupNorm

Transformer
→ LayerNorm / RMSNorm

Small-Batch Vision
→ GroupNorm

Style Transfer
→ InstanceNorm
```

Architecture determines the appropriate choice.

---

# 44. PyTorch Examples

### Dropout

```python
import torch.nn as nn

dropout = nn.Dropout(p=0.2)
```

### BatchNorm

```python
batch_norm = nn.BatchNorm1d(num_features=128)
```

### LayerNorm

```python
layer_norm = nn.LayerNorm(128)
```

### GroupNorm

```python
group_norm = nn.GroupNorm(
    num_groups=8,
    num_channels=128
)
```

---

# 45. Choosing Regularization

If the model is overfitting:

```text
Check:
    ↓
Data Augmentation
    ↓
Weight Decay
    ↓
Dropout
    ↓
Early Stopping
    ↓
Model Complexity
```

Do not blindly increase dropout.

---

# 46. Choosing Normalization

### CNN

Start by considering:

```text
BatchNorm
```

If batch sizes are very small:

```text
GroupNorm
```

may be preferable.

### Transformer

Usually consider:

```text
LayerNorm
RMSNorm
```

### Style Transfer

Commonly:

```text
InstanceNorm
```

---

# 47. Common Mistakes

### Mistake 1

> Dropout is used during inference.

Incorrect.

```text
Training → Dropout ON
Inference → Dropout OFF
```

---

### Mistake 2

> BatchNorm and LayerNorm work on exactly the same dimensions.

Incorrect.

Their normalization axes and dependence on batch statistics differ.

---

### Mistake 3

> Normalization always prevents overfitting.

Incorrect.

Normalization primarily helps optimization and training stability.

---

### Mistake 4

> More regularization is always better.

Incorrect.

Excessive regularization can cause underfitting.

---

### Mistake 5

> L2 regularization and AdamW are always identical.

Incorrect.

Decoupled weight decay in AdamW differs from simply adding an L2 penalty to the Adam loss.

---

# 48. Interview Questions

## Fundamentals

1. What is overfitting?
2. What is underfitting?
3. What is regularization?
4. Why is regularization required?
5. What is the bias-variance tradeoff?

## Regularization

6. Explain L1 regularization.
7. Explain L2 regularization.
8. L1 vs L2?
9. What is Elastic Net?
10. What is dropout?
11. Why does dropout reduce overfitting?
12. Why is dropout disabled during inference?
13. What is weight decay?
14. L2 regularization vs weight decay?
15. What is AdamW?
16. What is early stopping?
17. What is label smoothing?
18. What is data augmentation?

## Normalization

19. What is normalization?
20. Why is normalization useful?
21. Explain BatchNorm.
22. How does BatchNorm behave during training and inference?
23. Explain LayerNorm.
24. BatchNorm vs LayerNorm?
25. What is InstanceNorm?
26. What is GroupNorm?
27. What is RMSNorm?
28. LayerNorm vs RMSNorm?
29. Why is LayerNorm common in Transformers?
30. Why can BatchNorm struggle with very small batches?

---

# 49. Scenario-Based Questions

### Q1. Training accuracy is 99% but validation accuracy is 82%. What would you do?

Possible approaches:

```text
Check Data Leakage
        ↓
Data Augmentation
        ↓
Weight Decay
        ↓
Dropout
        ↓
Early Stopping
        ↓
Reduce Model Complexity
```

---

### Q2. Batch size is extremely small. Would you automatically choose BatchNorm?

No.

Consider:

```text
GroupNorm
LayerNorm
```

depending on the architecture.

---

### Q3. Your CNN is overfitting.

Potential approach:

```text
Data Augmentation
+
Weight Decay
+
Dropout if appropriate
+
Early Stopping
```

---

### Q4. Your Transformer becomes difficult to train as depth increases.

Investigate:

```text
Normalization Strategy
Learning Rate
Warmup
Initialization
Gradient Stability
Residual Connections
```

Pre-normalization architectures are often easier to optimize for deep Transformers.

---

### Q5. Validation performance becomes worse after adding heavy dropout.

Possible explanation:

```text
Too Much Regularization
        ↓
Underfitting
```

Reduce dropout or reconsider the overall regularization strength.

---

# 50. Quick Revision

```text
Overfitting
→ Model memorizes training patterns too closely

L1
→ Encourages sparse weights

L2
→ Penalizes large weights

Weight Decay
→ Shrinks weights during optimization

Dropout
→ Randomly removes activations during training

Early Stopping
→ Stops when validation performance stops improving

BatchNorm
→ Normalizes using batch-related statistics

LayerNorm
→ Normalizes features within each sample

InstanceNorm
→ Normalizes individual instances/channels

GroupNorm
→ Normalizes groups of channels

RMSNorm
→ RMS-based normalization without mean subtraction

AdamW
→ Adam with decoupled weight decay
```

---

# 51. Interview Mental Model

```text
                    MODEL TRAINING
                         │
          ┌──────────────┴──────────────┐
          ↓                             ↓
   GENERALIZATION                 TRAINING STABILITY
          │                             │
          ↓                             ↓
   Regularization                  Normalization
          │                             │
   ┌──────┼──────┐              ┌───────┼────────┐
   ↓      ↓      ↓              ↓       ↓        ↓
  L1     L2    Dropout       BatchNorm LayerNorm RMSNorm
   │      │      │              │       │        │
   └──────┴──────┘              └───────┴────────┘
          │
          ↓
    Better Generalization
```

The key distinction:

```text
Regularization
→ "Prevent the model from memorizing too much."

Normalization
→ "Make the learning process more stable and manageable."
```
