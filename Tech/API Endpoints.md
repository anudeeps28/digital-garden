---
type: atomic
tags: [coding/web-api]
date: 2026-03-24
---

# API Endpoints

## Idea
Endpoints are specific URLs your API exposes — each one is an address where clients can send requests to perform an action.

## Definition
An API endpoint is a combination of an [[HTTP Methods|HTTP method]] and a URL path that maps to a specific [[Controller]] action. For example, `POST /api/documents/upload` is an endpoint that accepts a file upload, while `GET /api/documents/{id}` retrieves a specific document. Endpoints define the public contract of your [[REST API]] — what operations are available and where to find them. In [[.NET 8]], endpoints are defined using route attributes on controller methods like `[Route("api/[controller]")]` and `[HttpPost("upload")]`. [[Swagger and OpenAPI]] auto-generates documentation for all endpoints.

## Source
KBA AI Document Ingestion project

---

## Compass

**Neighbors** — *what lives nearby*
[[Routes]] define the URL patterns that map to endpoints, while [[GraphQL Queries]] represent a similar concept but with a single endpoint and more flexible query structures.

**Clash** — *what pushes against this*
[[Internal Methods]] are private code that isn't exposed over HTTP, and [[Background Processing]] handles work that happens without an endpoint trigger.

**Roots** — *where this comes from*
Endpoints are the building blocks of a [[REST API]], and each [[Controller]] method defines one or more endpoints that serve as entry points for the API.

**Paths** — *where this leads*
Each endpoint returns appropriate [[HTTP Status Codes]], defines what it accepts and returns through [[Request and Response]] contracts, and can require [[Authentication]] for authorization.
