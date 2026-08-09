# Deep Learning & AI — Interview Preparation

> **Objective:** Build strong theoretical, practical, and interview-ready knowledge of **Deep Learning, NLP, Transformers, Generative AI, LLMs, RAG, AI Agents, and Production AI** for Data Scientist / AI / GenAI roles.

---

# 📚 Learning Roadmap

```text
Deep Learning
      ↓
Neural Networks
      ↓
CNN ───────────────→ Computer Vision
      ↓
RNN → LSTM → GRU
      ↓
Attention
      ↓
Transformers
      ↓
BERT / GPT
      ↓
LLMs
      ↓
Generative AI
      ↓
Prompt Engineering
      ↓
Embeddings
      ↓
Vector Databases
      ↓
RAG
      ↓
Advanced RAG
      ↓
Fine-Tuning
      ↓
LoRA / QLoRA
      ↓
AI Agents
      ↓
Tool Calling
      ↓
MCP
      ↓
Agentic AI
      ↓
AI System Design
      ↓
Deployment / LLMOps
      ↓
Interview Preparation
```

---

# 🟦 Phase 1 — Deep Learning Fundamentals

### 01. Deep Learning Fundamentals

**Core Topics**

* Artificial Neural Networks
* Deep Learning vs Machine Learning
* Neural Network Architecture
* Input Layer
* Hidden Layers
* Output Layer
* Parameters
* Weights
* Bias
* Forward Propagation
* Backpropagation
* Training vs Inference

**File:** `01_Deep_Learning_Fundamentals.md`

---

### 02. Neural Networks

* Perceptron
* Multi-Layer Perceptron
* Feed Forward Neural Network
* Neurons
* Weights and Bias
* Decision Boundary
* Computational Graph
* Forward Pass
* Backward Pass

**File:** `02_Neural_Networks.md`

---

### 03. Perceptron & MLP

* Single Perceptron
* Multi-Layer Perceptron
* Linear Separability
* XOR Problem
* Hidden Layers
* Universal Approximation

**File:** `03_Perceptron_and_MLP.md`

---

### 04. Backpropagation

* Chain Rule
* Gradient Calculation
* Error Propagation
* Computational Graph
* Vanishing Gradient
* Exploding Gradient
* Gradient Flow

**File:** `04_Backpropagation.md`

---

### 05. Activation Functions

Important:

* Sigmoid
* Tanh
* ReLU
* Leaky ReLU
* PReLU
* ELU
* GELU
* Softmax

Understand:

* Formula
* Graph
* Advantages
* Disadvantages
* Vanishing Gradient
* When to use

**File:** `05_Activation_Functions.md`

---

### 06. Loss Functions

* MSE
* MAE
* Binary Cross Entropy
* Categorical Cross Entropy
* Sparse Categorical Cross Entropy
* Hinge Loss
* Focal Loss

Understand which loss function is suitable for which problem.

**File:** `06_Loss_Functions.md`

---

### 07. Gradient Descent

* Batch Gradient Descent
* Stochastic Gradient Descent
* Mini-Batch Gradient Descent
* Learning Rate
* Learning Rate Scheduling
* Local Minima
* Global Minima
* Saddle Points

**File:** `07_Gradient_Descent.md`

---

### 08. Optimizers

Important:

* SGD
* Momentum
* AdaGrad
* RMSProp
* Adam
* AdamW
* Nadam

Understand:

```text
Optimizer
→ How it works
→ Advantages
→ Disadvantages
→ When to use
```

**File:** `08_Optimizers.md`

---

### 09. Regularization

* L1 Regularization
* L2 Regularization
* Dropout
* Early Stopping
* Data Augmentation
* Weight Decay

Focus on:

```text
Overfitting
      ↓
Regularization
      ↓
Better Generalization
```

**File:** `09_Regularization.md`

---

### 10. Batch Normalization

* Internal Covariate Shift
* Normalization
* Batch Statistics
* Training vs Inference
* BatchNorm vs LayerNorm

**File:** `10_Batch_Normalization.md`

---

### 11. Weight Initialization

* Zero Initialization
* Random Initialization
* Xavier / Glorot
* He Initialization
* Initialization and Vanishing Gradients

**File:** `11_Weight_Initialization.md`

---

