Embeddings — Complete Interview Notes for Data Science / ML / GenAI Engineer

Purpose: Interview-ready notes covering embedding fundamentals, mathematical intuition, NLP embeddings, sentence/document embeddings, Transformer embeddings, vector similarity, vector databases, RAG, evaluation, practical implementation, and common interview questions.

1. What is an Embedding?

An embedding is a numerical representation of an object such as:

Word
Sentence
Paragraph
Document
Image
Product
User
Audio
Query

The goal is to represent an object as a vector in a continuous numerical space where semantically similar objects are located closer together.

For example:

"king"
"queen"
"man"
"woman"
"car"
"banana"

can be represented as vectors:

king   → [0.21, -0.44, 0.72, ..., 0.18]
queen  → [0.25, -0.40, 0.69, ..., 0.21]
car    → [-0.81, 0.12, 0.03, ..., -0.55]
banana → [0.63, 0.77, -0.21, ..., 0.42]

The actual values have no direct human-readable meaning individually.

What matters is the relationship between vectors.

2. Simple Intuition

Suppose we have:

Dog
Cat
Apple
Car

An embedding model might map them into a vector space:

              Animal
                ↑
                |
        Dog ●   |   ● Cat
                |
                |
----------------+----------------→
                |
       Apple ●  |       ● Car
                |

The exact geometry depends on the embedding model and training objective.

The important idea:

Similar meanings tend to produce similar vector representations.

3. Why Do We Need Embeddings?

Computers cannot directly reason over raw text like humans.

Consider:

"I love machine learning"

A machine learning model needs numerical input.

One simple representation is:

[0, 1, 0, 0, 1, ...]

But simple representations such as one-hot encoding do not capture semantic relationships.

Embeddings provide dense numerical representations.

"I love machine learning"
          ↓
Embedding model
          ↓
[0.21, -0.42, 0.18, 0.77, ...]

This representation can then be used by ML systems.

4. One-Hot Encoding vs Embedding

Suppose vocabulary:

["cat", "dog", "car", "apple"]

One-hot encoding:

cat   → [1,0,0,0]
dog   → [0,1,0,0]
car   → [0,0,1,0]
apple → [0,0,0,1]

Every word is equally distant from every other word under ordinary Euclidean distance.

For example:

cat → [1,0,0,0]
dog → [0,1,0,0]

and:

cat → [1,0,0,0]
car → [0,0,1,0]

have the same Euclidean distance.

The representation does not naturally encode:

cat ≈ dog

Embedding:

cat → [0.21, 0.45, -0.11, 0.73]
dog → [0.23, 0.48, -0.08, 0.69]
car → [-0.72, 0.12, 0.64, -0.31]

Now similarity can be represented geometrically.

5. Sparse vs Dense Representation
One-hot

Usually:

[0, 0, 0, 0, 0, 0, 1, 0, 0, ...]

This is:

Sparse
High-dimensional
Mostly zeros
Embedding

Usually:

[0.21, -0.42, 0.73, 0.18, ...]

This is:

Dense
Lower-dimensional
Information-rich
6. What Does an Embedding Dimension Mean?

Suppose an embedding has dimension:

768

Then each object is represented as:

$$ \mathbf{x}\in\mathbb{R}^{768} $$

Example:

"machine learning"
        ↓
[0.13, -0.44, 0.21, ..., 0.72]

There are 768 numerical values.

Important:

A dimension does not necessarily correspond to one interpretable concept such as "animalness" or "sentiment."

The representation is usually distributed across dimensions.

7. Embedding Space

An embedding model maps an object into a vector space.

Mathematically:

$$ f(x)=\mathbf{v} $$

where:

$x$ = input
$f$ = embedding model
$\mathbf{v}$ = vector representation

For example:

$$ f(\text{"machine learning"})= [0.21,-0.43,0.71,\ldots] $$

The model tries to organize the space so that useful relationships are reflected in vector relationships.

8. Semantic Similarity

Consider:

Query:
"How can I reset my password?"

Documents:

A:
"Password reset instructions"

B:
"How to update your profile photo"

C:
"Machine learning tutorial"

A good semantic embedding model should produce:

similarity(query, A) → high

similarity(query, B) → lower

similarity(query, C) → very low

This is the foundation of:

Semantic search
RAG
Recommendation systems
Duplicate detection
Clustering
Classification
9. Vector Similarity

Once text is converted into vectors, we need a way to measure similarity.

Common metrics:

Cosine similarity
Dot product
Euclidean distance
10. Cosine Similarity

Cosine similarity measures the angle between two vectors.

For vectors $\mathbf{A}$ and $\mathbf{B}$:

$$ \text{cosine\_similarity}(A,B) = \frac{A\cdot B} {\|A\|\|B\|} $$

where:

$$ A\cdot B=\sum_{i=1}^{n}A_iB_i $$

and:

$$ \|A\|=\sqrt{\sum_{i=1}^{n}A_i^2} $$
11. Cosine Similarity Intuition

Consider:

A → ↗
B → ↗

They point in similar directions.

Cosine similarity is high.

If:

A → ↗

B → ↘

they point in different directions.

Similarity is lower or negative.

The key idea:

Cosine similarity focuses on the angle between vectors rather than their absolute magnitude.

12. Cosine Similarity Range

For general real-valued vectors:

$$ -1 \leq \cos(\theta)\leq1 $$

Interpretation:

+1 → same direction
 0 → orthogonal
-1 → opposite direction

In many modern text embedding applications, similarities often occupy a narrower practical range, so a fixed threshold should not be assumed universally.

13. Example of Cosine Similarity

Suppose:

$$ A=[1,2] $$ $$ B=[2,4] $$

Calculate dot product:

$$ A\cdot B=(1)(2)+(2)(4) $$ $$ =2+8=10 $$

Magnitudes:

