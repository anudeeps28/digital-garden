---
type: atomic
tags: [ai/llm]
date: 2026-03-24
---

# RAG (Retrieval-Augmented Generation)

## Idea
RAG is a pattern where you first retrieve relevant document chunks, then ask the AI to answer based only on those chunks — grounding the AI in real data.

## Definition
Retrieval-Augmented Generation combines information retrieval with [[LLM (Large Language Model)|LLM]] generation. Instead of asking the AI to answer from its training data (which may be wrong or outdated), you first search for relevant document chunks using semantic search (via [[Hybrid Search]] or [[Vector Search]]), then include those chunks in the [[Prompt Engineering|prompt]] as context, and ask the model to answer based only on what it was given. This "grounds" the response in actual source documents. In practice, when a user asks a question about specific documents, RAG retrieves the relevant chunks from those documents and feeds them to an LLM to generate an accurate, sourced answer.

## Source
Patrick Lewis, Ethan Perez, Aleksandara Piktus, et al., Meta AI. "Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks" (2020). Introduced RAG as a framework combining pretrained [[Vector Embedding|embeddings]] and language models for knowledge-intensive tasks.

---

## Neighbors — *what lives nearby*
RAG's retrieval step is essentially what [[Search Engines]] do — find the relevant information first, then present it. It's also analogous to an [[Open Book Exam]], where you answer with reference material rather than from memory.

## Clash — *what pushes against this*
[[Pure LLM Generation]] asks the AI without any retrieved context, which is prone to hallucination, whereas [[Keyword Search Only]] returns search results without AI synthesis.

## Roots — *where this comes from*
[[LLM (Large Language Model)]] is the foundation that RAG augments with grounded retrieval. The core insight comes from information retrieval research: pairing relevance-based document retrieval with generative synthesis creates more reliable, traceable answers than generation alone.

## Paths — *where this leads*
Documents must be [[Chunking|chunked]] before they can be retrieved, and chunks are [[Vector Embedding|embedded]] for semantic retrieval using [[Hybrid Search]] via [[Azure AI Search]]. These retrieved chunks are then injected into the [[Prompt Engineering|prompt]] for the model to synthesize an answer.
