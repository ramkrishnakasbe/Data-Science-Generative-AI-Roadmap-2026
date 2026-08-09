# AI — Interview Preparation Roadmap

> **Goal:** Build job-ready AI knowledge from fundamentals to advanced **Generative AI, RAG, LLMs, and AI Agents**.

---

## 📁 AI Roadmap

```text
AI/
│
├── README.md
│
├── 01_AI_Fundamentals.md
├── 02_Mathematics_for_AI.md
├── 03_Machine_Learning_for_AI.md
├── 04_Deep_Learning_Fundamentals.md
├── 05_NLP_Fundamentals.md
│
├── 06_Neural_Networks.md
├── 07_CNN.md
├── 08_RNN_LSTM_GRU.md
├── 09_Attention_Mechanism.md
├── 10_Transformers.md
│
├── 11_LLM_Fundamentals.md
├── 12_Generative_AI_Fundamentals.md
├── 13_Prompt_Engineering.md
├── 14_Embeddings.md
├── 15_Vector_Databases.md
│
├── 16_RAG_Fundamentals.md
├── 17_Advanced_RAG.md
├── 18_RAG_Evaluation.md
├── 19_LangChain.md
├── 20_LlamaIndex.md
│
├── 21_Fine_Tuning.md
├── 22_PEFT_LoRA_QLoRA.md
├── 23_Model_Quantization.md
├── 24_Hugging_Face.md
│
├── 25_AI_Agents.md
├── 26_Agentic_AI.md
├── 27_Tool_Calling.md
├── 28_MCP.md
├── 29_Multi_Agent_Systems.md
│
├── 30_Generative_AI_Architecture.md
├── 31_AI_Guardrails.md
├── 32_AI_Safety.md
├── 33_LLM_Evaluation.md
│
├── 34_AI_Deployment.md
├── 35_LLMOps.md
├── 36_MLOps_for_AI.md
├── 37_AI_Monitoring.md
├── 38_AI_Cost_Latency_Optimization.md
│
├── 39_Azure_AI.md
├── 40_AWS_Generative_AI.md
├── 41_GCP_Generative_AI.md
│
├── 42_GenAI_Project_Architecture.md
├── 43_GenAI_Interview_Questions.md
└── 44_GenAI_End_to_End_Project.md
```

---

# 1. AI Fundamentals

```text
AI
 ↓
Types of AI
 ↓
AI vs ML vs DL
 ↓
Supervised / Unsupervised / Reinforcement Learning
 ↓
Training / Validation / Testing
 ↓
Model Evaluation
 ↓
Overfitting / Underfitting
```

**File:** `01_AI_Fundamentals.md`

---

# 2. Mathematics for AI

```text
Linear Algebra
Probability
Statistics
Calculus
Optimization
```

**File:** `02_Mathematics_for_AI.md`

---

# 3. Machine Learning for AI

```text
Regression
Classification
Clustering
Feature Engineering
Feature Selection
Model Evaluation
Ensemble Learning
Hyperparameter Tuning
```

**File:** `03_Machine_Learning_for_AI.md`

---

# 4. Deep Learning

```text
Neural Networks
 ↓
Backpropagation
 ↓
Optimization
 ↓
CNN
 ↓
RNN
 ↓
LSTM / GRU
 ↓
Attention
 ↓
Transformers
```

**Files:** `04` → `10`

---

# 5. NLP Fundamentals

```text
Text Preprocessing
 ↓
Tokenization
 ↓
N-Grams
 ↓
TF-IDF
 ↓
Word Embeddings
 ↓
Semantic Similarity
 ↓
Attention
 ↓
Transformers
```

**File:** `05_NLP_Fundamentals.md`

---

# 6. Transformers

```text
Encoder
Decoder
Self-Attention
Multi-Head Attention
Positional Encoding
Feed Forward Network
Layer Normalization
Residual Connections
```

**File:** `10_Transformers.md`

---

# 7. LLM Fundamentals

```text
LLM
 ↓
Tokens
 ↓
Tokenization
 ↓
Embeddings
 ↓
Transformer
 ↓
Pretraining
 ↓
Instruction Tuning
 ↓
Alignment
 ↓
Inference
```

**File:** `11_LLM_Fundamentals.md`

---

# 8. Generative AI

```text
Generative AI
│
├── LLMs
├── Diffusion Models
├── GANs
├── VAEs
└── Multimodal AI
```

Focus primarily on:

```text
LLMs
Text Generation
Image Generation
Multimodal Models
Foundation Models
```

**File:** `12_Generative_AI_Fundamentals.md`

---

# 9. Prompt Engineering

