---
type: atomic
tags: [coding/database]
date: 2026-05-06
---

# JOIN (SQL)

## Idea
A JOIN combines rows from two or more tables by matching their [[Foreign Key|foreign keys]] to [[Primary Key|primary keys]] — it reassembles the full picture from data that was deliberately split apart.

## Definition
In a [[Relational Database]], data is split across [[Database Tables|tables]] to avoid redundancy. When you need the complete view, you use a JOIN to stitch tables back together. For example, if `orders` has a `user_id` foreign key pointing to `users`, a JOIN walks through orders, looks up each `user_id` in the users table, and returns combined rows with both order details and user names. The most common types: **INNER JOIN** returns only rows with matches in both tables. **LEFT JOIN** returns all rows from the left table, with NULLs where there's no match. **RIGHT JOIN** is the reverse. **FULL JOIN** returns all rows from both sides. In [[EF Core]], JOINs are expressed through LINQ and navigation properties — EF generates the SQL JOIN automatically.

## Source
Conversation with Claude — relational databases from first principles

---

## Neighbors — *what lives nearby*
[[LINQ]] is C#'s query syntax that [[EF Core]] translates into SQL JOINs, making it a kindred way of expressing relationships. JOINs fundamentally rely on [[Foreign Key|foreign keys]] to know which rows to match.

## Clash — *what pushes against this*
[[Denormalized Data]] bypasses the need for runtime JOINs by pre-joining and storing data flat, trading redundancy for performance. [[Subquery|Subqueries]] offer nested queries as an alternative approach when you don't want explicit JOINs.

## Roots — *where this comes from*
[[JOIN]] is one of [[SQL]]'s most powerful operations and sits at the heart of relational databases. [[Database Relationships]] define the structure that JOINs follow — every JOIN is expressing a relationship between tables.

## Paths — *where this leads*
[[EF Core]] generates JOIN queries automatically from C# navigation properties, abstracting away the SQL. [[Query Performance]] becomes critical when JOINs operate on large tables, requiring proper indexing and optimization.
