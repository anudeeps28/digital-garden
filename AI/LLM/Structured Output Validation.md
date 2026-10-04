---
type: atomic
tags: [ai/llm, coding/quality, coding/patterns]
date: 2026-10-04
---

# Structured Output Validation

## Idea
Ask the model for strict JSON, then check it in ordinary code against everything you know must be true, and abort the run if any check fails.

## Definition
A schema guarantees shape: fields exist and have the right types. It does not guarantee that the content is correct. **Structured output validation** adds a second layer of plain, deterministic checks after parsing. A worked example from a content-ideas step: the prompt demands a JSON contract, and code then verifies that the number of ideas per topic matches the target, every enum value (format, angle) is from the allowed list, no two hooks repeat, and every cited `source_url` actually appears in the input the model was given. That last check is the valuable one, because it catches hallucinated sources that look perfectly plausible. Any failure stops the run rather than shipping a partial or invented result.

```python
cited = {i["source_url"] for i in ideas}
assert cited <= input_urls, f"invented sources: {cited - input_urls}"
```

## Tools
- **Pydantic / Zod** — define the schema and parse the response into typed objects.
- **Instructor** — wraps LLM calls so they return validated Pydantic models, retrying on failure.
- **Provider structured outputs** — OpenAI's strict JSON-schema mode and similar features in other APIs constrain generation to the schema.

## Source
OpenAI introduced Structured Outputs with strict JSON-schema adherence in August 2024, after earlier "JSON mode". Libraries like Instructor (Jason Liu, 2023) popularised validating LLM output with Pydantic. Neither checks semantic facts like source membership; that layer is your own code.

---

## Compass

**Roots** — *where this comes from*
It applies [[Define Contract Before Implementation]] to a model: the contract is written first, and [[Runtime Schema Validation]] with something like [[Pydantic]] enforces its shape at the boundary.

**Paths** — *where this leads*
Failing checks feed an [[All-or-Nothing Run]], and the source-membership check is a cheap form of [[Field Verification]].

**Neighbors** — *what lives nearby*
[[Fail Fast Fail Loudly]] is the mindset behind aborting instead of patching, and [[Template-Based Extraction]] is the same idea for pulling fields out of documents.

**Clash** — *what pushes against this*
Strict aborts can make a pipeline brittle when one small field is off; some teams prefer a retry with the error fed back. And checks only catch what you thought to check, so a well-formed but bland answer still passes.
