---
type: atomic
tags: [coding/angular, frontend]
date: 2026-06-27
---

# Standalone Components

## Idea
Standalone components are Angular components that declare their own dependencies directly, doing away with the old NgModule ceremony.

## Definition
Before Angular 14, every component had to be declared inside an NgModule and that module had to import whatever the component needed. Standalone components flip this: the component itself carries an `imports: [...]` array listing exactly what it uses, so there's no separate module file to wire up. From Angular 17 onward this is the default. In practice, a standalone chat UI might have a chat shell, document viewer, and message list, each importing their own dependencies directly. Bootstrapping happens through `bootstrapApplication()` with a flat list of providers rather than a root module, which is also where [[MSAL Authentication]] and the [[APP_INITIALIZER]] config loader are registered.

## Source
Angular team at Google; introduced as a developer preview in Angular 14 (May 2022), became the recommended pattern in Angular 15, and the default in Angular 17 (November 2023). See the Angular documentation on standalone components and RFC 0016.

---

## Neighbors — *what lives nearby*
Standalone components still use Angular's [[Dependency Injection]] — they just declare imports locally. They are the modern building block of an [[Angular]] app, representing the framework's evolution toward more modular composition.

## Clash — *what pushes against this*
NgModule-based components represent the older pattern that required a central module to declare and wire everything, creating indirection and boilerplate that standalone components eliminate.

## Roots — *where this comes from*
This concept belongs to the broader [[Angular]] framework architecture that defines the fundamental building blocks of modern web applications.

## Paths — *where this leads*
Standalone components pair naturally with modern Angular features like [[Zoneless Change Detection]] that optimize performance. They also work seamlessly with the [[APP_INITIALIZER]] pattern, which is registered as a provider during standalone bootstrap to handle application startup logic.
