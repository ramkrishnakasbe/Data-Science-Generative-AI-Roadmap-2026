# Network Analysis

# Overview

Network Analysis (also known as **Graph Analysis**) is the study of relationships among entities using **graphs**. It helps analyze how objects are connected, how information flows, and which nodes are the most important within a network.

Unlike traditional tabular data, network data focuses on **relationships** rather than individual observations.

Network analysis combines concepts from **Graph Theory, Machine Learning, Statistics, and Data Mining**.

---

# Definition

A **network** is a collection of interconnected entities represented as a graph.

- **Entities** are represented as **Nodes (Vertices)**.
- **Relationships** between entities are represented as **Edges (Links)**.

Example:

```
Person A -------- Person B
      \             /
       \           /
        Person C
```

---

# Why Network Analysis?

Network analysis helps answer questions such as:

- Who is the most influential person in a social network?
- Which products are frequently bought together?
- What is the shortest route between two cities?
- How does a disease spread?
- Which bank accounts are involved in fraud?
- Which webpages should rank higher?

---

# Graph Terminology

## Node (Vertex)

Represents an object or entity.

Examples:

- Person
- Customer
- Product
- City
- Web Page

---

## Edge (Link)

Represents a relationship between two nodes.

Examples:

- Friendship
- Purchase
- Road
- Communication
- Hyperlink

---

## Degree

Number of edges connected to a node.

```
A ---- B ---- C

Degree(A)=1

Degree(B)=2

Degree(C)=1
```

For directed graphs:

- **In-Degree** → Incoming edges
- **Out-Degree** → Outgoing edges

---

# Types of Graphs

## 1. Undirected Graph

Relationships have no direction.

```
A ----- B
```

Example:

- Friendship
- Marriage

---

## 2. Directed Graph

Relationships have direction.

```
A -----> B
```

Example:

- Twitter Follow
- Web Links

---

## 3. Weighted Graph

Each edge has a weight.

```
Delhi ----- Mumbai

Weight = 1400 km
```

---

## 4. Unweighted Graph

All edges have equal importance.

---

## 5. Cyclic Graph

Contains cycles.

```
A → B → C

↑       ↓

←-------
```

---

## 6. Acyclic Graph

Contains no cycles.

Example:

Tree

---

# Graph Representation

## 1. Adjacency Matrix

```
      A B C

A     0 1 1

B     1 0 0

C     1 0 0
```

Advantages

- Fast edge lookup
- Simple implementation

Disadvantages

- High memory usage
- Poor for sparse graphs

---

## 2. Adjacency List

```
A → B,C

B → A

C → A
```

Advantages

- Memory efficient
- Preferred for sparse graphs

---

# Important Graph Properties

## Connected Graph

Every node is reachable.

---

## Disconnected Graph

Some nodes are isolated.

---

## Path

Sequence of connected nodes.

```
A → B → C → D
```

---

## Path Length

Number of edges in a path.

---

## Cycle

A path that starts and ends at the same node.

---

## Diameter

Longest shortest path in a graph.

---

## Density

Measures how connected a graph is.

```
Density

=

Actual Edges

------------------

Maximum Possible Edges
```

---

# Graph Traversal

Graph traversal means visiting every node.

---

## Breadth First Search (BFS)

Visits nodes level by level.

```
A

↓

B C

↓

D E F
```

Uses

- Queue
- Shortest path (unweighted graph)
- Social network analysis

Complexity

```
O(V + E)
```

---

## Depth First Search (DFS)

Explores one branch completely before backtracking.

Uses

- Stack / Recursion
- Cycle detection
- Topological sorting
- Connected components

Complexity

```
O(V + E)
```

---

# Shortest Path Algorithms

## Dijkstra Algorithm

Used when

- Positive edge weights

Applications

- Google Maps
- GPS Navigation

Complexity

```
O((V+E) log V)
```

---

## Bellman-Ford Algorithm

Supports

- Negative edge weights

Can detect

- Negative cycles

---

## Floyd-Warshall

Finds shortest paths between **all pairs of nodes**.

Complexity

```
O(V³)
```

---

# Minimum Spanning Tree (MST)

An MST connects all vertices with:

- Minimum total edge weight
- No cycles

Algorithms

- Prim's Algorithm
- Kruskal's Algorithm

Applications

- Road networks
- Electrical grids
- Computer networks

---

# Centrality Measures

Centrality identifies the **most important nodes** in a network.

---

## Degree Centrality

Measures

```
Number of Connections
```

Applications

- Popular users
- Social media influencers

---

## Closeness Centrality

Measures

```
Average distance

to every other node
```

Higher value

↓

Faster information spread.

---

## Betweenness Centrality

Measures

How often a node lies on the shortest path.

Applications

