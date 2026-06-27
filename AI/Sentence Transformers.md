---
type: atomic
tags: [ai, ai/llm]
date: 2026-06-26
---

# Sentence Transformers

## Idea
A library of pretrained models that map a sentence to a single dense vector for semantic similarity tasks.

## Definition
Sentence Transformers is a Python library offering pretrained models that turn whole sentences or passages into dense [[Vector Embedding|embeddings]], where semantic similarity becomes geometric closeness. For example, models like `all-MiniLM-L6-v2` produce 384-dimensional vectors suitable for encoding entire paragraphs. In practice, self-hosting these models on [[PyTorch]] (often CPU-only) via a lightweight API wrapper provides cost advantages over commercial embedding services. These embeddings then power [[Vector Search]] and [[Hybrid Search]] in [[RAG (Retrieval-Augmented Generation)]] pipelines.

## Source
Nils Reimers and Iryna Gurevych, "Sentence-BERT: Sentence Embeddings using Siamese BERT-Networks" (2019), AIFB, University of Karlsruhe. Open-source Python library released at https://github.com/UKPLab/sentence-transformers.

---

## Neighbors — *what lives nearby*
[[Vector Embedding]] is exactly what this library produces, turning text into dense vectors. [[Azure OpenAI]] is an alternative embeddings provider — a commercial option compared to self-hosting open-source models for cost-sensitive applications.

## Clash — *what pushes against this*
[[Tokens]] are the discrete sub-word units that text is broken into, whereas Sentence Transformers collapses an entire sentence or passage into a single continuous vector representation.

## Roots — *where this comes from*
This library serves as the foundation for [[RAG (Retrieval-Augmented Generation)]], the broader pipeline that combines retrieval and generation to augment LLM responses with grounded context.

## Paths — *where this leads*
The embeddings produced here enable [[Vector Search]], which performs nearest-neighbor retrieval to find semantically similar chunks, and can be combined with [[Hybrid Search]] to merge vector-based and keyword-based ranking. Upstream, [[Chunking]] determines which portions of text get embedded in the first place.