$$ \|A\|=\sqrt{1^2+2^2}=\sqrt5 $$ $$ \|B\|=\sqrt{2^2+4^2}=\sqrt{20} $$

Therefore:

$$ \cos(A,B)= \frac{10}{\sqrt5\sqrt{20}} $$ $$ =1 $$

Because $B$ is a scaled version of $A$, they point in exactly the same direction.

14. Dot Product Similarity

Dot product:

$$ A\cdot B= \sum_{i=1}^{n}A_iB_i $$

It considers both:

Direction
Magnitude

If vectors are normalized:

$$ \|A\|=\|B\|=1 $$

then:

$$ A\cdot B=\cos(A,B) $$

This is why normalized embeddings can make cosine similarity and inner-product search equivalent.

15. Euclidean Distance

Euclidean distance:

$$ d(A,B) = \sqrt{ \sum_{i=1}^{n}(A_i-B_i)^2 } $$

Smaller distance means vectors are closer.

For example:

A = [1,2]
B = [1,3]

Then:

$$ d(A,B)=\sqrt{(1-1)^2+(2-3)^2} $$ $$ =1 $$
16. Cosine vs Euclidean vs Dot Product
Metric	Main idea	Magnitude-sensitive?
Cosine similarity	Angle	Mostly no
Dot product	Alignment + magnitude	Yes
Euclidean distance	Straight-line distance	Yes

For semantic text search, cosine similarity is common, but the correct metric depends on the embedding model and retrieval system.

17. How Are Embeddings Created?

There are two broad approaches:

Text
 ↓
Embedding Model
 ↓
Vector

Embedding models can be trained using objectives designed to capture:

Word context
Sentence similarity
Semantic relationships
Query-document relevance
Contrastive relationships

Examples of embedding approaches:

Word2Vec
GloVe
FastText
Transformer-based embeddings
Sentence Transformers
Modern API-based embedding models
18. Word Embeddings

Word embeddings represent individual words.

Examples:

Word2Vec
GloVe
FastText

Example:

king → vector
queen → vector
man → vector
woman → vector

The embedding captures relationships learned from text.

19. Word2Vec

Word2Vec is a neural embedding approach introduced by researchers at Google.

It learns word representations from surrounding context.

Two main architectures:

CBOW
Skip-gram
20. CBOW

CBOW = Continuous Bag of Words

It predicts a target word from surrounding words.

Example:

"The cat ___ on the mat."

Context:

"The cat"
"on the mat"

Target:

sat

Conceptually:

Context words
     ↓
   CBOW
     ↓
Target word
21. Skip-Gram

Skip-gram works in the opposite direction.

It uses a target word to predict surrounding context words.

Example:

"The cat sat on the mat"

Target:

cat

Context:

the
sat

Conceptually:

Target word
     ↓
 Skip-Gram
     ↓
Context words
22. CBOW vs Skip-Gram
Feature	CBOW	Skip-Gram
Input	Context words	Target word
Predicts	Target	Context
Training	Generally faster	Generally slower
Rare words	Often weaker	Often useful
Architecture	Context → target	Target → context
23. GloVe

GloVe = Global Vectors for Word Representation.

It learns word vectors using global word co-occurrence statistics.

Core idea:

Words that occur in similar contexts tend to have similar representations.

For example:

doctor
nurse
hospital
patient

may have related embeddings because of contextual co-occurrence patterns.

24. FastText

FastText extends word embeddings by representing words using character n-grams.

Example:

playing

can be represented using subword pieces.

This helps with:

Rare words
Unknown words
Morphologically rich languages
Misspellings to some extent

FastText can therefore be useful when word morphology matters.

25. Static Embeddings

Word2Vec, GloVe, and traditional FastText embeddings are generally considered static embeddings.

A word gets approximately one learned vector regardless of its sentence context.

Example:

bank

in:

"I deposited money in the bank."

and:

"I sat near the river bank."

may receive the same base word embedding.

This creates a major limitation.

26. Contextual Embeddings

Modern Transformer-based models generate representations influenced by context.

Consider:

"I deposited money in the bank."

versus:

"I sat near the river bank."

The representation of "bank" can differ based on surrounding words.

This is called a contextual representation.

Examples of models producing contextual representations include:

BERT
RoBERTa
DeBERTa
Transformer-based sentence embedding models
27. Static vs Contextual Embeddings
Feature	Static	Contextual
Example	Word2Vec	BERT
Word vector	Mostly fixed	Context-dependent
Polysemy	Weak	Stronger
Context awareness	Low	High
Modern NLP	Less common	Very common
28. Word Embedding vs Sentence Embedding
Word embedding

Represents a word/token.

"apple"
   ↓
vector
Sentence embedding

Represents an entire sentence.

"I like apples."
       ↓
    vector

Sentence embeddings are especially important for:

Semantic search
RAG
Clustering
Classification
Duplicate detection
29. Document Embedding

A document can also be represented as a vector.

Document
   ↓
Embedding Model
   ↓
Vector

Example:

Annual financial report
          ↓
[0.13, -0.22, 0.71, ...]

The vector captures semantic characteristics of the document.

For long documents, directly embedding the entire document may be inappropriate because of context limits and loss of retrieval granularity.

This is why RAG systems usually use chunk-level embeddings.

30. Query Embedding

In semantic search, the user's query is also converted into a vector.

User Query
    ↓
Embedding Model
    ↓
Query Vector

Documents are embedded beforehand:

Documents
    ↓
Embedding Model
    ↓
Document Vectors

Then:

Query Vector
     ↓
Similarity Search
     ↓
Top-k Documents
31. Embeddings in Semantic Search

Traditional keyword search:

Query:
"How do I change my password?"

Document:
"Instructions for resetting your account credentials"

Keyword matching may fail because:

change ≠ resetting
password ≠ credentials

Semantic search can recognize that the meanings are related.

Pipeline:

Query
 ↓
