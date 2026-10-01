---
type: atomic
tags: [ai, ai/llm, ai/rag, coding/azure]
date: 2026-10-01
---

# Managed Search Service

## Idea
A hosted search engine that you fill with documents and query by keyword, by meaning, or both. In most enterprise RAG systems this is what actually finds the passages the model reads, so its quality caps the quality of the answers.

## Definition
A managed search service is a search engine the provider runs for you. You define an **index**, a schema of **fields** (text to search, filters, facets, and a vector field for [[Vector Embedding|embeddings]]), then push documents into it through an API, or let an **indexer** pull them on a schedule from a database or object storage, often cracking PDFs and [[Chunking|chunking]] them on the way in. At query time it serves three kinds of search: keyword search ranked by [[BM25 Scoring|BM25]], [[Vector Search|vector search]] over embeddings by similarity, and [[Hybrid Search|hybrid search]] that runs both and merges the rankings, usually with Reciprocal Rank Fusion. On top of that it can apply [[Semantic Re-ranking|semantic re-ranking]], where a cross-encoder model re-scores the top results by how well they actually answer the question. Filters (by tenant, date or document type) run alongside the search, which is how one index can serve many users safely. That's why it sits in the retrieval step of [[RAG (Retrieval-Augmented Generation)]]: the app embeds the question, runs a hybrid query with filters, and passes the top results to the model. Cost isn't per query. It's set by the **tier** plus **replicas** (copies for query throughput and availability) multiplied by **partitions** (shards for storage), so an idle index still costs money. Vector fields also eat into storage quickly.

## Providers
- **Azure** — Azure AI Search: indexes, indexers, integrated vectorization, hybrid queries and a semantic ranker; billed by tier × replicas × partitions.
- **AWS** — Amazon OpenSearch Service (managed OpenSearch with k-NN vector search; also a serverless mode) and Amazon Kendra (packaged enterprise search with connectors).
- **Google Cloud** — Vertex AI Search: managed, mostly configure-don't-build search and RAG over your data.
- **Others** — Elastic Cloud (managed Elasticsearch), Algolia (keyword-first, fast site search), and vector databases like Pinecone, a narrower alternative that does vector similarity well but needs more work for keyword search, re-ranking and indexing.

## Source
BM25 comes from Robertson and colleagues' Okapi work (1990s). Lucene-based engines (Elasticsearch, 2010) made it the default, and the cloud providers added vector and hybrid search from 2023 onward.

---

## Compass

**Roots** — *where this comes from*
It packages [[BM25 Scoring]], [[Vector Search]] and [[Hybrid Search]] into one hosted engine, fed by [[Chunking|chunked]] documents and [[Vector Embedding|embeddings]].

**Paths** — *where this leads*
It's the retrieval step of [[RAG (Retrieval-Augmented Generation)]], and what it returns becomes the [[Retrieval Context (Top-K)]] passed to the [[Managed LLM Service|model]].

**Neighbors** — *what lives nearby*
[[Semantic Re-ranking]] runs inside it as a second pass, and per-tenant filters are its version of [[Multi-Tenant Data Isolation]].

**Clash** — *what pushes against this*
It's a second copy of your data that has to be kept in sync, and indexer lag means answers can be stale. Its fixed tier cost is high for small workloads, where a vector extension in an existing database (like pgvector in [[PostgreSQL]]) may be enough.
