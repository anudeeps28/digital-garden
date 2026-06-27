---
type: atomic
tags: [coding/web-api]
date: 2026-03-24
---

# Swagger and OpenAPI

## Idea
Swagger/OpenAPI auto-generates interactive documentation for your API, letting you test endpoints directly in a browser.

## Definition
OpenAPI is a specification for describing [[REST API]] endpoints in a machine-readable format. Swagger is the tooling that renders this specification as a web page where you can see every [[API Endpoints|endpoint]], its parameters, [[HTTP Methods|methods]], expected [[Request and Response|request/response]] shapes, and [[HTTP Status Codes]]. In practice, when building [[.NET]] applications with Swashbuckle, the package automatically scans your [[Controller]] classes and generates a Swagger UI at `/swagger`. This makes it easy for developers to explore and test the API without writing any client code.

## Source
SmartBear Software introduced Swagger in 2011 as a framework for describing and documenting RESTful APIs. The OpenAPI Specification (OAS) evolved from Swagger; it was donated to the Linux Foundation in 2015 and is now maintained as the OpenAPI Initiative, with the specification being vendor-neutral and community-driven. Swagger UI is the reference implementation for rendering OpenAPI specifications as interactive documentation.

---

## Neighbors — *what lives nearby*
[[Postman]] is a standalone tool for testing APIs manually, providing similar hands-on exploration of endpoints. [[API Blueprint]] is another API documentation format that serves a comparable purpose of specifying API structure.

## Clash — *what pushes against this*
[[Undocumented APIs]] have no specification or documentation, standing in contrast to Swagger's machine-readable specification approach. [[Manual Documentation]], where API docs are written by hand, is error-prone and tends to get outdated quickly compared to auto-generated specifications.

## Roots — *where this comes from*
[[REST API]] is the architectural style that Swagger documents, providing the foundation for what OpenAPI describes.

## Paths — *where this leads*
[[API Endpoints]] are what Swagger lists and exposes in its UI, making them discoverable. [[DTOs (Data Transfer Objects)]] are visualized through Swagger's schema display, showing developers the expected data shapes. [[Authentication]] can be integrated into the Swagger UI, allowing developers to input auth tokens directly when testing endpoints.
