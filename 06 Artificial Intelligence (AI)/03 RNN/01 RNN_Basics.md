# Recurrent Neural Networks (RNN) — Basics

> **Job Preparation Notes | Data Science | Machine Learning | AI/Deep Learning**
>
> **Level:** Beginner → Intermediate
> **Prerequisites:** Python, NumPy, basic Neural Networks

---

# 1. What is an RNN?

**RNN (Recurrent Neural Network)** is a type of neural network designed to process **sequential data**, where the order of observations matters.

Examples:

* Text
* Speech
* Time series
* Sensor data
* Stock prices
* Weather data
* User activity
* Machine logs
* Audio signals
* Video sequences

The key characteristic of an RNN is that it maintains a **hidden state** that carries information from previous time steps.

### Basic idea

```text
Current Input + Previous Memory
              ↓
             RNN
              ↓
        New Memory
              ↓
         Next Time Step
```

Mathematically:

```text
h_t = f(x_t, h_{t-1})
```

Where:

* `x_t` = current input
* `h_{t-1}` = previous hidden state
* `h_t` = current hidden state

---

# 2. Why Do We Need RNN?

Traditional feed-forward neural networks assume that inputs are independent.

For example:

```text
Input 1 → Neural Network → Output
Input 2 → Neural Network → Output
Input 3 → Neural Network → Output
```

There is no built-in mechanism for remembering previous inputs.

But sequential data contains dependencies.

Consider:

> "I live in India and I speak ______."

The previous words provide useful context for predicting the next word.

An RNN processes:

```text
I
 ↓
live
 ↓
in
 ↓
India
 ↓
and
 ↓
I
 ↓
speak
```

and carries information through its hidden state.

---

# 3. What is Sequential Data?

Sequential data is data where **the order of observations is meaningful**.

### Example: Time Series

```text
Day 1 → 100
Day 2 → 120
Day 3 → 115
Day 4 → 140
Day 5 → ?
```

The previous values may help predict the next value.

### Example: Sentence

```text
I → love → machine → learning
```

Changing the order changes the meaning:

```text
machine → I → learning → love
```

Therefore, order matters.

---

# 4. Examples of Sequential Problems

## 4.1 NLP

```text
Text
 ↓
Tokenization
 ↓
Embedding
 ↓
RNN
 ↓
Classification
```

Applications:

* Sentiment analysis
* Text classification
* Named Entity Recognition
* Language modeling
* Text generation

---

## 4.2 Time-Series Forecasting

```text
Historical observations
          ↓
         RNN
          ↓
Future prediction
```

Applications:

* Demand forecasting
* Sales forecasting
* Energy forecasting
* Traffic prediction
* Sensor forecasting

---

## 4.3 Speech

Audio is naturally sequential:

```text
Audio frame 1
     ↓
Audio frame 2
     ↓
Audio frame 3
     ↓
Audio frame 4
```

RNNs can learn temporal dependencies between frames.

---

# 5. Feed-Forward Neural Network vs RNN

## Feed-Forward Neural Network

```text
Input
  ↓
Hidden Layer
  ↓
Output
```

Each input is processed independently.

---

## RNN

```text
x₁ → RNN → h₁
           ↓
x₂ → RNN → h₂
           ↓
x₃ → RNN → h₃
           ↓
x₄ → RNN → h₄
```

The previous hidden state is passed to the next time step.

### Key difference

> **Feed-forward networks have no recurrent memory mechanism, while RNNs maintain a hidden state that carries information across time steps.**

---

# 6. RNN Terminology

| Term                            | Meaning                                            |
| ------------------------------- | -------------------------------------------------- |
| Sequence                        | Ordered set of observations                        |
| Time step                       | One position in a sequence                         |
| Input `x_t`                     | Input at time `t`                                  |
| Hidden state `h_t`              | Memory at time `t`                                 |
| Previous hidden state `h_(t-1)` | Memory from previous step                          |
| Output `y_t`                    | Output at time `t`                                 |
| Sequence length                 | Number of time steps                               |
| Feature                         | Number of values at each time step                 |
| Recurrent connection            | Connection carrying information between time steps |
| RNN cell                        | Computation performed at each time step            |
| Unrolling                       | Expanding the RNN across time                      |

