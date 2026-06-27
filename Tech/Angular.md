---
type: atomic
tags: [coding/angular, frontend]
date: 2026-06-26
---

# Angular

## Idea
Angular is Google's TypeScript front-end framework for building single-page applications.

## Definition
Angular is a batteries-included framework (router, HTTP client, dependency injection, forms, change detection) written in and authored with [[TypeScript]]. Unlike a library, it dictates a lot of structure, which is why it scales well for real applications. Modern Angular emphasizes [[Standalone Components]] instead of NgModules, [[Zoneless Change Detection]], and [[Angular Signals]] for reactive state management. In practice, Angular applications often integrate with authentication systems like [[MSAL Authentication]] and use [[Runtime Config (Build Once Deploy Everywhere)]] patterns to enable a single build artifact to run across different environments.

## Source
Google, introduced in 2010; originally developed by Google engineers Misko Hevery and Adam Abrons. AngularJS (1.x) was the initial framework; Angular 2+ (2016 onwards) was a complete rewrite in TypeScript and became the modern standard.

---

## Compass

**Roots** — *where this comes from*
Angular emerges from Google's need to scale front-end development at enterprise scale. It builds on the Web Components model and the rise of TypeScript to bring structure and type safety to large single-page applications.

**Paths** — *where this leads*
Angular manifests through its building blocks like [[Standalone Components]], which form the foundation of modern Angular apps, and extends to [[MSAL Authentication]], which determines how the app logs users in and protects access.

**Neighbors** — *what lives nearby*
Angular is written in [[TypeScript]], the language that underpins its type-safe development, and it functions as a client that talks to a [[REST API]] on the backend, creating a clear separation between front-end and API layers.

**Clash** — *what pushes against this*
Angular is a client-side single-page application, standing in contrast to a plain server-rendered MVC view where HTML is generated on the server and sent to the browser.
