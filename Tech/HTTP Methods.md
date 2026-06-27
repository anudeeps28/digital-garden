---
type: atomic
tags: [coding/web-api]
date: 2026-03-24
---

# HTTP Methods

## Idea
HTTP methods are the verbs that tell an API what action to perform on a resource — GET reads, POST creates, PUT updates, DELETE removes.

## Definition
HTTP methods (also called HTTP verbs) define the type of operation a client wants to perform when calling a [[REST API]]. The four main methods are: **GET** (retrieve data without changing anything), **POST** (create a new resource), **PUT** (update an existing resource), and **DELETE** (remove a resource). Each [[API Endpoints|endpoint]] combines an HTTP method with a URL path — for example, `POST /api/resources` creates a new resource, while `GET /api/resources/123` retrieves one. In practice, [[Controller]] methods in [[CSharp]] are decorated with attributes like `[HttpGet]` or `[HttpPost]` to map to these verbs.

## Source
Roy Fielding, doctoral dissertation *Architectural Styles and the Design of Network-based Software Architectures* (2000); formalized in HTTP/1.1 specification RFC 7231 (2014).

---

## Compass

**Neighbors** — *what lives nearby*
[[CRUD Operations]] maps directly to HTTP methods — Create/Read/Update/Delete align perfectly with POST/GET/PUT/DELETE. At the database level, [[SQL]] provides the same operations with SELECT, INSERT, UPDATE, and DELETE, making HTTP methods the API-level equivalent of SQL commands.

**Clash** — *what pushes against this*
[[RPC Style APIs]] reject this verb-based approach entirely, using a single POST method for all operations instead. Similarly, [[GraphQL]] typically uses only POST for all queries and mutations, moving away from the semantic clarity that HTTP methods provide.

**Roots** — *where this comes from*
HTTP methods are foundational to [[REST API]] design, serving as the core principle that distinguishes REST from other architectural approaches. The question of when to use PUT vs PATCH for updates remains a key decision point in API design.

**Paths** — *where this leads*
Each HTTP method carries implications for [[HTTP Status Codes]] — the server responds with appropriate codes for each verb. In [[CSharp]], [[Controller|controllers]] map these methods to HTTP verbs through attributes, and [[Middleware]] can filter or intercept requests based on the HTTP method used.
