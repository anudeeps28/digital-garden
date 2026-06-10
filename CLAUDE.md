# Anudeep's Digital Garden — Claude Instructions

## Purpose
This is a personal knowledge base / digital garden. **Not** for work or project management. This vault is purely for capturing, connecting, and developing knowledge across:
- AI / LLMs / agents / prompt engineering
- Tech / programming / dev tools / systems
- Content creation / writing / media strategy
- Business / entrepreneurship / startups / strategy
- Mental models and thinking frameworks

---

## Vault Structure

```
Notes/
├── 00-Inbox/        ← raw captures, unprocessed; process these into proper notes
├── AI/              ← AI, ML, LLMs, agents, prompt engineering
├── Tech/            ← programming concepts, dev tools, languages, systems
├── Content/         ← content creation, writing, media, audience building
├── Business/        ← entrepreneurship, startups, strategy, finance, growth
├── Mental-Models/   ← mental models, heuristics, thinking frameworks
└── Templates/       ← note templates (do not create content notes here)
```

**Adding new folders:** When a knowledge area grows large enough to warrant its own folder (e.g., Finance, Leadership, Philosophy, Health), create a new top-level folder alongside the existing ones. Update this CLAUDE.md to document it. Folder location never affects `[[links]]` — notes connect across folders freely.

---

## Note Types

### 1. Atomic Note (primary note type)
Template: `Templates/Atomic-Note.md`
- One idea per note — concise, self-contained
- Uses the **Idea Compass** structure:
  - **Idea** — one-sentence summary
  - **Definition** — in own words
  - **Source** — origin
  - **Compass directions** — each direction is **1-2 sentences of natural prose** that explain the relationship, with `[[links]]` woven into the sentence (not bullet-listed). The sentence carries *why* the connection matters, not just *that* it exists:
    - **Roots** — where this comes from, the bigger theme or question it belongs to
    - **Paths** — where this leads, implications, what it unlocks
    - **Neighbors** — what lives nearby, ideas that resemble this and why
    - **Clash** — what pushes against this, where it breaks down
- Saved in the most relevant topic folder (AI/, Tech/, Content/, Business/, Mental-Models/)

### 2. Resource Note
Template: `Templates/Resource-Note.md`
- For capturing an article, book, video, podcast, or documentation source
- Spawns atomic notes from key ideas
- Saved in the most relevant topic folder

---

## Conventions

### Linking
- Use `[[Note Title]]` to link between notes — this is the core of the digital garden
- Every note should have **at least 2 links** to other notes (compass directions are a natural source)
- Link to concepts, not just topics — link the *idea*, not a vague folder

### Frontmatter
Every note has YAML frontmatter with at minimum:
```yaml
---
type: atomic | resource
tags: []
date: YYYY-MM-DD
---
```

### Tags
- Use tags for cross-cutting themes: `#mental-model`, `#ai/llm`, `#tech/python`, `#content/writing`, `#business/startup`, `#framework`
- Tags complement links — links show relationships, tags group by theme

### Inbox
- Raw/quick captures go in `00-Inbox/`
- Batch processed periodically — when user says "process the inbox", go through each note, convert to proper atomic notes using the Idea Compass template, file in the right folder, and wire up `[[links]]`

---

## How Claude Should Help

When creating notes:
1. Always use the appropriate template from `Templates/`
2. Place notes in the correct folder based on content
3. Write each Compass direction as **natural prose** — 1-2 tight sentences that explain the relationship, with `[[links]]` embedded mid-sentence. Never use bare bullet-pointed link lists. The prose should read like a smart person explaining a connection, not like metadata.
4. Link to concepts even if the target note doesn't exist yet (Obsidian creates them as stubs). Suggest related notes that already exist in the vault to link to.
5. Add meaningful frontmatter tags

When asked to capture an idea:
- Create an atomic note with full Idea Compass populated
- Suggest 2-3 additional atomic notes that could be spun off from the concept
- Identify existing notes in the vault to link to

When exploring connections:
- Use `[[double bracket links]]` aggressively — connecting concepts is the whole point
- If a concept is mentioned that doesn't have a note yet, flag it as a candidate for a new atomic note

When processing the inbox:
- Read each note in `00-Inbox/`
- **Notes with a clear source** (URL in filename, URL in content, or source explicitly mentioned) → process immediately:
  - Convert to proper atomic notes using the Idea Compass template
  - Move to the appropriate topic folder
  - Wire up `[[links]]` to existing notes in the vault
  - Suggest additional atomic notes that could be spawned
- **Notes without a clear source** → do NOT process yet. Pause and ask the user:
  - The user may remember the origin
  - Or research the original source online (find who coined it, what book/video/person popularized it, what the primary reference is)
  - Once the source is confirmed, then process the note as normal
