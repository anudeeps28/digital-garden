---
type: atomic
tags: [coding/testing]
date: 2026-06-26
---

# Playwright

## Idea
A robot that drives a real browser through the app the way a user would, then checks it behaved.

## Definition
Playwright is a browser-automation framework that launches a real browser and drives it through an application the way a user would, then asserts the results. In practice, E2E test suites use Playwright to exercise the front end, APIs, and database together as one system. It sits at the top of the testing pyramid: broad, realistic, and slower than unit tests, so it's best kept limited and high-value while [[Jest]] and [[xUnit]] handle the fast, numerous [[Unit Tests]]. Failures here surface exactly the cross-layer breakage that isolated tests miss, which is [[Fail Fast Fail Loudly]] at the system level.

## Source
Microsoft, first released 2019 as an open-source browser automation framework. Initial versions supported Chromium, Firefox, and WebKit across Windows, macOS, and Linux.

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
