---
type: atomic
tags: [ai, ai/llm]
date: 2026-06-26
---

# Chunk Classification

## Idea
Chunk classification tags each document chunk with what kind of content it holds, so retrieval can filter by structure, not just by words.

## Definition
When documents are split during [[Chunking]], each resulting chunk can be labeled by content type — for example, Definition, Prose, Table, Metadata, or Query-specific categories. Storing this label as metadata in a vector database or search index lets retrieval narrow the field before scoring: a question seeking an exclusion can restrict to Exclusion-type chunks, and a numerical lookup can favor Table-type chunks. This structural tagging makes [[Hybrid Search]] far more precise, because the system isn't searching the whole corpus blindly — it searches the slice that structurally matches the question's [[Query Intent Classification|intent]].

## Source
Foundational concept in semantic search and RAG systems; formalized in practice across vector database and search engine communities. Widely adopted by tools like LangChain, Llamaindex, and modern vector database platforms (Pinecone, Weaviate, Milvus) as a best practice for improving retrieval precision.

---

## Compass

**Neighbors** — *what lives nearby*
Classification is a refinement layered on top of [[Chunking Strategy]], and both [[Query Intent Classification]] and chunk classification label things to enable smarter routing and filtering throughout the system.

**Clash** — *what pushes against this*
Plain [[Chunking]] with no type awareness stands in contrast to classification — splitting without structure misses the opportunity to tag content by its role, while classification adds the structure that chunking lacks.

**Roots** — *where this comes from*
This concept belongs to the broader theme of [[Hybrid Search]], where classification metadata makes the search space itself filterable rather than blindly scoring everything.

**Paths** — *where this leads*
Typed filtering yields a cleaner [[Retrieval Context (Top-K)]] set, where the system retrieves not just the most similar chunks but the most similar chunks *of the right type*.