---

# 7. Basic RNN Architecture

The fundamental RNN structure is:

```text
             h(t-1)
                │
                ▼
x(t) ───────► [ RNN ] ───────► h(t)
                                │
                                ▼
                              y(t)
```

At every time step, the RNN receives:

```text
1. Current input
2. Previous hidden state
```

It produces:

```text
1. Current hidden state
2. Output
```

---

# 8. RNN Memory

The hidden state acts as the RNN's internal memory.

Consider:

```text
"I love Indian food because it is..."
```

When processing:

```text
"food"
```

the hidden state contains information derived from:

```text
"I"
"love"
"Indian"
"food"
```

Conceptually:

```text
x₁ → h₁
      ↓
x₂ → h₂
      ↓
x₃ → h₃
      ↓
x₄ → h₄
```

Each new hidden state depends on the previous hidden state.

---

# 9. Hidden State

The hidden state is one of the most important concepts in RNNs.

It represents information learned from previous time steps.

The basic equation is:

```text
h_t = f(W_xh x_t + W_hh h_(t-1) + b_h)
```

Where:

| Symbol    | Meaning                  |
| --------- | ------------------------ |
| `x_t`     | Current input            |
| `h_(t-1)` | Previous hidden state    |
| `W_xh`    | Input-to-hidden weights  |
| `W_hh`    | Hidden-to-hidden weights |
| `b_h`     | Hidden bias              |
| `f`       | Activation function      |
| `h_t`     | Current hidden state     |

The most important idea is:

```text
h_t depends on x_t and h_(t-1)
```

---

# 10. Output of an RNN

The output can be calculated from the hidden state.

A simple formulation is:

```text
y_t = g(W_hy h_t + b_y)
```

Where:

* `h_t` = current hidden state
* `W_hy` = hidden-to-output weights
* `b_y` = output bias
* `g` = output activation
* `y_t` = output

Therefore:

```text
Input
  +
Previous Hidden State
        ↓
     RNN Cell
        ↓
 Current Hidden State
        ↓
      Output
```

---

# 11. RNN Cell

An RNN cell represents the computation performed at one time step.

```text
          h(t-1)
             │
             ▼
x(t) ──► [ RNN Cell ]
             │
        ┌────┴────┐
        ▼         ▼
      h(t)       y(t)
```

The same RNN cell is reused for every time step.

This is called:

> **Parameter sharing**

---

# 12. Parameter Sharing

Suppose we have:

```text
x₁ → RNN
x₂ → RNN
x₃ → RNN
x₄ → RNN
```

These are not four separate models.

They use the same weights:

```text
W_xh
W_hh
W_hy
```

This significantly reduces the number of parameters.

### Interview question

**Q: Does an RNN use different weights at every time step?**

**Answer:**

No. The same recurrent weights are shared across time steps. This allows the model to process sequences of varying lengths while keeping the number of parameters independent of sequence length.

---

# 13. RNN Unrolling

An RNN can be represented as a loop:

```text
        ┌─────────────┐
        │             │
x_t ───►│    RNN      │───► h_t
        │             │
        └──────▲──────┘
               │
             h(t-1)
```

For understanding and training, we can **unroll** it across time:

```text
x₁ ──► RNN ──► h₁
               │
x₂ ──► RNN ──► h₂
               │
x₃ ──► RNN ──► h₃
               │
x₄ ──► RNN ──► h₄
```

Unrolling makes the recurrent dependency explicit.

---

# 14. Unrolled RNN Example

Suppose the sequence is:

```text
[10, 20, 30, 40]
```

The RNN processes:

```text
10 → h₁
     ↓
20 → h₂
     ↓
30 → h₃
     ↓
40 → h₄
```

The computation is:

```text
h₁ = f(x₁, h₀)

h₂ = f(x₂, h₁)

h₃ = f(x₃, h₂)

h₄ = f(x₄, h₃)
```

Therefore:

```text
h₄
```

contains information influenced by:

```text
x₁, x₂, x₃, x₄
```

although how well it preserves very old information is limited in vanilla RNNs.

---

# 15. Initial Hidden State

At the first time step, there is no previous hidden state.

Therefore we need:

```text
h₀
```

Commonly:

```text
h₀ = 0
```

So:

```text
h₁ = f(x₁, h₀)
```

Then:

```text
h₂ = f(x₂, h₁)
```

and so on.

---

# 16. Activation Function in Vanilla RNN

A traditional RNN commonly uses:

```text
tanh
```

The hidden state can be calculated as:

```text
h_t = tanh(W_xh x_t + W_hh h_(t-1) + b)
```

The `tanh` activation produces values approximately in:

```text
[-1, +1]
```

### Why tanh?

It is zero-centered and historically worked well for recurrent state representations.

However, using `tanh` does not eliminate the vanishing-gradient problem.

---

# 17. Simple Numerical Example

Assume:

```text
x_t = 2
h_(t-1) = 0.5

W_xh = 0.4
W_hh = 0.6
b = 0.1
```

Then:

```text
z = (0.4 × 2) + (0.6 × 0.5) + 0.1
```

```text
z = 0.8 + 0.3 + 0.1
```

```text
z = 1.2
```

Now:

```text
h_t = tanh(1.2)
```

Approximately:

```text
h_t ≈ 0.834
```

This becomes the memory passed to the next time step.

---

# 18. RNN Input Structure

A typical RNN input has three dimensions:

```text
(batch_size, sequence_length, features)
```

Example:

```text
(32, 10, 5)
```

means:

```text
32 → number of samples
10 → time steps per sequence
5  → features at each time step
```

Visual representation:

```text
32 sequences
    ↓
Each sequence has 10 time steps
    ↓
Each time step has 5 features
```

---

# 19. NLP Input Shape

Suppose:

```text
1000 sentences
20 words per sentence
```

Before embedding:

```text
(1000, 20)
```

After embedding with embedding dimension 128:

```text
(1000, 20, 128)
```

The RNN receives:

```text
batch_size
     ↓
sequence_length
     ↓
embedding_dimension
```

---

# 20. Time-Series Input Shape

Suppose:

```text
1000 training sequences
30 days per sequence
5 features per day
```

Input shape:

```text
(1000, 30, 5)
```

Example features:

```text
Sales
Price
Promotion
Temperature
Holiday
```

So each time step contains:

```text
[Sales, Price, Promotion, Temperature, Holiday]
```

---

# 21. RNN Output Types

RNNs can produce different output structures.

## Many-to-One

```text
x₁ → h₁
x₂ → h₂
x₃ → h₃
x₄ → h₄
          ↓
         y
```

Example:

```text
Review → Sentiment
```

---

## Many-to-Many

```text
x₁ → y₁
x₂ → y₂
x₃ → y₃
x₄ → y₄
```

Example:

```text
Words → POS Tags
```

---

## One-to-Many

```text
x
 ↓
y₁ → y₂ → y₃ → y₄
```

Example:

```text
Image → Caption
```

The complete architecture depends on the problem.

---

# 22. Common RNN Application Types

| Problem             | Input             | Output              |
| ------------------- | ----------------- | ------------------- |
| Sentiment analysis  | Text sequence     | Class               |
| Text classification | Text              | Class               |
| POS tagging         | Text              | Tag per token       |
| NER                 | Text              | Entity per token    |
| Forecasting         | Historical values | Future value        |
| Speech recognition  | Audio sequence    | Text                |
| Sequence generation | Sequence          | New sequence        |
| Machine translation | Sentence          | Translated sentence |

