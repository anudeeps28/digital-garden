---
type: atomic
tags: [coding/angular, frontend]
date: 2026-06-26
---

# APP_INITIALIZER

## Idea
APP_INITIALIZER is an Angular provider hook that runs async startup work — like fetching config.json — and makes the app wait for it before bootstrapping.

## Definition
You register a provider for the `APP_INITIALIZER` token whose factory returns a Promise (or Observable); Angular will not finish bootstrapping the app until that Promise resolves. This is the canonical place to do "load something the whole app needs before it starts." In the AI document ingestion project, the `PlanDocumentRAG.Web` Angular 19 app uses it to fetch [[Runtime Config (Build Once Deploy Everywhere)|config.json]] at startup via `firstValueFrom(http.get('config.json'))`, populating a `ConfigService` with the API base URL and MSAL settings. Because this completes before bootstrap, [[MSAL Authentication]] and other services can safely read the config the moment they're constructed — which is exactly what makes the build-once-deploy-everywhere pattern possible. (In newer Angular this is also expressed as `provideAppInitializer(...)`.)

## Source
AI document ingestion project

---

## Neighbors — *what lives nearby*
[[Runtime Config (Build Once Deploy Everywhere)]] is the pattern that APP_INITIALIZER enables, allowing you to defer bootstrap until essential configuration is loaded. [[Dependency Injection]] provides the mechanism for registering it as a provider in Angular's DI system.

## Clash — *what pushes against this*
Build-time `environment.ts` constants are baked in at compile time and need no async load, making them simpler but less flexible than the APP_INITIALIZER pattern.

## Roots — *where this comes from*
[[Angular]] provides this as part of its framework bootstrap lifecycle, giving developers a hook to inject async work early.

## Paths — *where this leads*
[[MSAL Authentication]] can safely read config the instant it's needed because APP_INITIALIZER ensures it's available before any service is constructed. [[Standalone Components]] register APP_INITIALIZER among their providers during standalone bootstrap, extending the pattern beyond traditional module-based applications.
