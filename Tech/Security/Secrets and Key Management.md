---
type: atomic
tags: [coding/security, coding/azure, devops, security, coding/identity]
date: 2026-10-01
---

# Secrets and Key Management

## Idea
Secrets shouldn't live in config files, environment variables or source control. Keep them in one guarded vault and have the app ask for them at runtime, proving who it is with its own identity, so there's nothing to leak and only one place to rotate.

## Definition
A secrets and key management service is a hosted vault for three kinds of sensitive material: **secrets** (passwords, [[Connection String|connection strings]], API keys), **cryptographic keys**, and **certificates**. The app no longer reads a password from a config file. It authenticates to the vault with its [[Workload Identity]] and fetches the secret when it starts, or every time it needs it, so the config holds only the vault's address and the secret's name. Who can read what is controlled by access policies or [[Role-Based Access Control (RBAC)|RBAC]]: one app gets read access to one secret, and nobody gets "manage everything" by default. Every read lands in an **audit log**. **Rotation** means swapping in a new value centrally without redeploying, and apps pick it up on their next fetch, provided they don't cache it forever. **Soft-delete** and **purge protection** keep a deleted secret or key recoverable for a retention period, which matters because a deleted encryption key makes every byte encrypted with it unreadable. Keys are special: they can be **HSM-backed** (stored in tamper-resistant hardware) and never leave the vault at all. The vault performs the encrypt, decrypt or sign operation itself and hands back only the result. That is how [[Customer-Managed Keys (CMK)]] and [[Transparent Data Encryption]] with your own key work. The usual gotcha is chicken-and-egg: whatever authenticates to the vault can't itself be a stored secret, and that's exactly the gap workload identity closes.

## Providers
- **Azure** — Key Vault for secrets, keys and certificates; Managed HSM for single-tenant, FIPS 140-3 Level 3 key storage.
- **AWS** — Secrets Manager for secrets (with built-in rotation), KMS for keys, and Systems Manager Parameter Store as the cheaper option for plain config and simple secrets.
- **Google Cloud** — Secret Manager for secrets, Cloud KMS (with Cloud HSM) for keys.
- **Others** — HashiCorp Vault (self-hosted or managed; adds dynamic, short-lived database credentials); Kubernetes Secrets are only base64-encoded unless backed by one of the above.

## Source
Hardware security modules and the PKCS#11 interface predate the cloud. Cloud vaults followed: AWS KMS (2014), Azure Key Vault (2015), AWS Secrets Manager (2018), Google Secret Manager (2020). HashiCorp Vault was released in 2015.

---

## Compass

**Roots** — *where this comes from*
It's what's left when you pull secrets out of [[Connection String|connection strings]] and config, and it only fully works alongside [[Workload Identity]], which removes the last stored credential.

**Paths** — *where this leads*
Holding keys in a vault makes [[Customer-Managed Keys (CMK)]] and [[Transparent Data Encryption]] with your own key possible, and [[Bicep Parameter File|parameter files]] can point to vault secrets instead of holding the values.

**Neighbors** — *what lives nearby*
[[Role-Based Access Control (RBAC)]] decides who can read which secret, and [[Private Endpoint]] keeps the vault itself off the public internet, part of [[Defence in Depth]].

**Clash** — *what pushes against this*
The vault becomes a dependency on every startup: if it's unreachable or throttled, apps can't boot. Caching secrets to avoid that undermines rotation, and a vault full of long-lived static secrets is still a list of static secrets. The best secret is one you no longer need, because identity-based access replaced it.
