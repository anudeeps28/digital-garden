---
type: atomic
tags: [coding/testing, frontend]
date: 2026-10-04
---

# Vitest

## Idea
Vitest is a fast test runner built on Vite that speaks Jest's API, so tests use the same build pipeline as the app.

## Definition
Vitest runs tests through Vite's own transform pipeline, so TypeScript, JSX, ES modules and path aliases work in tests exactly as in the app, with no separate Babel or ts-jest setup. The API is **Jest-compatible**: `describe`, `it`, `expect`, `vi.fn()` and `vi.mock()` mirror Jest's, so migrating is mostly a find-and-replace. It runs in watch mode by default, re-running only tests affected by a change. A useful feature for full-stack repos is **multi-project configuration**: one config defines several projects, for example server tests in the `node` environment and component tests in `jsdom`, each with its own include patterns and setup files, all run with one command and one coverage report. Coverage comes from V8 or Istanbul, and an experimental browser mode runs tests in a real browser. Its main limitation is that it assumes a Vite-compatible project; outside that world, Jest is still the default.

```ts
export default defineConfig({ test: { projects: [
  { test: { name: 'server', environment: 'node', include: ['server/**/*.test.ts'] } },
  { test: { name: 'web', environment: 'jsdom', include: ['web/**/*.test.tsx'] } },
]}})
```

## Source
Created by Anthony Fu, with Vladimir Sheremet and the Vite team, starting in December 2021; version 1.0 released December 2023.

---

## Compass

**Roots** — *where this comes from*
It is a successor to [[Jest]] for the Vite ecosystem, keeping its API while replacing its module system.

**Paths** — *where this leads*
Fast watch mode makes [[Unit Tests]] cheap enough to run on every save, and coverage output feeds a [[Code Coverage Gate]].

**Neighbors** — *what lives nearby*
[[Playwright]] covers end-to-end flows that Vitest's jsdom cannot, and [[Arrange-Act-Assert]] structures its tests like any other runner.

**Clash** — *what pushes against this*
Speed tempts you to mock heavily, but [[Mock Only at the Boundary]] still applies, and jsdom is not a real browser, so passing component tests are no proof the UI works.
