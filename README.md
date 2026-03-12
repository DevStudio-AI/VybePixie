<p align="center">
  <img src="docs/assets/vybepixie-banner.png" alt="VybePixie Banner" width="800" />
</p>

<h1 align="center">VybePixie</h1>

<p align="center">
  <strong>Deterministic AI-Powered 3D Asset Studio</strong>
</p>

<p align="center">
  A desktop application that turns text prompts and 2D images into production-ready 3D models, textures, and animations — with a guarantee that the same input always produces the same output. Every creative decision is recorded in a tamper-proof history, so you can replay, audit, and collaborate with confidence.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/platform-Windows%20%7C%20macOS%20%7C%20Linux-blue" alt="Platforms" />
  <img src="https://img.shields.io/badge/DCC%20Bridges-Blender%20%7C%20Maya%20%7C%20Houdini-green" alt="DCC Bridges" />
  <img src="https://img.shields.io/badge/rendering-Three.js%20%2B%20WebGL-orange" alt="Rendering" />
  <img src="https://img.shields.io/badge/AI-Self--Hosted%20%7C%20Multi--LLM-purple" alt="AI" />
  <img src="https://img.shields.io/badge/determinism-100%25-red" alt="Determinism" />
</p>

---

## What Makes It Different

Most AI generation tools are black boxes — run the same prompt twice, get different results. You can't audit what happened, can't reproduce it, and can't prove who created what.

VybePixie solves this with **event-sourced determinism**:

- **Same input = same output**, every time. Guaranteed.
- **Complete history** — every change recorded in an append-only ledger with blockchain-style hash chaining
- **Content-addressable** — every asset identified by its cryptographic hash, not a random ID
- **Tamper-evident** — if anyone modifies history, the hash chain breaks and you see it immediately

This matters for studios that need reproducible pipelines, regulatory compliance, or proof of creative authorship.

---

## Key Capabilities

### 🎨 AI Asset Generation
- **Text-to-3D** — Describe what you want, get a 3D mesh (Shap-E, Point-E, TripoSR, InstantMesh)
- **Image-to-3D** — Upload a photo or concept art, get a 3D reconstruction
- **Texture generation** — AI-powered PBR materials (SDXL, ControlNet, Stable Diffusion 3, FLUX)
- **Batch generation** — Cost-optimized bulk creation with quality control and budget tracking

### 🏗️ Professional 3D Pipeline
- **Mesh processing** — Optimization, LOD generation, UV unwrapping, cleanup
- **Material system** — 50+ procedural PBR presets, layered materials, metallic-roughness workflow
- **Rigging & skinning** — Automatic skeleton generation, inverse kinematics, retargeting
- **Animation** — Blend trees, state machines, montages, procedural motion, facial animation
- **Scene composition** — Hierarchical scene graphs with non-destructive layer editing

### 🔗 DCC Tool Bridges
| Bridge | Versions | Capabilities |
|--------|----------|-------------|
| **Blender** | 3.0 – 4.5 | Bi-directional sync, asset import/export |
| **Maya** | 2018 – 2025 | Studio-standard integration |
| **Houdini** | — | Procedural workflow integration |

**Export formats:** GLTF, USDZ, FBX, OBJ, VRM, USD, Point Clouds

**Engine targets:** Unity (URP/HDRP), Unreal Engine 5, Godot 4, Blender

### 🤖 AI Director System
- **Natural language interface** — Chat with the AI to guide creative decisions
- **Intent parsing** — LLM understands complex creative briefs
- **Multi-provider** — OpenAI, Anthropic, Google, XAI with automatic fallback chains
- **Self-hosted option** — Run AI models locally, no cloud dependency required

### 🔬 Procedural Generation
50+ algorithms built in:
- Noise generators (Perlin, Simplex, Worley)
- Signed Distance Functions (SDFs)
- L-systems for organic structures
- Heightmap generation
- Scatter and instancing
- Curve-based modeling

### ✅ Validation & Quality Control
- **50+ validators** — Geometry, materials, rigging, performance checks
- **Auto-fix engine** — Intelligent corrections for common issues
- **Budget system** — GPU/time cost tracking per generation
- **Governance gates** — Safety checks before final output

---

## Architecture Overview

VybePixie is a **Tauri hybrid desktop application** — a Rust-powered native container hosting a React frontend, backed by a Python engine for AI generation and 3D processing.

```
┌──────────────────────────────────────────────────────────────┐
│                    Tauri Desktop Container                    │
│            (Rust · Secure sandboxing · IPC bridge)           │
├──────────────────────────┬───────────────────────────────────┤
│                          │                                    │
│   React Frontend         │        Rust Backend                │
│   (src/)                 │        (src-tauri/)                │
│                          │                                    │
│   • Three.js 3D viewport │        • File system access        │
│   • Redux state mgmt     │        • Process management        │
│   • Professional UI      │        • Native dialogs            │
│     panels (10+)         │        • Shell commands             │
│   • Asset browser        │        • Security sandboxing        │
│                          │                                    │
└──────────────────────────┴───────────────────────────────────┘
              │                              │
              └──────────┬───────────────────┘
                         ▼
          ┌──────────────────────────────┐
          │    Python Backend Engine     │
          │    (localhost:8001)          │
          │                              │
          │  Event-Sourced Core          │
          │  ├── 12 Phase System         │
          │  ├── Deterministic Replay    │
          │  ├── Event Ledger (SQLite)   │
          │  └── State Reconstruction    │
          │                              │
          │  AI Generation Pipeline      │
          │  ├── Text-to-3D models       │
          │  ├── Image-to-3D             │
          │  ├── Texture diffusion       │
          │  └── GPU orchestration       │
          │                              │
          │  DCC Bridges                 │
          │  ├── Blender 3.0–4.5         │
          │  ├── Maya 2018–2025          │
          │  └── Houdini                 │
          └──────────────────────────────┘
```

