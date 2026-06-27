---
type: atomic
tags: [coding/csharp]
date: 2026-06-26
---

# ClosedXML

## Idea
A .NET library for building real Excel workbooks in code — sheets, formatting, formulas and all.

## Definition
ClosedXML is a C# library for generating native `.xlsx` Excel files programmatically — sheets, formatting, formulas, and styling all available through a fluent API. In practice, you build a workbook in memory with styled headers, multiple sheets, and typed cells, then stream or save it as a file. It's the rich-format counterpart to [[CsvHelper]]: use ClosedXML when you need a formatted, Excel-native deliverable with styling and structure, and reach for CSV when plain tabular data suffices. Both turn structured data — such as [[DTOs (Data Transfer Objects)|DTOs]] from a data layer — into something end users can open and work with in Excel.

## Source
Jean-Marie Alfonse, open-source project; first released 2009. See [ClosedXML on GitHub](https://github.com/ClosedXML/ClosedXML).

---

## Compass

**Neighbors** — *what lives nearby*
[[CsvHelper]] is the other export library I reach for, handling plain tabular data, while [[REST API]] is the channel through which the generated file gets streamed back to the user.

**Clash** — *what pushes against this*
[[JSON]] represents the opposite approach — a machine-to-machine format rather than a human-facing spreadsheet.

**Roots** — *where this comes from*
[[NuGet]] is the dependency manager that brings this third-party library into the project.

**Paths** — *where this leads*
The shaped [[DTOs (Data Transfer Objects)|DTOs]] coming out of the data layer are what get written into the workbook, making them the raw material for the export.
