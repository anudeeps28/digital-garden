---
type: atomic
tags: [coding, database, deployment, migrations]
date: 2026-04-02
---

# Migration Scripts (DBAUp)

## Idea
Hand-written SQL scripts that are version-controlled, run automatically during deployment, and tracked so they never run twice.

## Definition
When your app's database needs to change over time (new tables, new columns, schema changes), you need a reliable way to apply those changes across all environments (dev, test, prod). **Migration scripts** solve this.

**What a migration script is:** A SQL file that makes one specific change:
```sql
-- 001_add_status_column.sql
ALTER TABLE Documents ADD Status NVARCHAR(50) NOT NULL DEFAULT 'Pending';
```

**How DBAUp (DbUp) works:**
1. You drop SQL scripts into a versioned folder: `/scripts/db/1.0.x/`
2. The [[CI-CD Pipeline]] release pipeline has a **DBAUp task** that runs these scripts
3. A **ledger table** in the database tracks which scripts have already been executed
4. Scripts that already ran are **skipped** — safe to re-deploy without double-running
5. Scripts run in order (alphabetical/numerical) as the release moves through environments

**DBAUp vs EF Core Migrations:**

| | DBAUp | [[Database Migrations]] (EF Core) |
|---|---|---|
| Scripts | Hand-written SQL | Auto-generated from C# models |
| Control | Full control — you write exactly what runs | Framework decides the SQL |
| DBA-friendly | Yes — DBAs can review raw SQL | Less so — need to understand EF |
| Rollback | Manual (write a rollback script) | Built-in `Down()` method |

**In PlanDocumentRAG:** Franco set up DBAUp in the release pipeline. Scripts go in `/scripts/db/1.0.x/`. The pipeline runs them on each environment as the release progresses, and the ledger ensures no script runs twice.

## Source
Franco set this up for PlanDocumentRAG — 2026-04-01. Ticket DBA-13854 for deploy user setup. Database: `sql-test-plandocrag.database.windows.net` / `PlanDocumentDB`.

---

## Compass

**Neighbors** — *what lives nearby*
[[Database Migrations]] is EF Core's auto-generated approach to the same problem, while migration tools like Flyway and Liquibase solve the same versioned database change problem. Together with the [[CI-CD Pipeline]] that orchestrates their execution, these tools form a cohesive strategy for managing schema evolution across environments.

**Clash** — *what pushes against this*
Manual SQL execution — connecting to each database by hand and running scripts — represents the opposite approach with no tracking. At the extreme, there's "just modify the table in production" with no versioning, tracking, or safety at all.

**Roots** — *where this comes from*
This practice lives within [[Azure DevOps]], where the release pipeline runs the DBAUp task as part of deployment. The broader question it addresses is database versioning — how do you version-control a database the way you do code?

**Paths** — *where this leads*
Migration scripts are pure [[SQL]], which means you have full control over exactly what executes in each environment. This enables reproducible deployments where the same scripts run identically everywhere, and it creates an audit trail where the ledger shows exactly what ran and when.
