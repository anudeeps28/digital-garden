---
type: atomic
tags: [coding/web-api, coding/csharp]
date: 2026-03-24
---

# Controller

## Idea
A controller is a C# class that listens for incoming HTTP requests, processes them, and sends back responses.

## Definition
In [[ASP.NET Core]] (part of [[.NET 8]]), a controller is a class that inherits from `ControllerBase` and contains action methods mapped to [[API Endpoints]]. Each method handles a specific [[HTTP Methods|HTTP method]] and URL pattern — for example, a `DocumentsController` might have a `POST Upload()` method and a `GET GetById(int id)` method. Controllers receive data via [[FromForm Attribute|[FromForm]]] or [[FromQuery Attribute|[FromQuery]]] attributes, delegate business logic to services obtained through [[Dependency Injection]], and return [[DTOs (Data Transfer Objects)]] serialized as [[JSON]] with appropriate [[HTTP Status Codes]]. In [[Clean Architecture]], controllers live in the API layer.

## Source
AI document ingestion project

---

## Compass

**Neighbors** — *what lives nearby*
[[Minimal APIs]] provide a lightweight alternative to controllers in .NET 8, while [[Express Route Handlers]] are the JavaScript equivalent in Node.js, both serving similar request-routing purposes.

**Clash** — *what pushes against this*
Controllers contrast with the [[Service Layer]], which contains the business logic that controllers delegate to, and with [[Background Workers]], which process work independently without relying on HTTP requests.

**Roots** — *where this comes from*
Controllers are the implementation layer for [[REST API]] patterns and occupy the API layer within [[Clean Architecture]], grounding them in established architectural principles.

**Paths** — *where this leads*
Controllers define [[API Endpoints]], one for each action method, and sit within a request pipeline where [[Middleware]] filters requests before they reach the controller, ultimately transforming between [[Request and Response]] types to bridge HTTP and application domains.
