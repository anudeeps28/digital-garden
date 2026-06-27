---
type: atomic
tags: [coding/angular, frontend]
date: 2026-06-26
---

# Angular

## Idea
Angular is Google's TypeScript front-end framework for building single-page applications — the foundation of The project's UAT chat UI.

## Definition
Angular is a batteries-included framework (router, HTTP client, dependency injection, forms, change detection) written in and authored with [[TypeScript]]. Unlike a library, it dictates a lot of structure, which is why it scales well for real applications. In the AI document ingestion project, the `PlanDocumentRAG.Web` app is Angular 19 and serves the UAT chat interface where reviewers query plan documents and read LLM answers. It leans on the modern Angular surface: [[Standalone Components]] instead of NgModules, [[Zoneless Change Detection]], [[Angular Signals]] for reactive state, [[MSAL Authentication]] against [[Entra ID]], and a [[Runtime Config (Build Once Deploy Everywhere)|config.json]] loaded at startup so one build runs in every environment.

## Source
AI document ingestion project

---

## Compass

**Roots** — *where this comes from*
Angular emerges from the need to scale front-end development, and [[Runtime Config (Build Once Deploy Everywhere)]] is the paradigm that allows one Angular build to adapt across different environments.

**Paths** — *where this leads*
Angular manifests through its building blocks like [[Standalone Components]], which form the foundation of modern Angular apps, and extends to [[MSAL Authentication]], which determines how the app logs users in and protects access.

**Neighbors** — *what lives nearby*
Angular is written in [[TypeScript]], the language that underpins its type-safe development, and it functions as a client that talks to a [[REST API]] on the backend, creating a clear separation between front-end and API layers.

**Clash** — *what pushes against this*
Angular is a client-side single-page application, standing in contrast to a plain server-rendered MVC view where HTML is generated on the server and sent to the browser.
