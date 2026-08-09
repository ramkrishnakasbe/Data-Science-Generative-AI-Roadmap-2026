# Neural Networks

## 1. What is a Neural Network?

A **Neural Network (NN)** is a machine learning model made up of interconnected computational units called **neurons**. It learns relationships between inputs and outputs by adjusting **weights and biases** during training.

```text
Input Data
    ↓
Input Layer
    ↓
Hidden Layer(s)
    ↓
Output Layer
    ↓
Prediction
```

A neural network learns a function:

```text
ŷ = f(X; W, b)
```

Where:

* `X` = Input
* `W` = Weights
* `b` = Biases
* `ŷ` = Prediction
* `f` = Neural network function

---

# 2. Biological Inspiration

Artificial neural networks are loosely inspired by biological neurons.

### Biological Neuron

```text
Dendrites
   ↓
Cell Body
   ↓
Axon
   ↓
Other Neurons
```

### Artificial Neuron

```text
Inputs
  ↓
Weights
  ↓
Weighted Sum
  ↓
Activation
  ↓
Output
```

The analogy is conceptual; artificial neural networks do not reproduce the biological brain exactly.

---

# 3. Basic Neural Network Architecture

A basic neural network contains:

```text
Input Layer → Hidden Layer(s) → Output Layer
```

Example:

```text
        Hidden Layer
       ┌─────────────┐
x₁ ───→ │ ○           │
x₂ ───→ │ ○           │ ───→ ŷ
x₃ ───→ │ ○           │
       └─────────────┘
```

---

# 4. Layers in Neural Networks

## Input Layer

Receives the features.

Example:

```text
Age
Income
Experience
Credit Score
```

These become:

```text
x₁, x₂, x₃, x₄
```

The input layer generally does not perform the main nonlinear transformation itself.

---

## Hidden Layer

Hidden layers learn intermediate representations.

Example:

```text
Input
 ↓
Hidden Layer 1
 ↓
Hidden Layer 2
 ↓
Hidden Layer 3
 ↓
Output
```

The more hidden layers a network has, the deeper the network becomes.

---

## Output Layer

Produces the final prediction.

Examples:

### Regression

```text
Output = Predicted Price
```

### Binary Classification

```text
Output = Probability of Class 1
```

### Multi-Class Classification

```text
Output = Probabilities of all classes
```

---

# 5. What is a Neuron?

A neuron is the basic computational unit of a neural network.

It performs:

```text
Inputs
   ↓
Weighted Sum
   ↓
Bias
   ↓
Activation Function
   ↓
Output
```

Mathematically:

```text
z = w₁x₁ + w₂x₂ + ... + wₙxₙ + b
```

Then:

```text
a = f(z)
```

Where:

* `x` = Input
* `w` = Weight
* `b` = Bias
* `z` = Pre-activation
* `f` = Activation function
* `a` = Activation/output

---

# 6. Artificial Neuron

For three inputs:

```text
x₁ ── w₁ ──┐
x₂ ── w₂ ──┼──→ Σ + b → Activation → Output
x₃ ── w₃ ──┘
```

The neuron calculates:

```text
z = w₁x₁ + w₂x₂ + w₃x₃ + b
```

Then:

```text
a = f(z)
```

---

# 7. Weights

A **weight** determines how strongly an input contributes to a neuron.

For:

```text
z = w₁x₁ + w₂x₂
```

If:

```text
|w₁| > |w₂|
```

then `x₁` has a larger influence on the weighted sum, all else equal.

Weights are learned during training.

---

# 8. Bias

Bias is an additional learnable parameter.

```text
z = Wx + b
```

Bias provides flexibility by shifting the activation.

Without bias:

```text
z = Wx
```

With bias:

```text
z = Wx + b
```

Bias is especially important when learning decision boundaries that do not need to pass through the origin.

---

# 9. Parameters of a Neural Network

The main trainable parameters are:

```text
Weights
Biases
```

Example:

```text
Input neurons = 4
Output neurons = 3
```

Weight matrix:

```text
4 × 3 = 12 weights
```

Biases:

```text
3 biases
```

Total:

```text
12 + 3 = 15 parameters
```

---

# 10. Matrix Representation

For multiple neurons, matrix notation is used.

Instead of:

```text
z₁ = w₁₁x₁ + w₁₂x₂ + b₁
z₂ = w₂₁x₁ + w₂₂x₂ + b₂
z₃ = w₃₁x₁ + w₃₂x₂ + b₃
```

we write:

```text
Z = XW + b
```

Then:

```text
A = f(Z)
```

This matrix representation makes neural networks computationally efficient.

---

# 11. Example of Matrix Dimensions

Suppose:

```text
Input features = 4
Hidden neurons = 5
```

Then:

```text
X → 1 × 4
W → 4 × 5
b → 1 × 5
```

Therefore:

```text
Z = XW + b
```

has shape:

```text
1 × 5
```

The hidden layer produces 5 activations.

---

# 12. Fully Connected Layer

A **Fully Connected (FC)** layer, also called a **Dense layer**, connects every neuron in one layer to every neuron in the next layer.

```text
Input             Hidden

○ ─────────────── ○
○ ─────────────── ○
○ ─────────────── ○
○ ─────────────── ○
```

Every input neuron is connected to every output neuron.

---

# 13. Dense Layer

A Dense layer performs:

```text
Z = XW + b
```

followed by an activation function:

```text
A = f(Z)
```

Typical architecture:

```text
Dense
 ↓
ReLU
 ↓
Dense
 ↓
ReLU
 ↓
Dense
 ↓
Output
```

---

# 14. Forward Propagation

Forward propagation is the process of calculating the prediction from input to output.

Example:

```text
Input
 ↓
Layer 1
 ↓
Activation
 ↓
Layer 2
 ↓
Activation
 ↓
Output
```

For layer `l`:

```text
Z[l] = A[l-1]W[l] + b[l]
```

Then:

```text
A[l] = f(Z[l])
```

For the first layer:

```text
A[0] = X
```

---

# 15. Multi-Layer Forward Propagation

Suppose a network contains two hidden layers.

```text
Input
 ↓
Hidden Layer 1
 ↓
Hidden Layer 2
 ↓
Output
```

Calculations:

```text
Z[1] = XW[1] + b[1]
```

```text
A[1] = f(Z[1])
```

Then:

```text
Z[2] = A[1]W[2] + b[2]
```

```text
A[2] = f(Z[2])
```

Finally:

```text
Z[3] = A[2]W[3] + b[3]
```

```text
ŷ = g(Z[3])
```

Where `g` depends on the task.

---

# 16. Activation Functions

Activation functions introduce non-linearity.

Common functions:

* Sigmoid
* Tanh
* ReLU
* Leaky ReLU
* PReLU
* ELU
* GELU
* Softmax

---

# 17. Sigmoid

Formula:

```text
σ(z) = 1 / (1 + e^(-z))
```

Range:

```text
0 to 1
```

Common use:

```text
Binary Classification Output
```

Problem:

```text
Can suffer from vanishing gradients
```

---

# 18. Tanh

Formula:

```text
tanh(z) = (e^z - e^(-z)) / (e^z + e^(-z))
```

Range:

```text
-1 to 1
```

It is zero-centered but can still suffer from vanishing gradients.

---

# 19. ReLU

Formula:

```text
ReLU(z) = max(0, z)
```

Examples:

```text
ReLU(-5) = 0
ReLU(3) = 3
```

Advantages:

* Simple
* Computationally efficient
* Helps reduce vanishing-gradient issues compared with sigmoid/tanh in many settings

Problem:

```text
Dying ReLU
```

---

# 20. Leaky ReLU

Formula:

```text
LeakyReLU(z) = z       if z > 0
LeakyReLU(z) = αz      if z ≤ 0
```

Instead of producing exactly zero for negative inputs, it keeps a small negative slope.

---

# 21. Softmax

Softmax converts logits into a probability distribution across classes.

Formula:

```text
P(y=i) = e^(zᵢ) / Σⱼ e^(zⱼ)
```

Properties:

