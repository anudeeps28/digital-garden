---
type: atomic
tags: [coding/database]
date: 2026-05-06
---

# Self-Referential Relationship

## Idea
A self-referential relationship is when a table has a [[Foreign Key]] that points back to its own [[Primary Key]] — the table relates to itself.

## Definition
Sometimes both sides of a [[Database Relationships|relationship]] are the same entity. A `friendships` table where both `user_id` and `friend_id` point to the `users` table. An `employees` table where `manager_id` points back to another row in `employees`. A `categories` table where `parent_category_id` points to another category. This is how social networks (friendships), family trees (parent-child), org charts (manager-employee), threaded comments (reply-to), and hierarchical categories are modeled. The mechanics are the same as any other relationship — it's just that both foreign keys reference the same table. Self-referential relationships can be one-to-many (employee → manager) or many-to-many (user ↔ friends, using a [[Join Table]]).

## Source
Conversation with Claude — social network database example

---

## Compass

**Neighbors** — *what lives nearby*
The [[Foreign Key]] mechanism is the same, just pointing to the same table, and self-referential relationships are really a special case of the standard [[Database Relationships|relationship]] patterns.

**Clash** — *what pushes against this*
Standard cross-table relationships connect two different entities, whereas self-references turn inward, and [[Denormalized Data]] flattens hierarchies instead of modeling self-references properly.

**Roots** — *where this comes from*
Self-referential relationships demonstrate the flexibility of the [[Relational Database]] model, and they inherently raise the question of how to query recursive and hierarchical data efficiently through recursive CTEs.

**Paths** — *where this leads*
Self-joins in [[JOIN (SQL)|JOINs]] let you traverse hierarchies by joining a table to itself, unlocking the ability to model and query complex tree and graph structures directly within relational databases.
