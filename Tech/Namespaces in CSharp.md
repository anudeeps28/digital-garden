---
type: atomic
tags: [coding/csharp]
date: 2026-03-24
---

# Namespaces in CSharp

## Idea
Namespaces are folders for code — they organize classes into logical groups and prevent naming collisions.

## Definition
In [[CSharp]], a namespace is a way to group related classes, interfaces, and [[DTOs (Data Transfer Objects)]] under a hierarchical name like `MyApplication.Services.Auth`. They mirror project structure in [[Clean Architecture]] — each layer has its own namespace (e.g., `Domain`, `Application`, `Infrastructure`). Namespaces prevent two classes with the same name from conflicting and make `using` statements at the top of files act like import declarations, pulling in only the code you need.

## Source
Microsoft, introduced in C# 1.0 as part of the .NET Framework (2002). The concept draws from earlier language design principles, particularly C++'s namespace feature (introduced in C++ standard in 1998).

---

## Compass

**Neighbors** — *what lives nearby*
[[Modules in JavaScript]] provide JavaScript's way of organizing and importing code, much like namespaces do in C#. Similarly, [[Packages in Java]] serve as Java's equivalent organizational unit for grouping related code.

**Clash** — *what pushes against this*
[[Global Scope]] represents the opposite approach — dumping everything into one namespace with no organization, leading to chaos and naming conflicts.

**Roots** — *where this comes from*
Namespaces are a feature of [[CSharp]], the language that provides this organizational mechanism, and they closely align with [[Clean Architecture]]'s philosophy where namespaces reflect the layer structure of your application.

**Paths** — *where this leads*
[[NuGet]] packages expose their code through namespaces you import when consuming external libraries, and [[Dependency Injection]] relies on registering services from specific namespaces to wire up your application's dependencies.
