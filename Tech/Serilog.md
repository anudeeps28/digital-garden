---
type: atomic
tags: [coding/observability, coding/dotnet]
date: 2026-03-24
---

# Serilog

## Idea
Serilog is a .NET logging library that writes structured logs — key-value pairs instead of plain text strings, making logs searchable and queryable.

## Definition
Serilog is a [[NuGet]] logging library for [[.NET 8]] that produces [[Structured Logging|structured logs]]. Instead of `Log.Info("User 123 uploaded file plan.pdf")`, you write `Log.Info("User {UserId} uploaded file {FileName}", 123, "plan.pdf")` — the values are preserved as searchable properties. Serilog can write to multiple "sinks" simultaneously: the console, files, and [[Application Insights]]. In the project, Serilog is configured in `Program.cs` and used throughout the application to log request details, processing steps, errors, and performance data. These structured logs flow into App Insights where you can query them with KQL.

## Source
AI document ingestion project

---

## Neighbors — *what lives nearby*
[[NLog]] and [[log4net]] are other popular .NET logging libraries that serve similar purposes, while [[Microsoft.Extensions.Logging]] provides a built-in logging abstraction framework within .NET itself.

## Clash — *what pushes against this*
[[Console.WriteLine]] represents the unstructured, unsearchable alternative, and running with [[No Logging]] leaves you flying blind with no visibility into app behavior.

## Roots — *where this comes from*
Serilog is installed as [[NuGet]] packages and sits at the heart of [[Logging and Observability]], serving as the logging backbone for structured observability across your application.

## Paths — *where this leads*
Serilog produces [[Structured Logging]] entries that can be queried and analyzed, sends logs to [[Application Insights]] for centralized monitoring, and works with [[Middleware]] that logs every incoming request to build comprehensive visibility into application behavior.
