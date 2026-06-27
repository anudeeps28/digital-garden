---
type: atomic
tags: [coding/csharp, coding/architecture]
date: 2026-03-24
---

# DTOs (Data Transfer Objects)

## Idea
DTOs are simple classes whose only job is to carry data between layers or across network boundaries — no business logic, just properties.

## Definition
A Data Transfer Object is a plain [[CSharp]] class (or record) with properties but no methods or behavior. In [[Clean Architecture]], DTOs live in the Application layer and define the shape of data that moves between the API and the business logic. For example, a `DocumentUploadRequest` DTO carries the file, group number, and metadata from the [[Controller]] to the service layer, while a `DocumentResponse` DTO carries results back. DTOs prevent exposing internal database entities directly through the [[REST API]], which would create tight coupling and security risks.

## Source
AI document ingestion project

---

## Compass

**Roots** — *where this comes from*
DTOs enforce the separation of layers that [[Clean Architecture]] demands, ensuring that the [[REST API]] contract isn't tightly coupled to internal domain models.

**Paths** — *where this leads*
DTOs are serialized to and from [[JSON]] for API communication, and they shape what the [[Controller]] receives and returns, ultimately defining the request and response contract for [[Request and Response]] patterns.

**Neighbors** — *what lives nearby*
[[View Models]] serve a similar data-carrying purpose in UI frameworks, and [[Records in CSharp]] are the ideal construct for creating immutable DTOs in modern C#.

**Clash** — *what pushes against this*
[[Domain Entities]], by contrast, are rich objects packed with business logic rather than being simple data carriers, and [[Exposing Entities Directly]] bypasses DTOs entirely by sending database models over the wire—a practice that creates coupling and security problems.
