# 05_Backpropagation_and_Optimization.md

# 1. Backpropagation and Optimization

Backpropagation and optimization are the core mechanisms that allow neural networks to **learn from errors and update their parameters**.

```text
Input
  ↓
Forward Propagation
  ↓
Prediction
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

> Neural Network learns by calculating **how much each parameter contributed to the error** and then updating those parameters to reduce the error.

---

# 2. What is Backpropagation?

**Backpropagation** is an algorithm used to calculate the gradients of the loss with respect to the neural network's parameters.

It propagates the error information **backward from the output layer toward the input layer**.

```text
Forward:

Input → Hidden 1 → Hidden 2 → Output → Loss


Backward:

Loss → Hidden 2 → Hidden 1 → Input
```

Backpropagation itself calculates gradients. The **optimizer** uses those gradients to update parameters.

---

# 3. Why Backpropagation is Needed

Consider a network with millions of parameters.

We need to know:

```text
Which parameter should change?
How much should it change?
In which direction should it change?
```

Backpropagation calculates:

```text
∂Loss / ∂Weight
```

This tells us how sensitive the loss is to a particular weight.

---

# 4. Gradient

A gradient indicates the direction of steepest increase of a function.

For a parameter `w`:

```text
∂L / ∂w
```

means:

> How much does the loss change when the parameter `w` changes?

If:

```text
∂L / ∂w > 0
```

increasing `w` tends to increase the loss locally.

If:

```text
∂L / ∂w < 0
```

increasing `w` tends to decrease the loss locally.

---

# 5. Gradient Descent

Gradient descent updates parameters in the direction opposite to the gradient.

```text
w_new = w_old - η × ∂L/∂w
```

Where:

* `w` = parameter
* `L` = loss
* `η` = learning rate

The negative sign is important because the gradient points toward increasing loss.

---

# 6. Intuition Behind Gradient Descent

Imagine standing on a mountain and trying to reach the lowest point.

```text
       ●
      /
     /
    /        ← Current Position
   /
__/________________
        ↓
     Minimum
```

The gradient tells you which direction is uphill.

Gradient descent moves in the opposite direction:

```text
Gradient Direction
       ↑
       |
       ●
       |
       ↓
Update Direction
```

---

# 7. Loss Landscape

For a neural network, the loss depends on many parameters.

Conceptually:

```text
Loss
 ↑
 |        /\        /\
 |       /  \______/  \
 |   ___/              \___
 |__/                      \__
 +------------------------------→ Parameters
```

Training attempts to find parameter values that produce low loss.

Deep learning loss landscapes are generally high-dimensional and non-convex.

---

# 8. Local Gradient

Gradient-based optimization uses local information.

At the current parameter location:

```text
Current Point
     ↓
Calculate Gradient
     ↓
Choose Update Direction
     ↓
Move Parameters
```

Then the process repeats.

---

# 9. Learning Rate

The learning rate controls how large each parameter update is.

```text
w_new = w_old - η × gradient
```

### Very Small Learning Rate

```text
Tiny Updates
     ↓
Slow Training
```

### Very Large Learning Rate

```text
Large Updates
     ↓
Overshooting
     ↓
Unstable Training
```

### Appropriate Learning Rate

```text
Controlled Updates
     ↓
Better Convergence
```

---

# 10. Batch Gradient Descent

Batch Gradient Descent calculates the gradient using the entire training dataset.

```text
Entire Dataset
      ↓
Forward Pass
      ↓
Loss
      ↓
Gradient
      ↓
Update
```

Advantages:

* Stable gradient estimate
* Deterministic for fixed conditions

Disadvantages:

* Expensive for large datasets
* Requires processing the entire dataset before each update

---

# 11. Stochastic Gradient Descent

Stochastic Gradient Descent uses one training example per update.

```text
Sample 1 → Update
Sample 2 → Update
Sample 3 → Update
...
```

Advantages:

* Frequent updates
* Can escape some poor regions due to noisy gradients
* Useful for large datasets

Disadvantages:

* Noisy updates
* Less stable convergence

---

# 12. Mini-Batch Gradient Descent

Mini-batch gradient descent uses a subset of the training data.

```text
Dataset
   ↓
