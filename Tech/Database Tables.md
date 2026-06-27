---
type: atomic
tags: [coding/database]
date: 2026-03-24
---

# Database Tables

## Idea
Tables are like spreadsheets in a database — each row is one record, each column is a field, and they store structured data.

## Definition
In a relational database like [[Azure SQL]], data is organized into tables. Each table has a defined set of columns (fields with specific data types) and rows (individual records). For example, a customer table might have columns for `Id`, `Name`, `Email`, and `CreatedDate`. Tables are related to each other through [[Foreign Key|foreign keys]] — one table might reference another to establish relationships between entities. In [[CSharp]], tables map to entity classes, and [[EF Core]] handles the mapping between C# objects and database rows.

## Source
Edgar F. Codd, foundational concept in relational database theory introduced in his 1970 paper *A Relational Model of Data for Large Shared Data Banks*.

---

## Compass

**Neighbors** — *what lives nearby*
[[Spreadsheets]] have a similar visual concept with rows and columns, and [[CSV Files]] are the flat file equivalent of a single table.

**Clash** — *what pushes against this*
[[Document Databases]] store flexible JSON-like documents instead of rigid rows, while [[Key-Value Stores]] use simple key-to-value lookups without any columns.

**Roots** — *where this comes from*
[[SQL]] is the language for querying tables, and [[Azure SQL]] is the database engine that hosts them.

**Paths** — *where this leads*
Every table needs a [[Primary Key]] to uniquely identify each row, and tables link to each other through [[Foreign Key|foreign keys]]. In [[CSharp]], [[EF Core]] maps classes to database tables.
