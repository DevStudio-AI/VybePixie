# VybePixie — Security Model

> How VybePixie protects creative assets, game projects, and generated content across the full AI studio pipeline

---

## Overview

VybePixie's security model centers on three pillars: **tamper-evident integrity** (cryptographic proof that nothing has been altered), **sandboxed isolation** (Tauri's Rust-based security boundary), and **AI governance** (validation gates on all generated content — 3D assets, game logic, animation, and audio). Together, they ensure that creative work is protected, auditable, and trustworthy across the entire game and animation production pipeline.

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
| **Multi-agent governance** | Director, Producer, and TD agents cross-check each other's outputs |
| **Governance gates** | All AI output (3D, animation, audio, game logic) passes validation before acceptance |
| **Budget enforcement** | GPU/time/API-cost budgets prevent runaway generation |
| **Safety checks** | Content validation on generated assets, animations, and audio |
| **Game logic review** | Generated scripts and behavior trees validated before export |
| **Retry policies** | Controlled retry with exponential backoff and cost tracking |
| **Self-hosted option** | Run AI models locally — no data leaves the machine |
| **API key isolation** | Per-provider credential management with encrypted storage |

---

## Game Export Security

| Control | Implementation |
|---------|---------------|
| **Script validation** | Generated game scripts (GDScript, C#, Blueprints) are validated before export |
| **Asset integrity** | Exported assets are hash-verified against the content-addressable registry |
| **Project isolation** | Each game export is sandboxed in its own directory |
| **No code injection** | Generated game logic is sanitized — no arbitrary code paths |

---

## Audio Generation Security

| Control | Implementation |
|---------|---------------|
| **Voice synthesis isolation** | TTS API calls use scoped credentials with rate limiting |
| **Music generation audit** | All AI-composed audio recorded in event ledger with attribution |
| **Content filtering** | Generated voice and music pass through safety validation |

---

## Licensing Security

VybePixie uses cryptographic license verification designed for offline-first environments — studios and creators don't need an internet connection to validate their license.

| Control | Implementation |
|---------|---------------|
| **Offline verification** | License validated locally using asymmetric cryptography — no server call required |
| **Hardware binding** | License is bound to the specific machine it was activated on |
| **Tamper resistance** | License payload is cryptographically signed — any modification invalidates it |
| **Trial enforcement** | 14-day trial with automatic expiry, no bypass without valid license |
| **Tier-based gating** | Feature access enforced by tier level — graceful degradation, not hard lockout |
| **Credential isolation** | License files stored securely, separate from project data |

### Tier System

| Tier | Audience | Access |
|------|----------|--------|
| **Trial** | Evaluators | Full features, 14-day window |
| **Creator** | Indie devs | Full pipeline, single-seat |
| **Studio** | Teams | Multi-seat, priority features |
| **Enterprise** | Large studios | Custom terms, on-premise |

---

## Update Security

VybePixie uses Tauri's native auto-updater to deliver signed binary updates:

| Control | Implementation |
|---------|---------------|
| **Signed binaries** | Every update is cryptographically signed — unsigned code is rejected |
| **Manifest verification** | Update manifest is verified before download begins |
| **Atomic installation** | Updates are applied atomically — no partial or corrupted installs |
| **Rollback safety** | Failed updates don't corrupt the existing installation |

---

## Data Protection

| Scope | Protection |
|-------|-----------|
| **Project files** | Stored locally on user's machine (Tauri FS) |
| **Event ledger** | SQLite with integrity verification |
| **API credentials** | Encrypted storage via system keychain |
| **Game exports** | Local directory, user-controlled |
| **Audio files** | Generated locally, user-owned |
| **Temporary files** | Cleaned up on session end |
| **Cloud sync** | Optional, encrypted in transit |

---

*© 2024-2026 DevStudio AI Inc. All rights reserved.*
