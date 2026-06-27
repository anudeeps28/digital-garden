---
type: atomic
tags: [coding/csharp]
date: 2026-06-26
---

# ClosedXML

## Idea
A .NET library for building real Excel workbooks in code — sheets, formatting, formulas and all.

## Definition
ClosedXML is the C# library I use in the KBA AI Document Ingestion project to generate native `.xlsx` Excel files for plan-data exports. From a [[Controller]] action I build a workbook in memory — styled headers, multiple sheets, typed cells — and stream it back as a download through the [[REST API]]. It's the rich-format counterpart to [[CsvHelper]]: I reach for ClosedXML when the user wants a formatted, Excel-native deliverable, and for plain tabular dumps I use CSV instead. Both turn [[DTOs (Data Transfer Objects)|DTOs]] coming out of the data layer into something a business user can open.

## Source
KBA AI Document Ingestion project

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