### 12. Hyperparameter Tuning

Important parameters:

* Learning Rate
* Batch Size
* Epochs
* Number of Layers
* Number of Neurons
* Dropout
* Weight Decay
* Optimizer

Methods:

* Grid Search
* Random Search
* Bayesian Optimization

**File:** `12_Hyperparameter_Tuning.md`

---

# 🟦 Phase 2 — CNN & Computer Vision

## 13. CNN

Learn:

* Convolution
* Kernel / Filter
* Stride
* Padding
* Feature Map
* Receptive Field
* Pooling
* Max Pooling
* Average Pooling
* Flatten
* Fully Connected Layer

**File:** `13_CNN.md`

---

## 14. CNN Architectures

Important models:

```text
LeNet
AlexNet
VGG
GoogLeNet / Inception
ResNet
DenseNet
EfficientNet
```

**File:** `14_CNN_Architectures.md`

---

## 15. Transfer Learning

* Pretrained Models
* Feature Extraction
* Fine-Tuning
* Freezing Layers
* Unfreezing Layers
* ImageNet
* Transfer Learning Workflow

**File:** `15_Transfer_Learning.md`

---

## 16. Object Detection

Understand:

* Classification vs Detection
* Bounding Boxes
* IoU
* Precision / Recall
* mAP
* Anchor Boxes

Important models:

```text
R-CNN
Fast R-CNN
Faster R-CNN
YOLO
SSD
```

**File:** `16_Object_Detection.md`

---

## 17. YOLO

Focus on:

* YOLO architecture
* Grid-based detection
* Bounding boxes
* Confidence score
* Non-Maximum Suppression
* IoU
* mAP
* YOLO versions conceptually

**File:** `17_YOLO.md`

---

## 18. Image Segmentation

* Semantic Segmentation
* Instance Segmentation
* Panoptic Segmentation
* U-Net
* Mask R-CNN

Metrics:

* IoU
* Dice Score

**File:** `18_Segmentation.md`

---

# 🟦 Phase 3 — RNN & Sequential Models

## 19. RNN

* Sequential Data
* Hidden State
* Recurrent Connection
* Unrolled RNN
* Many-to-One
* Many-to-Many
* Vanishing Gradient
* Exploding Gradient

**File:** `19_RNN.md`

---

## 20. LSTM

Understand deeply:

* Cell State
* Hidden State
* Forget Gate
* Input Gate
* Output Gate
* Candidate Cell State
* Vanishing Gradient Solution

**File:** `20_LSTM.md`

---

## 21. GRU

* Update Gate
* Reset Gate
* Hidden State
* GRU vs LSTM

**File:** `21_GRU.md`

---

## 22. Seq2Seq

* Encoder
* Decoder
* Context Vector
* Teacher Forcing
* Sequence-to-Sequence Learning
* Limitations of Fixed Context

**File:** `22_Seq2Seq.md`

---

# 🟦 Phase 4 — Attention & Transformers

## 23. Attention Mechanism

**Very High Priority**

Understand:

```text
Query
Key
Value
```

Topics:

* Attention Scores
* Scaled Dot Product
* Self-Attention
* Cross-Attention
* Attention Weights

**File:** `23_Attention_Mechanism.md`

---

## 24. Self-Attention

* Query
* Key
* Value
* Attention Matrix
* Scaled Dot-Product
* Contextual Representation

**File:** `24_Self_Attention.md`

---

## 25. Transformer

**One of the most important topics in AI interviews.**

Architecture:

```text
Input
 ↓
Tokenization
 ↓
Embedding
 ↓
Positional Encoding
 ↓
Multi-Head Attention
 ↓
Add & Norm
 ↓
Feed Forward Network
 ↓
Add & Norm
 ↓
Output
```

Learn:

* Encoder
* Decoder
* Encoder-Decoder
* Self-Attention
* Cross-Attention
* Multi-Head Attention
* Positional Encoding
* Residual Connections
* Layer Normalization
* Feed Forward Network

**File:** `25_Transformers.md`

---

## 26. Transformer Architecture

Understand the original Transformer paper architecture.

Focus on:

* Encoder Block
* Decoder Block
* Masked Attention
* Cross Attention
* Positional Encoding
* LayerNorm
* Residual Connection

