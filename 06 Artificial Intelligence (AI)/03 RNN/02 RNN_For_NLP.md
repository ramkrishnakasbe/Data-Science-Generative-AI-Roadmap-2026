# RNN for NLP — Complete Notes

> **Job Preparation Notes | Data Science | Machine Learning | AI**
>
> **Level:** Beginner → Advanced
> **Focus:** RNN-based Natural Language Processing, Text Classification, Sequence Modeling, Text Generation, and Interview Preparation

---

# 1. RNN for NLP

Natural Language Processing deals with **text and language data**, which is inherently sequential.

Examples:

* Sentiment analysis
* Text classification
* Spam detection
* Intent classification
* Named Entity Recognition
* POS tagging
* Language modeling
* Text generation
* Next-word prediction
* Speech-to-text sequence modeling
* Machine translation

RNNs are suitable for NLP because they process tokens sequentially and maintain a hidden state containing information from previous tokens.

```text
Text
  ↓
Tokenization
  ↓
Integer Encoding
  ↓
Embedding
  ↓
RNN / LSTM / GRU
  ↓
Output Layer
  ↓
Prediction
```

---

# 2. Why Use RNN for NLP?

Consider:

```text
"I don't like this movie"
```

The meaning of:

```text
"like"
```

depends partly on:

```text
"don't"
```

Therefore, understanding a word can require information from previous words.

RNN processes:

```text
I
 ↓
don't
 ↓
like
 ↓
this
 ↓
movie
```

At every step, the hidden state carries information forward.

```text
x₁ → h₁
      ↓
x₂ → h₂
      ↓
x₃ → h₃
      ↓
x₄ → h₄
      ↓
x₅ → h₅
```

---

# 3. NLP Pipeline Using RNN

A typical RNN-based NLP pipeline:

```text
Raw Text
   ↓
Text Cleaning
   ↓
Tokenization
   ↓
Vocabulary Creation
   ↓
Integer Encoding
   ↓
Padding / Truncation
   ↓
Embedding
   ↓
RNN / LSTM / GRU
   ↓
Dense Layer
   ↓
Prediction
   ↓
Evaluation
```

For production:

```text
Training Data
     ↓
Preprocessing
     ↓
Tokenizer
     ↓
Model Training
     ↓
Validation
     ↓
Model Saving
     ↓
Deployment
     ↓
Inference
```

---

# 4. Text Preprocessing

Raw text usually requires preprocessing before being passed to an RNN.

Example:

```text
Original:

"I REALLY loved this Movie!!!"
```

Possible preprocessing:

```text
"i really loved this movie"
```

Common operations:

* Lowercasing
* Removing unwanted characters
* Handling punctuation
* Removing unnecessary whitespace
* Tokenization
* Handling URLs
* Handling special characters
* Handling emojis depending on the task

Important:

> Do not blindly remove every punctuation mark, stop word, or special token. Preprocessing should be driven by the problem.

For example:

```text
"not good"
```

Removing `"not"` could destroy important sentiment information.

---

# 5. Tokenization

Tokenization converts text into smaller units called **tokens**.

Example:

```text
"I love machine learning"
```

Word-level tokenization:

```text
["I", "love", "machine", "learning"]
```

These tokens are then mapped to numerical IDs.

---

# 6. Word-Level Tokenization

Each word becomes a token.

Example:

```text
"I love Python"
```

becomes:

```text
["I", "love", "Python"]
```

Vocabulary:

```text
I       → 1
love    → 2
Python  → 3
```

Encoded sequence:

```text
[1, 2, 3]
```

---

# 7. Character-Level Tokenization

Instead of words, individual characters are used.

Example:

```text
"hello"
```

becomes:

```text
h e l l o
```

Advantages:

* Handles unknown words better
* Small vocabulary
* Can model spelling patterns

Disadvantages:

* Longer sequences
* More computationally expensive
* Harder to learn semantic meaning

---

# 8. Subword Tokenization

Modern NLP frequently uses subword tokenization.

A word can be divided into smaller pieces.

Example:

```text
"unbelievable"
```

might be represented as:

```text
"un" + "believ" + "able"
```

Subword tokenization helps handle:

* Rare words
* Unknown words
* Large vocabularies
* Morphological variations

Modern Transformer systems commonly use subword-based tokenization.

---

# 9. Vocabulary

A vocabulary is the collection of tokens known by the model.

Example:

```text
Vocabulary:

hello
world
machine
learning
python
data
science
```

Each token receives an integer ID.

```text
hello     → 1
world     → 2
machine   → 3
learning  → 4
python    → 5
```

Special tokens may include:

```text
<PAD>
<UNK>
<START>
<END>
```

---

# 10. Unknown Token

Words not present in the vocabulary can be represented using an unknown token.

Example:

```text
<UNK>
```

Suppose vocabulary contains:

```text
machine
learning
python
```

but the sentence contains:

```text
"TensorFlow"
```

It may become:

```text
<UNK>
```

This is one reason subword tokenization became popular.

---

# 11. Integer Encoding

After tokenization, tokens are converted into integer IDs.