```text
0 ≤ P(y=i) ≤ 1
```

and:

```text
Σ P(y=i) = 1
```

Commonly used for multi-class classification output.

---

# 22. Output Layer Selection

| Problem                    | Output Activation |
| -------------------------- | ----------------- |
| Regression                 | Linear            |
| Binary Classification      | Sigmoid           |
| Multi-Class Classification | Softmax           |
| Multi-Label Classification | Sigmoid           |

---

# 23. Loss Function

Loss measures how wrong the model prediction is.

```text
Actual y
   ↓
Compare
   ↑
Predicted ŷ
   ↓
Loss
```

Common losses:

### Regression

```text
MSE
MAE
Huber Loss
```

### Binary Classification

```text
Binary Cross Entropy
```

### Multi-Class Classification

```text
Categorical Cross Entropy
Sparse Categorical Cross Entropy
```

---

# 24. Neural Network Training

Training follows an iterative process:

```text
Input
 ↓
Forward Propagation
 ↓
Prediction
 ↓
Loss Calculation
 ↓
Backpropagation
 ↓
Gradient Calculation
 ↓
Optimizer
 ↓
Weight Update
 ↓
Repeat
```

---

# 25. Backpropagation

Backpropagation calculates gradients of the loss with respect to model parameters.

Conceptually:

```text
Output
 ↓
Loss
 ↓
Backward Through Layers
 ↓
Gradients
 ↓
Parameter Updates
```

It relies on the **chain rule**.

For a parameter `w`:

```text
∂L / ∂w
```

represents how much the loss changes with respect to `w`.

---

# 26. Chain Rule

For:

```text
x → u → v → L
```

the derivative is:

```text
∂L/∂x
=
(∂L/∂v)
×
(∂v/∂u)
×
(∂u/∂x)
```

Deep networks use repeated applications of the chain rule during backpropagation.

---

# 27. Gradient Descent

Gradient descent minimizes the loss.

Basic update:

```text
w_new = w_old - η × ∂L/∂w
```

Where:

* `η` = learning rate
* `∂L/∂w` = gradient

The negative gradient points toward decreasing loss locally.

---

# 28. Optimizers

Important optimizers:

```text
SGD
Momentum
AdaGrad
RMSProp
Adam
AdamW
```

The optimizer determines how parameter updates are performed using gradients.

---

# 29. Learning Rate

Learning rate controls the size of parameter updates.

### Too Small

```text
Very Slow Training
```

### Too Large

```text
Unstable Training
```

### Appropriate

```text
Stable and Efficient Convergence
```

---

# 30. Epoch, Batch and Iteration

### Epoch

One complete pass through the training dataset.

### Batch

A subset of training samples processed together.

### Iteration

One parameter update using one batch.

Example:

```text
Dataset = 10,000 samples
Batch Size = 100
```

Iterations per epoch:

```text
10,000 / 100 = 100
```

---

# 31. Training Modes

## Batch Gradient Descent

Uses the complete training dataset for one update.

```text
All Data
 ↓
Gradient
 ↓
Update
```

---

## Stochastic Gradient Descent

Uses one sample per update.

```text
One Sample
 ↓
Gradient
 ↓
Update
```

---

## Mini-Batch Gradient Descent

Uses a subset of samples.

```text
Batch
 ↓
Gradient
 ↓
Update
```

Mini-batch training is commonly used in practical deep learning.

---

# 32. Overfitting

A neural network overfits when it learns training-specific patterns that do not generalize well.

Typical pattern:

```text
Training Loss ↓
Validation Loss ↑
```

Solutions:

* Dropout
* L1/L2 Regularization
* Early Stopping
* Data Augmentation
* More Data
* Reduce Model Complexity
* Transfer Learning

---

# 33. Underfitting

Underfitting occurs when the model cannot capture the underlying patterns.

Typical pattern:

```text
Training Performance = Poor
Validation Performance = Poor
```

Possible solutions:

* Increase model capacity
* Train longer
* Improve input representation
* Reduce excessive regularization
* Improve data quality

---

# 34. Dropout

