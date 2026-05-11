# Semantic Retrieval with Transformer Embeddings

This project explores transformer-based embeddings for semantic retrieval tasks using multiple fine-tuning strategies and retrieval enhancements.

The experiments compare different encoder architectures and training objectives, including:

- Sentence pair training
- Triplet training
- Hard negative mining
- Cross-encoder re-ranking
- Dynamic re-chunking

The full implementation, experiments, visualizations, and explanations are contained in the notebook with extensive markdown documentation and inline comments.

---

## Project Overview

The goal of this project is to improve dense semantic retrieval performance by studying how different fine-tuning techniques affect embedding quality.

We evaluate:

- Retrieval accuracy
- Ranking quality
- Context reduction efficiency
- Answer retention after chunk reduction

The project also investigates practical tradeoffs between retrieval quality and token consumption.

---

## Models Used

- `distilbert-base-uncased`
- `all-MiniLM-L6-v2`
- `BAAI/bge-base-en-v1.5`

Cross-encoders:
- `BAAI/bge-reranker-base`
- `cross-encoder/ms-marco-MiniLM-L-12-v2`

---

## Training Strategies

### 1. Sentence Pair Training
Fine-tuning using `(query, positive_chunk)` pairs with Multiple Negatives Ranking (MNR) loss.

### 2. Triplet Training
Training with:
- Query
- Positive chunk
- Negative chunk

using triplet loss.

### 3. Hard Negative Mining
The best-performing approach.

Hard negatives are mined from incorrect but semantically similar retrieval results, helping the model learn finer semantic distinctions.

---

## Retrieval Pipeline

### Bi-Encoder Retrieval
Initial retrieval using dense embeddings and cosine similarity.

### Cross-Encoder Re-ranking
Top-k retrieved chunks are rescored using a cross-encoder model.

### Dynamic Re-chunking
Retrieved chunks are reduced to the most relevant sentences using attention scores from the cross-encoder.

This significantly reduces token usage while preserving most correct answers.

---

## Results

Key findings:

- Hard negative training produced the strongest improvements.
- BGE achieved the best overall retrieval performance.
- Dynamic re-chunking reduced context size by ~44% while retaining ~91% of valid answers.

Best model:
- **BGE + Hard Negatives**
- Hit@1: **0.6845**
- MRR: **0.7941**

---

## Repository Structure

```text
.
├── mnlp-anil-joey-final.ipynb      # Full implementation and experiments
├── report.pdf                      # Final report
├── README.md