Embedding
 ↓
Query Vector
 ↓
Vector Search
 ↓
Relevant Chunks
32. Embeddings in RAG

RAG = Retrieval-Augmented Generation

Basic architecture:

                Documents
                    ↓
                 Chunking
                    ↓
               Embeddings
                    ↓
              Vector Database
                    │
                    │
User Query → Embedding
                    ↓
             Similarity Search
                    ↓
              Top-k Chunks
                    ↓
               LLM Prompt
                    ↓
                 Answer

Embeddings are responsible primarily for the retrieval layer.

33. RAG Example

Suppose company documents contain:

HR Policy
Leave Policy
Travel Policy
Insurance Policy
Procurement Policy

User asks:

"How many paid leaves can an employee take?"

Process:

Query
 ↓
Query embedding
 ↓
Vector search
 ↓
Leave Policy chunks
 ↓
Retrieved context
 ↓
LLM
 ↓
Answer

The LLM is not necessarily searching the database directly.

The retrieval system finds relevant chunks using vector similarity.

34. Why Chunking Matters

Suppose a 100-page PDF is embedded as one vector.

Problem:

One document
     ↓
One vector

A query about page 72 may retrieve the entire document, but retrieval becomes less precise.

Instead:

Document
   ↓
Chunk 1 → Vector 1
Chunk 2 → Vector 2
Chunk 3 → Vector 3
...
Chunk N → Vector N

Now retrieval can return specific relevant sections.

35. Chunk Size

Chunk size is an important RAG parameter.

Too small:

Context may become incomplete.
Important relationships may be lost.

Too large:

Retrieval becomes less precise.
More irrelevant text may enter the LLM context.
Token usage increases.

There is no universal best chunk size.

It depends on:

Document structure
Language
Query type
Embedding model
Retrieval strategy
LLM context window
36. Chunk Overlap

Suppose:

Chunk 1:
A B C D E

Chunk 2:
D E F G H

Here:

D E

is the overlap.

Why?

Because important information may cross chunk boundaries.

Overlap can help preserve contextual continuity.

37. Vector Database

A vector database stores embeddings and enables similarity search.

Examples:

FAISS
Pinecone
Weaviate
Milvus
Chroma
Qdrant
Elasticsearch/OpenSearch with vector capabilities
Azure AI Search with vector search

Typical stored record:

{
    "id": "chunk_001",
    "embedding": [...],
    "text": "...",
    "metadata": {
        "document": "HR_Policy.pdf",
        "page": 12
    }
}
38. Embedding Pipeline

A production embedding pipeline can look like:

Documents
    ↓
Extraction
    ↓
Cleaning
    ↓
Chunking
    ↓
Embedding Model
    ↓
Vector Generation
    ↓
Metadata
    ↓
Vector Database

Query pipeline:

User Query
    ↓
Query Embedding
    ↓
Vector Search
    ↓
Filtering
    ↓
Top-k
    ↓
Reranking
    ↓
LLM
39. Metadata Filtering

Vector similarity alone may not be enough.

Suppose a company has:

HR documents
Finance documents
Legal documents
Technical documents

User asks about:

Finance policy

You can combine semantic search with metadata filtering:

department = "Finance"

Then perform vector search only within matching records.

This is called filtered vector search.

40. Top-k Retrieval

Suppose:

Query → Vector

Search returns:

Chunk A → similarity 0.91
Chunk B → similarity 0.87
Chunk C → similarity 0.84
Chunk D → similarity 0.72
Chunk E → similarity 0.65

If:

k = 3

retrieve:

A
B
C

Choosing $k$ involves a precision-vs-context trade-off.

41. Similarity Threshold

Instead of always retrieving exactly $k$ results, you can also use a similarity threshold.

Example:

threshold = 0.80

Only results above the threshold are considered.

However:

Similarity scores are model- and dataset-dependent. A cosine score of 0.8 does not universally mean "80% semantic similarity."

Thresholds should be tuned using validation data.

42. Dense Retrieval

Embedding-based retrieval is often called dense retrieval.

Traditional keyword retrieval:

Sparse retrieval

Embedding retrieval:

Dense retrieval

Dense retrieval represents queries/documents as dense vectors.

43. Sparse vs Dense Retrieval
Feature	Sparse	Dense
Example	BM25	Embeddings
Based on	Terms	Semantic representation
Exact keyword matching	Strong	Can be weaker
Semantic matching	Limited	Strong
Vocabulary mismatch	Weak	Stronger
Interpretability	Higher	Lower
44. Hybrid Search

Hybrid search combines:

Keyword search
+
Vector search

Example:

BM25
   +
Dense embeddings
   ↓
Combined ranking

This is often powerful because:

Keyword search handles exact terms.
Vector search handles semantic similarity.

For example:

"GSTIN 27ABCDE..."

may benefit from lexical matching, while:

"How can I claim tax credit?"

may benefit strongly from semantic search.

45. Reranking

Initial vector retrieval may return:

Top 20 chunks

A reranker can examine:

Query + candidate document

and produce a better relevance ranking.

Pipeline:

Query
 ↓
Embedding retrieval
 ↓
Top 20
 ↓
Reranker
 ↓
Top 5
 ↓
LLM

This is commonly called retrieve-then-rerank.

46. Bi-Encoder vs Cross-Encoder
Bi-Encoder

Query and document are independently embedded.

Query → Encoder → Vector
Document → Encoder → Vector

Then similarity is calculated.

Advantage:

Documents can be embedded offline.
Very fast retrieval.
Cross-Encoder

The model receives query and document together.

Query + Document
       ↓
 Cross-Encoder
       ↓
 Relevance Score

Advantage:

Often stronger relevance judgment.

Disadvantage:

Computationally expensive for searching a huge corpus.

Therefore:

Bi-encoder → Retrieve candidates
Cross-encoder → Rerank candidates

is a common architecture.