**File:** `26_Transformer_Architecture.md`

---

# 🟦 Phase 5 — NLP & Language Models

## 27. NLP with Deep Learning

* Text Classification
* Sequence Classification
* Named Entity Recognition
* Sentiment Analysis
* Language Modeling
* Sequence Generation

**File:** `27_NLP_Deep_Learning.md`

---

## 28. Word Embeddings

* One-Hot Encoding
* Word2Vec
* CBOW
* Skip-Gram
* GloVe
* FastText
* Contextual Embeddings

**File:** `28_Word_Embeddings.md`

---

## 29. BERT

Understand:

* Encoder-only Transformer
* Bidirectional Context
* Masked Language Modeling
* Next Sentence Prediction
* Pretraining
* Fine-Tuning
* BERT Architecture

**File:** `29_BERT.md`

---

## 30. RoBERTa

* BERT improvements
* Dynamic Masking
* Training Strategy
* RoBERTa vs BERT

**File:** `30_RoBERTa.md`

---

## 31. T5

* Text-to-Text Framework
* Encoder-Decoder Transformer
* Pretraining
* Fine-Tuning

**File:** `31_T5.md`

---

## 32. GPT

Understand:

* Decoder-only Transformer
* Autoregressive Generation
* Next Token Prediction
* Pretraining
* Instruction Tuning
* Generation

**File:** `32_GPT.md`

---

# 🟦 Phase 6 — AI & Generative AI

## 33. AI Fundamentals

* AI
* Machine Learning
* Deep Learning
* Generative AI
* Predictive AI
* Discriminative Models
* Foundation Models

**File:** `33_AI_Fundamentals.md`

---

## 34. Generative AI

Understand:

* Generative vs Discriminative AI
* Foundation Models
* Text Generation
* Image Generation
* Audio Generation
* Video Generation
* Multimodal AI

**File:** `34_Generative_AI.md`

---

## 35. Generative Models

Important models:

```text
GAN
VAE
Diffusion Models
Autoregressive Models
LLMs
```

**File:** `35_Generative_AI_Models.md`

---

## 36. GAN

* Generator
* Discriminator
* Adversarial Training
* Minimax Objective
* Mode Collapse
* GAN Variants

**File:** `36_GAN.md`

---

## 37. VAE

* Encoder
* Latent Space
* Decoder
* Reconstruction Loss
* KL Divergence
* Reparameterization Trick

**File:** `37_VAE.md`

---

## 38. Diffusion Models

* Forward Diffusion
* Noise Addition
* Reverse Diffusion
* Denoising
* Latent Diffusion
* Stable Diffusion — Conceptual Understanding

**File:** `38_Diffusion_Models.md`

---

# 🟦 Phase 7 — LLMs

## 39. LLM Fundamentals

* What is an LLM?
* Parameters
* Tokens
* Context Window
* Pretraining
* Fine-Tuning
* Instruction Tuning
* Alignment
* Inference

**File:** `39_LLM_Fundamentals.md`

---

## 40. LLM Architecture

```text
Text
 ↓
Tokenizer
 ↓
Token Embeddings
 ↓
Positional Information
 ↓
Transformer Blocks
 ↓
Language Modeling Head
 ↓
Next Token
```

**File:** `40_LLM_Architecture.md`

---

## 41. Tokenization

* Token
* Vocabulary
* Subword Tokenization
* BPE
* WordPiece
* SentencePiece
* Token Count
* Context Window

**File:** `41_Tokenization.md`

---

## 42. LLM Pretraining

* Self-Supervised Learning
* Next Token Prediction
* Causal Language Modeling
* Masked Language Modeling
* Training Data
* Pretraining Objective

**File:** `42_LLM_Pretraining.md`

---

## 43. Instruction Tuning

* Instruction Dataset
* Supervised Fine-Tuning
* Instruction Following
* Alignment

**File:** `43_Instruction_Tuning.md`

---

## 44. RLHF

Understand conceptually:

```text
Pretrained LLM
      ↓
SFT
      ↓
Reward Model
      ↓
Human Preference
      ↓
RL Optimization
      ↓
Aligned Model
```

**File:** `44_RLHF.md`

---

## 45. DPO

* Preference Dataset
* Chosen Response
* Rejected Response
* Direct Preference Optimization
* DPO vs RLHF

