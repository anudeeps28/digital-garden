---
type: atomic
tags: [coding/testing]
date: 2026-06-26
---

# Playwright

## Idea
A robot that drives a real browser through the app the way a user would, then checks it behaved.

## Definition
Playwright is the browser-automation framework behind the KBA AI Document Ingestion project's end-to-end tests (they live under `tests/e2e`). It launches a real browser, clicks through the [[Angular]] UI, uploads a document, and asserts the result — exercising the front end, the [[REST API]], and the database together as one system. It sits at the top of the testing pyramid: broad, realistic, and slower, so I keep these few and high-value while [[Jest]] and [[xUnit]] handle the fast, numerous [[Unit Tests]]. Failures here surface exactly the cross-layer breakage that isolated tests miss, which is [[Fail Fast Fail Loudly]] at the system level.

## Source
KBA AI Document Ingestion project

---

## Compass

**Neighbors** — *what lives nearby*
Like [[Integration Tests]], Playwright exercises multiple layers together rather than testing one unit in isolation. Similarly, [[WebApplicationFactory]] provides API-level analogues of full-pipeline testing, combining components into realistic end-to-end workflows.

**Clash** — *what pushes against this*
[[Jest]] represents the opposite approach — fast, isolated unit tests that contrast with Playwright's slow, whole-app browser tests that require real infrastructure.

**Roots** — *where this comes from*
Playwright fits into the broader [[CI-CD Pipeline]], where the E2E suite runs as a gate before deployment, representing the integration-testing level of continuous deployment practices.

**Paths** — *where this leads*
Success in E2E testing feeds directly into [[Pre-deploy Approvals]], where green Playwright results provide the confidence needed to approve a release and push to production.