47. Embedding Model Selection

Important factors:

Language support
Domain
Embedding dimension
Context length
Retrieval quality
Latency
Cost
Model licensing
Hosting requirements
Security/privacy
Infrastructure compatibility

For example:

General documents
     ↓
General embedding model

while:

Highly specialized scientific/legal/technical corpus
     ↓
Evaluate domain-specific or strong general-purpose models

Do not choose an embedding model only because its dimension is larger.

48. Does Higher Dimension Mean Better Embeddings?

No.

For example:

384 dimensions

is not automatically worse than:

1536 dimensions

Quality depends on:

Training objective
Training data
Architecture
Domain
Evaluation benchmark
Retrieval task

Higher dimensions can increase:

Memory usage
Storage
Search cost
49. Embedding Dimension and Storage

Suppose:

1,000,000 vectors

Each vector:

1536 dimensions

Using 32-bit floating point:

$$ 1536\times4 = 6144\text{ bytes} $$

Approximately:

$$ 6\text{ KB/vector} $$

For one million vectors:

$$ \approx 6.144\text{ GB} $$

This is before considering:

metadata
indexes
database overhead
replicas

Therefore embedding dimension matters in production.

50. Embedding Quantization

Quantization reduces the number of bits used to store vector values.

For example:

float32
 ↓
float16
 ↓
int8

Benefits:

Lower memory usage
Faster computation in some systems
Lower storage cost

Potential trade-off:

Retrieval quality may degrade

Quantization should be evaluated rather than assumed harmless.

51. ANN — Approximate Nearest Neighbor Search

Exact nearest-neighbor search compares a query vector with every stored vector.

For millions of vectors, this can be expensive.

Approximate Nearest Neighbor (ANN) algorithms trade a small amount of exactness for much faster retrieval.

Popular approaches:

HNSW
IVF
Product Quantization
ScaNN
52. HNSW

HNSW = Hierarchical Navigable Small World

It creates a graph structure that allows efficient approximate nearest-neighbor search.

Conceptually:

Query vector
     ↓
Graph traversal
     ↓
Nearby vectors
     ↓
Top-k results

HNSW is widely used in modern vector search systems.

53. IVF

IVF = Inverted File Index

It partitions vectors into clusters.

Conceptually:

Vectors
   ↓
Clusters
 ┌──┼──┬──┐
 C1 C2 C3 C4

When searching, the system can search only relevant clusters instead of every vector.

54. Embedding Normalization

Suppose:

$$ v=[3,4] $$

Magnitude:

$$ \|v\|=5 $$

Normalized vector:

$$ v'=\frac{v}{\|v\|} $$

Therefore:

$$ v'= \left[ \frac35,\frac45 \right] $$

or:

[0.6, 0.8]

Normalization can be useful when using cosine similarity or inner-product search.

55. Embeddings Are Not "Knowledge"

An embedding is a representation.

It is not equivalent to a database containing explicit facts.

For example:

Embedding:
[0.23, -0.44, ...]

does not mean:

Company revenue = ₹500 crore

The vector encodes learned statistical/semantic information.

In RAG:

Embedding → helps retrieve information
LLM → generates answer using retrieved context
56. Embeddings vs LLMs
Embedding model

Primary output:

Vector

Primary use:

Search
Retrieval
Similarity
Clustering
Recommendation
LLM

Primary output:

Generated text

Primary use:

Generation
Reasoning
Summarization
Extraction
Question answering
Agent workflows

An LLM can sometimes produce embeddings internally, but production systems often use dedicated embedding models for retrieval.

57. Embedding Model vs Generative Model
Feature	Embedding Model	Generative LLM
Main output	Vector	Text/tokens
Search	Excellent use case	Not primary
Retrieval	Excellent	Not primary
Generation	No	Yes
Similarity	Excellent	Not primary
RAG role	Retrieval	Answer generation
Cost per retrieval	Often lower	Often higher
58. Embeddings and Classification

Embeddings can be used as features.

Pipeline:

Text
 ↓
Embedding
 ↓
Vector
 ↓
Classifier
 ↓
Class

For example:

Customer complaint
      ↓
Embedding
      ↓
[vector]
      ↓
Logistic Regression
      ↓
Complaint Category

This can be effective when a strong pretrained embedding model is available.

59. Embeddings and Clustering

Suppose we have 10,000 customer reviews.

Pipeline:

Reviews
   ↓
Embeddings
   ↓
Vectors
   ↓
Clustering
   ↓
Customer themes

Algorithms:

K-Means
DBSCAN
HDBSCAN
Hierarchical clustering

Potential discovered clusters:

Delivery problems
Product quality
Pricing
Customer service
Payment issues
60. Embeddings and Recommendation Systems

Users and products can be represented as vectors.

User → vector
Product → vector

Similarity can identify products relevant to the user.

For example:

User vector
     ↓
Nearest product vectors
     ↓
Recommendations

Embedding-based recommendation is common in modern retrieval systems.

61. Embeddings and Duplicate Detection

Suppose:

Sentence A:
"I want to cancel my subscription."

Sentence B:
"How can I terminate my subscription?"

Keyword overlap may be limited.

Embedding similarity can identify them as semantically similar.

Pipeline:

Text A → Embedding A
Text B → Embedding B
             ↓
       Similarity Score
62. Embeddings for Semantic Deduplication

For a large dataset:

Documents
   ↓
Embeddings
   ↓
Nearest-neighbor search
   ↓
Similarity threshold
   ↓
Potential duplicates

Important:

A high embedding similarity does not necessarily prove two records are exact duplicates.

It indicates semantic similarity.

63. Embeddings and Multimodal AI

Embeddings are not limited to text.

Images can be embedded:

Image
 ↓
Vision Encoder
 ↓
Image Vector

Text can be embedded:

Text
 ↓
Text Encoder
 ↓
Text Vector

