---
type: atomic
tags: [coding/web-api]
date: 2026-03-24
---

# JSON

## Idea
JSON is the standard text format APIs use to send and receive structured data — it looks like a dictionary of key-value pairs.

## Definition
JSON (JavaScript Object Notation) is a lightweight data interchange format that's easy for both humans and machines to read. It uses curly braces for objects (`{"name": "John", "age": 30}`), square brackets for arrays, and supports strings, numbers, booleans, and null. In [[REST API]] communication, [[DTOs (Data Transfer Objects)]] are automatically serialized to JSON for responses and deserialized from JSON for requests. [[.NET 8]] uses `System.Text.Json` by default for this conversion. In the project, JSON is also used for [[Template-Based Extraction]] schemas that define which fields to extract from plan documents.

## Source
AI document ingestion project

---

## Compass

**Neighbors** — *what lives nearby*
[[XML]] is an older, more verbose data format that serves a similar purpose, and [[YAML]] is a more human-readable format often used for configuration files.

**Clash** — *what pushes against this*
[[Binary Formats]] like Protocol Buffers and MessagePack are compact but not human-readable, while [[CSV]] handles flat tabular data without any nesting capability.

**Roots** — *where this comes from*
[[REST API]] depends on JSON as the standard data format for communication, and [[Request and Response]] bodies are where JSON gets carried between client and server.

**Paths** — *where this leads*
JSON maps to [[DTOs (Data Transfer Objects)]] — C# objects that serialize to and deserialize from JSON — and [[Swagger and OpenAPI]] documents JSON schemas for each endpoint. It also powers [[Template-Based Extraction]], which uses JSON templates to define which fields to extract from documents.