```text
Zero-Shot
Few-Shot
Role Prompting
System Prompts
Chain-of-Thought
Structured Output
Prompt Templates
Prompt Chaining
Function / Tool Calling
```

**File:** `13_Prompt_Engineering.md`

---

# 10. Embeddings

```text
Text
 ↓
Embedding Model
 ↓
Vector
 ↓
Similarity Search
```

Learn:

```text
Dense Embeddings
Semantic Similarity
Cosine Similarity
Embedding Models
Chunk Embeddings
Query Embeddings
```

**File:** `14_Embeddings.md`

---

# 11. Vector Databases

```text
Documents
 ↓
Chunking
 ↓
Embeddings
 ↓
Vector Database
 ↓
Similarity Search
```

Learn:

```text
FAISS
Pinecone
Chroma
Weaviate
Milvus
pgvector
```

**File:** `15_Vector_Databases.md`

---

# 12. RAG

```text
Documents
 ↓
Load
 ↓
Clean
 ↓
Chunk
 ↓
Embed
 ↓
Store
 ↓
Retrieve
 ↓
Augment Prompt
 ↓
LLM
 ↓
Answer
```

**File:** `16_RAG_Fundamentals.md`

---

# 13. Advanced RAG

```text
Naive RAG
 ↓
Hybrid Search
 ↓
Metadata Filtering
 ↓
Query Rewriting
 ↓
Query Expansion
 ↓
Reranking
 ↓
Context Compression
 ↓
Multi-Query Retrieval
 ↓
Parent-Child Retrieval
 ↓
Graph RAG
 ↓
Agentic RAG
```

**File:** `17_Advanced_RAG.md`

---

# 14. RAG Evaluation

```text
Retrieval Evaluation
 ↓
Context Relevance
 ↓
Context Recall
 ↓
Answer Relevance
 ↓
Faithfulness
 ↓
Groundedness
```

Tools:

```text
RAGAS
DeepEval
LangSmith
```

**File:** `18_RAG_Evaluation.md`

---

# 15. LLM Frameworks

```text
LangChain
LlamaIndex
Hugging Face
LangGraph
```

Focus on:

```text
Chains
Retrievers
Tools
Agents
Memory
Document Loaders
Vector Stores
Callbacks
Tracing
```

**Files:** `19_LangChain.md`, `20_LlamaIndex.md`

---

# 16. Fine-Tuning

```text
Pretrained Model
 ↓
Dataset
 ↓
Fine-Tuning
 ↓
Evaluation
 ↓
Deployment
```

Learn:

```text
Full Fine-Tuning
Instruction Tuning
Supervised Fine-Tuning
PEFT
LoRA
QLoRA
```

**Files:** `21` → `22`

---

# 17. Model Optimization

```text
Quantization
Pruning
Distillation
Caching
Batching
Speculative Decoding
```

Focus on:

```text
FP32
FP16
BF16
INT8
INT4
```

**File:** `23_Model_Quantization.md`

---

# 18. Hugging Face

Learn:

```text
Transformers
Datasets
Tokenizers
Model Hub
Pipelines
PEFT
```

**File:** `24_Hugging_Face.md`

---

# 19. AI Agents

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
 ↓
Final Answer
```

Learn:

```text
Agent
Tool
Memory
Planning
Reasoning
Tool Calling
Agent Loops
```

**File:** `25_AI_Agents.md`

---

# 20. Agentic AI

```text
Simple LLM
 ↓
LLM + Tools
 ↓
Single Agent
 ↓
Agentic Workflow
 ↓
Multi-Agent System
```

**File:** `26_Agentic_AI.md`

---

# 21. Tool Calling

```text
User
 ↓
LLM
 ↓
Tool Selection
 ↓
Function Call
 ↓
Tool Result
 ↓
LLM
 ↓
Final Response
```

**File:** `27_Tool_Calling.md`

---

# 22. MCP

Learn:

```text
Model Context Protocol
 ↓
MCP Client
 ↓
MCP Server
 ↓
Tools
Resources
Prompts
```

Focus on practical MCP architecture and integration.

**File:** `28_MCP.md`

---

# 23. Multi-Agent Systems

```text
Supervisor Agent
       ↓
 ┌─────┼─────┐
 ↓     ↓     ↓
Agent Agent Agent
 ↓     ↓     ↓
 └─────┼─────┘
       ↓
Final Result
```

**File:** `29_Multi_Agent_Systems.md`

---

# 24. GenAI Architecture

Learn end-to-end architecture:

```text
User
 ↓
Application
 ↓
API
 ↓
LLM / RAG / Agent
 ↓
Vector DB
 ↓
Tools / APIs
 ↓
