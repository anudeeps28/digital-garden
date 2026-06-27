---
type: atomic
tags: [coding/csharp]
date: 2026-06-26
---

# CsvHelper

## Idea
A .NET library that maps between C# objects and CSV rows so I don't hand-roll comma parsing.

## Definition
CsvHelper is a C# library for reading and writing CSV — handling the mechanical work of mapping [[DTOs (Data Transfer Objects)|DTOs]] to CSV rows (and back), with correct quoting, escaping, and header management. It avoids the trap of hand-rolling string concatenation for tabular exports. It's the lightweight, universally-openable counterpart to [[ClosedXML]]: CSV when the consumer needs raw data or another system will ingest it, Excel when formatting and cell-level control matter. In practice, such exports often stream through a [[Controller]] on a [[REST API]].

## Source
Josh Close, open-source library first released ~2009; maintained on GitHub at joshclose/CsvHelper.

---

## Compass

**Neighbors** — *what lives nearby*
[[ClosedXML]] serves a similar data-mapping role but for formatted Excel output, while [[DTOs (Data Transfer Objects)|DTOs]] are the objects that CsvHelper maps into rows.

**Clash** — *what pushes against this*
[[JSON]] represents the opposite approach — nested and structured payloads instead of the flat tabular rows that CSV provides.

**Roots** — *where this comes from*
[[NuGet]] is the package manager that brings this dependency into the project.

**Paths** — *where this leads*
The generated CSV is ultimately delivered through a [[REST API]] endpoint, where a [[Controller]] streams the output to clients.
