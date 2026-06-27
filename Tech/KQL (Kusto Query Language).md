---
type: atomic
tags: [devops]
date: 2026-06-26
---

# KQL (Kusto Query Language)

## Idea
A SQL-flavoured query language for asking telemetry questions like "show me every slow request in the last hour."

## Definition
KQL is the read-only query language behind [[Application Insights]] and Log Analytics, and it's how I actually investigate the the project AI Document Ingestion system in production. I write piped queries (`traces | where severityLevel >= 3 | summarize count() by operation_Name`) to find errors, trace a slow document-ingestion run, or chase a [[Percentile-Based-Performance-Metrics|p95 latency]] spike. Because the app emits [[Structured Logging|structured logs]] via [[Serilog]], the custom fields become first-class columns I can filter and aggregate on. KQL is where [[Fail Fast Fail Loudly]] pays off after deploy — loud, structured signals turn into answerable questions.

## Source
AI document ingestion project

---

## Neighbors — *what lives nearby*
KQL shares the same query-and-aggregate mindset as [[SQL]], though it queries a different data store, and it runs directly against [[Application Insights]], the telemetry store that powers these investigations.

## Clash — *what pushes against this*
While [[Unit Tests]] verify behaviour before you deploy, KQL lets you observe behaviour after the fact — one validates upfront, the other investigates in production.

## Roots — *where this comes from*
[[Structured Logging]] is what makes KQL queries powerful; the structured fields that emerge from proper logging become first-class columns you can filter and aggregate on.

## Paths — *where this leads*
KQL aggregations are how you compute the percentiles tracked in [[Percentile-Based-Performance-Metrics]], turning raw telemetry into actionable performance insights.