---

# 23. RNN for Sentiment Analysis

Example:

```text
"I really enjoyed this movie"
```

Pipeline:

```text
Text
 ↓
Tokenization
 ↓
Integer Encoding
 ↓
Embedding
 ↓
RNN/LSTM/GRU
 ↓
Dense
 ↓
Sigmoid
 ↓
Positive / Negative
```

For binary sentiment classification:

```text
Output = 0 → Negative
Output = 1 → Positive
```

---

# 24. RNN for Time-Series Forecasting

Suppose:

```text
Sales:

100
120
130
150
170
?
```

The model can learn patterns from historical observations.

Pipeline:

```text
Historical Data
      ↓
Data Cleaning
      ↓
Scaling
      ↓
Window Creation
      ↓
RNN
      ↓
Dense
      ↓
Forecast
```

Example:

```text
[100, 120, 130] → 150
[120, 130, 150] → 170
[130, 150, 170] → ?
```

---

# 25. Sliding Window

A sliding window converts a sequence into supervised learning samples.

Original:

```text
10 20 30 40 50 60
```

Window size:

```text
3
```

Generated samples:

```text
X = [10, 20, 30]
y = 40

X = [20, 30, 40]
y = 50

X = [30, 40, 50]
y = 60
```

This is extremely important for RNN-based time-series forecasting.

---

# 26. RNN with Keras

Basic implementation:

```python
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import SimpleRNN, Dense

model = Sequential([
    SimpleRNN(64),
    Dense(1)
])

model.compile(
    optimizer="adam",
    loss="mse"
)
```

Architecture:

```text
Input
  ↓
SimpleRNN(64)
  ↓
Dense(1)
  ↓
Prediction
```

---

# 27. RNN for Classification

Example:

```python
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Embedding, SimpleRNN, Dense

model = Sequential([
    Embedding(
        input_dim=10000,
        output_dim=128
    ),

    SimpleRNN(64),

    Dense(1, activation="sigmoid")
])
```

Architecture:

```text
Token IDs
    ↓
Embedding
    ↓
SimpleRNN
    ↓
Dense
    ↓
Sigmoid
    ↓
Class
```

---

# 28. `return_sequences`

This is a very common interview question.

### False

```python
SimpleRNN(64, return_sequences=False)
```

Returns the final output:

```text
x₁ → h₁
x₂ → h₂
x₃ → h₃
x₄ → h₄
          ↓
         h₄
```

Useful for many-to-one problems.

---

### True

```python
SimpleRNN(64, return_sequences=True)
```

Returns:

```text
[h₁, h₂, h₃, h₄]
```

Useful when:

* You need output at every time step.
* You want to stack another RNN layer.
* You are performing sequence labeling.

---

# 29. Stacking RNN Layers

Example:

```python
model = Sequential([
    Embedding(10000, 128),

    SimpleRNN(
        128,
        return_sequences=True
    ),

    SimpleRNN(64),

    Dense(1, activation="sigmoid")
])
```

Why `return_sequences=True` in the first RNN?

Because the second RNN requires a sequence as input.

```text
Embedding
    ↓
RNN Layer 1
    ↓
[h₁, h₂, ..., hₙ]
    ↓
RNN Layer 2
    ↓
Final Output
```

---

# 30. Padding

Natural language sequences have different lengths.

Example:

```text
"I love AI"

"I love machine learning"

"I love machine learning and deep learning"
```

Neural networks generally need batches with compatible tensor dimensions.

Therefore, sequences are padded.

Example:

```text
[10, 20, 30, 0, 0]

[10, 20, 40, 50, 0]

[10, 20, 40, 50, 60]
```

Here:

```text
0 = padding token
```

---

# 31. Masking

The model should not treat padding as meaningful information.

Masking allows the model to ignore padded positions.

Example:

```python
Embedding(
    input_dim=10000,
    output_dim=128,
    mask_zero=True
)
```

Conceptually:

```text
Actual tokens → Process
Padding       → Ignore
```

---

# 32. RNN and Embeddings

Text cannot directly be passed as strings.

A typical pipeline is:

```text
Text
 ↓
Tokenizer
 ↓
Integer IDs
 ↓
Embedding
 ↓
RNN
```

Example:

```text
"machine learning"
```

might become:

```text
[25, 73]
```

Embedding converts each ID into a dense vector:

```text
25 → [0.12, -0.31, 0.55, ...]
73 → [0.81,  0.22, -0.10, ...]
```

Then:

```text
Embedding Matrix
       ↓
RNN
```

---

# 33. RNN vs CNN

| Feature       | RNN                 | CNN                     |
| ------------- | ------------------- | ----------------------- |
| Main strength | Sequential patterns | Local/spatial patterns  |
| Common data   | Sequences           | Images / local patterns |
| Memory        | Hidden state        | No recurrent memory     |
| Computation   | Sequential          | Highly parallel         |
| NLP use       | Historically common | Also possible           |
| Images        | Not primary choice  | Excellent               |

---

# 34. RNN vs Traditional ML

For sequential problems:

### Traditional ML

You may need manually created lag features:

```text
sales_t-1
sales_t-2
sales_t-3
sales_t-7
```

Then:

```text
Features → ML Model → Prediction
```

### RNN

The model processes the sequence directly:

```text
[x₁, x₂, x₃, ..., x_t]
          ↓
         RNN
          ↓
     Prediction
```

RNNs can learn representations of temporal patterns automatically, although they still require appropriate preprocessing and sequence construction.

---

# 35. Advantages of RNN

### 1. Handles sequential data

Designed specifically for ordered data.

### 2. Parameter sharing

Same weights are reused across time steps.

### 3. Variable-length sequences

RNNs can theoretically process different sequence lengths.

### 4. Temporal dependencies

Can capture relationships between observations across time.

### 5. Broad applications

Useful for:

* NLP
* Time series
* Speech
* Sensor data

---

# 36. Limitations of Vanilla RNN

### 1. Vanishing gradients

Makes learning long-term dependencies difficult.

### 2. Exploding gradients

Can make training unstable.

### 3. Sequential computation

Limits parallelization.

### 4. Long sequences

Performance can degrade with very long sequences.

### 5. Memory limitation

The hidden state may not preserve all important historical information.

These limitations motivated:

```text
RNN
 ↓
LSTM / GRU
 ↓
Attention
 ↓
Transformer
```

---

# 37. RNN Training

The basic training process is:

```text
Input Sequence
      ↓
Forward Pass
      ↓
Predictions
      ↓
Loss Calculation
      ↓
Backpropagation Through Time
      ↓
Gradient Calculation
      ↓
Weight Update
      ↓
Next Batch
```

The process repeats over multiple epochs.

---

# 38. Loss Functions

The loss function depends on the task.

### Binary Classification

```python
loss="binary_crossentropy"
```

### Multi-Class Classification

```python
loss="categorical_crossentropy"
```

or:

```python
loss="sparse_categorical_crossentropy"
```

### Regression

```python
loss="mse"
```

---

# 39. Optimizers

Common optimizers:

* SGD
* Adam
* RMSprop

A common starting point:

```python
optimizer="adam"
```

RNN training can be sensitive to learning rate because recurrent networks are susceptible to unstable gradients.

---

# 40. Basic Training Example

```python
model.compile(
    optimizer="adam",
    loss="binary_crossentropy",
    metrics=["accuracy"]
)

history = model.fit(
    X_train,
    y_train,
    validation_data=(X_val, y_val),
    epochs=10,
    batch_size=32
)
```

---

# 41. Basic Overfitting Control

Common techniques:

* Dropout
* Recurrent dropout
* Early stopping
* Reduce model complexity
* More training data
* Regularization
* Hyperparameter tuning