Batch 1 → Update
Batch 2 → Update
Batch 3 → Update
```

This is the standard approach in most deep learning training pipelines.

---

# 13. Mini-Batch Size

Common batch sizes include:

```text
16
32
64
128
256
```

There is no universally optimal batch size.

It depends on:

* Dataset
* Model
* GPU memory
* Training stability
* Generalization
* Computational efficiency

---

# 14. Epoch vs Iteration

### Epoch

One complete pass through the training dataset.

### Iteration

One parameter update.

Example:

```text
Dataset = 10,000 samples
Batch Size = 100
```

Then:

```text
Iterations per Epoch = 10,000 / 100
                     = 100
```

If training for 20 epochs:

```text
Total Updates = 100 × 20
              = 2,000
```

---

# 15. Momentum

Standard gradient descent can move slowly when the optimization landscape has inconsistent curvature.

Momentum adds a running direction based on previous gradients.

Conceptually:

```text
Current Gradient
       +
Previous Movement
       ↓
Momentum
       ↓
Parameter Update
```

A common formulation is:

```text
v_t = βv_(t-1) + (1-β)g_t
```

Then:

```text
w_t = w_(t-1) - ηv_t
```

Where:

* `v` = velocity
* `β` = momentum coefficient
* `g` = gradient
* `η` = learning rate

---

# 16. Why Momentum Helps

Without momentum:

```text
↓ → ↓ ← ↓ → ↓
```

Updates can oscillate.

With momentum:

```text
→ → → → → → 
```

The optimizer can maintain useful movement in a consistent direction.

Momentum can:

* Accelerate progress in useful directions
* Reduce oscillation
* Improve convergence

---

# 17. AdaGrad

AdaGrad adapts the learning rate separately for each parameter.

It accumulates squared historical gradients.

Conceptually:

```text
Large Historical Gradients
        ↓
Smaller Future Updates
```

```text
Rare / Small Gradients
        ↓
Relatively Larger Updates
```

A simplified formulation:

```text
G_t = G_(t-1) + g_t²
```

Then:

```text
w_t = w_(t-1) - η / (√G_t + ε) × g_t
```

---

# 18. Limitation of AdaGrad

Because the accumulated squared gradients continually increase:

```text
G_t ↑
```

the effective learning rate can become increasingly small.

Eventually:

```text
Update Size → Very Small
```

This can cause training to slow significantly.

---

# 19. RMSProp

RMSProp addresses the continuously accumulating gradient problem of AdaGrad by using an exponentially weighted moving average.

```text
v_t = βv_(t-1) + (1-β)g_t²
```

Parameter update:

```text
w_t = w_(t-1) - η × g_t / (√v_t + ε)
```

The moving average gives more emphasis to recent gradients.

---

# 20. Adam

Adam stands for:

**Adaptive Moment Estimation**

Adam combines ideas from:

```text
Momentum
+
Adaptive Learning Rates
```

It maintains:

```text
First Moment → Mean of Gradients
Second Moment → Mean of Squared Gradients
```

---

# 21. Adam Equations

First moment:

```text
m_t = β₁m_(t-1) + (1-β₁)g_t
```

Second moment:

```text
v_t = β₂v_(t-1) + (1-β₂)g_t²
```

Bias correction:

```text
m̂_t = m_t / (1-β₁^t)
```

```text
v̂_t = v_t / (1-β₂^t)
```

Parameter update:

```text
w_t = w_(t-1) - η × m̂_t / (√v̂_t + ε)
```

---

# 22. Why Adam Is Popular

Adam is widely used because it:

* Adapts learning rates
* Uses momentum-like behavior
* Usually requires less manual tuning than basic SGD
* Works well across many deep-learning problems

However:

> Adam is not automatically better than SGD for every task.

---

# 23. Adam vs SGD

| Feature                | SGD                     | Adam                      |
| ---------------------- | ----------------------- | ------------------------- |
| Adaptive Learning Rate | No                      | Yes                       |
| Momentum               | Optional                | Built-in moment estimates |
| Memory                 | Lower                   | Higher                    |
| Convergence            | Can be slower           | Often faster initially    |
| Generalization         | Can be strong           | Often strong              |
| Tuning                 | Can require more tuning | Often easier initially    |

---

# 24. AdamW

AdamW separates weight decay from the gradient-based Adam update.

The key idea is:

```text
Adam
+
Decoupled Weight Decay
```

This can improve the behavior of regularization compared with naively adding L2 penalties to Adam.

AdamW is widely used in modern deep learning and Transformer training.

---

# 25. Weight Decay

Weight decay encourages parameters to remain smaller.

Conceptually:

```text
Large Weights
     ↓
