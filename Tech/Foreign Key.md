---
type: atomic
tags: [coding/database]
date: 2026-03-24
---

# Foreign Key

## Idea
A foreign key links one table to another — it's a column that references the primary key of a different table, creating a relationship.

## Definition
A foreign key is a column in one [[Database Tables|table]] that references the [[Primary Key]] of another table. For example, a `Plans` table might have a `GroupId` foreign key pointing to a `Groups` table, and `Groups` might have an `EmployerId` pointing to an `Employers` table, creating a hierarchy: Employer → Group → Plan. Foreign keys enforce **referential integrity** — you can't create a plan for a group that doesn't exist. In [[EF Core]], foreign keys are expressed as navigation properties (e.g., `public Group Group { get; set; }`) and EF generates the foreign key columns in relational databases like [[Azure SQL]].

## Source
E.F. Codd, "A Relational Model of Data for Large Shared Data Banks" (1970). The foundational paper that introduced the relational database model and formalized the concept of foreign keys as references maintaining referential integrity.

---

## Compass

**Neighbors** — *what lives nearby*
A [[Join Table]] serves as the middle table that uses pairs of foreign keys for many-to-many relationships. [[Navigation Properties]] are EF Core's C# representation of foreign key relationships, providing an object-oriented way to traverse these connections.

**Clash** — *what pushes against this*
[[Denormalized Data]] duplicates information instead of referencing it through foreign keys, trading referential integrity for performance. [[Unlinked Tables]] represent data silos with no relationships, avoiding the constraints that foreign keys impose.

**Roots** — *where this comes from*
[[Database Relationships]] are implemented through foreign keys, which enable one-to-many and many-to-many patterns. [[Database Tables]] are connected through foreign keys, creating the structured relationships that make relational databases work. Foreign keys always reference [[Primary Key|primary keys]], forming the foundation of relational design.

**Paths** — *where this leads*
[[EF Core]] manages foreign key relationships through navigation properties, abstracting away the low-level column details. [[JOIN (SQL)]] queries use foreign keys to combine data from multiple tables during queries. A [[Self-Referential Relationship]] occurs when a foreign key points back to its own table, enabling hierarchical structures like organizational trees.
