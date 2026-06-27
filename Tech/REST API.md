---
type: atomic
tags:
  - coding/web-api
date: 2026-03-24
---

# REST API

## Idea
A standard way of building web services that uses HTTP to let clients read, create, update, and delete resources.

## Definition
REST (Representational State Transfer) is an architectural style for designing networked applications. A REST API exposes resources (like documents, users, or groups) at specific URLs and uses [[HTTP Methods]] (GET, POST, PUT, DELETE) to perform operations on them. Each request is stateless — the server doesn't remember previous requests. Data is typically sent and received as [[JSON]]. In practice, REST APIs are implemented using frameworks like [[ASP.NET Core]], where [[Controller]] classes map incoming HTTP requests to handler methods.

## Source
Roy Fielding, doctoral dissertation *Architectural Styles and the Design of Network-based Software Architectures* (2000). REST emerged as a formalization of the architectural principles already embedded in HTTP/1.1.

---

## Neighbors — *what lives nearby*

[[GraphQL]] and [[gRPC]] are alternative API styles that serve similar purposes: GraphQL lets clients request exactly the data they need, while gRPC is a high-performance framework using protocol buffers instead of JSON.

## Clash — *what pushes against this*

[[SOAP]] is an older, XML-based protocol with strict contracts and heavier overhead that predates the simplicity of REST. The opposite architectural approach would be [[Monolithic UI]], which embeds all logic in server-rendered pages instead of exposing an API.

## Roots — *where this comes from*

REST APIs are a key component of [[Software Architecture]] and modern system design, sitting specifically in the API layer of [[Clean Architecture]]. A foundational question in building REST services is: how do you version a REST API as it evolves?

## Paths — *where this leads*

REST APIs expose [[API Endpoints]]—the specific URLs clients interact with—and use [[HTTP Status Codes]] to communicate success or failure. Documentation is typically generated automatically via [[Swagger and OpenAPI]], and security is enforced through [[Authentication]] to ensure only authorized callers can access the API.