Example:

```python
from tensorflow.keras.callbacks import EarlyStopping

early_stopping = EarlyStopping(
    monitor="val_loss",
    patience=3,
    restore_best_weights=True
)
```

---

# 42. RNN Debugging Checklist

When an RNN model performs poorly, check:

```text
□ Is the sequence constructed correctly?
□ Is the target aligned with the sequence?
□ Is there data leakage?
□ Is the data scaled appropriately?
□ Is sequence length appropriate?
□ Is the model too simple?
□ Is the model too large?
□ Is the learning rate appropriate?
□ Is the model overfitting?
□ Is the model underfitting?
□ Are gradients exploding?
□ Are gradients vanishing?
□ Is padding handled correctly?
□ Is masking required?
□ Is the evaluation split chronological for time series?
```

---

# 43. Important Interview Concept: Sequence Length

Sequence length determines how many time steps are given to the model.

Example:

```text
Sequence length = 5

[10, 20, 30, 40, 50]
```

Increasing sequence length can:

### Benefits

* Provide more historical context.
* Help learn longer dependencies.

### Problems

* More computation.
* More memory.
* Greater difficulty with gradients.
* Potentially more noise.
* Longer training time.

Therefore:

> Sequence length should be selected based on the problem and validated experimentally.

---

# 44. Important Interview Concept: Why Not Always Use RNN?

Because RNNs have important limitations:

```text
Long-term dependency problem
        +
Vanishing/exploding gradients
        +
Sequential computation
        +
Limited parallelization
```

For many modern applications, alternatives may be preferable:

```text
LSTM
GRU
CNN/Temporal CNN
Transformers
Traditional time-series models
Tree-based ML models
```

Model selection should depend on the data and business problem.

---

# 45. Real-World Model Selection

Suppose you have a sales forecasting problem.

Do not automatically choose LSTM.

Start with baselines:

```text
Naive Forecast
      ↓
Moving Average
      ↓
Statistical Model
      ↓
Tree-based ML
      ↓
RNN / LSTM / GRU
      ↓
Transformer / Advanced Model
```

Then compare:

* Accuracy
* Stability
* Training cost
* Inference latency
* Interpretability
* Maintenance
* Business impact

### Interview-quality answer

> "I would not select an RNN simply because the data is sequential. I would establish a strong baseline first, then evaluate whether the recurrent model provides meaningful improvement relative to its computational and operational complexity."

---

# 46. Beginner Interview Questions

## Q1. What is an RNN?

**Answer:**

An RNN is a neural network designed for sequential data. It processes inputs step by step and maintains a hidden state that carries information from previous time steps.

---

## Q2. Why do we use RNN?

**Answer:**

We use RNNs when the order and temporal dependencies between observations are important, such as text, speech, sensor data, and time-series data.

---

## Q3. What is hidden state?

**Answer:**

The hidden state is the internal representation that carries information from previous time steps and is updated using the current input.

---

## Q4. What is an RNN cell?

**Answer:**

An RNN cell performs the recurrent computation at one time step, combining the current input and previous hidden state to produce the current hidden state and potentially an output.

---

## Q5. Does an RNN have different weights at each time step?

**Answer:**

No. RNN parameters are shared across time steps.

---

# 47. Intermediate Interview Questions

## Q6. What is unrolling?

**Answer:**

Unrolling expands the recurrent computation across individual time steps so that the dependencies between hidden states can be represented explicitly.

---

## Q7. What is BPTT?

**Answer:**

BPTT, or Backpropagation Through Time, is the training procedure used to propagate errors backward through the unrolled time steps of an RNN.

---

## Q8. What is the main limitation of vanilla RNN?

**Answer:**

The major limitation is difficulty learning long-term dependencies due to vanishing and exploding gradients.

---

## Q9. What is `return_sequences=True`?

**Answer:**

