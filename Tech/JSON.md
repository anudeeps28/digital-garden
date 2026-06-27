---
type: atomic
tags: [coding/web-api]
date: 2026-03-24
---

# JSON

## Idea
JSON is the standard text format APIs use to send and receive structured data — it looks like a dictionary of key-value pairs.

## Definition
JSON (JavaScript Object Notation) is a lightweight data interchange format that's easy for both humans and machines to read. It uses curly braces for objects (`{"name": "John", "age": 30}`), square brackets for arrays, and supports strings, numbers, booleans, and null. In [[REST API]] communication, [[DTOs (Data Transfer Objects)]] are automatically serialized to JSON for responses and deserialized from JSON for requests. [[.NET 8]] uses `System.Text.Json` by default for this conversion. In practice, JSON is also used for defining schemas and configuration structures.

## Source
Douglas Crockford, first specified in 2001; now formalized in RFC 7158 (2013) and RFC 8259 (2017) as the standard data interchange format for the web.

---

## Compass

**Neighbors** — *what lives nearby*
[[XML]] is an older, more verbose data format that serves a similar purpose, and [[YAML]] is a more human-readable format often used for configuration files.

**Clash** — *what pushes against this*
[[Binary Formats]] like Protocol Buffers and MessagePack are compact but not human-readable, while [[CSV]] handles flat tabular data without any nesting capability.

**Roots** — *where this comes from*
[[REST API]] depends on JSON as the standard data format for communication, and [[Request and Response]] bodies are where JSON gets carried between client and server.

**Paths** — *where this leads*
JSON maps to [[DTOs (Data Transfer Objects)]] — strongly-typed objects that serialize to and deserialize from JSON — and [[Swagger and OpenAPI]] documents JSON schemas for each endpoint. It also powers data extraction workflows, which use JSON schemas to define structured data patterns.
