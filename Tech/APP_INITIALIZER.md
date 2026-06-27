---
type: atomic
tags: [coding/angular, frontend]
date: 2026-06-26
---

# APP_INITIALIZER

## Idea
APP_INITIALIZER is an Angular provider hook that runs async startup work — like fetching config.json — and makes the app wait for it before bootstrapping.

## Definition
You register a provider for the `APP_INITIALIZER` token whose factory returns a Promise (or Observable); Angular will not finish bootstrapping the app until that Promise resolves. This is the canonical place to do "load something the whole app needs before it starts." In practice, an Angular app may use it to fetch [[Runtime Config (Build Once Deploy Everywhere)|config.json]] at startup via `firstValueFrom(http.get('config.json'))`, populating a `ConfigService` with environment-specific settings like API base URL or authentication parameters. Because this completes before bootstrap, services like [[MSAL Authentication]] can safely read the config the moment they're constructed — which enables patterns like build-once-deploy-everywhere. (In newer Angular this is also expressed as `provideAppInitializer(...)`.)

## Source
Google Angular team; introduced in Angular 2 (2016) as part of the core bootstrap lifecycle. Documented in the official [Angular Platform Browser documentation](https://angular.io/api/platform-browser/APP_INITIALIZER).

---

## Neighbors — *what lives nearby*
[[Runtime Config (Build Once Deploy Everywhere)]] is the pattern that APP_INITIALIZER enables, allowing you to defer bootstrap until essential configuration is loaded. [[Dependency Injection]] provides the mechanism for registering it as a provider in Angular's DI system.

## Clash — *what pushes against this*
Build-time `environment.ts` constants are baked in at compile time and need no async load, making them simpler but less flexible than the APP_INITIALIZER pattern.

## Roots — *where this comes from*
[[Angular]]'s bootstrap lifecycle includes this provider token as a built-in mechanism for initializing application state before any components load, following the principle that prerequisites should be resolved before dependents are created.

## Paths — *where this leads*
Authentication services can safely read configuration at injection time because APP_INITIALIZER ensures such data is loaded before any service or component is instantiated. [[Standalone Components]] register APP_INITIALIZER among their providers during standalone bootstrap, extending the pattern beyond traditional module-based applications.
