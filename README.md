# financial-rag-challenge
# 🚀 Financial RAG Challenge

**Author:** [Yifan Wang]  
**Years Used:** 2018–2025  
**Data Source:** [Databricks OfficeQA](https://huggingface.co/datasets/databricks/officeqa)

A comparison of a **Baseline** vs **Engineered** Retrieval-Augmented Generation (RAG) system on U.S. Treasury Bulletins.

## 📊 Results

| Metric | Baseline (Simple) | Engineered (Improved) |
|---|---|---|
| Hit Rate@5 | 18.18% | **36.36%** ⬆️ 2x |
| MRR | 0.1136 | **0.3182** ⬆️ 3x |
| Groundedness | N/A | 33.33% |
| Factual Accuracy | 0.00% | 0.00% |
| Hallucination Rate | 0% | 66.67% |

## 🏗️ Architecture

| Component | Baseline | Engineered |
|---|---|---|
| Chunk size | 500 chars | **1500 chars** |
| Overlap | 0 | **300 chars** |
| Metadata | None | **year + month** |
| Retrieval filter | Semantic only | **Metadata + Semantic** |
| Vector DB | ChromaDB | ChromaDB |
| Embedding model | all-MiniLM-L6-v2 | all-MiniLM-L6-v2 |
| Generator | Gemini 2.5-flash-lite | Gemini 2.5-flash-lite |

## 🔍 Key Findings

1. **Retriever was the bottleneck.** Baseline Hit Rate@5 of 18% meant most queries never saw their source document.
2. **Metadata + larger chunks doubled retrieval.** Year/month filtering eliminated cross-year noise.
3. **New bottlenecks emerged.** Fixing retrieval exposed table-parsing failures and math limitations in the LLM.

## 📓 Notebook

See [`FinancialRAG_Challenge.ipynb`](./FinancialRAG_Challenge.ipynb) for full code, outputs, and reflection.
