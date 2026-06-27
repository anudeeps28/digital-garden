---
type: atomic
tags: [coding/database, coding/security]
date: 2026-03-24
---

# Connection String

## Idea
A connection string is the "address + password" your application uses to connect to a database — it tells the app where the database is and how to authenticate.

## Definition
A connection string is a formatted text string containing the server address, database name, and authentication credentials needed to connect to [[Azure SQL]] (or any database). A typical one looks like: `Server=myserver.database.windows.net;Database=KBADocIngestion;User Id=admin;Password=***;`. In the KBA project, connection strings are stored securely in [[Azure Key Vault]] — never hardcoded in source code. [[EF Core]] reads the connection string at startup to establish the database connection. Modern best practice uses **managed identity** through [[Entra ID]] instead of username/password, eliminating the need to store credentials at all.

## Source
KBA AI Document Ingestion project

---

## Neighbors — *what lives nearby*
Connection strings are similar to [[API Keys]] — another type of secret credential for accessing services — and conceptually like a [[URL]] for databases, since they provide a formatted address to a resource.

## Clash — *what pushes against this*
The opposite of a properly secured connection string is [[Hardcoded Credentials]], which embeds secrets directly in code (dangerous), or [[In-Memory Database]], which doesn't require a connection string at all.

## Roots — *where this comes from*
Connection strings exist because applications need to access [[Azure SQL]] — the database they connect to — and organizations must store them securely in something like [[Azure Key Vault]] rather than leaving them exposed.

## Paths — *where this leads*
[[EF Core]] uses the connection string to connect to the database when the application starts, and this connects to [[Security Concepts]] broadly, since connection strings must be kept secret to prevent unauthorized database access.
