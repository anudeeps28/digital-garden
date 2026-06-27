---
type: atomic
tags: [coding/database]
date: 2026-03-24
---

# Primary Key

## Idea
A primary key is a unique identifier for each row in a table — no two rows can share the same primary key value.

## Definition
Every [[Database Tables|table]] in a relational database needs a primary key — a column (or combination of columns) that uniquely identifies each record. Typically this is an auto-incrementing integer `Id` column or a GUID. Primary keys enforce uniqueness (you can't accidentally insert duplicate records) and serve as the target for [[Foreign Key|foreign keys]] in related tables. In [[EF Core]], a property named `Id` or `{ClassName}Id` is automatically treated as the primary key.

## Source
E.F. Codd, foundational concept in relational database theory introduced in *A Relational Model of Data for Large Shared Data Banks* (1970). Primary keys are a core mechanism of SQL, formalized in early SQL standards.

---

## Compass

**Neighbors** — *what lives nearby*
A [[GUID]] is often used as a primary key because it provides global uniqueness, while a [[Natural Key]] uses a real-world value like an SSN as the identifier instead of relying on an auto-generated one.

**Clash** — *what pushes against this*
Without a primary key constraint, you get [[Duplicate Records]] in your table; alternatively, a [[Composite Key]] combines multiple columns together to serve as the unique identifier rather than using a single column.

**Roots** — *where this comes from*
Primary keys are fundamental to [[Database Tables]] — every table has one — and they're defined using [[SQL]] in CREATE TABLE statements.

**Paths** — *where this leads*
Other tables reference primary keys through [[Foreign Key|foreign keys]] to create relationships between tables, and [[EF Core]] automatically detects and configures primary keys in your model.
