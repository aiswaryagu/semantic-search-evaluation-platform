# Metrics Reference

This document explains the information retrieval metrics used in this project, why they were chosen, and their trade-offs.

---

## Why These Metrics

Search systems return ranked lists of results. A simple accuracy score is not sufficient — the position of a relevant result matters as much as whether it appears at all. A relevant document ranked 10th is far less useful than one ranked 1st. These metrics capture that positional reality.

---

## Metrics

### NDCG@K — Normalised Discounted Cumulative Gain

Measures ranking quality by rewarding relevant results that appear higher in the list. Results are graded (0 to 3) rather than binary, so a highly relevant result contributes more than a marginally relevant one. The score is normalised against an ideal ranking, making it comparable across queries.

**Use case:** Primary metric for evaluating overall ranking quality.  
**Trade-off:** Requires graded relevance judgements, which are expensive to produce at scale.

---

### MAP — Mean Average Precision

Computes precision at each rank position where a relevant result appears, then averages across all queries. Rewards systems that rank relevant results consistently high across the entire result list.

**Use case:** Evaluating retrieval completeness across a query set.  
**Trade-off:** Treats all relevant documents as equally important — does not account for graded relevance.

---

### MRR — Mean Reciprocal Rank

Measures how high the first relevant result appears in the ranking. If the first relevant result is at rank 1, MRR is 1.0. At rank 2, it is 0.5. At rank 3, it is 0.33.

**Use case:** Best for navigational queries where the user wants a single correct answer.  
**Trade-off:** Only considers the first relevant result — ignores the rest of the ranked list.

---

### Precision@K

The proportion of results in the top K positions that are relevant. Simple and interpretable.

**Use case:** Evaluating how many of the top results are actually useful to the user.  
**Trade-off:** Does not penalise for the position of relevant results within K.

---

### Recall@K

The proportion of all relevant documents that appear in the top K results. Measures coverage.

**Use case:** Evaluating whether the system surfaces enough of the available relevant content.  
**Trade-off:** Can conflict with precision — improving recall often reduces precision.

---

### CTR by Rank Position

Click-through rate measured at each rank position in the result list. Higher positions naturally attract more clicks due to position bias.

**Use case:** Capturing real user behaviour signals from interaction logs.  
**Trade-off:** Confounded by position bias — users click higher results more regardless of relevance.

---

## Metric Selection for A/B Experiments

| Metric | Primary Use | Statistical Test |
|---|---|---|
| NDCG@10 | Primary success metric | Mann-Whitney U |
| CTR | User engagement proxy | Two-proportion z-test |
| Precision@5 | Top result quality | Mann-Whitney U |
| MRR | First relevant result position | Mann-Whitney U |

---

## BM25 vs Semantic Search

**BM25** is a lexical retrieval model based on term frequency and inverse document frequency. It is fast, interpretable, and strong on keyword queries.

**Semantic vector search** uses dense embeddings (SentenceTransformers) to match queries and documents by meaning rather than exact terms. It handles synonyms, paraphrasing, and intent better than BM25 but is computationally heavier.

This project benchmarks both approaches using the metrics above to quantify the trade-offs across different query types.
