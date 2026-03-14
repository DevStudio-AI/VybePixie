# VybePixie — Tech Stack

> Every technology choice across the desktop, frontend, backend, AI, game, animation, and audio layers

---

## Desktop Container (Tauri)

| Component | Choice | Why |
|-----------|--------|-----|
| **Framework** | Tauri 2.9 | Lightweight native container (vs. Electron), Rust security model |
| **Language** | Rust (2021 edition) | Memory safety, performance, zero-cost abstractions |
| **MSRV** | 1.77.2 | Stable Rust release baseline |
| **Plugins** | tauri-plugin-log, shell, dialog, fs, updater | Native OS integration + OTA updates (v2 plugin API) |
| **Auto-Updater** | tauri-plugin-updater 2.x | Signed binary updates with atomic install |
| **Serialization** | Serde 1.0 | Fast JSON serialization for IPC bridge |

---

## Frontend

| Component | Choice | Version | Why |
|-----------|--------|---------|-----|
| **UI Framework** | React | 18.3 | Component model, ecosystem, Three.js integration |
| **Build Tool** | Vite | 5.1 | Fast HMR, ESM-native, Tauri integration |
| **3D Rendering** | Three.js | 0.162 | Industry-standard WebGL library |
| **3D React** | @react-three/fiber | 8.15 | Declarative Three.js in React components |
| **3D Utilities** | @react-three/drei | 9.99 | Camera controls, gizmos, helpers, presets |
| **Global State** | Redux Toolkit | 2.2 | Predictable state for complex UI (15+ panels) |
| **Persistence** | Redux Persist | 6.0 | Survive app restarts, workspace recall |
| **Local State** | Zustand | 4.5 | Lightweight stores for isolated components |
| **Styling** | Tailwind CSS | 3.4 | Utility-first, rapid UI development |
| **Icons** | Lucide React | 0.330 | Clean, consistent iconography |
| **Routing** | React Router | 6.22 | View navigation within desktop app |
| **Virtualization** | TanStack React Virtual | 3.13 | Efficient rendering of large asset lists |
| **Immutable Updates** | Immer | Latest | Safe nested state mutations |
| **TypeScript** | 5.4 | Type safety across frontend codebase |
| **Testing** | Vitest | 1.3 | Fast, Vite-native test runner |
| **Linting** | ESLint | 8.57 | Code quality enforcement |

---

## Python Backend & Engine

| Component | Choice | Version | Why |
|-----------|--------|---------|-----|
| **Runtime** | Python | 3.11–3.13 | ML ecosystem, async support, type hints |
| **Package Manager** | Hatch | 1.9+ | Modern Python project management |
| **Type System** | Pydantic | 2.6–3.0 | Runtime validation with type inference |
| **Settings** | Pydantic Settings | 2.2+ | Environment-based configuration |
| **HTTP Client** | httpx | 0.27+ | Async HTTP for provider APIs |
| **3D Mesh Processing** | trimesh | 4.0+ | Mesh analysis, simplification, export |
| **Image Processing** | Pillow | 10.0+ | Texture manipulation |
| **Math** | NumPy 1.24+, SciPy 1.6+ | Linear algebra, spatial computation |
| **Noise Generation** | noise | 1.2.2+ | Perlin/Simplex noise for procedural gen |
| **Graph Processing** | NetworkX | 3.0+ | Scene graph DAG operations |
| **Config** | PyYAML | 6.0+ | Configuration file parsing |
| **Serialization** | msgpack | 1.0+ | Fast binary serialization for IPC |
| **Testing** | pytest | 8.0+ | Test framework |
| **Async Tests** | pytest-asyncio | 0.23+ | Async test support |
| **Coverage** | pytest-cov | 5.0+ | Test coverage reporting |
| **Linting** | ruff | Latest | Fast Python linter/formatter |
| **Type Checking** | mypy | Latest | Static type analysis |

---

## Web/API Layer

| Component | Choice | Why |
|-----------|--------|-----|
| **REST API** | FastAPI | High-performance async REST + WebSocket |
| **Task Queue** | Celery 5.3–6.0 | Distributed background job processing for GPU tasks |
| **Message Broker** | Redis 5.0–6.0 | Fast pub/sub and task distribution |
| **Database ORM** | SQLAlchemy 2.0 (async) | Async database access with type safety |
| **Database Driver** | AsyncPG 0.29+ | High-performance async PostgreSQL |
| **GraphQL** | Strawberry GraphQL 0.200+ | Type-safe GraphQL API layer |
| **File Upload** | python-multipart | Handling asset file uploads |
| **Schema Validation** | jsonschema 4.21+ | JSON schema validation for config files |

---

## AI/ML Stack

| Component | Choice | Version | Why |
|-----------|--------|---------|-----|
| **Framework** | PyTorch | 2.1+ | Industry-standard ML framework |
| **Vision** | TorchVision | Latest | Image processing pipelines |
| **Transformers** | HuggingFace Transformers | 4.36+ | Pre-trained model access |
| **Diffusion** | Diffusers | 0.25+ | Stable Diffusion, SDXL, FLUX pipelines |
| **Memory Optimization** | bitsandbytes | 0.41+ | Quantization for large models on consumer GPUs |
| **Attention** | xformers | 0.0.23+ | Memory-efficient attention kernels |
| **Acceleration** | accelerate | 0.25+ | Multi-GPU, mixed precision |
| **Model Hub** | HuggingFace Hub | 0.20+ | Model downloading and caching |
| **Background Removal** | rembg | 2.0.50+ | Image-to-3D preprocessing |
| **Mesh Simplification** | PyFQMR | 0.2+ | Fast quadric mesh reduction |
| **UV Mapping** | xatlas | 0.0.9+ | Automatic UV unwrapping |
| **Safe Tensors** | SafeTensors | Latest | Secure model weight loading |