Example:

```text
"I love NLP"
```

Tokenized:

```text
["I", "love", "NLP"]
```

Vocabulary:

```text
I     → 1
love  → 2
NLP   → 3
```

Encoded:

```text
[1, 2, 3]
```

The RNN does not directly understand these integer values as meaningful numerical quantities.

They are normally passed through an embedding layer.

---

# 12. Padding

Different sentences have different lengths.

Example:

```text
"I love AI"

"I love machine learning"

"I love machine learning using Python"
```

Numerical sequences may have different lengths:

```text
[1, 2, 3]

[1, 2, 4, 5]

[1, 2, 4, 5, 6, 7]
```

For batch processing, sequences are commonly padded.

Example:

```text
[1, 2, 3, 0, 0, 0]

[1, 2, 4, 5, 0, 0]

[1, 2, 4, 5, 6, 7]
```

Here:

```text
0 = padding token
```

---

# 13. Pre-Padding vs Post-Padding

### Pre-padding

Padding is added at the beginning:

```text
[0, 0, 1, 2, 3]
```

### Post-padding

Padding is added at the end:

```text
[1, 2, 3, 0, 0]
```

For many NLP applications, post-padding is commonly used, but the appropriate choice depends on the model and preprocessing pipeline.

---

# 14. Truncation

Very long sequences may need to be truncated.

Example:

```text
Maximum sequence length = 5
```

Original:

```text
[1, 2, 3, 4, 5, 6, 7, 8]
```

After truncation:

```text
[1, 2, 3, 4, 5]
```

Truncation strategy should be selected carefully because removing important tokens can reduce model performance.

---

# 15. Padding and Masking

Padding introduces artificial tokens.

Example:

```text
[10, 20, 30, 0, 0]
```

The RNN should not interpret `0` as meaningful text.

Masking tells the network:

```text
10 → use
20 → use
30 → use
0  → ignore
0  → ignore
```

Keras example:

```python
from tensorflow.keras.layers import Embedding

embedding = Embedding(
    input_dim=10000,
    output_dim=128,
    mask_zero=True
)
```

---

# 16. One-Hot Encoding

Another way to represent tokens is one-hot encoding.

Suppose vocabulary:

```text
["cat", "dog", "bird"]
```

Then:

```text
cat  → [1, 0, 0]
dog  → [0, 1, 0]
bird → [0, 0, 1]
```

Problems:

* High dimensionality
* Sparse representation
* No semantic similarity
* Memory inefficient for large vocabularies

This motivates embeddings.

---

# 17. Word Embeddings

Word embeddings represent tokens as dense numerical vectors.

Example:

```text
machine
    ↓
[0.12, -0.45, 0.87, 0.22, ...]
```

Words with similar meanings can have similar vector representations.

Conceptually:

```text
king
queen
man
woman
```

are represented in a continuous vector space.

Embedding methods include:

* Word2Vec
* GloVe
* FastText
* Trainable embedding layers

---

# 18. Embedding Layer

A neural network can learn embeddings during training.

Example:

```python
from tensorflow.keras.layers import Embedding

Embedding(
    input_dim=10000,
    output_dim=128
)
```

Meaning:

```text
10000 → vocabulary size
128   → embedding dimension
```

Input:

```text
(batch_size, sequence_length)
```

Output:

```text
(batch_size, sequence_length, embedding_dimension)
```

Example:

```text
Input:

(32, 20)

After embedding:

(32, 20, 128)
```

---

# 19. Word2Vec

Word2Vec learns word representations based on contextual relationships.

Two major architectures:

### CBOW

Predicts a target word from surrounding words.

```text
context → target
```

### Skip-gram

Predicts surrounding words from a target word.

```text
target → context
```

Word2Vec produces static word embeddings.

---

# 20. GloVe

**GloVe = Global Vectors for Word Representation**

GloVe learns word representations using global word co-occurrence statistics.

The intuition:

> Words that occur in similar contexts tend to have similar representations.

---

# 21. FastText

FastText represents words using character n-grams.

This helps with:

* Rare words
* Morphological variations
* Misspellings
* Out-of-vocabulary words

Example:

```text
"playing"
```

can be represented partly through subword information.

---

# 22. Static vs Contextual Embeddings

### Static Embeddings

A word has one vector.

Examples:

* Word2Vec
* GloVe
* FastText

Problem:

```text
bank
```

has different meanings:

```text
river bank
financial bank
```

but static embeddings assign essentially one representation to the word.

### Contextual Embeddings

The representation depends on surrounding context.

Transformers such as BERT introduced highly effective contextual representations.

---

# 23. RNN + Embedding Architecture

A typical architecture:

```text
Token IDs
    ↓
Embedding
    ↓
RNN
    ↓
Dense
    ↓
Prediction
```

Example:

```python
model = Sequential([
    Embedding(10000, 128),
    SimpleRNN(64),
    Dense(1, activation="sigmoid")
])
```

---

# 24. Many-to-One NLP

Many-to-one means:

```text
Many Input Tokens
        ↓
      One Output
```

Example:

```text
"I really enjoyed this movie"
              ↓
          Positive
```

Applications:

* Sentiment classification
* Spam detection
* Intent classification
* Topic classification
* Toxicity classification

---

# 25. Text Classification

Text classification assigns one or more labels to text.

Examples:

```text
Email → Spam / Not Spam

Review → Positive / Negative

Question → Billing / Technical / Account

News → Sports / Politics / Business
```

Pipeline:

```text
Text
 ↓
Tokenization
 ↓
Encoding
 ↓
Padding
 ↓
Embedding
 ↓
RNN/LSTM/GRU
 ↓
Dense
 ↓
Class Prediction
```

---

# 26. Binary Text Classification

Binary classification has two classes.

Example:

```text
Positive
Negative
```

Typical architecture:

```text
Embedding
   ↓
LSTM
   ↓
Dense(1)
   ↓
Sigmoid
```

Output:

```text
0.92
```

Interpretation:

```text
92% estimated probability of positive class
```

Threshold:

```text
>= 0.5 → Positive
< 0.5  → Negative
```

The threshold should be selected based on the business objective rather than blindly assuming `0.5`.

---

# 27. Binary Classification Code

```python
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Embedding, LSTM, Dense

model = Sequential([
    Embedding(
        input_dim=10000,
        output_dim=128,
        mask_zero=True
    ),

    LSTM(64),

    Dense(
        1,
        activation="sigmoid"
    )
])

model.compile(
    optimizer="adam",
    loss="binary_crossentropy",
    metrics=["accuracy"]
)
```

---

# 28. Multiclass Text Classification

Suppose:

```text
Sports
Politics
Business
Technology
```

Architecture:

```text
Embedding
   ↓
LSTM
   ↓
Dense(4)
   ↓
Softmax
```

Example output:

```text
[0.05, 0.10, 0.05, 0.80]
```

Prediction:

```text
Technology
```

For integer class labels:

```python
loss="sparse_categorical_crossentropy"
```

For one-hot labels:

```python
loss="categorical_crossentropy"
```

---

# 29. Multilabel Text Classification

A document can belong to multiple categories.

Example:

```text
Article
 ↓
Technology = 1
AI         = 1
Finance    = 0
Sports     = 0
```

Architecture:

```text
LSTM
 ↓
Dense(number_of_labels)
 ↓
Sigmoid
```

Why sigmoid?

Because each label is independently predicted.

---

# 30. Sentiment Analysis

Sentiment analysis determines the emotional polarity of text.

Example:

```text
"I love this product"
```

Prediction:

```text
Positive
```

Possible classes:

```text
Positive
Negative
Neutral
```

More advanced systems may predict:

```text
Very Positive
Positive
Neutral
Negative
Very Negative
```

---

# 31. Sentiment Analysis Pipeline

```text
Dataset
   ↓
Text Cleaning
   ↓
Train/Validation/Test Split
   ↓
Tokenizer
   ↓
Vocabulary
   ↓
Integer Encoding
   ↓
Padding
   ↓
Embedding
   ↓
LSTM/GRU
   ↓
Dense
   ↓
Prediction
   ↓
Evaluation
```

Important:

> Fit the tokenizer/vocabulary using training data only to avoid leakage.

---

# 32. Spam Detection

Example:

```text
"Congratulations! You won a free prize."
```

Prediction:

```text
Spam
```

Architecture:

```text
Text
 ↓
Tokenizer
 ↓
Embedding
 ↓
RNN/LSTM/GRU
 ↓
Sigmoid
 ↓
Spam / Not Spam
```

Evaluation should consider:

* Precision
* Recall
* F1-score
* PR-AUC

Accuracy alone may be misleading when classes are imbalanced.

---

# 33. Intent Classification

Intent classification determines what the user wants.

Example:

```text
"How can I reset my password?"
```

Possible intent:

```text
Password Reset
```

Example categories:

```text
Account
Payment
Refund
Password
Technical Support
Order Status
```

Pipeline:

```text
User Query
   ↓
Tokenizer
   ↓
Embedding
   ↓
LSTM/GRU
   ↓
Dense
   ↓
Intent
```

---

# 34. Many-to-Many NLP

Many-to-many models produce an output for each input token.

```text
Token₁ → Label₁
Token₂ → Label₂
Token₃ → Label₃
Token₄ → Label₄
```

Applications:

* POS tagging
* Named Entity Recognition
* Token classification

---

# 35. POS Tagging

POS = Part of Speech.

Example:

```text
"Ram works at Heritage Foods"
```

Possible labels:

```text
Ram       → PROPN
works     → VERB
at        → ADP
Heritage  → PROPN
Foods     → PROPN
```

Architecture:

```text
Tokens
 ↓
Embedding
 ↓
BiLSTM
 ↓
Dense per token
 ↓
POS Tag
```

---

# 36. Named Entity Recognition

NER identifies entities in text.

Example:

```text
"Ram works at Heritage Foods in Hyderabad."
```

Possible entities:

```text
Ram              → PERSON
Heritage Foods   → ORGANIZATION
Hyderabad        → LOCATION
```