Penalty
     ↓
Smaller Parameters
```

A simplified update can be represented as:

```text
w_t = w_(t-1) - η × update - ηλw_(t-1)
```

Where:

* `λ` = weight decay coefficient

---

# 26. Learning Rate Scheduling

A fixed learning rate may not be optimal throughout training.

Instead:

```text
Training Progress
       ↓
Learning Rate Changes
```

Common strategies:

```text
Step Decay
Exponential Decay
Cosine Annealing
One-Cycle
Warmup
Reduce on Plateau
```

---

# 27. Step Learning Rate Decay

The learning rate is reduced at predefined points.

Example:

```text
Epoch 1-10   → 0.001
Epoch 11-20  → 0.0001
Epoch 21-30  → 0.00001
```

This can allow:

```text
Early Training → Larger Steps
Later Training → Smaller Steps
```

---

# 28. Exponential Learning Rate Decay

Learning rate decreases exponentially.

Conceptually:

```text
η_t = η_0 × γ^t
```

Where:

* `η_0` = initial learning rate
* `γ` = decay factor
* `t` = training step/epoch

---

# 29. Cosine Annealing

Cosine annealing gradually changes the learning rate according to a cosine schedule.

A common formulation:

```text
η_t = η_min + 1/2(η_max - η_min)
      × [1 + cos(πt/T)]
```

Where:

* `η_max` = maximum learning rate
* `η_min` = minimum learning rate
* `T` = schedule duration

It is widely used in modern deep learning training.

---

# 30. Learning Rate Warmup

Warmup starts training with a small learning rate and gradually increases it.

```text
Learning Rate
 ↑
 |        _________
 |      /
 |    /
 |  /
 | /
 +----------------→ Training Steps
   Warmup
```

Why?

Large initial updates can destabilize training, particularly for large or sensitive models.

Warmup is commonly used in Transformer training.

---

# 31. ReduceLROnPlateau

The learning rate is reduced when a monitored metric stops improving.

Example:

```text
Validation Loss
↓ ↓ ↓ ↓ → → →
          ↓
     Plateau Detected
          ↓
Learning Rate Reduced
```

Useful when the appropriate decay timing is not known in advance.

---

# 32. Gradient Clipping

Gradient clipping limits excessive gradient magnitude.

Example:

```text
Original Gradient
      ↓
Very Large
      ↓
Clip
      ↓
Controlled Gradient
```

Two common approaches:

```text
Gradient Clipping by Value
Gradient Clipping by Norm
```

---

# 33. Gradient Clipping by Value

Each gradient component is constrained to a range.

Example:

```text
[-1, 1]
```

A gradient of:

```text
5.7
```

could become:

```text
1.0
```

---

# 34. Gradient Clipping by Norm

Instead of independently clipping each component, the overall gradient norm is limited.

Conceptually:

```text
If ||g|| > threshold:

g ← g × threshold / ||g||
```

This preserves the direction while limiting magnitude.

---

# 35. Saddle Points

In high-dimensional neural network optimization, saddle points can be important.

A saddle point has directions where the function:

```text
Increases in one direction
Decreases in another
```

Conceptually:

```text
      \     /
       \   /
        \ /
        / \
       /   \
      /     \
```

Optimization can become slow near flat regions or saddle points.

---

# 36. Local Minima

A local minimum is a point lower than nearby points.

```text
Loss
 ↑
 |       \      /
 |        \____/
 |             \____
 +----------------------→ Parameters
          Local Minimum
