---
type: atomic
tags: [devops, coding/testing]
date: 2026-06-26
---

# CodeQL

## Idea
A static analyzer that reads code as a queryable database and hunts for security holes before they ship.

## Definition
CodeQL is GitHub's static-analysis engine that scans source for security vulnerabilities — SQL injection, unsafe deserialization, leaked secrets — as an automated step in the [[CI-CD Pipeline]]. On the KBA AI Document Ingestion project it runs against the C# code without executing it, treating the codebase as a database it can query for dangerous patterns. It's a security-focused sibling of the [[Code Coverage Gate]]: both are machine gates that can fail the build, embodying [[Fail Fast Fail Loudly]] by catching problems in CI rather than in production. It complements human [[Pull Request]] review and [[Code Rabbit]] rather than replacing them.

## Source
KBA AI Document Ingestion project

---

## Compass

**Neighbors** — *what lives nearby*
[[Code Coverage Gate]] is another automated CI quality gate that works alongside CodeQL, and [[Code Rabbit]] provides similar automated review tooling on pull requests.

**Clash** — *what pushes against this*
[[Pull Request]] review relies on human eyes to find issues, whereas CodeQL uses automated static scanning without that human judgment.

**Roots** — *where this comes from*
CodeQL operates as a scanning step within the [[CI-CD Pipeline]], forming part of the automated quality gates in the build process.

**Paths** — *where this leads*
A clean CodeQL scan supports moving toward [[Pre-deploy Approvals]], removing a blocker to releasing the code.
