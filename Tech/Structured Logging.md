---
type: atomic
tags: [coding/observability]
date: 2026-03-24
---

# Structured Logging

## Idea
Structured logging records log entries as key-value pairs instead of plain text — making them searchable, filterable, and machine-readable.

## Definition
Traditional logging writes free-form strings: `"Error processing document plan.pdf for group 123"`. Structured logging preserves the data as properties: `{Event: "ProcessingError", FileName: "plan.pdf", GroupNumber: 123, Error: "timeout"}`. This means you can later query logs like "show me all errors for group 123" or "find all timeout errors in the last hour." Libraries like [[Serilog]] produce structured logs that can be sent to analysis platforms where they're queryable using tools like Kusto Query Language (KQL). This is essential for debugging production issues in complex systems with multiple components and services.

## Source
Industry standard formalized in the 2010s as observability became central to operations. Serilog, ELK Stack (Elasticsearch, Logstash, Kibana), and Splunk popularized structured logging for production systems.

---

## Compass

**Neighbors** — *what lives nearby*
[[JSON Logging]] is a common format for structured logs, and [[Metrics]] represent another form of structured telemetry that tracks numbers over time.

**Clash** — *what pushes against this*
[[Plain Text Logs]] are unstructured log strings that are hard to search, and [[Console Output]] is similarly ephemeral, unstructured, and unsearchable.

**Roots** — *where this comes from*
[[Logging and Observability]] treats structured logging as a pillar of effective observability, and [[Serilog]] is the library that produces the structured logs themselves.

**Paths** — *where this leads*
Structured logs are queried and analyzed in [[Application Insights]], which makes [[Debugging]] faster by enabling you to find and fix issues through powerful log search and filtering.