```

In deep networks, the optimization landscape is highly complex.

Modern optimization research generally focuses on the broader geometry of the loss landscape rather than assuming training is simply trapped in poor local minima.

---

# 37. Saddle Points vs Local Minima

| Feature            | Local Minimum        | Saddle Point                 |
| ------------------ | -------------------- | ---------------------------- |
| Nearby directions  | Mostly increase      | Some increase, some decrease |
| Gradient           | Often zero           | Often zero                   |
| Optimization issue | Can slow convergence | Can slow convergence         |

---

# 38. Gradient Noise

Mini-batch gradients are estimates of the full-data gradient.

Therefore:

```text
Mini-Batch Gradient
      ≈
Full Dataset Gradient
```

but not exactly.

Different batches produce different gradients:

```text
Batch 1 → Gradient A
Batch 2 → Gradient B
Batch 3 → Gradient C
```

This stochasticity can sometimes help exploration of the optimization landscape.

---

# 39. Batch Size and Optimization

Small batch:

```text
More Gradient Noise
More Updates
Lower Memory
```

Large batch:

```text
Less Gradient Noise
Fewer Updates per Epoch
Higher Memory
```

Changing batch size can affect:

* Training speed
* Memory usage
* Gradient noise
* Generalization
* Learning-rate requirements

---

# 40. Learning Rate vs Batch Size

These hyperparameters interact.

If batch size changes significantly, the optimal learning rate may also change.

Do not assume:

```text
Larger Batch = Always Better
```

or:

```text
Smaller Batch = Always Better
```

The best combination depends on the model, hardware, dataset, and training objective.

---

# 41. Early Stopping

Early stopping terminates training when validation performance stops improving.

Example:

```text
Epoch
1   ↓
2   ↓
3   ↓
4   ↓
5   ↓
6   →
7   →
8   ↑
```

If validation loss has not improved for a specified number of epochs:

```text
Stop Training
```

This is controlled using **patience**.

---

# 42. Patience

Patience defines how many consecutive epochs without improvement are allowed before stopping.

Example:

```text
Patience = 5
```

The training process can tolerate five epochs without improvement before stopping.

---

# 43. Early Stopping with Best Weights

A practical implementation often restores the model parameters from the epoch with the best validation performance.

```text
Training
   ↓
Best Validation Score
   ↓
Later Performance Worsens
   ↓
Stop
   ↓
Restore Best Weights
```

---

# 44. Optimizer Hyperparameters

Common optimizer hyperparameters include:

```text
Learning Rate
Momentum
β₁
β₂
Weight Decay
Epsilon
```

For Adam, commonly used defaults include:

```text
β₁ ≈ 0.9
β₂ ≈ 0.999
```

but these are not universal rules.

---

# 45. Adam vs AdamW

| Feature              | Adam                                       | AdamW       |
| -------------------- | ------------------------------------------ | ----------- |
| Adaptive Moments     | Yes                                        | Yes         |
| Weight Decay         | Can be coupled depending on implementation | Decoupled   |
| Modern Deep Learning | Common                                     | Very common |
| Transformers         | Used                                       | Widely used |

---

# 46. Optimizer Selection Strategy

A practical starting point:

### Standard Deep Learning

```text
Adam / AdamW
```

### Large-Scale Modern Models

```text
AdamW and architecture-specific optimizers/schedules
```

### Some CNN Training

```text
SGD + Momentum
```

can be highly effective.

### Research / Specialized Models

Experiment with:

```text
Adam
AdamW
SGD
Other task-specific optimizers
```

Do not choose an optimizer solely because it is popular.

---

# 47. Optimizer Does Not Fix Bad Data

If the dataset contains:

```text
Incorrect Labels
Missing Information
Data Leakage
Bad Preprocessing
Distribution Shift
```

changing:

```text
Adam → SGD
```

will not solve the underlying problem.

Always verify the data pipeline first.

---

# 48. Numerical Stability

Training can become unstable because of:

```text
Very Large Values
Very Small Values
Large Gradients
Poor Initialization
Large Learning Rate
```

Common techniques:

```text
Normalization
Stable Loss Implementations
Gradient Clipping
Learning Rate Control
Proper Initialization
```

---

# 49. Backpropagation with Multiple Layers

For a network:

```text
X
 ↓
Layer 1
 ↓
Layer 2
 ↓
Layer 3
 ↓
