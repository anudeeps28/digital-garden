---
type: atomic
tags: [coding/testing, coding/dotnet]
date: 2026-03-24
---

# Moq

## Idea
Moq is a library for creating fake/mock versions of services so you can test code without connecting to real Azure services or databases.

## Definition
Moq (pronounced "mock") is a [[NuGet]] mocking library for [[CSharp]]. It creates fake implementations of [[Interfaces in CSharp|interfaces]] at runtime — for example, `new Mock<IBlobStorageClient>()` creates a fake blob storage client that you can configure to return specific data. This lets [[Unit Tests]] verify business logic without calling real [[Azure Blob Storage]], [[Azure SQL]], or [[Azure OpenAI]]. You can also verify that specific methods were called: `mock.Verify(x => x.UploadAsync(It.IsAny<Stream>()), Times.Once)`. Moq works because the project uses [[Dependency Injection]] — services depend on interfaces, not concrete classes.

## Source
AI document ingestion project

---

## Compass

**Roots** — *where this comes from*
[[Unit Tests]] are what Moq enables through isolated testing, and [[Interfaces in CSharp]] are what Moq creates fake implementations of.

**Paths** — *where this leads*
Moq is a core tool for writing [[Unit Tests]], and it works seamlessly with [[Dependency Injection]] which enables mock injection.

**Neighbors** — *what lives nearby*
[[NSubstitute]] and [[FakeItEasy]] are both popular .NET mocking libraries that serve similar purposes, while [[Test Doubles]] is the general concept that encompasses mocks, stubs, fakes, and spies.

**Clash** — *what pushes against this*
Using [[Real Dependencies]] in tests means slower and flaky execution compared to mocked services, and [[Integration Tests]] intentionally use real services rather than mocks.