Dropout randomly sets a proportion of activations to zero during training.

```text
Before:

○ ○ ○ ○ ○

After:

○ X ○ X ○
```

Purpose:

```text
Reduce Overfitting
```

Dropout is generally disabled during standard inference.

---

# 35. Batch Normalization

Batch Normalization normalizes layer activations using statistics from the mini-batch during training.

Benefits:

* More stable optimization
* Faster convergence in many settings
* Can provide some regularization

Important:

```text
BatchNorm ≠ LayerNorm
```

LayerNorm is particularly important in Transformer architectures.

---

# 36. Weight Initialization

Weights should be initialized carefully.

Important methods:

### Xavier / Glorot

Commonly associated with:

```text
Sigmoid
Tanh
```

### He Initialization

Commonly associated with:

```text
ReLU
```

Poor initialization can contribute to:

* Vanishing gradients
* Exploding gradients
* Slow convergence

---

# 37. Vanishing Gradient

Vanishing gradients occur when gradients become extremely small.

```text
Small Gradient
      ↓
Small Updates
      ↓
Slow Learning
```

Common causes:

* Deep networks
* Saturating activation functions
* Poor initialization

Solutions:

* ReLU-family activations
* Better initialization
* Residual connections
* Normalization
* Appropriate architecture

---

# 38. Exploding Gradient

Exploding gradients occur when gradients become excessively large.

```text
Large Gradient
      ↓
Huge Updates
      ↓
Unstable Training
```

Solutions:

* Gradient clipping
* Proper initialization
* Lower learning rate
* Normalization
* Residual architectures

---

# 39. Gradient Clipping

Gradient clipping limits gradient magnitude.

Conceptually:

```text
Large Gradient
      ↓
Clip
      ↓
Controlled Gradient
      ↓
Stable Update
```

Commonly useful for training some recurrent neural networks.

---

# 40. Number of Hidden Layers

A network with one hidden layer:

```text
Input
 ↓
Hidden
 ↓
Output
```

A deeper network:

```text
Input
 ↓
Hidden 1
 ↓
Hidden 2
 ↓
Hidden 3
 ↓
Output
```

More depth allows hierarchical representation learning but increases optimization and computational challenges.

---

# 41. Number of Neurons

The number of neurons determines the capacity of a layer.

Too few:

```text
Underfitting
```

Too many:

```text
Higher Computational Cost
Potential Overfitting
```

The optimal architecture depends on the problem.

---

# 42. Universal Approximation Theorem

A sufficiently wide neural network with an appropriate nonlinear activation can approximate a broad class of continuous functions under certain assumptions.

Important interview point:

> The theorem does not mean that one hidden layer is always practical or that any function can be learned perfectly with finite data and computation.

Deep networks are useful because they can learn hierarchical representations efficiently for many problems.

---

# 43. Perceptron

The perceptron is one of the simplest neural models.

```text
Inputs
 ↓
Weighted Sum
 ↓
Threshold
 ↓
Output
```

Basic form:

```text
y = step(Wx + b)
```

The perceptron can learn linearly separable problems.

---

# 44. Limitation of Perceptron

A single-layer perceptron cannot solve non-linearly separable problems such as XOR.

```text
AND → Can learn
OR  → Can learn
XOR → Cannot learn with a single linear decision boundary
```

Adding hidden layers and nonlinear activation functions allows neural networks to represent more complex relationships.

---

# 45. Multi-Layer Perceptron

An **MLP** is a feed-forward neural network containing one or more hidden layers.

```text
Input
 ↓
Dense + Activation
 ↓
Dense + Activation
 ↓
Dense + Activation
 ↓
Output
```

MLPs are commonly used for:

* Tabular data
* Classification
* Regression
* Function approximation

---

# 46. Feed-Forward Neural Network

In a feed-forward network, information flows in one direction:

```text
Input
 ↓
Hidden Layers
 ↓
Output
```

There are no recurrent connections.

Examples:

```text
Perceptron
MLP
Basic Dense Neural Network
```

---

# 47. Feed-Forward vs Recurrent