Loss
```

The backward pass calculates:

```text
∂L/∂W₃
∂L/∂W₂
∂L/∂W₁
```

The chain rule connects the derivatives.

```text
Loss
 ↓
Layer 3 Gradient
 ↓
Layer 2 Gradient
 ↓
Layer 1 Gradient
```

---

# 50. Computational Graph Perspective

Consider:

```text
x → z → a → L
```

where:

```text
z = wx + b
```

```text
a = f(z)
```

```text
L = loss(a, y)
```

Backpropagation computes:

```text
∂L/∂w
```

using:

```text
∂L/∂a
×
∂a/∂z
×
∂z/∂w
```

This is the chain rule applied systematically.

---

# 51. Jacobian

For vector-valued functions, derivatives can be represented using a **Jacobian matrix**.

If:

```text
y = f(x)
```

where both `x` and `y` are vectors:

```text
J = ∂y/∂x
```

The Jacobian contains partial derivatives describing how each output changes with respect to each input.

This becomes important when discussing:

* Backpropagation
* Vectorized neural networks
* Recurrent networks
* Automatic differentiation

---

# 52. Hessian

The **Hessian** contains second-order derivatives.

For a scalar loss `L`:

```text
H = ∂²L / ∂w²
```

The Hessian provides information about curvature.

```text
Gradient → First-order information
Hessian  → Second-order information
```

Most standard neural-network training uses first-order optimization because computing and storing full Hessians is expensive for large models.

---

# 53. First-Order vs Second-Order Optimization

| Feature             | First-Order | Second-Order          |
| ------------------- | ----------- | --------------------- |
| Uses                | Gradients   | Gradients + Curvature |
| Example             | SGD, Adam   | Newton-type methods   |
| Computational Cost  | Lower       | Higher                |
| Deep Learning Usage | Very common | Less common           |

---

# 54. Automatic Differentiation

Modern frameworks automatically calculate gradients.

Examples:

```text
PyTorch → Autograd
TensorFlow → GradientTape
```

Concept:

```text
Forward Computation
        ↓
Computational Graph
        ↓
Automatic Differentiation
        ↓
Gradients
```

This eliminates the need to manually derive gradients for every parameter.

---

# 55. PyTorch Backpropagation

Example:

```python id="9w7r7u"
loss.backward()
```

This computes gradients for parameters that require gradients.

Then:

```python id="4ocx8p"
optimizer.step()
```

updates the parameters.

Before the next update:

```python id="s4h2h4"
optimizer.zero_grad()
```

is commonly used to clear accumulated gradients.

---

# 56. Typical PyTorch Training Loop

```python id="j7zq3d"
for X_batch, y_batch in train_loader:

    optimizer.zero_grad()

    predictions = model(X_batch)

    loss = loss_fn(predictions, y_batch)

    loss.backward()

    optimizer.step()
```

The sequence is:

```text
Zero Gradients
      ↓
Forward Pass
      ↓
Calculate Loss
      ↓
Backward Pass
      ↓
Update Parameters
```

---

# 57. Why Do We Zero Gradients?

In PyTorch, gradients accumulate by default.

Without clearing them:

```text
Current Gradient
+
Previous Gradient
+
Older Gradient
```

would accumulate.

Therefore:

```python id="9ep9lz"
optimizer.zero_grad()
```

is normally called before calculating the next batch's gradients.

---

# 58. Gradient Accumulation

Sometimes gradient accumulation is intentionally used.

Example:

```text
Batch 1 → Gradient
Batch 2 → Gradient
Batch 3 → Gradient
Batch 4 → Update
```

This can simulate a larger effective batch size when GPU memory is limited.

Effective batch size can be approximated as:

```text
Micro-Batch Size × Accumulation Steps
```

---

# 59. Mixed Precision Training

Mixed precision uses lower-precision numerical formats where appropriate.

Common formats include:

```text
FP32
FP16
BF16
```

Benefits:

* Lower memory usage
* Faster computation on supported hardware
* Larger effective batch sizes

Modern deep learning commonly uses:

```text
FP16 / BF16
```

with appropriate numerical safeguards.

---

# 60. Gradient Scaling

With FP16 training, very small gradients can underflow.

Gradient scaling helps:

```text
Small Gradient
      ↓
