---
type: atomic
tags: [coding/web-api, coding/csharp]
date: 2026-03-24
---

# Middleware

## Idea
Middleware is code that runs on every HTTP request before it reaches your controller — used for cross-cutting concerns like authentication, logging, and error handling.

## Definition
In [[ASP.NET Core]] ([[.NET 8]]), middleware components form a pipeline that each request passes through. Each piece of middleware can inspect or modify the [[Request and Response|request]], do some work, and then pass it to the next middleware in the chain — or short-circuit and return a response immediately (e.g., rejecting unauthenticated requests). Common middleware includes: [[Authentication]] (validating [[Bearer Token|tokens]]), [[Serilog|logging]] (recording each request), error handling (catching exceptions and returning proper [[HTTP Status Codes]]), and CORS (allowing cross-origin requests). Middleware is registered in `Program.cs` and runs in the order it's added.

## Source
AI document ingestion project

---

## Roots — *where this comes from*
Middleware is part of the [[REST API]] request pipeline, and lives in the [[Clean Architecture]] API layer as a foundational pattern for handling cross-cutting concerns consistently.

## Paths — *where this leads*
[[Authentication]] middleware validates tokens before the request reaches the controller, while [[Serilog]] logging middleware records request/response details, and both can feed telemetry data to [[Application Insights]] for monitoring and observability.

## Neighbors — *what lives nearby*
[[Express Middleware]] implements the same concept in Node.js/Express environments, and [[Interceptors]] follow a similar pattern in other frameworks like Angular and Spring.

## Clash — *what pushes against this*
[[Controller|Controllers]] handle specific endpoint logic rather than cross-cutting concerns, and [[Inline Checks]] — putting auth/logging code directly in every controller method — defeat the purpose of middleware by creating duplication and maintenance burden.
