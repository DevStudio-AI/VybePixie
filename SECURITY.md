# VybePixie — Security Model

> How VybePixie protects creative assets, ensures integrity, and enables trusted collaboration

---

## Overview

VybePixie's security model centers on two pillars: **tamper-evident integrity** (cryptographic proof that nothing has been altered) and **sandboxed isolation** (Tauri's Rust-based security boundary). Together, they ensure that creative work is protected, auditable, and trustworthy.

---

## Tamper-Proof Event History

The most critical security feature. Every action in VybePixie produces an immutable event stored in a hash-chained ledger.

### How It Works

```
Event N:
  prev_hash: SHA-256 of Event N-1
  data:      Canonical JSON (sorted keys, no whitespace)
  hash:      SHA-256(prev_hash + canonical_data)
```

**Properties:**
- **Append-only** — Events are never modified or deleted
- **Chain verification** — Each event's hash incorporates the previous event's hash
- **Tamper detection** — Modifying any event breaks all subsequent hashes
- **Reproducibility** — Replaying the event stream from genesis reconstructs the exact same state

### Why It Matters
- **Authorship proof** — Cryptographic evidence of who created what and when
- **Regulatory compliance** — Auditable trail for studios with compliance requirements
- **Collaboration trust** — Multiple contributors can verify the integrity of shared work
- **IP protection** — Provenance chain for generated assets

---

## Content-Addressed Identity

Every entity in VybePixie (assets, events, nodes) is identified by the SHA-256 hash of its canonical bytes — not random UUIDs.

| Property | Benefit |
|----------|---------|
| **Deterministic IDs** | Same content always gets the same ID |
| **Deduplication** | Identical assets automatically detected |
| **Integrity verification** | ID itself proves content hasn't been altered |
| **Version tracking** | Any change produces a new hash (new version) |

---

## Tauri Security Sandbox

VybePixie runs inside a Tauri container, which provides Rust-enforced security boundaries:

### Permission System

| Resource | Access Control |
|----------|---------------|
| **File system** | Whitelisted directories only — no unrestricted disk access |
| **Shell commands** | Explicitly permitted commands only |
| **Network** | CSP-controlled external connections |
| **Native dialogs** | Scoped to application context |
| **IPC bridge** | Type-checked command interface between frontend and backend |

### Content Security Policy (CSP)

Strict CSP prevents:
- Unauthorized script execution (XSS protection)
- Unauthorized resource loading
- Data exfiltration via embedded content

---

## Role-Based Access Control (RBAC)

For multi-user and studio environments:

| Role | Capabilities |
|------|-------------|
| **Viewer** | Browse assets, view scene graph, inspect properties |
| **Creator** | Generate assets, edit scenes, run AI pipelines |
| **Admin** | Manage users, configure settings, access audit logs |

All role assignments are recorded in the event ledger for auditability.

---

## Audit Trail

Every operation produces a logged event:

| Data Captured | Purpose |
|---------------|---------|
| **Actor** | Who performed the action |
| **Action type** | What was done (generate, edit, export, delete) |
| **Timestamp** | When it occurred (logical time) |
| **Input parameters** | What inputs were provided |
| **Output hash** | What was produced (content-addressed) |
| **Event hash** | Cryptographic proof of this event's integrity |

---

## AI Generation Security

| Control | Implementation |
|---------|---------------|
| **Governance gates** | AI output passes through validation before acceptance |
| **Budget enforcement** | GPU/time budgets prevent runaway generation |
| **Safety checks** | Content validation on generated assets |
| **Retry policies** | Controlled retry with exponential backoff |
| **Self-hosted option** | Run AI models locally — no data leaves the machine |

---

## Data Protection

| Scope | Protection |
|-------|-----------|
| **Project files** | Stored locally on user's machine (Tauri FS) |
| **Event ledger** | SQLite with integrity verification |
| **API credentials** | Encrypted storage via system keychain |
| **Temporary files** | Cleaned up on session end |
| **Cloud sync** | Optional, encrypted in transit |

---

*© 2024-2026 DevStudio AI. All rights reserved.*
