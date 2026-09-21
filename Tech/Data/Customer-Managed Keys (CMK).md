---
type: atomic
tags: [coding/security, coding/azure, coding/database]
date: 2026-09-16
---

# Customer-Managed Keys (CMK)

## Idea
With a platform-managed key, the cloud provider can decrypt your data. With a customer-managed key, they can't — because you hold the key and can destroy it.

## Definition
Customer-managed keys means the encryption key protecting a service's data lives in a key vault you control, rather than one the platform owns. The service is granted permission to *use* the key, not to possess it — so revoking that permission renders the data unreadable immediately, and deleting the key makes the revocation permanent. This is sometimes called *bring your own key*, and in multi-tenant systems a dedicated key per tenant becomes a hard isolation boundary and a credible "delete my data" story. The operational weight is real: you now own key rotation, you own the availability of the vault (if it's unreachable, the database stops), and you own the consequences of losing the key. That's why CMK is usually a premium-tier feature rather than a default — it's a genuine transfer of responsibility, not a setting.

## Source
Available across major clouds as CMK / BYOK — Azure Key Vault with Azure SQL and Storage, AWS KMS customer-managed keys, Google Cloud KMS — driven largely by regulatory and enterprise procurement requirements.

---

## Compass

**Roots** — *where this comes from*
CMK is the upgrade on top of [[Transparent Data Encryption]], which by default uses a key the provider controls.

**Paths** — *where this leads*
A key per tenant strengthens [[Multi-Tenant Data Isolation]] and makes cryptographic erasure a real deletion mechanism.

**Neighbors** — *what lives nearby*
[[Managed Identity]] is how the service proves it may use the key without holding a secret of its own.

**Clash** — *what pushes against this*
You've swapped "the provider could read my data" for "I could lock myself out permanently". For most workloads the platform-managed key is the better risk trade; CMK earns its keep when a contract or regulator demands it.
