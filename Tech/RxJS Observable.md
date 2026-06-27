---
type: atomic
tags: [coding/angular, frontend]
date: 2026-06-26
---

# RxJS Observable

## Idea
An Observable is a stream of values over time that you subscribe to — Angular's standard way of modelling anything asynchronous, especially HTTP calls.

## Definition
RxJS (Reactive Extensions for JavaScript) gives you Observables: lazy streams that emit zero or more values, then complete or error. Nothing happens until you `.subscribe()`, and you can transform streams with operators like `map`, `switchMap`, and `catchError`. Angular's `HttpClient` returns Observables, so in the KBA AI-Doc-Ingestion project the `PlanDocumentRAG.Web` Angular 19 chat UI consumes them everywhere it talks to the [[REST API]] — sending a chat query and receiving the answer, and posting thumbs-up/down feedback. The startup config loader even bridges to a promise via `firstValueFrom(http.get('config.json'))`. Observables pair with [[Angular Signals]]: the stream models the async request, while a signal holds the resolved state for the template.

## Source
KBA AI Document Ingestion project

---

## Neighbors — *what lives nearby*

Both [[Angular Signals]] and Observables are reactive patterns, but they handle different concerns: Observables excel at modeling async streams over time, while signals track state updates for the template to react to. Similarly, [[Async Await in CSharp]] on the backend solves the same async-handling problem, just with a different syntax and ecosystem.

## Clash — *what pushes against this*

A one-shot [[Promise]] resolves a single value once and then settles permanently, whereas an Observable can emit many values over time and be cancelled by unsubscribing, making them fundamentally different in cardinality and cancellation semantics.

## Roots — *where this comes from*

[[Angular]] itself weaves RxJS throughout its HTTP and forms APIs, making Observables the idiomatic way to handle async operations across the entire framework.

## Paths — *where this leads*

[[HTTP Interceptor|Interceptors]] operate directly on the same Observable request pipeline, allowing you to transform or side-effect on every request and response. Additionally, every call to a [[REST API]] surfaces as an Observable, so mastering them is essential for building Angular applications that talk to servers.