### 12-Phase Engine Architecture

| Phase | System | Purpose |
|-------|--------|---------|
| 0 | Core & Event Ledger | Hashing, IDs, events, determinism foundation |
| 1 | World Model | Scene graph, nodes, transforms |
| 2 | Asset Registry | Content-addressable storage, versioning |
| 3 | Edit System | Non-destructive edits, undo history |
| 4 | Planning | Agent budgets, task decomposition |
| 5 | Generation | AI pipelines with cost tracking |
| 6 | Assembly | Scene building, LOD, linking |
| 7 | Validation | 50+ rules, budget enforcement |
| 8 | Fixes | Auto-fix engine, governance gates |
| 9 | Procedural | 50+ generation algorithms |
| 10 | Director | LLM orchestration, intent parsing |
| 11 | Ingestion | Data import, gap detection |
| 12 | DCC Bridges | Blender, Maya, Houdini sync |

> Full architecture deep-dive in [ARCHITECTURE.md](ARCHITECTURE.md)

---

## Tech Stack

| Layer | Technologies |
|-------|-------------|
| **Desktop** | Tauri 2.9 (Rust 2021 edition) |
| **Frontend** | React 18, Three.js, Redux Toolkit, Tailwind CSS, Vite |
| **3D** | @react-three/fiber, @react-three/drei |
| **Backend** | Python 3.11+, Pydantic 2, SQLAlchemy 2 (async) |
| **AI/ML** | PyTorch 2.1+, Diffusers, Transformers, xformers |
| **API** | GraphQL (Strawberry), REST, WebSocket |
| **Task Queue** | Celery + Redis |
| **Storage** | SQLite (event ledger), PostgreSQL (API data) |
| **Testing** | Vitest (frontend), pytest (backend) |

> Full breakdown in [TECH_STACK.md](TECH_STACK.md)

---

## Workspace UI

The workspace provides a full professional editing environment:

```
┌──────────────────────────────────────────────────────┐
│  Menu Bar  │  Toolbar (modes, view controls)         │
├────────────┼─────────────────────────┬───────────────┤
│            │                         │               │
│  Scene     │    3D Viewport          │  Properties   │
│  Graph     │    (Three.js WebGL)     │  Inspector    │
│  Panel     │                         │               │
│            │                         │               │
│            │                         ├───────────────┤
│            │                         │               │
│            │                         │  Asset        │
│            │                         │  Browser      │
│            │                         │               │
├────────────┴─────────────────────────┴───────────────┤
│  Timeline / Sequencer  │  AI Chat  │  Console        │
└────────────────────────┴───────────┴─────────────────┘
```

**Available panels:** Scene Graph, Properties, Timeline, Asset Browser, AI Chat, Console, Validation Dashboard, Mesh Editor, Storyboard, Multiplayer

---

## Security Model

| Feature | Implementation |
|---------|---------------|
| **Tauri sandboxing** | Rust-enforced security boundary between web and native |
| **Content Security Policy** | Strict CSP prevents unauthorized resource loading |
| **File system isolation** | Controlled FS access through Tauri permission system |
| **Tamper-proof history** | Blockchain-style hash chaining on event ledger |
| **RBAC** | Role-based access for multi-user/studio environments |
| **Audit trail** | Every creation, edit, and export is logged |

> Full security details in [SECURITY.md](SECURITY.md)

---

## Screenshots

<p align="center">
  <em>Screenshots coming soon.</em>
</p>

<!-- 
<p align="center">
  <img src="docs/screenshots/viewport.png" alt="3D Viewport" width="600" />
  <br><em>3D Viewport with AI-generated asset</em>
</p>

<p align="center">
  <img src="docs/screenshots/generation.png" alt="Text-to-3D" width="600" />
  <br><em>Text-to-3D generation pipeline in action</em>
</p>
-->

---

## Project Status

VybePixie is in **active development**. The core engine and UI are functional:

- ✅ Event-sourced deterministic core (12-phase system)
- ✅ Tauri desktop application with professional UI
- ✅ Three.js 3D viewport with real-time rendering
- ✅ AI generation pipeline (text-to-3D, image-to-3D, textures)
- ✅ DCC bridges (Blender, Maya, Houdini)
- ✅ 50+ procedural generation algorithms
- ✅ Validation engine with auto-fix
- ✅ Multi-provider LLM orchestration
- 🔄 Studio beta preparation

---

## License

This repository contains documentation and architecture references only. The source code is proprietary and not publicly available.

**© 2024-2026 DevStudio AI Inc.. All rights reserved.**

See [LICENSE](LICENSE) for details.