It makes the RNN return an output for every time step instead of returning only the final output.

---

## Q10. Why do we use padding?

**Answer:**

Padding makes sequences of different lengths compatible with batch processing by bringing them to a common length.

---

# 48. Advanced Interview Questions

## Q11. Why does RNN suffer from vanishing gradients?

Because during BPTT, gradients are repeatedly multiplied across time steps. If the effective multiplication factors are small, the gradients can shrink exponentially as they move toward earlier time steps.

---

## Q12. How does LSTM solve the problem?

LSTM introduces a cell state and gating mechanisms that provide a more effective path for information and gradients to flow across long sequences.

---

## Q13. Why can't an RNN process all time steps in parallel?

Because:

```text
h_t depends on h_(t-1)
```

Therefore, the current step cannot be computed until the previous hidden state is available.

---

## Q14. How can exploding gradients be controlled?

Common approaches include:

* Gradient clipping
* Appropriate learning rates
* Proper initialization
* Architecture changes such as LSTM/GRU

---

## Q15. Why is RNN generally not preferred for modern LLMs?

Traditional RNNs process sequences sequentially and struggle with long-range dependencies. Transformer architectures use attention and offer much better parallelization and long-context modeling capabilities.

---

# 49. RNN Mental Model

Remember this:

```text
Sequential Data
      ↓
Current Input
      +
Previous Hidden State
      ↓
   RNN Cell
      ↓
Current Hidden State
      +
Output
      ↓
Next Time Step
```

The central equation:

```text
h_t = f(x_t, h_(t-1))
```

And the central limitation:

```text
Repeated Gradient Multiplication
             ↓
Vanishing / Exploding Gradients
             ↓
Difficulty Learning Long-Term Dependencies
```

---

# 50. Interview Cheat Sheet

```text
RNN
│
├── Designed for sequential data
│
├── Maintains hidden state
│
├── h_t depends on x_t and h_(t-1)
│
├── Same weights shared across time
│
├── Can be unrolled through time
│
├── Trained using BPTT
│
├── Problems:
│     ├── Vanishing gradients
│     └── Exploding gradients
│
├── Gradient clipping → helps exploding gradients
│
├── LSTM → gates + cell state
│
├── GRU → simpler gated RNN
│
├── return_sequences=True
│     → output at every time step
│
├── Many-to-One
│     → sequence classification
│
├── Many-to-Many
│     → sequence labeling
│
└── Major limitation
      → sequential computation + long-term dependency issues
```

---

# 51. What You Must Be Able to Explain in an Interview

Before moving to the next RNN topic, you should be able to explain **without memorizing**:

1. What sequential data is.
2. Why ordinary neural networks struggle with sequential dependencies.
3. What an RNN is.
4. What a hidden state represents.
5. How information flows between time steps.
6. What an RNN cell does.
7. Why weights are shared.
8. What unrolling means.
9. The basic RNN equation.
10. What the initial hidden state is.
11. What many-to-one and many-to-many mean.
12. What `return_sequences` does.
13. Why padding is required.
14. Why masking is useful.
15. How RNNs are used for NLP.
16. How RNNs are used for time series.
17. Why RNNs suffer from vanishing gradients.
18. What exploding gradients are.
19. Why LSTM and GRU were introduced.
20. Why Transformers became more popular.

---

# 52. Next Topic

After understanding these fundamentals, move to:

```text
03_RNN_Mathematics.md
```

The mathematics file should cover:

```text
RNN forward propagation
        ↓
Weight matrices
        ↓
Parameter dimensions
        ↓
Matrix multiplication
        ↓
Activation functions
        ↓
Loss calculation
        ↓
Gradient calculation
        ↓
BPTT mathematics
        ↓
Vanishing gradient derivation
        ↓
Exploding gradient derivation
```

> **Goal:** Don't just know how to use `SimpleRNN()`. Be able to explain **what happens inside the RNN mathematically and why it behaves the way it does.**
