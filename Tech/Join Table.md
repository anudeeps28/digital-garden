---
type: atomic
tags: [coding/database]
date: 2026-05-06
---

# Join Table

## Idea
A join table is a middle table whose only job is to connect two other tables in a many-to-many relationship — it holds pairs of [[Foreign Key|foreign keys]].

## Definition
When two [[Database Tables|tables]] have a many-to-many [[Database Relationships|relationship]] (e.g., students and courses), there's no clean way to store the connection with a single foreign key in either table. The solution is a **join table** (also called junction table, bridge table, or associative table) that sits between them. It has at minimum two foreign key columns — one pointing to each side. For example, an `enrollments` table with `student_id` and `course_id`. Each row represents one connection: "this student is in this course." Join tables often carry extra data about the relationship itself — like a grade, enrollment date, or role. In [[EF Core]], many-to-many relationships can be configured with an explicit join entity or EF can create the join table implicitly.

## Source
Conversation with Claude — database relationships from first principles

---

## Compass

**Neighbors** — *what lives nearby*
Join tables are built from pairs of [[Foreign Key|foreign keys]] and implement the many-to-many pattern that [[Database Relationships|database relationships]] require.

**Clash** — *what pushes against this*
Instead of using join tables, you could store all data in one flat table — [[Denormalized Data]] — or use a direct foreign key in one table, though this approach only works for one-to-many relationships, not many-to-many.

**Roots** — *where this comes from*
Join tables are a fundamental pattern in [[Relational Database|relational design]], emerging from the core constraint that many-to-many relationships can't work with just a single foreign key column in either table.

**Paths** — *where this leads*
Querying through a join table requires joining three tables with [[JOIN (SQL)|SQL joins]], and in [[EF Core]], many-to-many relationships can be either auto-generated or explicitly configured with join entities.
