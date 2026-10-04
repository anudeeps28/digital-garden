---
type: atomic
tags: [api, coding/web-api, coding/patterns]
date: 2026-10-04
---

# Read Payloads Are Not Write Payloads

## Idea
What an API gives you back is not what it will accept from you, so never round-trip a read response straight into a create or update call.

## Definition
Read responses are shaped for display: they include server-assigned ids, timestamps, computed fields, expiring links and nulls for "not set". Write endpoints are shaped for validation: they reject unknown fields, enforce length limits and demand specific shapes. Treating the two as the same object works in a demo and fails in production on the first record that has an edge case. A worked example: a sync job copied content blocks from a notes service's read endpoint directly into the same service's create endpoint. Most records went through, but some failed with `400 Bad Request` because a block had a `null` icon (allowed on read, rejected on write), a text run longer than 2,000 characters (returned whole, but capped on write), or a hosted-file URL that had already expired. Worse, the failed rows stayed flagged for retry, so the job failed again every hour. The fix was a **pure sanitising function** that maps the read shape to the write shape (drop nulls, split long text, re-upload or skip expiring files), covered by unit tests built from real failing payloads. The general rule: model the request and response as separate types, and put an explicit transformation between them.

## Source
A widely stated API-design practice: separate input and output models (OpenAPI's `readOnly`/`writeOnly` flags, distinct request and response schemas in frameworks like FastAPI). It echoes the robustness principle from Jon Postel (RFC 760, 1980) and CQRS's split of read and write models (Greg Young, around 2010).

---

## Compass

**Roots** — *where this comes from*
It is a specific case of keeping [[DTOs (Data Transfer Objects)]] per direction rather than one shared shape, and of the asymmetry that [[Swagger and OpenAPI]] encodes with read-only and write-only fields.

**Paths** — *where this leads*
The mapping belongs in [[Pure Functions]] so it can be tested from captured payloads, and the write side benefits from [[Runtime Schema Validation]] before the request even leaves your process.

**Neighbors** — *what lives nearby*
[[Pydantic]] makes the split cheap with separate create and read models, and [[Idempotency]] matters for the same job, since a retried write must not create duplicates.

**Clash** — *what pushes against this*
Separate shapes mean more types and more mapping code, which feels like duplication against a single shared model. A retry loop that keeps failing on bad data is also a form of [[Silent Failure]] unless something alerts after repeated 400s.