**File:** `45_DPO.md`

---

## 46. LLM Inference

* Temperature
* Top-K
* Top-P
* Greedy Decoding
* Beam Search
* Sampling
* Context Window
* KV Cache

**File:** `46_LLM_Inference.md`

---

## 47. Hallucination

* What is hallucination?
* Causes
* Factual Hallucination
* Contextual Hallucination
* Reducing Hallucination
* RAG
* Grounding
* Evaluation

**File:** `47_Hallucination.md`

---

# 🟦 Phase 8 — Prompt Engineering

## 48. Prompt Engineering

* Zero-Shot
* One-Shot
* Few-Shot
* Role Prompting
* System Prompt
* Context
* Constraints
* Structured Prompt
* Prompt Templates

**File:** `48_Prompt_Engineering.md`

---

## 49. Prompt Techniques

* Chain-of-Thought
* Self-Consistency
* ReAct
* Tree-of-Thought — Conceptual
* Few-Shot
* Prompt Chaining
* Decomposition

**File:** `49_Prompt_Techniques.md`

---

## 50. Structured Output

* JSON Output
* Schema
* Function Calling
* Output Validation
* Pydantic Models

**File:** `50_Structured_Output.md`

---

# 🟦 Phase 9 — Embeddings & Vector Search

## 51. Embeddings

* Dense Embeddings
* Sparse Embeddings
* Semantic Similarity
* Cosine Similarity
* Euclidean Distance
* Embedding Dimensions
* Query Embeddings
* Document Embeddings

**File:** `51_Embeddings.md`

---

## 52. Semantic Search

* Semantic Similarity
* Vector Search
* Query-Document Similarity
* Nearest Neighbor Search
* ANN

**File:** `52_Semantic_Search.md`

---

## 53. Vector Databases

Important technologies:

```text
FAISS
Pinecone
Chroma
Weaviate
Milvus
pgvector
```

Topics:

* Vector Index
* Similarity Search
* Metadata Filtering
* ANN
* HNSW

**File:** `53_Vector_Databases.md`

---

## 54. Hybrid Search

```text
Keyword Search
       +
Vector Search
       ↓
Hybrid Search
```

Learn:

* BM25
* Dense Retrieval
* Sparse Retrieval
* Hybrid Retrieval
* Score Fusion

**File:** `54_Hybrid_Search.md`

---

## 55. Reranking

* Initial Retrieval
* Candidate Documents
* Reranker
* Cross Encoder
* Final Context

**File:** `55_Reranking.md`

---

# 🟦 Phase 10 — RAG

## 56. RAG Fundamentals

**Very High Priority**

```text
Documents
 ↓
Parsing
 ↓
Chunking
 ↓
Embedding
 ↓
Vector DB
 ↓
Retriever
 ↓
Context
 ↓
Prompt
 ↓
LLM
 ↓
Answer
```

Learn:

* Why RAG?
* RAG vs Fine-Tuning
* RAG Components
* Retrieval
* Augmentation
* Generation

**File:** `56_RAG_Fundamentals.md`

---

## 57. RAG Pipeline

* Document Ingestion
* Document Parsing
* Chunking
* Embeddings
* Indexing
* Retrieval
* Prompt Construction
* Generation
* Citation / Source Grounding

**File:** `57_RAG_Pipeline.md`

---

## 58. Document Chunking

Important strategies:

* Fixed-size Chunking
* Recursive Chunking
* Semantic Chunking
* Sentence Chunking
* Paragraph Chunking
* Parent-Child Chunking

Understand:

* Chunk Size
* Chunk Overlap
* Retrieval Quality
* Context Size

**File:** `58_Document_Chunking.md`

---

## 59. Retrieval Strategies

* Dense Retrieval
* Sparse Retrieval
* Hybrid Retrieval
* Metadata Filtering
* Similarity Search
* MMR
* Top-K Retrieval

**File:** `59_Retrieval_Strategies.md`

---

## 60. Advanced RAG

* Query Rewriting
* Query Expansion
* Query Decomposition
* Multi-Query RAG
* Contextual Compression
* Reranking
* Parent-Document Retrieval
* Multi-Hop Retrieval
* Graph RAG
* Agentic RAG

