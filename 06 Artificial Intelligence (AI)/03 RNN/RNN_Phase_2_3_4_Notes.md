# Deep Learning Study Notes: Recurrent Neural Networks (RNNs)
## Modules Covered: Phase 2, Phase 3, and Phase 4

---

# Phase 2: Vanilla RNN Architecture & Forward Propagation

## 2.1 Core Mathematical Formulation

A Recurrent Neural Network (RNN) processes sequences by maintaining an internal **hidden state** vector $h_t$ that acts as a summary of all past information up to timestep $t$.

### 1. Hidden State Transition Equation
At each timestep $t$, the hidden state $h_t$ is updated using the current input vector $x_t$ and the previous hidden state $h_{t-1}$:

$$h_t = \tanh(W_{hh} h_{t-1} + W_{xh} x_t + b_h)$$

Where:
- $x_t \in \mathbb{R}^{d}$: Input vector at timestep $t$ ($d$ = input feature dimension).
- $h_t \in \mathbb{R}^{h}$: Hidden state vector at timestep $t$ ($h$ = hidden unit dimension).
- $h_{t-1} \in \mathbb{R}^{h}$: Hidden state vector from previous timestep $t-1$. Initial hidden state $h_0$ is usually initialized to a vector of zeros.
- $W_{xh} \in \mathbb{R}^{h \times d}$: Weight matrix for input-to-hidden connections.
- $W_{hh} \in \mathbb{R}^{h \times h}$: Weight matrix for hidden-to-hidden recurrent connections.
- $b_h \in \mathbb{R}^{h}$: Bias vector for hidden activation.
- $\tanh$: Hyperbolic tangent non-linear activation function mapping values to the range $(-1, 1)$.

### 2. Output Prediction Equation
Depending on the task topology (e.g., Many-to-Many or Many-to-One), an output vector $\hat{y}_t$ is calculated from the hidden state $h_t$:

$$\hat{y}_t = \text{softmax}(W_{hy} h_t + b_y)$$

Where:
- $\hat{y}_t \in \mathbb{R}^{K}$: Predicted probability distribution over $K$ output classes at step $t$.
- $W_{hy} \in \mathbb{R}^{K \times h}$: Weight matrix for hidden-to-output connections.
- $b_y \in \mathbb{R}^{K}$: Bias vector for output layer.

---

## 2.2 Parameter Sharing Mechanism

Unlike Feedforward Neural Networks (FFNNs) which assign distinct weight matrices to every layer, or Convolutional Neural Networks (CNNs) which share spatial filters across grid positions, an RNN **shares the exact same set of parameters $(W_{xh}, W_{hh}, W_{hy}, b_h, b_y)$ across all timesteps $t \in \{1, 2, \dots, T\}$.**

### Key Benefits of Parameter Sharing:
1. **Generalization Across Sequence Positions:** Patterns learned at the beginning of a sequence (e.g., a subject-verb agreement rule) apply identically at any point in the text.
2. **Variable-Length Processing:** Because weight dimensions depend on feature size ($d$) and hidden size ($h$) rather than sequence length ($T$), the model can handle inputs of arbitrary temporal length $T$.
3. **Parameter Efficiency:** The number of trainable parameters remains constant regardless of sequence duration $T$.

---

## 2.3 Vectorized Implementation from Scratch (Pure Python & NumPy)

```python
import numpy as np

class VanillaRNN:
    def __init__(self, input_dim: int, hidden_dim: int, output_dim: int):
        self.input_dim = input_dim
        self.hidden_dim = hidden_dim
        self.output_dim = output_dim

        # Weight Initialization (Xavier / Glorot initialization)
        self.W_xh = np.random.randn(hidden_dim, input_dim) * np.sqrt(2.0 / (input_dim + hidden_dim))
        self.W_hh = np.random.randn(hidden_dim, hidden_dim) * np.sqrt(2.0 / (hidden_dim + hidden_dim))
        self.W_hy = np.random.randn(output_dim, hidden_dim) * np.sqrt(2.0 / (hidden_dim + output_dim))

        # Biases initialized to zeros
        self.b_h = np.zeros((hidden_dim, 1))
        self.b_y = np.zeros((output_dim, 1))

    def softmax(self, z: np.ndarray) -> np.ndarray:
        exp_z = np.exp(z - np.max(z, axis=0, keepdims=True))
        return exp_z / np.sum(exp_z, axis=0, keepdims=True)

    def forward(self, X: np.ndarray) -> tuple[dict, dict]:
        """
        Forward pass for Vanilla RNN.
        
        Parameters:
            X: Input sequence matrix of shape (T, input_dim, batch_size)
               For simplicity in vectorization, batch_size=1 here (shape: T, d, 1).
        
        Returns:
            h_states: Dictionary mapping timestep t -> hidden state h_t
            y_hats: Dictionary mapping timestep t -> output probability distribution y_hat_t
        """
        T = X.shape[0]
        h_states = {}
        y_hats = {}

        # Initial hidden state h_0 = 0
        h_states[-1] = np.zeros((self.hidden_dim, 1))

        for t in range(T):
            x_t = X[t]  # Shape: (input_dim, 1)

            # Recurrent state computation: h_t = tanh(W_hh * h_{t-1} + W_xh * x_t + b_h)
            linear_h = np.dot(self.W_hh, h_states[t-1]) + np.dot(self.W_xh, x_t) + self.b_h
            h_states[t] = np.tanh(linear_h)

            # Output computation: y_hat_t = softmax(W_hy * h_t + b_y)
            linear_y = np.dot(self.W_hy, h_states[t]) + self.b_y
            y_hats[t] = self.softmax(linear_y)

        return h_states, y_hats

# Example Usage Demonstration
if __name__ == "__main__":
    np.random.seed(42)
    T_steps, d_in, h_dim, K_out = 5, 10, 16, 3
    
    rnn = VanillaRNN(input_dim=d_in, hidden_dim=h_dim, output_dim=K_out)
    X_dummy = np.random.randn(T_steps, d_in, 1)
    
    h_states, y_hats = rnn.forward(X_dummy)
    print(f"Forward Pass Completed Successfully.")
    print(f"Final Hidden State Shape at t={T_steps-1}: {h_states[T_steps-1].shape}")
    print(f"Final Output Probabilities Shape: {y_hats[T_steps-1].shape}")
```