---

## Third-Party AI APIs

### 3D Generation

| Service | Models | Purpose |
|---------|--------|---------|
| **Meshy API v2** | Text-to-3D, Image-to-3D, Multi-Image-to-3D | Primary external 3D generation |
| **Tripo3D** | Text-to-3D | Alternative 3D provider |
| **Luma AI** | Image-to-3D | Image-based 3D reconstruction |

### Image Generation

| Service | Purpose |
|---------|---------|
| **OpenAI DALL-E** | Texture concepts, concept art |
| **Stability.ai** | Stable Diffusion API for PBR materials |

### Audio Generation

| Service | Purpose |
|---------|---------|
| **ElevenLabs** | Voice synthesis — multi-speaker TTS with personality |
| **PlayHT** | Alternative TTS provider |
| **Suno** | AI music composition |
| **Udio** | Alternative AI music generation |

### LLM Providers

| Provider | Models | Primary Use |
|----------|--------|-------------|
| **Anthropic** | Claude 4.x series | Creative direction, complex planning |
| **OpenAI** | GPT-5 series | Game logic, code generation |
| **Google** | Gemini 3.x | Multi-modal understanding |
| **xAI** | Grok 4.x | Alternative reasoning |
| **DeepSeek** | Chat, Coder, Reasoner | Cost-effective generation |
| **ZhipuAI** | GLM 4.x series | Additional LLM capacity |

---

## Game Engine Export

| Engine | Version | Export Contents |
|--------|---------|----------------|
| **Godot** | 4.x | Complete project: .tscn scenes, GDScript, assets, project.godot |
| **Unity** | 2022+ | Complete project: scenes, C# scripts, prefabs, URP/HDRP materials |
| **Unreal Engine** | 5.x | Complete project: levels, Blueprints, materials, asset packs |
| **Blender** | 3.0–4.5 | .blend files with full scene hierarchy + DCC bridge |

---

## DCC Tool Bridges

| Tool | Versions | Integration Type |
|------|----------|-----------------|
| **Blender** | 3.0 – 4.5 | Python addon, socket IPC, real-time bi-directional sync |
| **Maya** | 2018 – 2025 | MEL/Python plugin, rigging and animation export |
| **Houdini** | — | HDA support, procedural workflow integration |
| **3DS Max** | — | Legacy pipeline import/export |

---

## 3D Format Support

| Format | Type | Notes |
|--------|------|-------|
| **GLTF/GLB** | Mesh + Materials | Primary exchange format |
| **USDZ** | Universal Scene | Apple ecosystem, AR |
| **FBX** | Mesh + Animation | Unity/Unreal standard |
| **OBJ** | Mesh | Legacy compatibility |
| **VRM** | Character | VTuber/avatar standard |
| **USD** | Universal Scene | Pixar/studio standard |
| **EXR** | Texture (32-bit) | HDR lighting/environment |
| **PNG/JPEG/WebP** | Texture | Standard image formats |

---

## Rendering

| Component | Technology | Purpose |
|-----------|-----------|---------|
| **Real-Time** | GL/ANGLE via Three.js | Live viewport editing, animation preview |
| **Path Tracer** | CPU/GPU ray tracing | Photorealistic final renders |
| **Post-Processing** | Custom pipeline | Bloom, DoF, motion blur, color grading, tone mapping |
| **HDR Color** | sRGB, linear, ACEScg | Professional color management pipeline |
| **XR/AR/VR** | WebXR, ARKit, ARCore, Meta Quest | Immersive output targets |

---

## Animation Runtime

| Component | Purpose |
|-----------|---------|
| **Blend Trees** | Weighted blending between animation clips |
| **State Machines** | Hierarchical FSMs with transition rules |
| **IK Solver** | Inverse kinematics — foot placement, hand targeting, look-at |
| **Mocap Pipeline** | BVH/FBX import, noise removal, retargeting |
| **Secondary Physics** | Spring bones, cloth, jiggle physics, tails, wings, hair |
| **Facial Animation** | Blendshapes, lip sync, eye tracking |
| **Ragdoll** | Full physics-driven character animation |
| **Animation Events** | Frame-triggered gameplay actions |

---

## Event Ledger & Storage

| Component | Choice | Why |
|-----------|--------|-----|
| **Event Store** | SQLite | Embedded, single-file, fast appends, portable |
| **Content Hashing** | SHA-256 | Cryptographic content addressing |
| **Canonical Form** | JSON (sorted keys, no whitespace) | Deterministic serialization |
| **Snapshots** | SQLite checkpoints | Fast state reconstruction without full replay |
| **API Database** | PostgreSQL | Relational data for API services |

---

## Licensing & Distribution

| Component | Choice | Why |
|-----------|--------|-----|
| **License Verification** | Offline-first cryptographic validation | No phone-home required — works air-gapped |
| **Hardware Binding** | Machine-specific activation | Prevents unauthorized license sharing |
| **Tier System** | Trial → Creator → Studio → Enterprise | Feature gating by plan level |
| **Auto-Updater** | Tauri native updater plugin | Signed OTA updates with atomic install |
| **CLI Management** | Built-in license subcommands | `activate`, `status`, `hwid` for developer-friendly workflow |

---

*© 2024-2026 DevStudio AI Inc. All rights reserved.*
