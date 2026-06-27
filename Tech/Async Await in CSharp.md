---
type: atomic
tags: [coding/csharp]
date: 2026-03-24
---

# Async Await in CSharp

## Idea
Async/await is C#'s pattern for writing non-blocking code that waits for slow operations (like file uploads or database calls) without freezing the application.

## Definition
In [[CSharp]], `async` marks a method as asynchronous, and `await` pauses execution until a long-running task completes — but instead of blocking the thread, it frees it up to handle other work. This is critical in web APIs where you don't want one slow database call to hold up every other incoming request. An async method returns a `Task` or `Task<T>` instead of a direct value. The [[.NET 8]] runtime manages the thread scheduling behind the scenes. In the project, nearly every service method is async because it calls [[Azure Blob Storage]], [[Azure SQL]], or [[Azure OpenAI]].

## Source
AI document ingestion project

---

## Compass

**Neighbors** — *what lives nearby*
[[JavaScript Promises]] provide JavaScript's equivalent pattern for handling asynchronous operations in much the same way. [[Reactive Programming]] represents another approach to managing async data streams and concurrent execution.

**Clash** — *what pushes against this*
[[Synchronous Code]] uses blocking execution that waits in place, tying up the thread and preventing concurrent work. [[Multi-threading]] requires manually managing threads rather than using the compiler-generated state machines that async/await provides.

**Roots** — *where this comes from*
[[CSharp]] is the language that provides this feature, and [[.NET 8]] is the runtime that manages async thread scheduling underneath. The fundamental question driving this pattern is how to handle errors in async code differently than in synchronous code.

**Paths** — *where this leads*
[[REST API]] controllers use async to handle many concurrent HTTP requests efficiently without blocking. [[Azure Functions]] relies on async as essential for event-triggered serverless functions. [[EF Core]] database queries use async methods like `SaveChangesAsync()` throughout application code.
