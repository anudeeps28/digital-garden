---
type: atomic
tags: [coding/web-api, coding/csharp]
date: 2026-03-24
---

# FromQuery Attribute

## Idea
`[FromQuery]` tells a controller to read a parameter from the URL query string — like `?groupNumber=123`.

## Definition
In [[ASP.NET Core]], the `[FromQuery]` attribute binds a [[Controller]] method parameter to a value in the URL's query string. For example, `GET /api/documents?groupNumber=123` would map to a method parameter `[FromQuery] string groupNumber`. This is commonly used for optional filters, search terms, and pagination parameters on GET [[API Endpoints|endpoints]]. Unlike [[FromForm Attribute|[FromForm]]], which reads from uploaded form data, `[FromQuery]` reads from the URL itself, making it visible and bookmarkable.

## Source
AI document ingestion project

---

## Compass

**Neighbors** — *what lives nearby*
[[FromForm Attribute]] reads from form data instead of the query string, while [[FromRoute]] reads from URL path segments like `/api/documents/{id}`, and [[FromBody]] reads from the request body. These are the other binding sources available in ASP.NET Core.

**Clash** — *what pushes against this*
[[FromForm Attribute]] reads from form post data rather than the URL, and [[Request Body]] keeps data hidden in the body rather than visible in the URL, making `[FromQuery]` unsuitable for sensitive information.

**Roots** — *where this comes from*
`[FromQuery]` decorates [[Controller]] method parameters as part of the binding system, and [[REST API|query parameters are a standard REST convention]] for filtering and customizing requests.

**Paths** — *where this leads*
Query parameters extend [[API Endpoints|endpoint functionality]] by allowing flexible filtering and pagination, and they're documented by [[Swagger and OpenAPI|tools like Swagger]] that automatically generate endpoint documentation including query parameters.