---

# Phase 3: Backpropagation Through Time (BPTT)

## 3.1 BPTT Mathematical Derivation

To update parameters in an unrolled RNN, we use **Backpropagation Through Time (BPTT)**. Consider a Many-to-Many sequence task over $T$ steps using Cross-Entropy loss at each timestep:

$$L_t = -\sum_{k=1}^K y_{t,k} \log(\hat{y}_{t,k})$$

The Total Sequence Loss is:

$$L = \sum_{t=1}^T L_t$$

```
   L_1          L_2                  L_T
    |            |                    |
  y_hat_1      y_hat_2              y_hat_T
    |            |                    |
   h_1  ----->  h_2  -----> ... ----> h_T
    |            |                    |
   x_1          x_2                  x_T
```

### Derivation for Output Weights ($W_{hy}$)
$W_{hy}$ directly impacts $L_t$ at timestep $t$ via $\hat{y}_t$:

$$\frac{\partial L}{\partial W_{hy}} = \sum_{t=1}^T \frac{\partial L_t}{\partial W_{hy}} = \sum_{t=1}^T \frac{\partial L_t}{\partial \hat{y}_t} \frac{\partial \hat{y}_t}{\partial z_t^y} \frac{\partial z_t^y}{\partial W_{hy}} = \sum_{t=1}^T (\hat{y}_t - y_t) h_t^T$$

### Derivation for Recurrent Weights ($W_{hh}$)
Because $W_{hh}$ influences $h_t$, and $h_t$ influences $h_{t+1}, h_{t+2}, \dots, h_T$, the total gradient of loss $L_t$ with respect to $W_{hh}$ requires propagating backwards from timestep $t$ all the way to $k=1$:

$$\frac{\partial L_t}{\partial W_{hh}} = \sum_{k=1}^t \frac{\partial L_t}{\partial h_t} \cdot \frac{\partial h_t}{\partial h_k} \cdot \frac{\partial h_k}{\partial W_{hh}}$$

Where the temporal Jacobian chain term $\frac{\partial h_t}{\partial h_k}$ is defined by:

$$\frac{\partial h_t}{\partial h_k} = \prod_{j=k+1}^t \frac{\partial h_j}{\partial h_{j-1}}$$

Summing across all loss timesteps $t$:

$$\frac{\partial L}{\partial W_{hh}} = \sum_{t=1}^T \sum_{k=1}^t \frac{\partial L_t}{\partial h_t} \left( \prod_{j=k+1}^t \frac{\partial h_j}{\partial h_{j-1}} \right) \frac{\partial h_k}{\partial W_{hh}}$$

---

## 3.2 Truncated BPTT

For long sequences (e.g., $T = 10,000$ tokens), computing exact BPTT presents severe challenges:
1. **Computational Bottleneck:** Computing $\mathcal{O}(T^2)$ matrix multiplications per optimization step is extremely slow.
2. **Memory Overheads:** Retaining all $T$ hidden state matrices in GPU RAM leads to Out-Of-Memory (OOM) errors.

### Mechanism of Truncated BPTT
Instead of propagating gradients through the entire sequence of length $T$:
1. Unroll the forward pass across the full sequence or chunks of length $k_1$.
2. Limit backpropagation to a fixed temporal window of length $k_2$ steps (where $k_2 \ll T$, typically 20 to 100 steps).
3. The hidden state $h$ is passed forward continuously as context, but computational backpropagation graphs are detached after every $k_2$ steps.

```
Sub-sequence 1: [x_1, ..., x_k2]  ---> Compute Loss ---> Backprop k2 steps ---> Update W
                                                                 | (Detach Gradient)
Sub-sequence 2: [x_{k2+1}, ..., x_{2k2}] ---> Forward Pass from h_{k2} ---> Backprop k2 steps
```