A sequence model produces one prediction per token.

```text
Token → Entity Label
```

---

# 37. BIO Tagging

NER often uses BIO tagging.

```text
B = Beginning
I = Inside
O = Outside
```

Example:

```text
"Ram works at Heritage Foods"
```

Possible labels:

```text
Ram       → B-PER
works     → O
at        → O
Heritage  → B-ORG
Foods     → I-ORG
```

---

# 38. Sequence Labeling Architecture

```text
Input Tokens
      ↓
Embedding
      ↓
BiLSTM / BiGRU
      ↓
Dense
      ↓
Softmax
      ↓
Label for Each Token
```

For every token:

```text
Token₁ → Label₁
Token₂ → Label₂
...
Tokenₙ → Labelₙ
```

---

# 39. `return_sequences=True` for Sequence Labeling

For sequence classification:

```python
LSTM(64)
```

can return the final representation.

For token-level classification:

```python
LSTM(
    64,
    return_sequences=True
)
```

is required because we need:

```text
h₁, h₂, h₃, ..., hₙ
```

rather than only:

```text
hₙ
```

---

# 40. Bidirectional RNN for NLP

Language often depends on both previous and following context.

Example:

```text
"Apple released a new phone."
```

To understand `"Apple"`, information after it can be useful.

Bidirectional models process:

```text
Forward:
x₁ → x₂ → x₃ → x₄

Backward:
x₁ ← x₂ ← x₃ ← x₄
```

The representations are combined.

Common architectures:

```text
BiRNN
BiLSTM
BiGRU
```

---

# 41. Bidirectional LSTM

Example:

```python
from tensorflow.keras.layers import Bidirectional, LSTM

model.add(
    Bidirectional(
        LSTM(64),
        merge_mode="concat"
    )
)
```

If the forward LSTM has 64 units and the backward LSTM has 64 units:

```text
Output size = 128
```

when using concatenation.

---

# 42. When Not to Use Bidirectional RNN

Bidirectional models require future context.

For real-time processing:

```text
Current token
     ↓
Prediction
```

future tokens may not yet exist.

Therefore, bidirectional models are generally unsuitable for tasks requiring strictly causal predictions, such as some real-time forecasting or streaming applications.

---

# 43. Stacked RNN/LSTM

Multiple recurrent layers can be stacked.

```python
model = Sequential([
    Embedding(10000, 128),

    LSTM(
        128,
        return_sequences=True
    ),

    LSTM(64),

    Dense(1, activation="sigmoid")
])
```

Architecture:

```text
Embedding
    ↓
LSTM 128
    ↓
LSTM 64
    ↓
Dense
```

The first LSTM must return sequences because the second LSTM expects a sequence.

---

# 44. `return_state`

Some recurrent layers can return their final hidden and cell states.

Conceptually:

```python
output, hidden_state, cell_state = LSTM(...)(inputs)
```

For LSTM:

```text
Output
Hidden State
Cell State
```

This becomes especially useful in encoder-decoder architectures.

---

# 45. Language Modeling

Language modeling estimates the probability of a sequence.

Conceptually:

```text
P(word_t | previous words)
```

Example:

```text
"I love machine"
```

Model predicts:

```text
"learning"
```

Architecture:

```text
Previous Tokens
      ↓
Embedding
      ↓
RNN/LSTM/GRU
      ↓
Dense
      ↓
Softmax over Vocabulary
```

---

# 46. Next-Word Prediction

Suppose training text is:

```text
"I love machine learning"
```

Training examples can be:

```text
Input                 Target

"I"                   "love"

"I love"              "machine"

"I love machine"      "learning"
```

The model learns:

```text
Previous Words → Next Word
```

---

# 47. Next-Word Prediction Architecture

```text
Input Tokens
     ↓
Embedding
     ↓
LSTM
     ↓
Dense(Vocabulary Size)
     ↓
Softmax
     ↓
Next Token
```

Example:

```text
Input:
"I love"

Prediction:

machine → 0.70
Python  → 0.10
data    → 0.08
deep    → 0.05
...
```

---

# 48. Text Generation

After training a language model:

```text
Seed Text
   ↓
Model
   ↓
Next Token
   ↓
Append Token
   ↓
Model
   ↓
Next Token
   ↓
Repeat
```

Example:

```text
Seed:
"I love"

Prediction:
"machine"

New sequence:
"I love machine"

Prediction:
"learning"

Final:
"I love machine learning"
```

---

# 49. Greedy Decoding

Greedy decoding chooses the highest-probability token.

Example:

```text
machine → 0.70
learning → 0.20
Python → 0.10
```

Select:

```text
machine
```

Advantages:

* Simple
* Fast

Disadvantages:

* Can produce repetitive or less diverse text

---

# 50. Temperature

Temperature controls the randomness of sampling.

Conceptually:

```text
Low temperature
→ more deterministic

High temperature
→ more random
```

Very low temperature:

```text
Predictable
```

Very high temperature:

```text
Unstable / incoherent
```

---

# 51. Sampling

Instead of always selecting the highest-probability token, sampling can select from the probability distribution.