Scale Up
      ↓
Backpropagation
      ↓
Unscale
      ↓
Parameter Update
```

BF16 generally has a wider dynamic range than FP16 and often requires less aggressive scaling, though training still needs appropriate numerical handling.

---

# 61. Optimization Pipeline

```text
                  MODEL TRAINING
                       │
                       ↓
                Forward Pass
                       │
                       ↓
                  Loss Value
                       │
                       ↓
                Backpropagation
                       │
                       ↓
                   Gradients
                       │
          ┌────────────┴────────────┐
          ↓                         ↓
     Gradient Clipping        Gradient Scaling
          │                         │
          └────────────┬────────────┘
                       ↓
                   Optimizer
                       ↓
               Parameter Update
                       ↓
              Learning Rate Schedule
                       ↓
                  Next Batch
```

---

# 62. Common Optimization Problems

### Problem 1 — Loss Not Decreasing

Check:

```text
Learning Rate
Loss Function
Data
Labels
Initialization
Architecture
Optimizer
Gradient Flow
```

---

### Problem 2 — Loss Explodes

Possible causes:

```text
Learning Rate Too High
Exploding Gradients
Numerical Instability
Poor Initialization
```

Try:

```text
Lower Learning Rate
Gradient Clipping
Better Initialization
Normalization
```

---

### Problem 3 — Training Is Very Slow

Check:

```text
Learning Rate Too Low
Batch Size
Model Size
Hardware Utilization
Data Loading
Optimizer
```

---

### Problem 4 — Training Loss Improves but Validation Does Not

Possible:

```text
Overfitting
```

Consider:

```text
Early Stopping
Regularization
Data Augmentation
More Data
Smaller Model
```

---

# 63. Optimization Checklist

Before changing the optimizer:

```text
1. Verify Data
2. Verify Labels
3. Verify Loss
4. Check Output Activation
5. Check Learning Rate
6. Check Gradient Magnitudes
7. Check Initialization
8. Check Batch Size
9. Check Normalization
10. Check Model Architecture
```

Then experiment with:

```text
Optimizer
Learning Rate Schedule
Weight Decay
Gradient Clipping
```

---

# 64. Important Interview Comparisons

Prepare these:

```text
Gradient Descent vs Stochastic Gradient Descent
Batch vs Mini-Batch Training
SGD vs Adam
Adam vs AdamW
AdaGrad vs RMSProp
Momentum vs Standard SGD
Learning Rate vs Batch Size
Gradient Clipping vs Gradient Scaling
Weight Decay vs L2 Regularization
First-Order vs Second-Order Optimization
Epoch vs Iteration
Gradient vs Hessian
Backpropagation vs Gradient Descent
```

---

# 65. Common Interview Questions

## Backpropagation

1. What is backpropagation?
2. Why is backpropagation required?
3. How does backpropagation work?
4. What is the chain rule?
5. What is a gradient?
6. What is the difference between forward propagation and backpropagation?
7. Does backpropagation update weights?
8. What is automatic differentiation?

## Optimization

9. What is gradient descent?
10. What is learning rate?
11. What happens if learning rate is too high?
12. What happens if learning rate is too low?
13. What is SGD?
14. What is mini-batch gradient descent?
15. What is momentum?
16. What is Adam?
17. What is AdamW?
18. Adam vs SGD?
19. AdaGrad vs RMSProp?
20. What is weight decay?

## Advanced

21. What is a learning-rate scheduler?
22. What is warmup?
23. Why is gradient clipping used?
24. What is gradient accumulation?
25. What is mixed precision?
26. FP16 vs BF16?
27. What is gradient scaling?
28. What is a saddle point?
29. What is the Hessian?
30. First-order vs second-order optimization?

---

# 66. Scenario-Based Interview Questions

### Q1. Your training loss is oscillating heavily. What would you investigate?

```text
Learning Rate
      ↓
Batch Size
      ↓
Gradient Magnitude
      ↓
Optimizer
      ↓