---

# Phase 4: Training Pathologies & Solutions

## 4.1 The Vanishing Gradient Problem

### Mathematical Proof
Consider the temporal Jacobian product in the BPTT derivation:

$$\frac{\partial h_j}{\partial h_{j-1}} = \text{diag}\left(1 - \tanh^2(z_j)\right) \cdot W_{hh}^T$$

Where $z_j = W_{hh} h_{j-1} + W_{xh} x_j + b_h$.

Thus, propagating a gradient from timestep $t$ back to timestep $k$:

$$\frac{\partial h_t}{\partial h_k} = \prod_{j=k+1}^t \text{diag}\left(1 - \tanh^2(z_j)\right) \cdot W_{hh}^T$$

Let $J_j = \text{diag}\left(1 - \tanh^2(z_j)\right) W_{hh}^T$. Taking matrix norms:

$$\left\| \frac{\partial h_t}{\partial h_k} \right\| \le \prod_{j=k+1}^t \|J_j\| \le \left( \gamma_1 \gamma_2 \right)^{t-k}$$

Where:
- $\gamma_1 = \max \|1 - \tanh^2(z)\| \le 1.0$.
- $\gamma_2 = \lambda_{\max}(W_{hh})$, the largest eigenvalue (spectral radius) of $W_{hh}$.

### Consequence:
If the absolute largest eigenvalue $\lambda_{\max}(W_{hh}) < 1$, as temporal distance $(t - k) \to \infty$, the gradient term decays exponentially:

$$\lim_{(t-k) \to \infty} \left\| \frac{\partial h_t}{\partial h_k} \right\| = 0$$

### Practical Impact:
The network becomes incapable of learning long-range context dependencies. Early timesteps receive zero gradient updates from late-stage losses, effectively giving the network short-term memory loss.

---

## 4.2 The Exploding Gradient Problem

### Mathematical Proof
Conversely, if $\gamma_2 = \lambda_{\max}(W_{hh}) > 1$ and non-linearities do not saturate, then as temporal span $(t - k)$ grows large:

$$\lim_{(t-k) \to \infty} \left\| \frac{\partial h_t}{\partial h_k} \right\| = \infty$$

### Practical Impact:
1. **Unstable Weight Updates:** Parameter updates take massive steps, destroying previously learned representations.
2. **Numeric Instability:** Matrix values exceed floating-point capacity, causing loss and gradients to evaluate to `NaN` (Not a Number) or `Inf`.

---

## 4.3 Mitigation Strategies

| Strategy | Target Issue | Mechanics & Description |
| :--- | :--- | :--- |
| **Gradient Clipping (Norm)** | Exploding Gradients | Rescales total gradient norm if it exceeds a maximum threshold $g_{\max}$. |
| **Gradient Clipping (Value)** | Exploding Gradients | Hard element-wise clipping of gradient values to $[ -c, c ]$. |
| **Orthogonal Initialization** | Vanishing/Exploding | Initializes $W_{hh}$ such that $W_{hh}^T W_{hh} = I$, keeping eigenvalues $\lambda = 1$. |
| **Gated Architectures (LSTM/GRU)** | Vanishing Gradients | Replaces simple recurrent connections with additive constant error carousels. |

### Gradient Clipping Algorithms

#### 1. Gradient Norm Clipping (Recommended)
Calculates the global Euclidean norm of all parameter gradients $g$:

$$\text{if } \|g\|_2 > g_{\max} \implies g \leftarrow g \cdot \frac{g_{\max}}{\|g\|_2}$$

*Preserves gradient direction while constraining maximum step magnitude.*

#### PyTorch Implementation:
```python
import torch
import torch.nn as nn

# Model definition dummy
model = nn.RNN(input_size=10, hidden_size=20)
optimizer = torch.optim.Adam(model.parameters(), lr=1e-3)

# Inside Training Loop:
# 1. Compute loss & backward pass
# loss.backward()

# 2. Clip Gradients by Norm (e.g., threshold = 1.0)
nn.utils.clip_grad_norm_(model.parameters(), max_norm=1.0)

# 3. Update Weights
optimizer.step()
```

#### 2. Gradient Value Clipping
Clips each individual element $g_i$ within range $[-c, c]$:

$$g_i \leftarrow \max(-c, \min(c, g_i))$$

*Caution: Alters the direction of the gradient vector in high-dimensional space.*

---

## Summary Comparison Matrix

| Concept | Vanilla RNN | Truncated BPTT | Gated Network (LSTM/GRU) |
| :--- | :--- | :--- | :--- |
| **Max Sequence Horizon** | Short ($\sim 10-20$ steps) | Medium ($\sim 50-100$ steps) | Long ($\sim 1000+$ steps) |
| **Gradient Stability** | Prone to Vanishing/Exploding | Reduces Exploding risk | Solves Vanishing via additive identity |
| **Computational Overhead** | Low ($\mathcal{O}(T)$) | Reduced ($\Delta t = k_2$) | Higher ($\mathcal{O}(4T)$ or $\mathcal{O}(3T)$) |
