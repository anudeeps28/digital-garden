---
type: atomic
tags: [coding/angular, frontend]
date: 2026-06-26
---

# Standalone Components

## Idea
Standalone components are Angular components that declare their own dependencies directly, doing away with the old NgModule ceremony.

## Definition
Before Angular 14, every component had to be declared inside an NgModule and that module had to import whatever the component needed. Standalone components flip this: the component itself carries an `imports: [...]` array listing exactly what it uses, so there's no separate module file to wire up. From Angular 17 onward this is the default. In the AI document ingestion project, the `PlanDocumentRAG.Web` Angular 19 chat UI is built entirely from standalone components — the chat shell, the document viewer, and the message list each import their own pieces. Bootstrapping happens through `bootstrapApplication()` with a flat list of providers rather than a root module, which is also where [[MSAL Authentication]] and the [[APP_INITIALIZER]] config loader are registered.

## Source
AI document ingestion project

---

## Neighbors — *what lives nearby*
Standalone components still use Angular's [[Dependency Injection]] — they just declare imports locally. They are the modern building block of an [[Angular]] app, representing the framework's evolution toward more modular composition.

## Clash — *what pushes against this*
NgModule-based components represent the older pattern that required a central module to declare and wire everything, creating indirection and boilerplate that standalone components eliminate.

## Roots — *where this comes from*
This concept belongs to the broader [[Angular]] framework architecture that defines the fundamental building blocks of modern web applications.

## Paths — *where this leads*
Standalone components pair naturally with modern Angular features like [[Zoneless Change Detection]] that optimize performance. They also work seamlessly with the [[APP_INITIALIZER]] pattern, which is registered as a provider during standalone bootstrap to handle application startup logic.
