---
type: atomic
tags: [coding/dotnet, coding/csharp]
date: 2026-03-24
---

# .NET 8

## Idea
.NET 8 is the cross-platform runtime and framework that compiles and executes [[CSharp]] code, providing the standard library, tooling, and hosting model for modern applications.

## Definition
.NET 8 is a Long-Term Support (LTS) release of Microsoft's open-source development platform. It includes the Common Language Runtime (CLR) that executes compiled C# code, a massive Base Class Library (BCL), and frameworks like ASP.NET Core for building [[REST API]] services. It handles memory management, just-in-time compilation, and provides built-in support for [[Dependency Injection]], configuration, logging (e.g., [[Serilog]]), and middleware pipelines. .NET 8 runs on Windows, Linux, and macOS, making it ideal for [[Docker]] containerized deployments.

## Source
KBA AI Document Ingestion project

---

## Compass

**Roots** — *where this comes from*
[[CSharp]] is the primary language that targets this runtime, and understanding the broader question of how .NET 8's minimal API model compares to the traditional controller-based approach helps contextualize its design philosophy.

**Paths** — *where this leads*
.NET 8 powers [[NuGet]] package management to extend functionality with third-party libraries, enables [[EF Core]] as the ORM framework for database access, commonly gets containerized with [[Docker]] for deployment, and integrates [[Dependency Injection]] as a first-class feature of the hosting model.

**Neighbors** — *what lives nearby*
[[Java JDK]] is Java's equivalent runtime and standard library, while [[Node.js]] serves as JavaScript's server-side runtime environment.

**Clash** — *what pushes against this*
[[Python Interpreter]] operates through runtime interpretation rather than compiling to IL then JIT-compiling, and [[Serverless Functions]] abstract away the runtime entirely.
