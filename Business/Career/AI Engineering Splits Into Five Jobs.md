---
type: atomic
tags: [business/career, ai/engineering, ai/agents]
date: 2026-11-14
---

# AI Engineering Splits Into Five Jobs

## Idea
Once models got good enough, the hard part moved from building AI to using it, and "working in AI" split into five distinct jobs.

## Definition
When the frontier model already exists, the remaining work is everything around it, and each piece is turning into its own role. At a small startup one person still does all five.

1. **AI Engineer:** builds the system around an existing model, including what data it sees, which tools it can call, and what happens when it is wrong.
2. **Inference Engineer:** most of a model's lifetime cost is answering prompts, not training. This role makes serving faster and cheaper through quantisation, batching and serving stacks such as vLLM.
3. **Forward Deployed Engineer:** a solutions architect who also builds. They sit inside a customer's team and ship the integration into its old systems.
4. **AI Evaluation Engineer:** "it seems fine" doesn't hold up once AI is talking to customers. They build evals that run on every model or prompt change, sometimes with another model as judge, so hallucinations are caught before users see them.
5. **AI Security Engineer:** an agent that can read your email can also read a hidden instruction in that email. They find prompt-injection holes and decide what an agent may touch.

## Source
Captured from my own reel on how AI roles are changing (October 2026).

- **AI Engineer** as a named discipline comes from swyx's "The Rise of the AI Engineer" (Latent Space, 30 June 2023).
- **Forward Deployed Engineer** is Palantir's term from the 2010s. FDE job postings rose more than 800% between January and September 2025, as OpenAI and Anthropic built FDE and applied-AI teams.
- **vLLM** came from UC Berkeley (Kwon et al., PagedAttention, SOSP 2023).
- "Inference engineer" became a recognised title over 2025–26, though naming still varies (model serving, inference systems).

The capture's "people are getting millions" for FDE roles is an exaggeration for most hires and is left out.

---

## Compass

**Roots** — *where this comes from*
This is what [[A Job Is a Bundle of Tasks]] looks like when one bundle is pulled apart: once model-building got concentrated in a few labs, the tasks around it became separate jobs. It also follows from [[Depth Is Cheap]], because the model is the cheap, borrowed depth, and the value sits in the system around it.

**Paths** — *where this leads*
Each role has a home in this vault: the AI engineer builds the [[Agent Harness]] and [[RAG (Retrieval-Augmented Generation)]] pipelines, the evaluation engineer owns [[Evals]] and [[LLM-as-a-Judge]], the inference engineer lives in [[Model Tiering]], and the security engineer applies [[Defence in Depth]] and [[Read-Only by Default]] to agents.

**Neighbors** — *what lives nearby*
It pairs with [[Plant Seeds, Don't Climb Ladders]], since being shallow across all five and deep in one is the T-shape for this field, and with [[Ship Reps, Not Grunt Work]], which explains where the hiring growth is going.

**Clash** — *what pushes against this*
Role names in a hype cycle are unstable. Some of these will merge back together or be automated by the next generation of tooling, the same way "webmaster" disappeared. It is a map of 2026, not a permanent taxonomy.
