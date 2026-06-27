---
type: atomic
tags: [coding/web-api]
date: 2026-03-24
---

# Request and Response

## Idea
A request is what the client sends to the API (data, headers, method), and a response is what the API sends back (status code, data, headers).

## Definition
In a [[REST API]], every interaction is a request-response cycle. The **request** contains: the [[HTTP Methods|HTTP method]], the URL ([[API Endpoints|endpoint]]), headers (like authorization [[Bearer Token|tokens]]), and optionally a body (like [[JSON]] data or a file via [[FromForm Attribute|[FromForm]]]). The **response** contains: an [[HTTP Status Codes|HTTP status code]], response headers, and optionally a body (usually [[JSON]] containing [[DTOs (Data Transfer Objects)|DTOs]]). In [[CSharp]], the [[Controller]] receives the request, processes it, and returns an `IActionResult` wrapping the response. [[Middleware]] can modify both requests and responses as they flow through the pipeline.

## Source
Roy Fielding, *Architectural Styles and the Design of Network-based Software Architectures* (doctoral dissertation, 2000); formalized in HTTP/1.1 RFC 7231 (2014).

---

## Compass

**Neighbors** — *what lives nearby*
A request is like a [[Function Call and Return|function call]], where the response serves as the return value, making the two sides of this interaction mirror computational patterns. This concept appears across distributed systems as [[Message Passing]], where the same request-response cycle enables communication between distant components.

**Clash** — *what pushes against this*
[[WebSockets]] represent a fundamentally different approach, using persistent bidirectional connections instead of discrete request-response pairs that require opening and closing connections. [[Event-Driven Architecture]] diverges further by adopting fire-and-forget patterns where systems emit events without waiting for responses, inverting the synchronous request-response model entirely.

**Roots** — *where this comes from*
Request-response is the fundamental interaction pattern in [[REST API]], where every operation adheres to this cycle. The structure of requests is governed by [[HTTP Methods]], which specify the type of operation being requested and determine how the interaction unfolds.

**Paths** — *where this leads*
The shape and content of request and response bodies are defined by [[DTOs (Data Transfer Objects)]], which standardize how data moves between client and server. [[JSON]] is the dominant format for encoding this data in both directions, and every response includes an [[HTTP Status Codes|HTTP status code]] that communicates the outcome of the request to the client.
