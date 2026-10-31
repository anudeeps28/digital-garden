---
type: atomic
tags: [coding/devops, infrastructure]
date: 2026-10-31
---

# Snowflake Servers

## Idea
A server that was set up and patched by hand becomes one of a kind, like a snowflake. Nobody can rebuild it exactly, and no two of them match.

## Definition
A snowflake server is a machine whose configuration has built up through manual changes over time: someone logged in, installed a package, edited a config file, applied a hotfix. Each change makes sense on its own, but no record of the whole exists. The machines then **drift apart**: Server A got the security patch and Server B didn't, or staging runs a different library version from production. When a snowflake dies, you rebuild it from memory. The fix is to hold the server's full setup in a text file you keep in version control. **Configuration management** tools (CFEngine, Puppet, Chef, Ansible) apply that file to existing machines. **Provisioning** tools such as Terraform or [[Bicep]] create the machines themselves. A stronger version of the fix is the **phoenix server**: never patch a server in place, but throw it away and rebuild it from the recipe. That idea leads to the "pets vs cattle" framing. Pets are named, nursed back to health and irreplaceable. Cattle are numbered and replaced when they get sick.

## Source
Martin Fowler, "SnowflakeServer" and "PhoenixServer" on his bliki (2012) ([martinfowler.com](https://martinfowler.com/bliki/SnowflakeServer.html)). The "pets vs cattle" analogy is usually credited to Bill Baker of Microsoft and was popularised by Randy Bias around 2012, though I couldn't confirm that from a primary source.

---

## Compass

**Roots** — *where this comes from*
It is the server-side version of [[It Works on My Machine]]: an environment nobody wrote down is an environment nobody can reproduce.

**Paths** — *where this leads*
[[Infrastructure as Code]] turns the server into a file you can review and rebuild. Immutable artifacts like a [[Docker Image]] or a [[Virtual Machines|VM image]] go further and make in-place changes pointless.

**Neighbors** — *what lives nearby*
[[Documentation Drift]] is the same decay in prose: the written description and the real thing slowly stop matching. [[Single Source of Truth]] is the principle both violate.

**Clash** — *what pushes against this*
Some systems really are pets: a legacy database on special hardware, or a licensed appliance that can't be scripted. Running re-apply tools also only catches drift in the settings those tools manage; a hand change outside their scope stays invisible.