If both are mapped into a shared vector space, cross-modal retrieval becomes possible.

Example:

Text query
   ↓
Text embedding
   ↓
Search image embeddings
   ↓
Relevant images

This is a key idea in multimodal retrieval systems.

64. Embedding Alignment

For multimodal models, different modalities can be mapped into a shared embedding space.

Example:

Image → Vector ─┐
                ├→ Shared embedding space
Text  → Vector ─┘

Then:

"red sports car"

can be compared against image embeddings.

This enables:

Image-text retrieval
Zero-shot classification
Cross-modal search
65. Contrastive Learning

Many modern embedding models use contrastive learning ideas.

The goal is roughly:

Positive pairs
→ Pull together

Negative pairs
→ Push apart

Example:

Query:
"How to reset password?"

Positive:
"Password reset instructions"

Negative:
"Employee travel policy"

Training encourages:

$$ sim(Query,Positive) > sim(Query,Negative) $$

This helps create useful embedding spaces for retrieval.

66. Contrastive Loss Intuition

A simplified objective tries to increase similarity for positive pairs and decrease similarity for negative pairs.

For example:

$$ L = -\log \frac{ e^{sim(q,p)/\tau} }{ \sum_j e^{sim(q,d_j)/\tau} } $$

where:

$q$ = query
$p$ = positive document
$d_j$ = candidate documents
$\tau$ = temperature parameter
$sim$ = similarity function

You do not need to memorize every contrastive loss equation for most interviews, but you should understand the idea.

67. Temperature in Contrastive Learning

Temperature controls how strongly the model distinguishes similarity scores.

In:

$$ e^{sim(q,d)/\tau} $$

smaller $\tau$ makes the distribution sharper.

Larger $\tau$ makes it softer.

It is a hyperparameter used in many contrastive learning objectives.

68. Sentence Transformers

Sentence Transformers are models designed to produce meaningful sentence/paragraph embeddings.

Typical architecture:

Sentence
   ↓
Transformer
   ↓
Pooling
   ↓
Sentence embedding

A sentence can then be compared using:

cosine similarity
dot product
Euclidean distance

This architecture is widely useful for semantic search.

69. Pooling

Transformer models usually produce representations for multiple tokens.

For example:

[CLS] I like machine learning [SEP]

The model produces:

Token 1 → vector
Token 2 → vector
Token 3 → vector
...

To obtain one sentence vector, we need a pooling strategy.

Common methods:

Mean pooling
Max pooling
CLS pooling
Learned pooling
70. Mean Pooling

Suppose token embeddings are:

$$ h_1,h_2,\ldots,h_n $$

Mean pooling:

$$ v= \frac{1}{n} \sum_{i=1}^{n}h_i $$

This produces one vector representing the sequence.

When padding is present, a proper attention mask should be used so padding tokens do not distort the mean.

71. CLS Pooling

BERT-style models often contain a special [CLS] token.

Conceptually:

[CLS] sentence tokens [SEP]
  ↓
Transformer
  ↓
CLS representation
  ↓
Sentence representation

However, the raw CLS representation is not automatically the best semantic embedding for every retrieval task.

A model trained specifically for sentence embeddings may perform better.

72. Embedding Model Fine-Tuning

A pretrained embedding model can be fine-tuned for a domain.

Example:

General embedding model
          ↓
Company support data
          ↓
Fine-tuning
          ↓
Domain-specific embedding model

Potential benefits:

Better domain retrieval
Better terminology handling
Better query-document matching

Potential problems:

Overfitting
Catastrophic forgetting
Training complexity
Data quality requirements
73. Domain-Specific Embeddings

Suppose your company has:

SAP
Purchase Orders
Material Codes
Milk Procurement
Dairy Products
SKU
SMP
Butter
DORB

A generic embedding model may understand many concepts, but domain-specific evaluation can reveal retrieval weaknesses.

Fine-tuning or selecting a stronger domain-capable embedding model can improve performance.

74. Embedding Evaluation

Do not evaluate embeddings only by looking at vectors.

Evaluate them based on the downstream task.

For retrieval:

Recall@k
Precision@k
MRR
nDCG
Hit Rate

For semantic similarity:

Correlation with human similarity judgments

For RAG:

Context relevance
Context recall
Answer correctness
Faithfulness
75. Recall@k

Suppose:

Relevant documents = {A, B, C}

Retrieved top-5:

A, X, Y, B, Z

Relevant retrieved:

A, B

Then:

$$ Recall@5 = \frac{2}{3} $$

Recall@k answers:

How many of the relevant items were retrieved within the top $k$?

76. Precision@k

Precision@k answers:

How many of the retrieved top-$k$ results are relevant?

If:

Top 5:
A, X, Y, B, Z

and:

A and B are relevant

then:

$$ Precision@5= \frac{2}{5}=0.4 $$
77. MRR

MRR = Mean Reciprocal Rank

For one query:

$$ RR=\frac{1}{rank\ of\ first\ relevant\ result} $$

If the first relevant result is rank 2:

$$ RR=\frac12 $$

Across multiple queries:

$$ MRR= \frac{1}{N} \sum_{i=1}^{N}RR_i $$

MRR strongly rewards getting a relevant result near the top.

78. nDCG

nDCG = Normalized Discounted Cumulative Gain

It evaluates ranking quality while accounting for graded relevance.

Useful when:

Highly relevant
Relevant
Partially relevant
Irrelevant

are different categories.

The key interview idea:

nDCG evaluates not just whether relevant documents are retrieved, but how well they are ranked.

79. Embedding Drift

Embedding behavior can change when:

The underlying model changes
Data distribution changes
Domain terminology changes
Documents change significantly

If you change the embedding model, existing vectors usually need to be regenerated because vectors from different embedding spaces are generally not directly comparable.

Important:

Do not casually mix embeddings generated by incompatible models in the same vector index.

