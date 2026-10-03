---
aliases: [tech/migration-scripts-(dbaup), tech/data/migration-scripts-(dbaup)]
type: atomic
tags: [coding, database, deployment, migrations]
date: 2026-04-02
---

# Migration Scripts

## Idea
Hand-written SQL scripts that are version-controlled, run automatically during deployment, and tracked so they never run twice.

## Definition
When your app's database needs to change over time (new tables, new columns, schema changes), you need a reliable way to apply those changes across all environments (dev, test, prod). **Migration scripts** solve this.

**What a migration script is:** A SQL file that makes one specific change:
```sql
-- 0001_add_status_column.sql
ALTER TABLE Documents ADD Status NVARCHAR(50) NOT NULL DEFAULT 'Pending';
```

**How a script runner works:**
1. You drop SQL scripts into a versioned folder, numbered so they sort in order (`0001_…`, `0002_…`)
2. The release stage of the [[CI-CD Pipeline]] runs a tool that applies them
3. A **ledger table** in the database records which scripts have already been executed
4. Scripts that already ran are **skipped**, so re-deploying is safe
5. Scripts run in order as the release moves through environments

**Hand-written scripts vs generated migrations:**

| | Hand-written scripts | [[Database Migrations]] (e.g. EF Core) |
|---|---|---|
| Scripts | Hand-written SQL | Generated from the code's data model |
| Control | Full control: you write exactly what runs | The framework decides the SQL |
| DBA-friendly | Yes: DBAs can review raw SQL | Less so: you need to understand the framework |
| Rollback | Manual: write a [[Rollback Scripts\|rollback script]] | Built-in `Down()` method |

## Tools
- **.NET**: DbUp, a library that runs numbered SQL scripts and keeps the ledger table.
- **Java and others**: Flyway (versioned `V` scripts) and Liquibase (changesets in SQL, XML or YAML).
- **Azure**: Azure DevOps release pipelines can run any of these as a step; SQL projects (DACPACs) are a state-based alternative.
- **AWS / Google Cloud**: no built-in runner; the same tools run as a pipeline step against RDS or Cloud SQL.

## Source
DbUp project documentation (dbup.readthedocs.io); Redgate's Flyway documentation on versioned migrations.

---

## Compass

**Neighbors** — *what lives nearby*
[[Database Migrations]] is the framework-generated approach to the same problem, and tools like Flyway and Liquibase sit in between, running versioned scripts with richer tracking. All of them rely on the [[CI-CD Pipeline]] to apply changes the same way in every environment.

**Clash** — *what pushes against this*
Manual SQL execution means connecting to each database by hand and running scripts with no tracking. At the extreme, there's "just modify the table in production", with no versioning, no record and no way back.

**Roots** — *where this comes from*
The broader question is database versioning: how do you version-control a database the way you do code? Scripts usually run as a step in the release half of the [[Build Pipeline vs Release Pipeline|release pipeline]].

**Paths** — *where this leads*
Migration scripts are pure [[SQL]], so you control exactly what runs in each environment. That gives you reproducible deployments, an audit trail in the ledger table, and a natural place to keep each change's [[Rollback Scripts|rollback]].
