---
type: atomic
tags: [ai, ai/llm, coding/azure, devops]
date: 2026-10-01
---

# Managed LLM Service

## Idea
You don't run the GPUs. A cloud provider hosts the model, you call an endpoint and pay per token, and in exchange you get the enterprise controls (private networking, data residency, a promise your data isn't used for training) that a company needs before it will send real data to a model.

## Definition
A managed LLM service lets you use a [[LLM (Large Language Model)|large language model]] through a cloud provider's API instead of hosting the model yourself. The provider owns the GPU fleet, scaling and model serving. You pick a model from a catalogue, sometimes create a named **deployment** of it in a region, and get an HTTPS endpoint. Billing is per [[Tokens|token]], with input and output tokens priced separately, or you buy **provisioned throughput** for guaranteed capacity at a fixed rate. Capacity is a **quota** measured in tokens per minute (and requests per minute). Go over it and you get HTTP 429s, so callers need [[Rate Limiting]]-aware retries with [[Exponential Backoff]]. What you get on top of the bare model is enterprise packaging: [[Private Endpoint|private networking]] so prompts never cross the public internet, a contractual promise that prompts and outputs aren't used for training, **regional data residency**, **content filters** on input and output, and the same identity, logging and billing as the rest of your cloud. Compared with calling the model vendor directly, you get those controls and one bill, but new models and features often arrive later, and regional capacity can run out. Compared with self-hosting [[Open Weights vs Closed Models|open-weight models]], you avoid running GPUs but give up control over the exact model version, which the provider eventually retires on its own schedule.

## Providers
- **Azure** — Azure OpenAI in Azure AI Foundry: OpenAI models as named deployments with TPM quotas, plus a catalogue of other vendors' and open models.
- **AWS** — Amazon Bedrock: Anthropic, Meta, Mistral, Amazon and other models behind one API, with provisioned throughput.
- **Google Cloud** — Vertex AI: Gemini plus Model Garden (including Anthropic and open models).
- **Others** — calling the vendor directly (Anthropic API, OpenAI API): newest models first, fewer cloud-integration controls.

## Source
OpenAI's public API (2020) set the pattern. Azure OpenAI Service became generally available in January 2023, Amazon Bedrock in September 2023, and Google brought generative models to Vertex AI in 2023.

---

## Compass

**Roots** — *where this comes from*
It's the hosting choice for an [[LLM (Large Language Model)]], and its costs and limits are all counted in [[Tokens]].

**Paths** — *where this leads*
Per-token pricing makes [[Selective LLM Usage]] and tight [[Prompt Engineering|prompts]] a cost decision as well as a quality one. The same service usually also serves the [[Vector Embedding|embeddings]] behind [[RAG (Retrieval-Augmented Generation)]].

**Neighbors** — *what lives nearby*
[[Open Weights vs Closed Models]] is the other side of the decision, and the [[Managed Search Service]] is the retrieval half of most enterprise LLM systems built on it.

**Clash** — *what pushes against this*
You rent behaviour you don't control: models are versioned and retired on the provider's schedule, so outputs can change under you, quota is shared and can run out, and at high, steady volume running your own open-weight model can be cheaper.