| Feature         | Feed-Forward NN               | RNN                    |
| --------------- | ----------------------------- | ---------------------- |
| Direction       | Forward                       | Recurrent              |
| Memory          | No internal sequence memory   | Has hidden state       |
| Sequential Data | Not naturally designed for it | Designed for sequences |
| Example         | MLP                           | LSTM                   |

---

# 48. Neural Network Capacity

Model capacity refers to the ability of a model to represent complex functions.

Capacity increases with factors such as:

* Number of parameters
* Number of layers
* Number of neurons
* Architecture complexity

Higher capacity is not automatically better.

```text
Too Little Capacity
       ↓
Underfitting

Appropriate Capacity
       ↓
Good Generalization

Too Much Capacity
       ↓
Potential Overfitting
```

---

# 49. Parameters vs Hyperparameters

| Parameters              | Hyperparameters      |
| ----------------------- | -------------------- |
| Learned during training | Set/tuned externally |
| Weights                 | Learning Rate        |
| Biases                  | Batch Size           |
| Model learns them       | Number of Layers     |
| Updated using optimizer | Dropout Rate         |
|                         | Number of Epochs     |

---

# 50. Model Architecture vs Model Parameters

### Architecture

Defines the structure:

```text
Input
 ↓
Dense(128)
 ↓
ReLU
 ↓
Dense(64)
 ↓
ReLU
 ↓
Dense(1)
```

### Parameters

Values learned within that architecture:

```text
Weights
Biases
```

---

# 51. Classification Neural Network

Example binary classification:

```text
Input Features
      ↓
Dense Layer
      ↓
ReLU
      ↓
Dense Layer
      ↓
ReLU
      ↓
Output Layer
      ↓
Sigmoid
      ↓
Probability
```

Example:

```text
P(Default) = 0.82
```

If threshold = `0.5`:

```text
0.82 ≥ 0.5
```

Prediction:

```text
Default
```

---

# 52. Multi-Class Neural Network

Example:

```text
Input
 ↓
Hidden Layers
 ↓
Output Layer
 ↓
Softmax
```

Output:

```text
Class A = 0.10
Class B = 0.70
Class C = 0.20
```

Prediction:

```text
Class B
```

---

# 53. Regression Neural Network

Example:

```text
Input
 ↓
Dense
 ↓
ReLU
 ↓
Dense
 ↓
ReLU
 ↓
Output
 ↓
Linear
```

Output:

```text
Predicted Sales = 1520.5
```

---

# 54. Neural Network for Tabular Data

Typical architecture:

```text
Numerical / Categorical Features
              ↓
       Preprocessing
              ↓
          Dense Layer
              ↓
            ReLU
              ↓
          Dense Layer
              ↓
            ReLU
              ↓
          Output Layer
```

For many tabular datasets, tree-based models such as XGBoost, LightGBM, or Random Forest may be strong baselines and should be compared against neural networks.

---

# 55. Neural Network for Images

For images, CNNs are generally more suitable than a basic MLP because CNNs exploit spatial structure.

```text
Image
 ↓
Convolution
 ↓
Activation
 ↓
Pooling
 ↓
Convolution
 ↓
Pooling
 ↓
Flatten / Global Pooling
 ↓
Dense
 ↓
Output
```

---

# 56. Neural Network for Sequential Data

Traditional RNN-based architecture:

```text
Sequence
 ↓
RNN / LSTM / GRU
 ↓
Hidden Representation
 ↓
Output
```

Modern sequence modeling often uses:

```text
Sequence
 ↓
Transformer
 ↓
Output
```

---

# 57. Neural Network Families

```text
Neural Networks
│
├── Feed-Forward
│   ├── Perceptron
│   └── MLP
│
├── CNN
│   └── Computer Vision
│
├── RNN
│   ├── LSTM
│   └── GRU
│
├── Transformer
│   ├── BERT
│   ├── GPT
│   └── T5
│
└── Generative Models
    ├── GAN
    ├── VAE
    └── Diffusion
```

---

# 58. Residual Connections

Residual connections help information and gradients flow through deep networks.

Basic formulation:

```text
Output = F(x) + x
```

Architecture:

```text
       ┌───────────────┐
       │               │
x ─────┼──→ F(x) ──────┼──→ Add → Output
       │               ↑
       └───────────────┘
```

They are fundamental to architectures such as **ResNet**.

---

# 59. Computational Graph

A computational graph represents mathematical operations as nodes and dependencies.

Example:

```text
x
 ↓
× w
 ↓
+ b
 ↓
Activation
 ↓
ŷ
 ↓
Loss
```

During:

```text
Forward Pass → Compute values
Backward Pass → Compute gradients
```

Modern deep learning frameworks use computational graphs/autodifferentiation to calculate gradients.

---

# 60. Automatic Differentiation

Deep learning frameworks can automatically calculate gradients.

Examples:

* PyTorch Autograd
* TensorFlow GradientTape

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

This avoids manually deriving gradients for every model parameter.

---

# 61. Neural Network Training Example

Suppose we have:

```text
Input:
x₁ = 2
x₂ = 3
```

Weights:

```text
w₁ = 0.5
w₂ = 0.2
```

Bias:

```text
b = 0.1
```

Weighted sum:

```text
z = w₁x₁ + w₂x₂ + b
```

```text
z = (0.5 × 2) + (0.2 × 3) + 0.1
```

```text
z = 1.7
```

Using ReLU:

```text
a = ReLU(1.7)
```

```text
a = 1.7
```

This output can become input to the next layer.

---

# 62. Complete Neural Network Learning Process

```text
              Training Data
                    ↓
              Input Features
                    ↓
              Neural Network
                    ↓
             Forward Propagation
                    ↓
                Prediction
                    ↓
              Loss Function
                    ↓
              Backpropagation
                    ↓
                 Gradients
                    ↓
                Optimizer
                    ↓
             Update Parameters
                    ↓
                Next Batch
                    ↓
               Next Epoch
                    ↓
               Validation
                    ↓
          Hyperparameter Tuning
                    ↓
             Final Evaluation
                    ↓
                Deployment
```

---

# 63. Practical Hyperparameters

Important hyperparameters to tune:

```text
Learning Rate
Batch Size
Number of Epochs
Number of Hidden Layers
Number of Neurons
Activation Function
Optimizer
Dropout Rate
Weight Decay
Learning Rate Scheduler
```

---

# 64. Debugging a Neural Network

If training loss does not decrease:

Check:

```text
Data
 ↓
Labels
 ↓
Preprocessing
 ↓
Model Architecture
 ↓
Activation Functions
 ↓
Loss Function
 ↓
Learning Rate
 ↓
Optimizer
 ↓
Weight Initialization
```

### If training loss decreases but validation loss increases:

Likely:

```text
Overfitting
```

Try:

```text
Dropout
Regularization
Early Stopping
Data Augmentation
More Data
Simpler Model
```

### If both training and validation performance are poor:

Likely possibilities:

```text
Underfitting
Poor Features / Representation
Incorrect Architecture
Poor Optimization
Insufficient Training
Data Quality Problems
```

---

# 65. Important Neural Network Comparisons

Prepare these thoroughly:

```text
Neuron vs Perceptron
Perceptron vs MLP
MLP vs CNN
MLP vs RNN
CNN vs RNN
RNN vs LSTM
LSTM vs GRU
RNN vs Transformer
Shallow vs Deep Network
Parameter vs Hyperparameter
Epoch vs Iteration
Batch vs Epoch
Forward Propagation vs Backpropagation
BatchNorm vs LayerNorm
SGD vs Adam
L1 vs L2
Dropout vs Regularization
Training vs Inference
```

---

# 66. Common Interview Questions

## Basic

1. What is a neural network?
2. What is a neuron?
3. What are weights and biases?
4. Why do we need bias?
5. What is a hidden layer?
6. What is a Dense layer?
7. What is an MLP?
8. What is a feed-forward neural network?
9. What is a perceptron?
10. What is the XOR problem?

## Forward Propagation

