---
type: atomic
tags: [coding/security, coding/patterns, frontend, api]
date: 2026-10-04
---

# Runtime Schema Validation

## Idea
Static types disappear when the code runs, so any data crossing a trust boundary has to be checked against a schema at runtime before the program believes it.

## Definition
[[TypeScript]] types are erased at compile time. Writing `JSON.parse(msg) as ClientMessage` does not check anything; it just tells the compiler to stop worrying. Runtime schema validation closes that gap: you declare the expected shape once as a schema, **parse** untrusted input through it, and get either a correctly typed value or an error. With Zod, for example, a socket protocol can be a `discriminatedUnion` on the `"type"` field, so each message kind has its own exact shape and unknown kinds are rejected. Good schemas also encode limits the type system cannot, like maximum string lengths and array sizes, which protects memory and storage. Messages that fail to parse are **dropped** (and logged), never half-processed. The same schema then produces the static type, so the runtime check and the compile-time type can never drift apart. Apply it at every boundary: request bodies, WebSocket frames, environment variables, third-party API responses, LLM output and anything read from storage.

## Tools
- **Zod** — TypeScript-first schemas with inferred types; the most common choice.
- **Valibot, ArkType, Yup** — lighter or alternative TS options.
- **Pydantic** — the Python equivalent, built on type hints.

## Source
The principle is Alexis King's "Parse, don't validate" (2019): turn unstructured input into a type that proves it is valid, rather than checking and passing the raw data along. Zod was created by Colin McDonnell in 2020.

---

## Compass

**Roots** — *where this comes from*
It is the TypeScript cousin of [[Pydantic]], and it applies [[Default-Deny Allowlisting]] to data: only shapes you explicitly described are let in.

**Paths** — *where this leads*
A [[Shared Contract Package]] can export the same schemas to client and server, and [[Structured Output Validation]] is the same move applied to model responses.

**Neighbors** — *what lives nearby*
[[WebSocket]] servers need it most, since every frame is untrusted, and [[Fail Fast Fail Loudly]] describes how a failed parse should behave at startup for config.

**Clash** — *what pushes against this*
Parsing everything costs CPU and boilerplate, and trusting internal data feels safe until it is not. Over-strict schemas can also break clients on harmless additions, which is the tension behind [[Read Payloads Are Not Write Payloads]].
