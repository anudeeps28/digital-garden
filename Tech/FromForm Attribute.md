---
type: atomic
tags: [coding/web-api, coding/csharp]
date: 2026-03-24
---

# FromForm Attribute

## Idea
`[FromForm]` tells a controller to read a parameter from a multipart form upload rather than the JSON body.

## Definition
In [[ASP.NET Core]], [[Controller]] action parameters are bound from the request body by default (as [[JSON]]). The `[FromForm]` attribute overrides this, telling the framework to read the value from form data instead — which is how file uploads work. When a client uploads a PDF to the the project ingestion API, the file comes as `multipart/form-data`, and the controller uses `[FromForm] IFormFile file` to receive it. This is essential for the document upload [[API Endpoints|endpoint]] where files and metadata are submitted together.

## Source
AI document ingestion project

---

## Compass

**Neighbors** — *what lives nearby*
[[FromQuery Attribute]] reads from the URL query string instead, [[FromBody]] reads from the JSON request body (the default), and [[FromRoute]] reads from URL path parameters — all are binding sources that tell the framework where to find the data.

**Clash** — *what pushes against this*
[[JSON]] represents sending data as JSON in the request body, which is the opposite approach to form data submission.

**Roots** — *where this comes from*
[[Controller]] action methods use `[FromForm]` to decorate their parameters, and [[Request and Response]] architecture controls how request data is read and processed throughout the pipeline.

**Paths** — *where this leads*
[[Ingestion]] endpoints use `[FromForm]` to receive uploaded documents, and those files are then stored in [[Azure Blob Storage]] for persistence.