11. What happens during forward propagation?
12. How is the output of a neuron calculated?
13. What is `Z = WX + b`?
14. What is an activation?
15. Why do we need nonlinear activation functions?

## Backpropagation

16. What is backpropagation?
17. What is a gradient?
18. How does the chain rule work in neural networks?
19. What is gradient descent?
20. What is the role of an optimizer?

## Optimization

21. What is learning rate?
22. What happens if learning rate is too high?
23. What happens if learning rate is too low?
24. SGD vs Adam?
25. What is momentum?
26. What is gradient clipping?

## Generalization

27. What is overfitting?
28. How do you prevent overfitting?
29. What is dropout?
30. What is L2 regularization?
31. What is early stopping?
32. What is batch normalization?

## Architecture

33. Why can't a single perceptron solve XOR?
34. What is an MLP?
35. Why are CNNs useful for images?
36. Why are RNNs useful for sequences?
37. Why are Transformers preferred for many modern NLP applications?
38. What are residual connections?
39. What is the vanishing-gradient problem?
40. What is the exploding-gradient problem?

---

# 67. Frequently Asked Scenario Questions

### Q1. Your neural network has very high training accuracy but low validation accuracy. What will you do?

Answer direction:

```text
Overfitting
 ↓
Check Data Split
 ↓
Regularization
 ↓
Dropout
 ↓
Early Stopping
 ↓
Data Augmentation
 ↓
Reduce Model Complexity
 ↓
More Data
```

---

### Q2. Training loss is not decreasing. What will you check?

```text
Learning Rate
Loss Function
Labels
Data Preprocessing
Activation Function
Weight Initialization
Optimizer
Architecture
Gradient Flow
```

---

### Q3. Why does a deep network sometimes perform worse than a shallow network?

Possible reasons:

* Overfitting
* Vanishing gradients
* Exploding gradients
* Poor initialization
* Optimization difficulty
* Insufficient regularization
* Inappropriate architecture

---

### Q4. Why can't we use a linear activation in every layer?

Because composition of linear transformations is still a linear transformation.

```text
Linear
 ↓
Linear
 ↓
Linear
```

is mathematically equivalent to another linear transformation.

Nonlinear activations allow the network to learn nonlinear functions.

---

# 68. Key Formulas

### Neuron

```text
z = Wx + b
```

### Activation

```text
a = f(z)
```

### Layer

```text
Z[l] = A[l-1]W[l] + b[l]
```

### Output

```text
A[l] = f(Z[l])
```

### Gradient Descent

```text
w_new = w_old - η × ∂L/∂w
```

### Sigmoid

```text
σ(z) = 1 / (1 + e^(-z))
```

### ReLU

```text
ReLU(z) = max(0, z)
```

### Softmax

```text
P(y=i) = e^(zᵢ) / Σⱼ e^(zⱼ)
```

---

# 69. Quick Revision

```text
Neural Network
      ↓
Layers
      ↓
Neurons
      ↓
Weights + Bias
      ↓
Weighted Sum
      ↓
Activation
      ↓
Prediction
      ↓
Loss
      ↓
Backpropagation
      ↓
Gradient
      ↓
Optimizer
      ↓
Parameter Update
      ↓
Repeat
```

---

# 70. Interview Takeaway

For interviews, understand a neural network from these **five levels**:

### Level 1 — Structure

```text
Input → Hidden Layers → Output
```

### Level 2 — Neuron

```text
z = Wx + b
a = f(z)
```

### Level 3 — Training

```text
Forward Pass
→ Loss
→ Backpropagation
→ Gradient
→ Optimizer
→ Update
```

### Level 4 — Generalization

```text
Overfitting
Underfitting
Regularization
Dropout
BatchNorm
Early Stopping
```

### Level 5 — Architecture Selection

```text
Tabular Data → MLP / Tree Models
Images → CNN / Vision Transformers
Sequences → RNN / LSTM / GRU / Transformers
Text → Transformers
Generative AI → Transformer-based LLMs
```

The key interview expectation is to explain **how a neural network converts input into predictions, how it learns through backpropagation and optimization, and how you would choose and troubleshoot the architecture for a real-world problem**.
