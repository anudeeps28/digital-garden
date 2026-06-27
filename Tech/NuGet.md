---
type: atomic
tags: [coding/dotnet]
date: 2026-03-24
---

# NuGet

## Idea
NuGet is the package manager for .NET — it lets you install and manage third-party libraries in your project.

## Definition
NuGet is to [[.NET 8]] what npm is to JavaScript — a central repository of reusable code packages. You add a package (like [[Moq]] or [[Serilog]]) via `dotnet add package` or Visual Studio, and NuGet downloads it plus all its dependencies. Packages are listed in the `.csproj` file and restored automatically on build. In practice, you can leverage specialized libraries for testing ([[xUnit]], [[Moq]]), logging ([[Serilog]]), and database access ([[EF Core]]) rather than building everything from scratch.

## Source
Microsoft, introduced in 2010 as the official package manager for the .NET ecosystem. First released as part of NuGet 1.0, it became the standard dependency management tool for C# and .NET projects.

---

## Compass

**Neighbors** — *what lives nearby*
NuGet fills the same niche as other language ecosystems — [[npm]] for JavaScript, [[pip]] for Python, and [[Maven]] for Java all serve as central repositories where developers share and discover reusable packages.

**Clash** — *what pushes against this*
The opposite approach is [[Writing Everything From Scratch]], where you build every utility yourself instead of leveraging packages. Another alternative is [[Vendoring]], where you copy source code directly into your repository rather than maintaining a reference to an external package.

**Roots** — *where this comes from*
NuGet exists within the broader [[.NET 8]] ecosystem it serves, and a key underlying question is how you evaluate whether a NuGet package is trustworthy and maintained.

**Paths** — *where this leads*
NuGet enables the adoption of specialized libraries like [[PdfPig]] for PDF parsing, [[xUnit]] for testing, [[Serilog]] for structured logging, and [[EF Core]] for database access — each solving a distinct problem within your .NET applications.