Example:

```text
machine   0.50
learning  0.30
Python    0.15
data      0.05
```

Sampling can create more diverse text.

---

# 52. Sequence-to-Sequence NLP

Sequence-to-sequence models map:

```text
Input Sequence
       ↓
Output Sequence
```

Examples:

* Machine translation
* Text summarization
* Question answering
* Dialogue generation

Architecture:

```text
Input
 ↓
Encoder
 ↓
Context
 ↓
Decoder
 ↓
Output
```

---

# 53. Encoder

The encoder processes the input sequence.

```text
x₁ → x₂ → x₃ → x₄
                 ↓
          Encoder State
```

The encoder creates representations containing information about the input.

---

# 54. Decoder

The decoder generates the output sequence.

```text
Encoder Representation
          ↓
       Decoder
          ↓
y₁ → y₂ → y₃ → y₄
```

The decoder generates tokens sequentially.

---

# 55. Teacher Forcing

During training, the decoder can receive the actual previous target token.

Without teacher forcing:

```text
Prediction₁
    ↓
Prediction₂
    ↓
Prediction₃
```

With teacher forcing:

```text
Actual₁
   ↓
Actual₂
   ↓
Actual₃
```

This can make training faster and more stable.

---

# 56. Exposure Bias

During training:

```text
Decoder receives correct previous tokens.
```

During inference:

```text
Decoder receives its own previous predictions.
```

This difference creates:

> **Exposure Bias**

An incorrect prediction early in generation can influence later predictions.

---

# 57. Attention

Traditional encoder-decoder RNNs could compress the input into a fixed-size representation.

For long sequences, this can become a bottleneck.

Attention allows the decoder to access different encoder states.

```text
Encoder:

h₁   h₂   h₃   h₄
 \    |   /    /
   Attention
       ↓
    Decoder
```

The decoder can focus on relevant parts of the input for each generated token.

---

# 58. Attention Intuition

Suppose translating:

```text
"I am learning AI"
```

When generating the translation for:

```text
"AI"
```

the decoder should focus more strongly on the encoder representation corresponding to `"AI"`.

Attention creates weighted combinations of encoder states.

---

# 59. RNN vs LSTM vs GRU for NLP

| Feature              | RNN         | LSTM         | GRU                    |
| -------------------- | ----------- | ------------ | ---------------------- |
| Long-term dependency | Poor        | Good         | Good                   |
| Gates                | No          | Yes          | Yes                    |
| Cell state           | No          | Yes          | No separate cell state |
| Parameters           | Low         | High         | Medium                 |
| Training             | Fast/simple | More complex | Usually simpler        |
| NLP suitability      | Basic       | Strong       | Strong                 |

---

# 60. RNN vs Transformer for NLP

| Feature                 | RNN          | Transformer    |
| ----------------------- | ------------ | -------------- |
| Recurrence              | Yes          | No             |
| Processing              | Sequential   | Parallelizable |
| Long-range dependencies | Difficult    | Strong         |
| Training parallelism    | Limited      | High           |
| Context modeling        | Hidden state | Self-attention |
| Modern LLMs             | No           | Yes            |
| Large-scale NLP         | Limited      | Dominant       |

Modern systems such as BERT and GPT-style architectures use Transformers rather than traditional RNNs.

---

# 61. RNN NLP Evaluation Metrics

Metrics depend on the task.

## Binary Classification

* Accuracy
* Precision
* Recall
* F1-score
* ROC-AUC
* PR-AUC

## Multiclass Classification

* Accuracy
* Macro F1
* Weighted F1
* Precision
* Recall
* Confusion Matrix

## NER / POS

* Token-level precision
* Token-level recall
* Token-level F1
* Entity-level F1

## Language Modeling

* Cross-entropy
* Perplexity

---

# 62. Perplexity

Perplexity is commonly used for language models.

Conceptually:

```text
Perplexity = exp(cross entropy)
```

Lower perplexity generally indicates that the model assigns higher probability to the actual sequence.

However, perplexity should be compared carefully across datasets/tokenizers.

---

# 63. Data Leakage in NLP

Data leakage occurs when information from validation/test data influences training.

Incorrect:

```text
All Data
   ↓
Tokenizer
   ↓
Train/Test Split
```

The vocabulary may contain information from the test set.

Better:

```text
Raw Data
   ↓
Train/Test Split
   ↓
Fit Tokenizer on Train
   ↓
Transform Train
   ↓
Transform Test
```

The same principle applies to:

* Vocabulary
* Normalization
* Feature extraction
* Preprocessing statistics

---

# 64. Train / Validation / Test Split

For text classification:

```text
Dataset
   ↓
Train
Validation
Test
```

Example:

```text
70% → Train
15% → Validation
15% → Test
```

The exact ratio can vary.

For temporal text data, splitting should respect time when the deployment scenario is temporal.

---

# 65. Class Imbalance

Suppose:

```text
95% → Not Spam
5%  → Spam
```

A model predicting:

```text
Not Spam
```

for every example achieves:

```text
95% accuracy
```