Momentum
```

Potential actions:

```text
Reduce Learning Rate
Use Gradient Clipping
Adjust Batch Size
Try Different Optimizer
```

---

### Q2. Your loss becomes NaN after several iterations.

Check:

```text
Learning Rate
Exploding Gradients
Input Values
Loss Implementation
Numerical Stability
Mixed Precision
```

Potential solutions:

```text
Lower Learning Rate
Gradient Clipping
Stable Loss Function
Normalize Inputs
Check FP16/BF16 Training
```

---

### Q3. Adam trains quickly but generalization is worse than SGD.

Do not assume Adam is always inferior.

Investigate:

```text
Learning Rate
Weight Decay
Scheduler
Training Duration
Regularization
Data
```

Try:

```text
AdamW
SGD + Momentum
Different Learning Rate
Different Weight Decay
```

and compare validation/test performance.

---

### Q4. GPU memory is insufficient for the desired batch size.

Possible approaches:

```text
Reduce Batch Size
        +
Gradient Accumulation
```

Other options:

```text
Mixed Precision
Smaller Model
Gradient Checkpointing
```

---

### Q5. Training becomes unstable at the beginning of a large Transformer model.

Possible techniques:

```text
Learning Rate Warmup
Appropriate Initialization
Gradient Clipping
Stable Optimizer Configuration
Mixed Precision Handling
```

---

# 67. Practical Mental Model

```text
                NEURAL NETWORK LEARNING

Input
 ↓
Forward Pass
 ↓
Prediction
 ↓
Loss
 ↓
"How wrong am I?"
 ↓
Backpropagation
 ↓
"Which parameters caused the error?"
 ↓
Gradients
 ↓
Optimizer
 ↓
"How should I change them?"
 ↓
Parameter Update
 ↓
Repeat
```

---

# 68. Key Distinction

A common interview mistake is saying:

> "Backpropagation updates the weights."

More accurately:

```text
Backpropagation
      ↓
Computes Gradients
      ↓
Optimizer
      ↓
Uses Gradients
      ↓
Updates Weights
```

So:

```text
Backpropagation ≠ Optimizer
```

They work together but perform different jobs.

---

# 69. Final Revision

### Backpropagation

```text
Calculates Gradients
```

### Gradient

```text
Direction / Rate of Local Change
```

### Gradient Descent

```text
Moves Parameters Opposite the Gradient
```

### Optimizer

```text
Defines How Parameters Are Updated
```

### Learning Rate

```text
Controls Update Magnitude
```

### Scheduler

```text
Controls Learning Rate Over Training
```

### Gradient Clipping

```text
Controls Excessively Large Gradients
```

### Early Stopping

```text
Stops Training When Validation Performance Stops Improving
```

### Adam

```text
Adaptive Optimization + Moment Estimates
```

### AdamW

```text
Adam + Decoupled Weight Decay
```

---

# 70. Core Interview Formula Sheet

### Gradient Descent

```text
w_new = w_old - η × ∂L/∂w
```

### Momentum

```text
v_t = βv_(t-1) + (1-β)g_t
```

```text
w_t = w_(t-1) - ηv_t
```

### RMSProp

```text
v_t = βv_(t-1) + (1-β)g_t²
```

```text
w_t = w_(t-1) - η × g_t/(√v_t + ε)
```

### Adam

```text
m_t = β₁m_(t-1) + (1-β₁)g_t
```

```text
v_t = β₂v_(t-1) + (1-β₂)g_t²
```

```text
m̂_t = m_t/(1-β₁^t)
```

```text
v̂_t = v_t/(1-β₂^t)
```

```text
w_t = w_(t-1) - η × m̂_t/(√v̂_t + ε)
```

---

# 71. Interview Takeaway

For a Data Scientist interview, be able to explain this complete chain:

```text
Input
  ↓
Forward Propagation
  ↓
Loss Function
  ↓
Backpropagation
  ↓
Gradient
  ↓
Optimizer
  ↓
Learning Rate
  ↓
Parameter Update
```

And troubleshoot:

```text
Loss Not Decreasing
Loss Exploding
Vanishing / Exploding Gradients
Overfitting
Slow Training
NaN Loss
GPU Memory Limitations
```

The most important distinction to remember:

```text
Backpropagation → Calculates "what to change"
Optimizer       → Decides "how to change it"
Learning Rate   → Controls "how much to change"
```
