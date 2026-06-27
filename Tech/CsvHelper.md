---
type: atomic
tags: [coding/csharp]
date: 2026-06-26
---

# CsvHelper

## Idea
A .NET library that maps between C# objects and CSV rows so I don't hand-roll comma parsing.

## Definition
CsvHelper is the C# library I use in the AI document ingestion project for reading and writing CSV — primarily for CSV plan-data exports. It maps a collection of [[DTOs (Data Transfer Objects)|DTOs]] straight to rows (and back), handling quoting, escaping, and headers correctly instead of me concatenating strings and inviting bugs. It's the lightweight, universally-openable counterpart to [[ClosedXML]]: CSV when the consumer just needs raw tabular data or another system will ingest it, Excel when formatting matters. The export typically streams out through a [[Controller]] on the [[REST API]].

## Source
AI document ingestion project

---

## Compass

**Neighbors** — *what lives nearby*
[[ClosedXML]] is the other export library in the same project, serving a similar data-mapping role but for formatted Excel output, while [[DTOs (Data Transfer Objects)|DTOs]] are the objects that CsvHelper maps into rows.

**Clash** — *what pushes against this*
[[JSON]] represents the opposite approach — nested and structured payloads instead of the flat tabular rows that CSV provides.

**Roots** — *where this comes from*
[[NuGet]] is the package manager that brings this dependency into the project.

**Paths** — *where this leads*
The generated CSV is ultimately delivered through a [[REST API]] endpoint, where a [[Controller]] streams the output to clients.