**File:** `60_Advanced_RAG.md`

---

## 61. RAG Evaluation

Metrics:

* Context Precision
* Context Recall
* Faithfulness
* Answer Relevance
* Groundedness
* Answer Correctness

Tools:

* RAGAS
* DeepEval
* LangSmith

**File:** `61_RAG_Evaluation.md`

---

# 🟦 Phase 11 — Fine-Tuning

## 62. Fine-Tuning

* Pretrained Model
* Dataset Preparation
* Training
* Validation
* Fine-Tuned Model
* Evaluation

Understand:

```text
RAG vs Fine-Tuning
Prompt Engineering vs Fine-Tuning
```

**File:** `62_Fine_Tuning.md`

---

## 63. Supervised Fine-Tuning

* Instruction Dataset
* Input / Output Pairs
* Training Objective
* Evaluation
* Dataset Quality

**File:** `63_SFT.md`

---

## 64. PEFT

* Parameter-Efficient Fine-Tuning
* Adapters
* LoRA
* QLoRA

**File:** `64_PEFT.md`

---

## 65. LoRA

Understand:

* Low-Rank Matrices
* Frozen Base Model
* Trainable Parameters
* Rank
* Alpha
* Dropout
* Advantages

**File:** `65_LoRA.md`

---

## 66. QLoRA

* Quantized Base Model
* LoRA Adapters
* 4-bit Quantization
* NF4
* Memory Efficiency

**File:** `66_QLoRA.md`

---

## 67. Model Quantization

* FP32
* FP16
* BF16
* INT8
* INT4
* Post-Training Quantization
* Quantization-Aware Training

**File:** `67_Model_Quantization.md`

---

# 🟦 Phase 12 — AI Frameworks

## 68. Hugging Face

* Transformers
* Tokenizers
* Datasets
* Model Hub
* Pipelines
* PEFT

**File:** `68_Hugging_Face.md`

---

## 69. LangChain

* Models
* Prompts
* Chains
* Retrievers
* Tools
* Agents
* Memory
* Vector Stores

**File:** `69_LangChain.md`

---

## 70. LlamaIndex

* Data Connectors
* Document Indexing
* Retrieval
* Query Engines
* RAG
* Agents

**File:** `70_LlamaIndex.md`

---

## 71. LangGraph

* State
* Nodes
* Edges
* Graph Workflows
* Agent Orchestration
* Human-in-the-Loop

**File:** `71_LangGraph.md`

---

# 🟦 Phase 13 — AI Agents

## 72. AI Agents

```text
LLM
 ↓
Reasoning
 ↓
Tool Selection
 ↓
Tool Execution
 ↓
Observation
 ↓
Next Action
```

Learn:

* Agent
* Tools
* Memory
* Planning
* Reasoning
* State

**File:** `72_AI_Agents.md`

---

## 73. Agentic AI

* Agentic Workflow
* Autonomous Agents
* Planning
* Reflection
* Reasoning
* Human-in-the-Loop
* Agent State

**File:** `73_Agentic_AI.md`

---

## 74. ReAct

```text
Reason
 ↓
Act
 ↓
Observe
 ↓
Reason
 ↓
Act
```

Understand how ReAct combines reasoning and tool usage.

**File:** `74_ReAct.md`

---

## 75. Tool Calling

* Function Calling
* Tool Definition
* Tool Selection
* Tool Execution
* Tool Results
* Error Handling
* Tool Security

**File:** `75_Tool_Calling.md`

---

## 76. MCP

**Model Context Protocol**

Learn:

* MCP Client
* MCP Server
* Tools
* Resources
* Prompts
* Context Exchange
* MCP Architecture

**File:** `76_MCP.md`

---

## 77. Multi-Agent Systems

* Supervisor Agent
* Worker Agents
* Specialized Agents
* Agent Communication
* Shared State
* Sequential Agents
* Parallel Agents

**File:** `77_Multi_Agent_Systems.md`

---

# 🟦 Phase 14 — Production AI

## 78. AI System Design

Learn to design:

```text
User
 ↓
API
 ↓
Application
 ↓
RAG / Agent
 ↓
LLM
 ↓
Vector DB / Tools
 ↓
Guardrails
 ↓
Response
 ↓
Monitoring
```

Focus on:

* Scalability
* Reliability
* Security
* Latency
* Cost
* Availability

**File:** `78_AI_System_Design.md`

---

## 79. GenAI Architecture

* RAG Architecture
* Agent Architecture
* LLM Application Architecture
* API Layer
* Vector DB
* Cache
* Queue
* Monitoring

**File:** `79_GenAI_Architecture.md`

---

## 80. Guardrails

* Input Validation
* Output Validation
* Content Filtering
* Schema Validation
* Tool Permissions
* PII Protection
* Human Approval

**File:** `80_AI_Guardrails.md`

---

## 81. AI Safety

* Prompt Injection
* Jailbreaking
* Data Leakage
* Hallucination
* Bias
* Toxicity
* Privacy
* Unauthorized Tool Usage

**File:** `81_AI_Safety.md`

---

## 82. LLM Evaluation

* Correctness
* Relevance
* Faithfulness
* Groundedness
* Safety
* Hallucination
* LLM-as-a-Judge
* Human Evaluation

**File:** `82_LLM_Evaluation.md`

---

## 83. AI Monitoring

Monitor:

* Latency
* Token Usage
* Cost
* Error Rate
* Hallucination
* Retrieval Quality
* Model Quality
* User Feedback

**File:** `83_AI_Monitoring.md`

---

## 84. LLMOps

* Prompt Versioning
* Model Versioning
* Experiment Tracking
* Evaluation
* Tracing
* Monitoring
* Cost Tracking
* Feedback Loop

**File:** `84_LLMOps.md`

---

## 85. AI Deployment

* FastAPI
* REST API
* Docker
* Model Serving
* GPU Inference
* Authentication
* Scaling
* CI/CD

**File:** `85_AI_Deployment.md`

---

## 86. Inference Optimization

* Quantization
* Batching
* Caching
* KV Cache
* Streaming
* Smaller Models
* Model Routing
* Speculative Decoding

**File:** `86_Inference_Optimization.md`

---

## 87. Cost & Latency Optimization

```text
Quality
   ↕
Latency
   ↕
Cost
```

Learn:

* Model Selection
* Prompt Optimization
* Token Optimization
* Caching
* Batching
* Quantization
* Efficient Retrieval
* Model Routing

**File:** `87_Cost_Latency_Optimization.md`

---

# 🟦 Phase 15 — Cloud AI

## 88. Azure AI

Important:

* Azure OpenAI
* Azure AI Foundry
* Azure AI Search
* Azure Machine Learning
* Azure Storage
* Azure AI Services

**File:** `88_Azure_AI.md`

---

## 89. AWS Generative AI

Important:

* Amazon Bedrock
* Bedrock Agents
* SageMaker
* S3
* Lambda
* CloudWatch

**File:** `89_AWS_Generative_AI.md`

---

## 90. GCP Generative AI

Important:

* Vertex AI
* Gemini
* BigQuery
* Cloud Storage

**File:** `90_GCP_Generative_AI.md`

---

# 🟦 Phase 16 — Interview Preparation

## 91. Deep Learning Interview Questions

Cover:

* Neural Networks
* Backpropagation
* Activation Functions
* Loss Functions
* Optimizers
* CNN
* RNN
* LSTM
* GRU
* Attention
* Transformers

**File:** `91_Deep_Learning_Interview_Questions.md`

---

## 92. GenAI Interview Questions

Cover:

* LLMs
* Prompt Engineering
* Embeddings
* Vector DB
* RAG
* Fine-Tuning
* LoRA
* Agents
* MCP
* LLMOps

**File:** `92_GenAI_Interview_Questions.md`

---

## 93. RAG Interview Questions

Focus on:

* RAG Architecture
* Chunking
* Embeddings
* Retrieval
* Hybrid Search
* Reranking
* Advanced RAG
* RAG Evaluation
* RAG vs Fine-Tuning

**File:** `93_RAG_Interview_Questions.md`

---

## 94. LLM Interview Questions

* Transformer
* Tokenization
* Context Window
* Pretraining
* Fine-Tuning
* RLHF
* DPO
* Inference
* Hallucination
* Quantization

**File:** `94_LLM_Interview_Questions.md`

---

## 95. AI Agent Interview Questions