- Traffic control
- Fraud detection

---

## Eigenvector Centrality

Importance depends on the importance of neighboring nodes.

Used in

- Social networks
- Citation networks

---

## PageRank

Developed by Google.

Ranks webpages based on incoming links.

Higher-quality incoming links

↓

Higher PageRank.

---
# Network Properties

Network properties describe the overall structure and characteristics of a graph. They help us understand how nodes are connected, how efficiently information flows, and how tightly the network is organized.

---

# 1. Path

## Definition

A **path** is a sequence of nodes connected by edges that allows movement from one node to another.

Example

```
A ----- B ----- C ----- D
```

Possible paths from **A to D**

```
A → B → C → D
```

Length of Path

```
Number of edges traversed.
```

In the above example,

```
Path Length = 3
```

### Types of Paths

### Simple Path

A path in which no node is repeated.

Example

```
A → B → C → D
```

---

### Closed Path (Cycle)

Starts and ends at the same node.

Example

```
A → B → C → A
```

---

# 2. Shortest Path

## Definition

The **Shortest Path** is the path between two nodes having the minimum total distance (or minimum number of edges).

Example

```
      B
     / \
A---     ---D
     \ /
      C
```

Possible paths

```
A → B → D

Distance = 8

A → C → D

Distance = 5
```

Shortest Path

```
A → C → D
```

### Applications

- Google Maps
- GPS Navigation
- Network Routing
- Flight Planning
- Robot Navigation

### Algorithms

- BFS (Unweighted Graph)
- Dijkstra Algorithm
- Bellman-Ford Algorithm
- Floyd-Warshall Algorithm
- A* Algorithm

---

# 3. Average Path Length (APL)

## Definition

Average Path Length is the **average number of steps required to travel between every pair of nodes in a network.**

It measures how efficiently information travels through the network.

Formula

```
Average Path Length

=

Sum of all shortest path lengths

---------------------------------

Number of node pairs
```

### Interpretation

- Small APL → Faster communication
- Large APL → Slower communication

Example

```
Social Network

Average Path Length = 4
```

This means any two people are connected through approximately four intermediate connections.

### Applications

- Social Networks
- Communication Networks
- Internet Routing
- Transportation Networks

---

# 4. Diameter

## Definition

The **Diameter** of a graph is the **longest shortest path** between any two nodes.

It represents the maximum distance needed to travel between any pair of nodes.

Example

```
A ----- B ----- C ----- D ----- E
```

Shortest paths

```
A → E = 4
```

No other shortest path is longer.

Therefore,

```
Diameter = 4
```

### Interpretation

- Small Diameter → Compact network
- Large Diameter → Spread-out network

### Applications

- Internet Topology
- Social Networks
- Transportation Planning

---

# 5. Density

## Definition

Density measures **how many edges are present compared to the maximum possible number of edges.**

It tells us how well connected the graph is.

---

### Formula (Undirected Graph)

```
Density

=

2E

-----------

V(V-1)
```

Where

```
E = Number of Edges

V = Number of Vertices
```

---

### Formula (Directed Graph)

```
Density

=

E

-----------

V(V-1)
```

---

### Range

```
0 ≤ Density ≤ 1
```

| Density | Meaning |
|----------|---------|
| 0 | No connections |
| 1 | Fully connected graph |

### Interpretation

High Density

- Highly connected network
- Faster communication
- More redundancy

Low Density

- Sparse network
- Fewer relationships
- Lower communication efficiency

### Applications

- Social Networks
- Biological Networks
- Computer Networks
- Recommendation Systems

---

# 6. Clustering Coefficient

## Definition

The **Clustering Coefficient** measures how closely the neighbors of a node are connected to each other.

It indicates the tendency of nodes to form clusters or communities.

Example

```
      B
     / \
A -------- C
```

Here,

A's neighbors (B and C) are also connected.

Hence,

High Clustering Coefficient.

---

### Formula (Local Clustering Coefficient)

```
Clustering Coefficient

=

Number of Existing Connections

--------------------------------------

Maximum Possible Connections
```

For a node

```
CC(v)

=

2E

------------

k(k-1)
```

Where

- **E** = Number of edges among neighboring nodes
- **k** = Number of neighboring nodes

---

### Range

```
0 ≤ CC ≤ 1
```

| Value | Meaning |
|--------|---------|
| 0 | Neighbors are not connected |
| 1 | Every neighbor is connected to every other neighbor |

---

### Global Clustering Coefficient

Average of the local clustering coefficients of all nodes in the graph.

It gives an overall measure of how clustered the entire network is.

---

### Applications

- Social Network Analysis
- Community Detection
- Recommendation Systems
- Protein Interaction Networks
- Fraud Detection

---

# Summary of Network Properties

