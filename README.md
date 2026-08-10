# ML-Lab

A personal laboratory for studying, implementing, experimenting with, and documenting **Machine Learning, Deep Learning, LLMs, and AI Systems**.

This repository is primarily a **learning and documentation space**. The goal is not to build a polished ML library, but to develop deep understanding by moving between mathematical reasoning, implementation, experiments, benchmarks, and technical notes.

---

## Purpose

The objective of `ML-Lab` is to understand what happens **under the abstractions**.

Instead of only using high-level libraries and APIs, this repository documents the journey from:

```text
Mathematics
    ↓
Numerical Computing
    ↓
Classical Machine Learning
    ↓
Deep Learning
    ↓
Autograd
    ↓
Transformers
    ↓
LLMs
    ↓
Inference
    ↓
Distributed Systems
    ↓
Storage
    ↓
AI Infrastructure
```

The emphasis is on **understanding, implementation, experimentation, and measurement**.

---

## What This Repository Contains

### 01 · Python + NumPy

Foundations of numerical computing:

* Python for scientific and ML engineering
* NumPy internals
* `ndarray`
* shapes and dtypes
* strides and memory layout
* views and copies
* broadcasting
* vectorization
* matrix operations
* performance experiments

### 02 · Mathematical Foundations

* Linear algebra
* Probability
* Calculus
* Optimization
* Gradient descent
* SGD
* Momentum
* Adam
* Regularization

### 03 · Classical Machine Learning

Implementations and experiments involving:

* Linear regression
* Logistic regression
* K-means
* PCA
* Decision trees
* Optimization
* Metrics
* Regularization
* Bias and variance
* Cross-validation
* Calibration
* Data leakage

### 04 · Deep Learning

* Neural networks
* Backpropagation
* Computational graphs
* Autograd
* MLPs
* CNNs
* RNNs
* PyTorch
* Training systems
* GPU execution
* Mixed precision
* Training performance

### 05 · Transformers + LLMs

* Attention
* Multi-head attention
* Positional representations
* RoPE
* RMSNorm
* SwiGLU
* Transformer architecture
* Tokenization
* GPT
* Language-model training
* Autoregressive generation

### 06 · Inference Systems

* KV cache
* Batching
* Continuous batching
* Quantization
* GPU memory
* TTFT
* TPOT
* Throughput
* Concurrency
* Scheduling
* Admission control
* Speculative decoding

### 07 · Distributed Systems

* Replication
* Partitioning
* Consistency
* Transactions
* Quorums
* Failure detection
* Distributed logs
* Distributed key-value stores
* Failure injection
* Recovery

### 08 · Storage + Consensus

* WAL
* MemTables
* SSTables
* B+ trees
* LSM trees
* Bloom filters
* Compaction
* MVCC
* Raft
* Leader election
* Log replication
* Persistence
* Recovery

### 09 · Distributed AI Systems

The final stage connects the previous work into a distributed AI platform involving:

```text
API Gateway
     ↓
Scheduler
     ↓
Inference Workers
     ↓
Model Runtime
     ↓
KV Cache
     ↓
Storage
```

with additional concerns such as:

* Model versions
* Routing
* Rate limiting
* Batching
* Streaming
* Retries
* Observability
* Agents
* Tools
* Memory
* Retrieval
* Evaluation

---

## Learning Philosophy

The repository follows a simple loop:

```text
Study
  ↓
Derive
  ↓
Implement
  ↓
Experiment
  ↓
Measure
  ↓
Document
  ↓
Question assumptions
  ↓
Repeat
```

Whenever practical, concepts are explored from multiple levels:

**Mathematics → Algorithm → Implementation → System → Performance**

For example:

```text
Matrix multiplication
        ↓
Algebraic formulation
        ↓
Naive implementation
        ↓
NumPy implementation
        ↓
Memory layout
        ↓
Cache behavior
        ↓
Vectorization
        ↓
Benchmark
```

The intention is to understand not only **what works**, but **why it works and where it breaks**.

---

## Documentation

The repository is deliberately documentation-heavy.

Experiments should answer concrete questions rather than simply demonstrate APIs.

Examples:

* Why does a NumPy transpose often produce a view?
* What exactly do strides represent?
* When does slicing allocate memory?
* Why does broadcasting avoid explicit copies?
* Why can vectorization be dramatically faster than Python loops?
* What determines matrix multiplication performance?
* How does backpropagation emerge from the chain rule?
* Why does attention have its particular computational complexity?
* Why does KV caching change LLM inference complexity?
* Where does inference latency actually come from?
* What happens when a distributed node fails halfway through an operation?

---

## Repository Structure

```text
ML-Lab/
│
├── README.md
│
├── 01-python-numpy/
├── 02-mathematics/
├── 03-classical-ml/
├── 04-production-ml/
├── 05-deep-learning/
├── 06-autograd/
├── 07-transformers/
├── 08-gpt/
├── 09-inference/
├── 10-serving/
├── 11-distributed-systems/
├── 12-distributed-kv/
├── 13-storage/
├── 14-raft/
└── 15-16-capstone/
```

The structure may evolve as the experiments become more sophisticated.

---

## References

The main learning path is supported by books, papers, source code, experiments, and implementations.

Important references include:

* *Mathematics for Machine Learning*
* *Hands-On Machine Learning*
* *Deep Learning* — Goodfellow, Bengio, Courville
* *Designing Data-Intensive Applications*
* *Database Internals*
* *Operating Systems: Three Easy Pieces*
* *Computer Systems: A Programmer's Perspective*

And papers including:

* Adam
* ResNet
* Attention Is All You Need
* BERT
* GPT
* RoPE
* FlashAttention
* vLLM
* MapReduce
* Dynamo
* Bigtable
* Kafka
* Raft

---

## Status

🚧 **Active learning repository**

The repository will evolve continuously as concepts are studied, implemented, tested, benchmarked, and documented.

> **Understand the abstraction. Then understand what is underneath it.**