but is useless for spam detection.

Use:

* Precision
* Recall
* F1
* PR-AUC
* Confusion Matrix
* Class weights
* Resampling where appropriate

---

# 66. Overfitting in RNN NLP

Symptoms:

```text
Training accuracy ↑
Validation accuracy ↓
```

or:

```text
Training loss ↓
Validation loss ↑
```

Solutions:

* Dropout
* Recurrent dropout
* Early stopping
* Reduce model size
* Reduce embedding dimension
* More training data
* Regularization
* Vocabulary control
* Hyperparameter tuning

---

# 67. Hyperparameters

Important parameters:

```text
Vocabulary size
Embedding dimension
Sequence length
Number of RNN units
Number of recurrent layers
Dropout
Learning rate
Batch size
Epochs
Optimizer
Gradient clipping
```

Example:

```python
Embedding(
    input_dim=20000,
    output_dim=128
)

LSTM(
    128,
    dropout=0.2
)
```

---

# 68. Choosing Sequence Length

Short sequence:

```text
Pros:
- Faster
- Less memory

Cons:
- Less context
```

Long sequence:

```text
Pros:
- More context

Cons:
- More computation
- More memory
- Potentially harder optimization
- More noise
```

Select sequence length based on:

* Dataset
* Task
* Distribution of text lengths
* Validation performance
* Computational constraints

---

# 69. Choosing Vocabulary Size

Very small vocabulary:

```text
More <UNK>
Less semantic detail
```

Very large vocabulary:

```text
More parameters
More memory
More rare words
```

Vocabulary size should be selected experimentally.

Subword tokenization can reduce the need for a huge word-level vocabulary.

---

# 70. Dropout in RNN NLP

Example:

```python
LSTM(
    128,
    dropout=0.2,
    recurrent_dropout=0.2
)
```

`dropout` regularizes inputs/connections associated with the layer.

`recurrent_dropout` applies dropout to recurrent connections in implementations that support it.

Purpose:

> Reduce overfitting.

---

# 71. Gradient Clipping

RNNs can suffer from exploding gradients.

Example:

```python
from tensorflow.keras.optimizers import Adam

optimizer = Adam(
    learning_rate=0.001,
    clipnorm=1.0
)
```

Gradient clipping limits gradient magnitude and can stabilize training.

---

# 72. Complete Text Classification Example

```python
import tensorflow as tf

from tensorflow.keras import Sequential
from tensorflow.keras.layers import (
    Embedding,
    LSTM,
    Dense,
    Dropout
)

vocab_size = 10000
max_length = 100
embedding_dim = 128

model = Sequential([
    Embedding(
        input_dim=vocab_size,
        output_dim=embedding_dim,
        mask_zero=True
    ),

    LSTM(128),

    Dropout(0.3),

    Dense(
        1,
        activation="sigmoid"
    )
])

model.compile(
    optimizer="adam",
    loss="binary_crossentropy",
    metrics=["accuracy"]
)

model.summary()
```

Architecture:

```text
Input Token IDs
      ↓
Embedding
      ↓
LSTM
      ↓
Dropout
      ↓
Dense
      ↓
Sigmoid
      ↓
Binary Prediction
```

---

# 73. Training the Model

```python
history = model.fit(
    X_train,
    y_train,
    validation_data=(X_val, y_val),
    epochs=10,
    batch_size=32
)
```

Monitor:

```text
Training Loss
Validation Loss
Training Accuracy
Validation Accuracy
```

---

# 74. Prediction

```python
predictions = model.predict(X_test)
```

For binary classification:

```python
predicted_labels = (
    predictions >= 0.5
).astype(int)
```

Again, the threshold can be tuned depending on the desired precision/recall trade-off.

---

# 75. Confusion Matrix

For binary classification:

```text
                 Actual
              0          1

Predicted 0   TN         FN

Predicted 1   FP         TP
```

From this:

```text
Precision = TP / (TP + FP)

Recall = TP / (TP + FN)

F1 = 2 × Precision × Recall /
     (Precision + Recall)
```

---

# 76. Error Analysis

Do not stop at the metric.

Inspect incorrect predictions.

Example:

```text
Text:
"The movie was not bad."

Actual:
Positive

Predicted:
Negative
```

Potential issue:

```text
Negation handling
```

Another example:

```text
"The battery is sick!"
```

The model may interpret:

```text
"sick" = negative
```

while in context it may be positive slang.

Error analysis helps identify:

* Negation issues
* Sarcasm
* Ambiguous language
* Rare words
* Domain-specific vocabulary
* Spelling errors
* Long-context problems

---

# 77. NLP-Specific Challenges

RNN-based NLP systems may struggle with:

### Negation

```text
"not good"
```

### Sarcasm

```text
"Great, another bug!"
```

### Ambiguity

```text
"I went to the bank."
```

### Long context

Important information may appear far earlier.

### Rare words

Unseen vocabulary can become `<UNK>`.

### Domain-specific terminology

Medical, legal, financial, and technical language may require specialized vocabulary.

---

# 78. Real-World NLP Architecture

A production text-classification system may look like:

```text
User Input
    ↓
API
    ↓
Text Validation
    ↓
Preprocessing
    ↓
Tokenizer
    ↓
Padding
    ↓
RNN/LSTM/GRU
    ↓
Prediction
    ↓
Post-processing
    ↓
Response
```

Deployment stack could include:

```text
Python
TensorFlow/Keras
FastAPI
Docker
Cloud
Monitoring
```

---

# 79. Training vs Inference

Training:

```text
Text
 ↓
Tokenizer
 ↓
Padding
 ↓
Model
 ↓
Loss
 ↓
Backpropagation
```

Inference:

```text
New Text
 ↓
Same Tokenizer
 ↓
Same Preprocessing
 ↓
Padding
 ↓
Model
 ↓
Prediction
```

Critical rule:

> The exact preprocessing/tokenization configuration used during training must be preserved for inference.

---

# 80. Saving Tokenizer and Model

The model alone is not enough.

You must preserve:

```text
Model
Tokenizer
Vocabulary
Sequence length
Preprocessing rules
Label mapping
```

For example:

```text
"positive" → 1
"negative" → 0
```

This mapping must remain consistent during inference.

---

# 81. Production Monitoring

Monitor:

### Model metrics

* Precision
* Recall
* F1
* Prediction confidence

### System metrics

* Latency
* Throughput
* Memory
* CPU/GPU usage

### Data metrics

* Vocabulary changes
* Input length distribution
* Unknown token rate
* Distribution drift

---

# 82. Common RNN NLP Problems

| Problem                                         | Possible Cause                          |
| ----------------------------------------------- | --------------------------------------- |
| Low training accuracy                           | Underfitting                            |
| High training / low validation accuracy         | Overfitting                             |
| NaN loss                                        | Exploding gradients / bad learning rate |
| Slow training                                   | Long sequences / large model            |
| Poor long-context performance                   | Vanilla RNN limitation                  |
| Too many unknown tokens                         | Vocabulary too small                    |
| Poor performance on rare words                  | Sparse training examples                |
| Model predicts majority class                   | Class imbalance                         |
| Bad inference results                           | Preprocessing mismatch                  |
| High validation performance but poor production | Distribution shift / leakage            |

---

# 83. RNN NLP Interview Questions — Beginner

## Q1. Why are RNNs useful for NLP?

Because text is sequential and the order of tokens matters. RNNs maintain a hidden state that carries information from previous tokens.

---

## Q2. What is tokenization?

Tokenization converts text into smaller units such as words, subwords, or characters.

---

## Q3. Why can't we directly pass text to an RNN?

Neural networks operate on numerical tensors, so text must first be converted into numerical representations.

---

## Q4. What is an embedding?

An embedding maps discrete tokens to dense numerical vectors that can capture useful semantic or syntactic relationships.

---

## Q5. Why is padding required?

Because sequences have different lengths, while batch processing generally requires compatible tensor dimensions.

---

# 84. Intermediate Interview Questions

## Q6. Why do we use `mask_zero=True`?

To tell the embedding/recurrent pipeline that zero-valued padded positions should be ignored.

---

## Q7. What is the difference between many-to-one and many-to-many?

Many-to-one produces one output for an entire sequence, such as sentiment classification.

Many-to-many produces an output for each time step, such as POS tagging or NER.

---

## Q8. Why use `return_sequences=True`?

When subsequent layers require the complete sequence of hidden states, such as stacked recurrent layers or token-level classification.

---

## Q9. Why use Bidirectional LSTM for NER?

NER can benefit from both preceding and following context when the full sentence is available.

---

## Q10. Why can RNNs struggle with long sentences?

Because information must pass through many recurrent steps, which can lead to vanishing gradients and difficulty preserving long-range dependencies.

---

# 85. Advanced Interview Questions

## Q11. Why is LSTM generally better than vanilla RNN for NLP?

LSTM introduces a cell state and gates that provide better control over information flow and make learning long-term dependencies easier.

---

## Q12. Why might GRU be preferred over LSTM?

GRU has a simpler architecture and fewer parameters, which can result in faster training and lower computational requirements while still handling long-term dependencies effectively.

---

## Q13. Why are Transformers preferred for modern NLP?

Transformers use self-attention, which provides strong long-range dependency modeling and allows highly parallelizable training.

---

## Q14. Why is Bidirectional RNN unsuitable for causal generation?

Because it uses future context. During causal generation, future tokens are not available.

---

## Q15. What is teacher forcing?

Teacher forcing feeds the actual previous target token into the decoder during training rather than always using the decoder's previous prediction.

---

# 86. Scenario-Based Interview Questions

## Scenario 1

**Your LSTM has 95% training accuracy but only 72% validation accuracy. What would you do?**

Possible answer:

```text
1. Check for overfitting.
2. Inspect train/validation distributions.
3. Check data leakage.
4. Add dropout.
5. Use early stopping.
6. Reduce model complexity.
7. Tune embedding dimension.
8. Tune sequence length.
9. Increase training data if possible.
10. Evaluate class-wise performance.
```

---