| Property | Definition | Interpretation |
|----------|------------|----------------|
| Path | Sequence of connected nodes | Connectivity between nodes |
| Shortest Path | Minimum distance between two nodes | Efficient routing |
| Average Path Length | Average shortest path among all node pairs | Overall communication efficiency |
| Diameter | Longest shortest path | Size of the network |
| Density | Ratio of existing edges to maximum possible edges | Connectivity of the graph |
| Clustering Coefficient | Degree to which neighbors are connected | Community structure and local cohesiveness |

# Community Detection

Communities are groups of densely connected nodes.

Example

```
Friends

within

same college
```

Algorithms

- Louvain
- Girvan-Newman
- Label Propagation

Applications

- Customer segmentation
- Social media analysis
- Fraud rings

---

# Link Prediction

Predicts future connections.

Example

LinkedIn

```
People You May Know
```

Methods

- Common Neighbors
- Jaccard Similarity
- Adamic-Adar
- Preferential Attachment

---

# Graph Embedding

Converts graph nodes into numerical vectors.

Purpose

- Machine Learning
- Node Classification
- Link Prediction

Popular Algorithms

- DeepWalk
- Node2Vec
- LINE

---

# Graph Neural Networks (GNN)

Traditional neural networks work on tabular or image data.

Graphs require specialized neural networks.

Popular GNN Models

- Graph Convolutional Network (GCN)
- Graph Attention Network (GAT)
- GraphSAGE

Applications

- Drug Discovery
- Fraud Detection
- Recommendation Systems
- Social Networks

---

# Knowledge Graph

A Knowledge Graph stores information as triples.

```
Subject

Predicate

Object
```

Example

```
Elon Musk

Founder Of

SpaceX
```

Applications

- Google Search
- ChatGPT
- Semantic Search
- Question Answering

---

# Python Libraries

## NetworkX

Most popular graph library.

```python
import networkx as nx

G = nx.Graph()

G.add_edge("A","B")

G.add_edge("B","C")

print(G.nodes())

print(G.edges())
```

---

## Visualizing a Graph

```python
import matplotlib.pyplot as plt
import networkx as nx

G = nx.Graph()

G.add_edges_from([
    ("A","B"),
    ("A","C"),
    ("B","D")
])

nx.draw(G, with_labels=True)

plt.show()
```

---

# Applications

- Social Network Analysis
- Fraud Detection
- Recommendation Systems
- Transportation Networks
- Computer Networks
- Cybersecurity
- Supply Chain Optimization
- Financial Transaction Analysis
- Disease Spread Modeling
- Search Engines
- Knowledge Graphs

---

# Advantages

- Captures relationships between entities.
- Reveals hidden patterns.
- Identifies influential nodes.
- Supports recommendation systems.
- Useful for fraud detection and social network analysis.

---

# Limitations

- Large graphs require high computational resources.
- Visualization becomes difficult for massive networks.
- Dynamic graphs are challenging to maintain.
- Some graph algorithms have high time complexity.

---

# Interview Questions

### 1. What is Network Analysis?

Network Analysis is the study of relationships among entities using graph structures consisting of nodes and edges.

---

### 2. Difference between Directed and Undirected Graph?

- Directed graphs have edge direction.
- Undirected graphs have bidirectional relationships.

---

### 3. What is the difference between BFS and DFS?

| BFS | DFS |
|------|------|
| Level-wise traversal | Depth-wise traversal |
| Uses Queue | Uses Stack/Recursion |
| Finds shortest path in unweighted graphs | Used for cycle detection and topological sorting |

---

### 4. What is a Minimum Spanning Tree?

A subset of edges that connects all vertices with the minimum total weight and no cycles.

---

### 5. What is PageRank?

PageRank is a graph-based ranking algorithm that assigns importance to web pages based on the number and quality of incoming links.

---

### 6. What is Graph Embedding?

Graph Embedding converts nodes into low-dimensional vectors while preserving graph structure, enabling machine learning tasks such as node classification and link prediction.

---

### 7. What are Graph Neural Networks?

Graph Neural Networks are deep learning models specifically designed to process graph-structured data by aggregating information from neighboring nodes.

---

# Summary

Network Analysis is the study of interconnected data using graph theory. It models real-world entities as **nodes** and their relationships as **edges**, enabling analysis of connectivity, influence, shortest paths, communities, and hidden structures. Core concepts include graph representations, traversal algorithms (BFS/DFS), shortest path algorithms (Dijkstra, Bellman-Ford), minimum spanning trees, centrality measures, community detection, graph embeddings, Graph Neural Networks (GNNs), and knowledge graphs. It is widely applied in social networks, recommendation systems, fraud detection, cybersecurity, transportation, and search engines.
