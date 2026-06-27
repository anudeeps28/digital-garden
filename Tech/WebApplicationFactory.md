---
type: atomic
tags: [coding/testing, coding/csharp]
date: 2026-06-26
---

# WebApplicationFactory

## Idea
A test host that boots the real API in-memory so tests hit the whole pipeline, not a stubbed slice.

## Definition
`WebApplicationFactory<T>` is the ASP.NET Core helper that spins up my actual [[DotNet 8]] API in-process — routing, [[Middleware]], DI, [[Controller]]s and all — without binding a real port. In the AI document ingestion project this is the backbone of the [[Integration Tests]]: a real HTTP request flows through the genuine [[REST API]] pipeline (often against a test database) so I catch wiring bugs that [[Unit Tests]] never see. I usually override DI registrations to swap real dependencies for fakes, which is the integration-test counterpart to using [[Moq]] in unit tests.

## Source
AI document ingestion project

---

## Compass

**Neighbors** — *what lives nearby*
[[Integration Tests]] use WebApplicationFactory as their engine to make end-to-end testing possible, and these tests run under the [[xUnit]] framework that orchestrates them.

**Clash** — *what pushes against this*
[[Unit Tests]] isolate a single class in complete isolation, whereas WebApplicationFactory exercises the entire stack end-to-end.

**Roots** — *where this comes from*
This sits at the heart of testing the [[REST API]] itself — the full pipeline that handles real HTTP requests in-memory.

**Paths** — *where this leads*
Integration tests built with WebApplicationFactory push code coverage past the threshold required by a [[Code Coverage Gate]], verifying that the whole pipeline is exercised.