Response
 ↓
Monitoring
```

**File:** `30_Generative_AI_Architecture.md`

---

# 25. AI Safety & Guardrails

```text
Prompt Injection
Jailbreaking
Data Leakage
Hallucination
Toxicity
PII
Unauthorized Tool Usage
```

Guardrails:

```text
Input Validation
Output Validation
Content Filtering
Access Control
Human-in-the-Loop
```

**Files:** `31` → `32`

---

# 26. LLM Evaluation

Learn:

```text
Accuracy
Relevance
Faithfulness
Groundedness
Toxicity
Bias
Hallucination
Latency
Cost
```

**File:** `33_LLM_Evaluation.md`

---

# 27. AI Deployment

```text
Model
 ↓
API
 ↓
Container
 ↓
Cloud
 ↓
Monitoring
```

Learn:

```text
FastAPI
Docker
REST APIs
CI/CD
Model Serving
GPU Inference
```

**File:** `34_AI_Deployment.md`

---

# 28. LLMOps

```text
Data
 ↓
Prompt
 ↓
Model
 ↓
Evaluation
 ↓
Deployment
 ↓
Monitoring
 ↓
Feedback
 ↓
Improvement
```

Focus on:

```text
Prompt Versioning
Model Versioning
Tracing
Evaluation
Monitoring
Cost Tracking
Latency
Caching
```

**File:** `35_LLMOps.md`

---

# 29. AI Monitoring

Monitor:

```text
Latency
Token Usage
Cost
Errors
Hallucination
Retrieval Quality
Model Performance
Drift
```

**File:** `37_AI_Monitoring.md`

---

# 30. Cost & Latency Optimization

```text
Model Selection
 ↓
Prompt Optimization
 ↓
Caching
 ↓
Batching
 ↓
Quantization
 ↓
Smaller Models
 ↓
Efficient Retrieval
```

**File:** `38_AI_Cost_Latency_Optimization.md`

---

# 31. Cloud AI

## Azure

```text
Azure OpenAI
Azure AI Foundry
Azure AI Search
Azure Machine Learning
Azure Storage
```

**File:** `39_Azure_AI.md`

## AWS

```text
Amazon Bedrock
Amazon SageMaker
Amazon S3
AWS Lambda
Bedrock Agents
```

**File:** `40_AWS_Generative_AI.md`

## GCP

```text
Vertex AI
Gemini
BigQuery
Cloud Storage
```

**File:** `41_GCP_Generative_AI.md`

---

# 32. End-to-End GenAI Project

Build at least one production-style project:

```text
User
 ↓
Frontend / API
 ↓
Authentication
 ↓
RAG Pipeline
 ↓
Embedding Model
 ↓
Vector DB
 ↓
Retriever
 ↓
Reranker
 ↓
LLM
 ↓
Guardrails
 ↓
Response
 ↓
Monitoring
```

**File:** `44_GenAI_End_to_End_Project.md`

---

# 33. Priority Order

## 🔴 Must Know

```text
AI Fundamentals
ML Fundamentals
Deep Learning
NLP
Transformers
LLMs
Generative AI
Prompt Engineering
Embeddings
Vector Databases
RAG
Advanced RAG
LLM Evaluation
LangChain
AI Agents
Tool Calling
MCP
Deployment
LLMOps
```

## 🟠 Important

```text
Fine-Tuning
LoRA
QLoRA
Quantization
Hugging Face
LlamaIndex
Guardrails
AI Safety
Multi-Agent Systems
Cloud AI
Cost Optimization
```

## 🟢 Advanced

```text
Graph RAG
Agentic RAG
Advanced Agent Architectures
Multimodal AI
Model Distillation
Inference Optimization
Distributed LLM Serving
Advanced LLMOps
```

---

# 34. Final Roadmap

```text
AI Fundamentals
       ↓
Machine Learning
       ↓
Deep Learning
       ↓
NLP
       ↓
Transformers
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
RAG Evaluation
       ↓
Fine-Tuning
       ↓
LLMOps
       ↓
AI Agents
       ↓
Agentic AI
       ↓
Tool Calling
       ↓
MCP
       ↓
Multi-Agent Systems
       ↓
AI Safety / Guardrails
       ↓
Deployment
       ↓
Cloud AI
       ↓
Production GenAI Project
       ↓
Interview Preparation
```

---

## 🎯 Job-Ready Target

```text
Data Scientist
      +
ML / DL
      +
LLMs
      +
RAG
      +
Vector DB
      +
Prompt Engineering
      +
Agents
      +
MCP
      +
Cloud
      +
Deployment
      +
LLMOps
      =
AI / GenAI Data Scientist
```
