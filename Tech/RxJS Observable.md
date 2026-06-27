---
type: atomic
tags: [coding/angular, frontend]
date: 2026-06-26
---

# RxJS Observable

## Idea
An Observable is a stream of values over time that you subscribe to — Angular's standard way of modelling anything asynchronous, especially HTTP calls.

## Definition
RxJS (Reactive Extensions for JavaScript) gives you Observables: lazy streams that emit zero or more values, then complete or error. Nothing happens until you `.subscribe()`, and you can transform streams with operators like `map`, `switchMap`, and `catchError`. Angular's `HttpClient` returns Observables, making them the standard way to handle asynchronous operations throughout the framework — sending requests and receiving responses. Observables can be bridged to promises via `firstValueFrom()` when needed. Observables pair with [[Angular Signals]]: the stream models the async request, while a signal holds the resolved state for the template.

## Source
Microsoft Reactive Extensions (Rx) team; RxJS first released circa 2010 as the JavaScript port of Reactive Extensions. The Reactive Extensions library was created as a unified API for asynchronous event-based programming, initially released for .NET.

---

## Neighbors — *what lives nearby*

Both [[Angular Signals]] and Observables are reactive patterns, but they handle different concerns: Observables excel at modeling async streams over time, while signals track state updates for the template to react to. Similarly, [[Async Await in CSharp]] on the backend solves the same async-handling problem, just with a different syntax and ecosystem.

## Clash — *what pushes against this*

A one-shot [[Promise]] resolves a single value once and then settles permanently, whereas an Observable can emit many values over time and be cancelled by unsubscribing, making them fundamentally different in cardinality and cancellation semantics.

## Roots — *where this comes from*

[[Angular]] itself weaves RxJS throughout its HTTP and forms APIs, making Observables the idiomatic way to handle async operations across the entire framework.

## Paths — *where this leads*

[[HTTP Interceptor|Interceptors]] operate directly on the same Observable request pipeline, allowing you to transform or side-effect on every request and response. Additionally, every call to a [[REST API]] surfaces as an Observable, so mastering them is essential for building Angular applications that talk to servers.