80. Changing an Embedding Model in Production

Suppose:

Old Model → 768 dimensions

is replaced by:

New Model → 1536 dimensions

You cannot simply insert the new vectors and expect the old and new vectors to behave consistently.

Typical migration:

New embedding model
        ↓
Re-embed documents
        ↓
Build new vector index
        ↓
Evaluate retrieval
        ↓
Switch production traffic

A version field can help:

embedding_model = "model_v2"
81. Embedding Caching

Embedding generation can be expensive for large corpora.

If the same content is embedded repeatedly, cache the result.

Example:

Document
   ↓
Hash
   ↓
Check cache
   ↓
Existing embedding?
   ├── Yes → Reuse
   └── No  → Generate → Store

This reduces:

API cost
Latency
Compute
82. Batch Embedding

Instead of embedding one document at a time:

Doc 1 → Model
Doc 2 → Model
Doc 3 → Model

use batches:

[Doc 1, Doc 2, Doc 3, ...]
            ↓
         Model
            ↓
       [Vectors]

Batching can improve throughput.

83. Embedding Pipeline for Millions of Documents

A production pipeline may look like:

Data Source
    ↓
Document Extraction
    ↓
Cleaning
    ↓
Chunking
    ↓
Deduplication
    ↓
Batch Embedding
    ↓
Validation
    ↓
Vector Index
    ↓
Metadata Store

Important production considerations:

Retry handling
Rate limits
API failures
Idempotency
Versioning
Monitoring
Batch size
Cost tracking
84. Embedding API Failure Handling

If using an external embedding API:

Document
   ↓
Embedding API
   ↓
Failure?
 ┌─┴─┐
No  Yes
│    ↓
Store Retry
     ↓
Retry limit
     ↓
Dead-letter/error queue

A production system should not silently lose documents when embedding generation fails.

85. RAG Retrieval Failure

Suppose the user asks:

"What is our maternity leave policy?"

But vector search returns:

Travel policy
Procurement policy
Security policy

Possible reasons:

Poor chunking
Weak embedding model
Query ambiguity
Metadata not used
Incorrect similarity metric
Poor indexing
Domain terminology mismatch
Insufficient retrieval depth

Do not immediately blame the LLM.

First inspect:

Query
 ↓
Embedding
 ↓
Retrieved chunks
 ↓
Similarity scores
 ↓
Reranking
 ↓
Prompt
 ↓
LLM
86. Embedding vs Keyword Search

Consider:

Query:
"How can I terminate my subscription?"

Document:

"Instructions for cancelling your membership."

Keyword matching may have weak overlap.

Embedding search can capture:

terminate ≈ cancel
subscription ≈ membership

This is one of the primary benefits of semantic search.

87. When Embeddings Can Fail

Embeddings are not magic.

Potential failure cases:

Exact identifiers
Invoice ID: INV-938472

Keyword/metadata search may be better.

Numbers
"₹4,52,381"

Semantic similarity may not reliably preserve exact numeric distinctions.

Negation
"Employee is eligible"

vs:

"Employee is not eligible"

Depending on the model, these can sometimes be surprisingly close.

Very similar documents

Small differences can be difficult to retrieve correctly.

Domain-specific terminology

Generic embeddings may not understand specialized vocabulary sufficiently.

88. Hybrid Retrieval for Better RAG

A strong production RAG system may use:

User Query
     ↓
 ┌───┴────────┐
 ↓            ↓
BM25       Embedding
 ↓            ↓
Keyword     Semantic
Search      Search
 └────┬───────┘
      ↓
  Fusion/Reranking
      ↓
 Relevant Chunks
      ↓
      LLM

This combines the strengths of lexical and semantic retrieval.

89. Reciprocal Rank Fusion

RRF can combine multiple ranked lists.

A common formulation:

$$ RRF(d)= \sum_{r\in R} \frac{1}{k+rank_r(d)} $$

where:

$d$ = document
$R$ = retrieval systems/rankings
$rank_r(d)$ = rank of document $d$ in ranking $r$
$k$ = smoothing constant

For example:

BM25 ranking
+
Vector ranking

can be combined using RRF.

90. Important Embedding Interview Question
Question:

"What is an embedding?"

Interview-ready answer:

An embedding is a dense numerical representation of an object such as text, image, or document in a continuous vector space. The embedding model learns a representation where relationships between vectors can capture useful semantic or task-specific relationships. Embeddings are commonly used for semantic search, retrieval, clustering, recommendation, classification, and RAG systems.

91. Interview Question: Why Use Embeddings in RAG?
Answer:

Embeddings allow documents and user queries to be represented in the same vector space. We can embed the user's query, perform similarity search against precomputed document or chunk embeddings, retrieve the most relevant context, and then provide that context to the LLM for answer generation.

92. Interview Question: Why Not Use Keyword Search?
Answer:

Keyword search is very strong for exact terms, identifiers, and lexical matching, but it can struggle when the query and document use different words with similar meanings. Embedding-based semantic search can capture semantic relationships. In production, I would often consider hybrid retrieval because keyword and semantic retrieval are complementary.

93. Interview Question: What Is Cosine Similarity?
Answer:

Cosine similarity measures the cosine of the angle between two vectors. It is calculated as the dot product divided by the product of their magnitudes.

$$ cos(A,B)= \frac{A\cdot B} {\|A\|\|B\|} $$

A larger value generally indicates that the vectors point in more similar directions.

94. Interview Question: Why Do We Normalize Embeddings?
Answer:

Normalization converts vectors to unit length. This is useful when cosine similarity is desired and can also make cosine similarity equivalent to dot-product similarity for normalized vectors. It can additionally make vector magnitudes less influential in similarity calculations.

95. Interview Question: What Is the Difference Between Word and Sentence Embeddings?
Answer:

Word embeddings represent individual words or tokens, while sentence embeddings represent an entire sentence or text span as a single vector. Sentence embeddings are especially useful for semantic search, clustering, duplicate detection, and retrieval because they represent the meaning of a larger text unit.

96. Interview Question: What Is a Contextual Embedding?
Answer:

A contextual embedding is a representation whose value depends on the surrounding context. For example, the representation of the word "bank" can differ between "river bank" and "bank account." Transformer-based models are widely used to create contextual representations.

97. Interview Question: What Is the Difference Between Word2Vec and BERT?
Answer:
Feature	Word2Vec	BERT
Type	Word embedding	Transformer
Context	Mostly static	Contextual
Representation	Word-level	Token/context representation
Architecture	Shallow neural embedding	Transformer encoder
Polysemy	Limited	Better
Typical use	Word similarity/features	NLP representations/tasks
98. Interview Question: What Is the Difference Between LLM and Embedding Model?
Answer:

An embedding model converts text or other inputs into vectors optimized for representation and similarity-related tasks. An LLM primarily generates or transforms tokens and can perform tasks such as reasoning, summarization, extraction, and question answering. In RAG, the embedding model is typically used for retrieval while the LLM is used for generation.

99. Interview Question: What Is a Vector Database?
Answer:

A vector database or vector-capable search system stores embeddings along with metadata and provides efficient similarity search, often using approximate nearest-neighbor indexes. It is commonly used in semantic search, recommendation systems, and RAG pipelines.

100. Interview Question: What Happens if I Change the Embedding Model?
Answer:

The new model creates vectors in a potentially different embedding space. Existing vectors generally should not be mixed directly with vectors from the new model. I would re-embed the corpus, build or migrate to a new index, evaluate retrieval quality, and then switch production traffic.

101. Interview Question: How Would You Improve a Poor RAG Retrieval System?

A structured debugging approach:

1. Check document extraction
        ↓
2. Check chunking
        ↓
3. Check embedding model
        ↓
4. Check query embedding
        ↓
5. Check similarity metric
        ↓
6. Check metadata filters
        ↓
7. Increase/reduce top-k
        ↓
8. Add reranking
        ↓
9. Consider hybrid search
        ↓
10. Evaluate Recall@k / MRR / nDCG

The key is to identify whether the problem is:

Data problem
Embedding problem
Retrieval problem
Reranking problem
Prompt problem
LLM generation problem
102. End-to-End RAG Example

Suppose a company has:

5000 PDF documents

Pipeline:

PDFs
 ↓
Text extraction
 ↓
Cleaning
 ↓
Chunking
 ↓
Embedding model
 ↓
Vector database

User:

"What is the policy for work-from-home?"

Query pipeline:

Question
 ↓
Query embedding
 ↓
Vector similarity search
 ↓
Top 20 chunks
 ↓
Metadata filtering
 ↓
Reranker
 ↓
Top 5 chunks
 ↓
Prompt construction
 ↓
LLM
 ↓
Answer

The embedding model handles the semantic retrieval component.

103. Production RAG Architecture
                  DOCUMENT PIPELINE
                         │
                         ▼
                  Document Sources
                         │
                         ▼
                  Text Extraction
                         │
                         ▼
                     Chunking
                         │
                         ▼
                  Embedding Model
                         │
                         ▼
                 Vector Database
                         │
                         │
                         │
User ──► Query ──► Embedding Model
                         │
                         ▼
                  Vector Retrieval
                         │
                         ▼
                 Metadata Filtering
                         │
                         ▼
                    Reranking
                         │
                         ▼
                 Context Selection
                         │
                         ▼
                    Prompt
                         │
                         ▼
                       LLM
                         │
                         ▼
                     Response
104. Embedding Security Considerations

Embeddings can represent information about the source data.

Production systems should consider:

Access control
Tenant isolation
Metadata security
Encryption
Data retention
PII handling
Sensitive documents
Permission-aware retrieval

For example:

User A
 ↓
Query
 ↓
Retriever
 ↓
Only documents User A is authorized to access

Do not rely only on semantic similarity to enforce authorization.

105. Multi-Tenant RAG

Suppose a SaaS application has:

Customer A
Customer B
Customer C

Each customer has private documents.

The vector store must prevent:

Customer A query
       ↓
Customer B document

Use metadata such as:

tenant_id

and apply authorization filters before returning results.

106. Embedding Cost

Embedding cost depends on factors such as:

Number of documents
Number of chunks
Tokens per chunk
Embedding model
API pricing
Re-embedding frequency

If:

1 million chunks

are embedded initially, the cost may be substantial.

Optimization strategies:

Deduplication
Caching
Batch processing
Incremental indexing
Avoid unnecessary re-embedding
107. Embedding Latency

Query latency:

Query
 ↓
Embedding generation
 ↓
Vector search
 ↓
Reranking
 ↓
LLM

Embedding latency is one component of total RAG latency.

Production monitoring should measure each stage separately:

embedding_latency
retrieval_latency
reranking_latency
llm_latency
total_latency
108. Embedding Quality vs Retrieval Quality

A powerful interview distinction:

A good embedding model is not necessarily sufficient for a good retrieval system.

Retrieval quality also depends on:

Chunking
Metadata
Index configuration
Similarity metric
Query formulation
Top-k
Reranking
Filtering
Document quality

Therefore:

Embedding quality
        ≠
End-to-end RAG quality
109. Embedding Evaluation Dataset

For a production RAG system, create evaluation examples:

Query
Expected relevant chunks
Expected documents

Example:

Query	Relevant Document
"What is the leave policy?"	HR Leave Policy
"How do I raise a purchase order?"	Procurement SOP
"What is the reimbursement limit?"	Travel Policy

Then calculate:

Recall@k
Precision@k
MRR
nDCG
110. Embedding Evaluation Example

Suppose:

100 test queries

For each query:

Expected relevant chunk

If top-5 retrieval finds the expected chunk for 92 queries:

