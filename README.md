# Semantic Search Evaluation Platform

An end-to-end search quality evaluation pipeline simulating the analytical measurement layer for enterprise search and retrieval systems.

---

## Project Overview

Modern search systems — whether powering academic discovery, clinical knowledge bases, or e-commerce — require systematic measurement to prove that ranking changes actually improve retrieval quality. This project builds that measurement layer from the ground up.

Using the MS MARCO public benchmark dataset, this project:

- Computes standard information retrieval metrics across query result sets
- Compares lexical (BM25) and semantic (vector search) retrieval approaches
- Simulates a controlled A/B experiment evaluating ranking improvements
- Delivers a self-service dashboard tracking search health metrics over time

---

## Modules

### Module 1 - Search Relevance Metrics Engine
- Implements NDCG@K, MAP, MRR, Precision@K, Recall@K
- Compares BM25 vs semantic vector search using SentenceTransformers
- Identifies retrieval gaps and ranking quality issues across query sets
- Dataset: MS MARCO Passage Ranking dev subset

### Module 2 - A/B Experimentation Framework
- Generates synthetic session data simulating two retrieval system variants
- Implements power analysis, two-proportion z-test, Mann-Whitney U, confidence intervals
- Produces reusable experiment report with go/no-go recommendation
- Designed to mirror real search ranking experiment workflows

### Module 3 - Search Analytics Dashboard
- Streamlit dashboard tracking NDCG trends, CTR by rank position, zero-result rate, query volume
- DuckDB local warehouse as the analytical layer
- Self-service design for both technical and business stakeholders

---

## Stack

Python, SQL, DuckDB, Streamlit, Plotly, pandas, numpy, scipy, statsmodels, rank-bm25, sentence-transformers, FAISS

---

## Dataset

MS MARCO Passage Ranking dev subset — a public benchmark dataset containing real search queries and graded relevance labels, widely used in information retrieval research.

---

## Status

🚧 In progress — Module 1 under active development

---

## Repo Structure