* Agents
* ReAct
* Tool Calling
* Memory
* Planning
* Agentic AI
* MCP
* Multi-Agent Systems

**File:** `95_AI_Agent_Interview_Questions.md`

---

## 96. AI System Design Interview

Practice designing:

* Enterprise RAG
* Document Q&A
* AI Chatbot
* Recommendation System
* AI Search
* Agentic Workflow
* Multi-Agent System
* LLM Application

**File:** `96_AI_System_Design_Interview.md`

---

## 97. End-to-End AI Project

Build at least one complete project:

```text
Business Problem
       ↓
Data
       ↓
Data Processing
       ↓
Embedding
       ↓
Vector DB
       ↓
RAG / Agent
       ↓
LLM
       ↓
Guardrails
       ↓
FastAPI
       ↓
Docker
       ↓
Cloud
       ↓
Monitoring
```

**File:** `97_End_to_End_AI_Project.md`

---

# ⭐ Priority Levels

## 🔴 Tier 1 — Must Master

```text
Neural Networks
Backpropagation
Gradient Descent
Activation Functions
Loss Functions
Optimizers
Regularization

CNN
RNN
LSTM
GRU

Attention
Self-Attention
Transformers

BERT
GPT
LLM Fundamentals

Prompt Engineering
Embeddings
Vector Databases

RAG
Advanced RAG
Hybrid Search
Reranking
RAG Evaluation

Fine-Tuning
SFT
PEFT
LoRA
QLoRA

AI Agents
ReAct
Tool Calling
MCP

LLM Evaluation
AI System Design
LLMOps
Deployment
```

---

# 🟠 Tier 2 — Important

```text
Transfer Learning
LeNet
AlexNet
VGG
Inception
ResNet
EfficientNet

Seq2Seq
Encoder-Decoder

RoBERTa
T5

GAN
VAE
Diffusion Models

Quantization
Knowledge Distillation

Hugging Face
LangChain
LlamaIndex
LangGraph

Multi-Agent Systems
Graph RAG
Agentic RAG

Guardrails
AI Safety
AI Monitoring
Cloud AI
```

---

# 🟢 Tier 3 — Conceptual

```text
Advanced CNN Architectures
Advanced GAN Architectures
Advanced Diffusion Architectures
Distributed Training
GPU Architecture
Advanced RL
Research-Level LLM Architectures
```

---

# 🎯 Interview Preparation Strategy

For every topic, prepare these **8 questions**:

```text
1. What is it?
2. Why do we need it?
3. How does it work?
4. What is the architecture?
5. What are the important parameters?
6. What are the advantages and limitations?
7. When would you use it?
8. How is it different from alternatives?
```

For important models, additionally prepare:

```text
Architecture
↓
Mathematical Intuition
↓
Training
↓
Inference
↓
Advantages
↓
Limitations
↓
Real-world Use Case
↓
Python Implementation
↓
Interview Questions
```

---

# 🏆 Final Job-Oriented Path

```text
                DEEP LEARNING
                     │
                     ↓
              Neural Networks
                     │
             ┌───────┴───────┐
             ↓               ↓
            CNN          RNN/LSTM/GRU
             │               │
             └───────┬───────┘
                     ↓
                 Attention
                     ↓
                Transformers
                     ↓
              BERT / GPT
                     ↓
                    LLM
                     ↓
              Generative AI
                     ↓
           Prompt Engineering
                     ↓
                 Embeddings
                     ↓
              Vector Database
                     ↓
                    RAG
                     ↓
               Advanced RAG
                     ↓
               Fine-Tuning
                     ↓
               LoRA / QLoRA
                     ↓
                 AI Agents
                     ↓
               Tool Calling
                     ↓
                    MCP
                     ↓
              Agentic AI
                     ↓
             AI System Design
                     ↓
          Deployment / LLMOps
                     ↓
              Cloud / Production
                     ↓
             Interview Questions
                     ↓
                    JOB
```

## 🎯 End Goal

```text
Data Scientist
      +
Deep Learning
      +
NLP
      +
Transformers
      +
LLMs
      +
Generative AI
      +
RAG
      +
Fine-Tuning
      +
AI Agents
      +
MCP
      +
AI System Design
      +
Cloud / Deployment
      =
Job-Ready AI / GenAI Data Scientist
```