$$ Recall@5= \frac{92}{100}=0.92 $$

So:

Recall@5 = 92%

This is more meaningful than saying:

"My embedding similarity score is 0.89."
111. Important Distinction: Similarity Score vs Accuracy

A similarity score such as:

0.87

is not the same as:

87% accuracy

Similarity is a mathematical measure between vectors.

Accuracy is an evaluation metric based on correct predictions.

Never say:

"Our embedding has 90% accuracy because cosine similarity is 0.90."

That is incorrect.

112. Embedding Dimensions and Model Trade-Off

Suppose:

Model A → 384 dimensions
Model B → 768 dimensions
Model C → 1536 dimensions

You should evaluate:

Retrieval quality
+
Latency
+
Memory
+
Storage
+
Cost

The best production model is not necessarily the model with the highest dimension.

113. Important Terms to Remember
Embedding

Dense vector representation.

Vector space

Numerical space containing embeddings.

Semantic similarity

Similarity based on meaning.

Cosine similarity

Angle-based similarity.

Vector database

System for storing/searching vectors.

Dense retrieval

Embedding-based retrieval.

Sparse retrieval

Keyword-based retrieval such as BM25.

Hybrid retrieval

Sparse + dense retrieval.

Reranker

Model that reorders retrieved candidates.

ANN

Approximate nearest-neighbor search.

HNSW

Graph-based ANN indexing method.

Chunking

Splitting documents into smaller pieces.

Contrastive learning

Learning to bring positive pairs closer and negative pairs farther apart.

114. Final Interview Cheat Sheet
EMBEDDING
    │
    ├── Numerical representation
    │
    ├── Dense vector
    │
    ├── Semantic relationships
    │
    ├── Similarity
    │      ├── Cosine
    │      ├── Dot Product
    │      └── Euclidean
    │
    ├── Applications
    │      ├── Semantic Search
    │      ├── RAG
    │      ├── Recommendation
    │      ├── Clustering
    │      └── Classification
    │
    └── Retrieval
           │
           ├── Dense Search
           ├── Sparse Search
           ├── Hybrid Search
           ├── Reranking
           └── ANN
115. Must-Know Questions for Data Scientist / ML Engineer / GenAI Engineer Interviews
What is an embedding?
Why do we need embeddings?
Embedding vs one-hot encoding?
Sparse vs dense representation?
What does embedding dimension mean?
What is an embedding space?
What is semantic similarity?
Explain cosine similarity mathematically.
Cosine similarity vs dot product?
Cosine similarity vs Euclidean distance?
Why normalize embeddings?
What is Word2Vec?
CBOW vs Skip-gram?
What is GloVe?
What is FastText?
Static vs contextual embeddings?
What is a contextual embedding?
Word embedding vs sentence embedding?
What is a document embedding?
What is mean pooling?
What is CLS pooling?
What is Sentence Transformer?
Why are embeddings used in RAG?
Explain the RAG embedding pipeline.
Why do we chunk documents?
What is chunk overlap?
What is a vector database?
What is dense retrieval?
What is sparse retrieval?
Dense vs sparse retrieval?
What is hybrid search?
What is reranking?
Bi-encoder vs cross-encoder?
What is ANN?
What is HNSW?
What is IVF?
How do you choose an embedding model?
Does higher embedding dimension mean better quality?
What happens if you change the embedding model?
How do you evaluate embedding quality?
What is Recall@k?
What is Precision@k?
What is MRR?
What is nDCG?
How do you debug poor RAG retrieval?
How can embeddings fail?
How do you handle exact IDs and numbers?
How do you implement metadata filtering?
How do you handle multi-tenant RAG?
How do you reduce embedding cost?
How do you reduce embedding latency?
What is embedding caching?
What is embedding normalization?
What is contrastive learning?
What is temperature in contrastive learning?
What is multimodal embedding?
How are embeddings used in recommendation systems?
How are embeddings used in clustering?
How are embeddings used in classification?
Embedding model vs LLM?
116. 30-Second Interview Answer

"An embedding is a dense numerical representation of data such as text, images, or documents in a vector space. The embedding model is trained so that useful relationships are represented by relationships between vectors. In GenAI applications, embeddings are especially important for semantic search and RAG. We convert documents into chunk-level vectors, store them in a vector database, convert the user's query into a vector, retrieve the most similar chunks using a metric such as cosine similarity or dot product, optionally rerank them, and provide the retrieved context to an LLM for generation."

117. One-Minute RAG + Embedding Explanation

"In a RAG system, I first extract and clean documents, split them into meaningful chunks, and generate an embedding for each chunk using an embedding model. I store those vectors along with metadata in a vector database. When a user submits a query, I generate its embedding using the same embedding model and perform similarity search against the document embeddings. I retrieve the top relevant chunks, optionally apply metadata filtering and a reranker, and then pass the selected context to the LLM. I evaluate the retrieval layer using metrics such as Recall@k, MRR, and nDCG, rather than relying only on raw similarity scores."

118. Final Mental Model

Remember this entire topic as:

TEXT
 ↓
EMBEDDING MODEL
 ↓
VECTOR
 ↓
VECTOR SPACE
 ↓
SIMILARITY
 ↓
RETRIEVAL
 ↓
RERANKING
 ↓
CONTEXT
 ↓
LLM
 ↓
ANSWER

For interviews:

Embedding
    ↓
Representation

Cosine / Dot Product
    ↓
Similarity

Vector DB
    ↓
Storage + Retrieval

ANN
    ↓
Fast Search

Hybrid Search
    ↓
Keyword + Semantic

Reranker
    ↓
Better Ordering

RAG
    ↓
Retrieve + Generate

Evaluation
    ↓
Recall@k / MRR / nDCG

Core principle:

Embeddings convert meaning into a numerical space so that machines can efficiently compare, retrieve, organize, and reason over representations of data.
