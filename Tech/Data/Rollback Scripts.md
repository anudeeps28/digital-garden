---
type: atomic
tags: [coding/database, devops, migrations]
date: 2026-10-03
---

# Rollback Scripts

## Idea
Every change to a database's structure should ship with a second script that undoes it, so if a release goes wrong there is always a tested way back.

## Definition
A schema change, such as adding a column or a table, is written as a script and committed alongside the code. A rollback script is its partner: a second script, kept right next to it, that puts the database back the way it was. If the change causes trouble after release, the team runs the rollback instead of improvising SQL under pressure.

How you get the rollback depends on how the repo changes its database:
- **Hand-written scripts** ([[Migration Scripts|migration scripts]]): numbered SQL files run in order, with a ledger table recording which have run. Nothing writes the undo for you, so each forward script needs a hand-written rollback script beside it.
- **Migration tools** ([[Database Migrations]]): you change the code's data model and the tool generates a file holding both directions, an "up" that makes the change and a "down" that reverses it. The "down" *is* the rollback. You just have to check it actually does the reverse.

So the rule is the same everywhere: follow the format the repo already uses, and make sure each change has a way back.

Two caveats keep this honest. First, a rollback can't always bring back data. If the change dropped a column, the rollback can recreate the column but not the values that were in it, and anything written after the release may not fit the old shape. Second, a rollback you've never run is a guess, just like a backup you've never restored. Run it on a throwaway local database before it's needed. Never hand-run either direction against a shared or live database. That's the pipeline's job.

## Tools
- **EF Core (.NET)**: generated migrations contain `Up()` and `Down()`; `dotnet ef database update <PreviousMigration>` runs the downs.
- **Rails ActiveRecord**: `change`, or explicit `up`/`down`; `rails db:rollback`.
- **Flyway**: versioned `V` scripts go forward; separate `U` undo scripts (paid editions) go back.
- **Liquibase**: each changeset can declare a `rollback` block; many change types generate one automatically.
- **DbUp**: forward-only by design; rollbacks are hand-written scripts.

## Source
Up/down migrations were popularised by Ruby on Rails' ActiveRecord Migrations (2005). Current references: Microsoft's EF Core documentation ("Managing Migrations"), Redgate's Flyway documentation ("Undo migrations") and Liquibase's documentation ("Rollback").

---

## Compass

**Roots** — *where this comes from*
It's the safety half of [[Database Migrations]]: once schema changes are versioned like code, the next question is how you un-ship one.

**Paths** — *where this leads*
Teams that take rollbacks seriously end up splitting risky changes into safe steps (add the new column, move the data, and drop the old one only in a later release) so the way back never destroys anything. That's the [[Expand and Contract]] pattern.

**Neighbors** — *what lives nearby*
A [[Restore Drill]] is the same instinct at the backup level: an undo you haven't practised isn't an undo. [[Release Stages]] give the rollback a place to be tried before production does.

**Clash** — *what pushes against this*
Many teams prefer to [[Roll Forward]] instead: fix the problem with a new change rather than reversing the old one. Rollbacks can't recover lost data, and a rarely-run rollback script is often the least-tested code in the repo.