## Scenario 2

**Your RNN loss becomes NaN. What would you investigate?**

```text
1. Learning rate
2. Exploding gradients
3. Input values
4. Data preprocessing
5. Invalid numerical values
6. Gradient clipping
7. Model initialization
```

---

## Scenario 3

**Your model performs poorly on long sentences.**

Investigate:

```text
1. Sequence length
2. Truncation strategy
3. Vanilla RNN limitations
4. LSTM/GRU
5. Bidirectional architecture
6. Attention
7. Transformer-based approaches
```

---

## Scenario 4

**Your dataset has 95% negative and 5% positive examples. Accuracy is 95%. Is the model good?**

No.

Check:

```text
Precision
Recall
F1
PR-AUC
Confusion Matrix
```

The model may simply be predicting the majority class.

---

## Scenario 5

**Your model performs well during testing but poorly after deployment.**

Investigate:

```text
1. Training/inference preprocessing mismatch
2. Vocabulary mismatch
3. Data drift
4. Domain shift
5. Label distribution change
6. Unknown-token rate
7. Sequence length distribution
8. Production pipeline bugs
```

---

# 87. RNN NLP Interview Cheat Sheet

```text
RNN NLP
│
├── Text
│    ↓
├── Tokenization
│    ↓
├── Integer Encoding
│    ↓
├── Padding / Truncation
│    ↓
├── Embedding
│    ↓
├── RNN / LSTM / GRU
│    ↓
├── Output
│
├── Many-to-One
│    └── Sentiment / Classification
│
├── Many-to-Many
│    └── NER / POS
│
├── Language Modeling
│    └── Next-Word Prediction
│
├── Sequence-to-Sequence
│    └── Encoder → Decoder
│
├── Attention
│    └── Focus on relevant encoder states
│
└── Limitations
     ├── Vanishing gradients
     ├── Exploding gradients
     ├── Long-range dependency
     └── Sequential computation
```

---

# 88. Key Formulas

### RNN Hidden State

```text
h_t = tanh(W_xh x_t + W_hh h_(t-1) + b_h)
```

### Output

```text
y_t = g(W_hy h_t + b_y)
```

### Binary Cross Entropy

```text
L = -[y log(p) + (1-y) log(1-p)]
```

### Precision

```text
Precision = TP / (TP + FP)
```

### Recall

```text
Recall = TP / (TP + FN)
```

### F1

```text
F1 = 2 × Precision × Recall
     -------------------------
     Precision + Recall
```

### Perplexity

```text
Perplexity = exp(Cross Entropy)
```

---

# 89. Final Mental Model

The complete RNN-based NLP workflow:

```text
                 RAW TEXT
                    │
                    ▼
             Text Preprocessing
                    │
                    ▼
               Tokenization
                    │
                    ▼
             Integer Encoding
                    │
                    ▼
            Padding / Masking
                    │
                    ▼
                Embedding
                    │
                    ▼
             RNN / LSTM / GRU
                    │
          ┌─────────┼─────────┐
          ▼         ▼         ▼
      Classification NER    Generation
          │         │         │
          ▼         ▼         ▼
       One Label  Per Token  Next Token
```

The most important conceptual chain is:

```text
Text
 ↓
Tokens
 ↓
Numbers
 ↓
Vectors
 ↓
Sequential Representation
 ↓
Prediction
```

And the progression of NLP architectures is:

```text
Bag of Words / TF-IDF
        ↓
Word Embeddings
        ↓
RNN
        ↓
LSTM / GRU
        ↓
Seq2Seq
        ↓
Attention
        ↓
Transformer
        ↓
BERT / GPT-style architectures
```

---

# 90. Must-Know Topics for Interviews

You should be able to explain:

```text
✓ NLP preprocessing
✓ Tokenization
✓ Vocabulary
✓ Integer encoding
✓ Padding
✓ Truncation
✓ Masking
✓ One-hot encoding
✓ Word embeddings
✓ Word2Vec
✓ GloVe
✓ FastText
✓ RNN + Embedding
✓ Many-to-one
✓ Many-to-many
✓ Text classification
✓ Sentiment analysis
✓ Multiclass classification
✓ Multilabel classification
✓ POS tagging
✓ NER
✓ BIO tagging
✓ Language modeling
✓ Next-word prediction
✓ Text generation
✓ Bidirectional RNN
✓ LSTM for NLP
✓ GRU for NLP
✓ Sequence-to-sequence
✓ Encoder-decoder
✓ Teacher forcing
✓ Exposure bias
✓ Attention
✓ RNN vs LSTM
✓ RNN vs GRU
✓ RNN vs Transformer
✓ Data leakage
✓ Class imbalance
✓ Overfitting
✓ Evaluation metrics
✓ Error analysis
✓ Production preprocessing
✓ Deployment considerations
```

> **Interview-level understanding:** You should be able to take a raw text-classification problem, explain the complete preprocessing pipeline, justify the choice of RNN/LSTM/GRU, explain the tensor shapes, implement the model, select appropriate metrics, diagnose model problems, and explain when a Transformer would be a better choice.
