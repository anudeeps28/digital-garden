---
type: atomic
tags: [coding/web-api]
date: 2026-03-24
---

# HTTP Status Codes

## Idea
Status codes are three-digit numbers that tell the client whether a request succeeded, failed, or needs something else — like 200 OK, 404 Not Found, or 500 Server Error.

## Definition
Every [[REST API]] response includes an HTTP status code indicating the outcome. They're grouped by category: **2xx** (success — 200 OK, 201 Created, 204 No Content), **4xx** (client error — 400 Bad Request, 401 Unauthorized, 403 Forbidden, 404 Not Found), and **5xx** (server error — 500 Internal Server Error, 503 Service Unavailable). In [[CSharp]] controllers, you return these using methods like `Ok()`, `BadRequest()`, `NotFound()`, or `StatusCode(500)`. Choosing the right code makes your API predictable and easier to debug.

## Source
KBA AI Document Ingestion project

---

## Compass

**Neighbors** — *what lives nearby*
[[Exit Codes]] serve a similar concept in command-line programs, where 0 signals success and non-zero values indicate failure.

**Clash** — *what pushes against this*
[[Unstructured Error Handling]] represents the opposite approach — returning 200 for everything and embedding error information in the response body instead.

**Roots** — *where this comes from*
Status codes are fundamental to [[REST API]] conventions and work hand-in-hand with [[HTTP Methods]], where different methods typically return different status codes depending on the operation's outcome.

**Paths** — *where this leads*
[[Controller|Controllers]] return specific status codes, while [[Middleware]] error-handling logic can catch exceptions and translate them into proper codes, and [[Swagger and OpenAPI]] documentation specifies which status codes each endpoint can return.
