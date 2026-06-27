---
type: atomic
tags: [coding/devops, coding/review, ai]
date: 2026-04-24
---

# Code Rabbit

## Idea
Code Rabbit is an AI-powered code review bot that posts inline comments on every [[Pull Request]] — catching bugs, style issues, and missing tests before a human reviewer ever opens the file.

## Definition
Code Rabbit installs as a GitHub/Azure DevOps app and triggers on PR open and on every new commit. It reads the diff (and surrounding context), generates structured review comments, and threads them like a human reviewer would. Comments are categorized — `Refactor`, `Potential issue`, `Nitpick`, `LGTM` — and frequently include suggested-edit blocks the author can apply with one click. Workflow integration: each comment thread starts as "open" and the author either fixes the code or replies with reasoning. The bot will re-evaluate after each push and resolve threads it considers addressed. The project uses it as the first review pass — by the time a human reviewer arrives, the obvious issues are already gone. **Risks worth tracking:** false positives on framework-specific patterns; over-reliance leading to skipped human review; and prompt-injection in comment bodies. The mental model: "another reviewer who reads everything but doesn't always understand context."

## Source
CI/CD learning session — The project's PR review workflow.

---

## Compass

**Neighbors** — *what lives nearby*
Microsoft's [[GitHub Copilot for PRs]] is the competing AI reviewer in this space, while [[SonarQube]] and similar tools provide a non-AI counterpart through static analysis. Earlier in the same workflow, [[Pre-commit hooks]] like linters catch issues before they reach a PR.

**Clash** — *what pushes against this*
The opposite extreme is doing no automated review and relying on humans only, or conversely, deploying auto-approve bots — the dangerous mirror that blindly accepts all changes.

**Roots** — *where this comes from*
Code Rabbit operates within the [[Pull Request]] workflow and is part of the broader trend toward AI code review.

**Paths** — *where this leads*
As automated review absorbs the obvious issues, human reviewer workflows shift to focus on architecture and intent rather than nitpicks. It also spawns "babysit-pr" workflows that systematically handle Code Rabbit's comment volume, and creates feedback loops where you teach the bot what false positives to ignore.
