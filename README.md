# ONOX 3D — Scene Layer

> **ONOX Systems** · onoxsystems.com · Bilbao, Euskadi
> Managed & orchestrated by **ONIX** — the internal AI agent hub.
> Forked from [pascalorg/editor](https://github.com/pascalorg/editor) · MIT License

---

## What is ONOX 3D?

ONOX 3D is the spatial visualization and scene-editing layer of the ONOX Systems platform. It provides real-time 3D building editing capabilities powered by React Three Fiber and WebGPU, fully integrated into the ONOX agent ecosystem and controlled by ONIX.

This layer enables ONOX agents to:
- Create, update and delete 3D scene nodes programmatically
- Visualize client projects, spaces and structures in real time
- Expose scene state via WebSocket/REST to the ONIX orchestration layer
- Auto-update from upstream architectural improvements

---

## Repository Architecture

Turborepo monorepo with three main packages:

```
onox-3d/
├── apps/
│   └── editor/              # Next.js app — ONOX 3D UI
├── packages/
│   ├── core/                # @onox/scene-core — schemas, state, systems
│   └── viewer/              # @onox/scene-viewer — 3D rendering (R3F + WebGPU)
├── tooling/                 # Shared ESLint, TypeScript, Biome configs
├── .github/workflows/       # CI/CD + upstream sync + ONIX notifications
├── TEAM.md                  # Internal team, roles and meeting protocol
├── ROADMAP.md               # Versioned roadmap with criteria-based dates
└── STUDIES.md               # Technical research compiled by the internal team
```

### Package Responsibilities

| Package | Responsibility |
|---|---|
| `@onox/scene-core` | Node schemas (Zod), scene state (Zustand + IndexedDB + undo/redo), geometry systems, spatial queries, event bus |
| `@onox/scene-viewer` | 3D rendering via React Three Fiber, WebGPU renderer, default camera/controls, post-processing |
| `apps/editor` | ONOX-branded UI, tools, selection management, ONIX bridge |

---

## ONIX Integration

All scene operations are orchestrated by **ONIX** — no scene mutation happens outside the agent layer.

```
ONIX Agent
    ↓  WebSocket / REST
onix-api  →  POST /scene/command
    ↓
useScene.createNode() / updateNode() / deleteNode()
    ↓
Node marked dirty → System recomputes geometry
    ↓
Event Bus emits 'scene:updated'
    ↓
ONIX notifies Mario (chat / Telegram / Notion log)
```

### ONIX Scene Bridge

```typescript
// packages/onox-agents/src/scene-bridge.ts
export class ONIXSceneBridge {
  executeCommand(cmd: SceneCommand) {
    const { createNode, updateNode, deleteNode } = useScene.getState()
    switch (cmd.type) {
      case 'CREATE': return createNode(cmd.node, cmd.parentId)
      case 'UPDATE': return updateNode(cmd.id, cmd.updates)
      case 'DELETE': return deleteNode(cmd.id)
    }
  }
  subscribe(callback: (event: string, data: unknown) => void) {
    emitter.on('*', callback)
  }
}
```

---

## Tech Stack

| Layer | Technology |
|---|---|
| Framework | Next.js 16 + React 19 |
| 3D Engine | Three.js (WebGPU renderer) |
| React 3D | React Three Fiber + Drei |
| State | Zustand + Zundo (undo/redo) + IndexedDB persistence |
| Schema | Zod |
| Geometry | three-bvh-csg (Boolean CSG operations) |
| Monorepo | Turborepo + Bun |
| CI/CD | GitHub Actions |
| Hosting | Vercel (3d.onoxsystems.com) |
| Auth | Supabase (shared with ONOX platform) |
| Notifications | N8N webhook → ONIX → Telegram/Notion |

---

## Accounts & Services

| Service | Account | Role |
|---|---|---|
| GitHub | marioperezfuertes-svg | Owner — all ONOX repos |
| Vercel | onoxsystems@gmail.com | Hosting — onoxsystems.com + 3d.onoxsystems.com |
| Supabase | onoxsystems@gmail.com | Auth + DB (shared ONOX platform) |
| Cloudflare | onoxsystems@gmail.com | DNS — onoxsystems.com |
| N8N | Local Docker (onox_n8n) | Automation — upstream sync + ONIX webhooks |
| Notion | mario@onoxsystems.com | Docs, meeting notes, roadmap log |
| npm | onoxsystems | Package publishing @onox/scene-core, @onox/scene-viewer |
| Resend | mario@onoxsystems.com | Transactional email (nexo@onoxsystems.com) |
| Telegram Bot | ONIX_bot | ONIX alerts — upstream updates, deploy status |

---

## Deployment

### Production

```
https://3d.onoxsystems.com   →  Vercel (main branch auto-deploy)
```

### Local (Docker)

```bash
# From onox-core (C:\Users\nitropc\Desktop\onix-personal)
docker compose up onox-3d -d

# Runs at http://localhost:3001
# Connected to onox_postgres, onox_redis via internal Docker network
```

### Environment Variables

```env
NEXT_PUBLIC_APP_URL=https://3d.onoxsystems.com
NEXT_PUBLIC_ONIX_WS_URL=wss://api.onoxsystems.com
NEXT_PUBLIC_SUPABASE_URL=https://xxxx.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=xxxx
SUPABASE_SERVICE_KEY=xxxx
ONIX_WEBHOOK_SECRET=xxxx
```

---

## Upstream Sync (Auto-update from Pascal)

Every Monday at 08:00 CET, a GitHub Action checks for new commits in `pascalorg/editor:main`.
If changes exist in `packages/`, ONIX is notified via webhook and informs Mario.
Mario reviews and approves the merge — ONIX executes.

```yaml
# .github/workflows/sync-pascal-upstream.yml
on:
  schedule:
    - cron: '0 7 * * 1'   # Monday 08:00 CET
  workflow_dispatch:
```

See full workflow in `.github/workflows/sync-pascal-upstream.yml`.

---

## Team

See [TEAM.md](./TEAM.md) for full team structure, roles, and meeting protocol.

| Person / Agent | Role |
|---|---|
| Mario Pérez Fuertes | CEO & Product Lead — final decision on all dates and scope |
| ONIX | Internal AI orchestrator — research, compile, alert, execute |
| Javier (SDR Agent) | Commercial outreach & lead management |
| Nexo | Coordination & communications hub |
| Laura | Legal & compliance |
| Agora | Commercial strategy |

---

## Studies & Research

See [STUDIES.md](./STUDIES.md) for all technical research compiled by the internal team.

Current active studies:
- `[ST-01]` WebGPU vs WebGL performance benchmark — ONOX 3D scenes (Q1 2026)
- `[ST-02]` Vercel Edge vs Docker local — latency analysis for 3D asset serving
- `[ST-03]` Pascal upstream adoption rate — what to merge vs what to discard
- `[ST-04]` Multi-tenant scene isolation — architecture for B2B clients
- `[ST-05]` ECS pattern vs scene graph — agent-driven geometry updates

---

## Roadmap

See [ROADMAP.md](./ROADMAP.md) for full versioned roadmap.

> Dates are set by Mario in ONOX Team meetings after reviewing compiled studies.
> ONIX presents findings — Mario decides — dates are committed.

| Version | Focus | Status | Target |
|---|---|---|---|
| v0.1 | Fork + ONOX branding + README | ✅ Done | Mar 2026 |
| v0.2 | ONIX Scene Bridge + WebSocket API | 🔄 In progress | Apr 2026 |
| v0.3 | Supabase multi-tenant auth + scene persistence | 📋 Planned | May 2026 |
| v0.4 | 3d.onoxsystems.com production deploy + Vercel | 📋 Planned | May 2026 |
| v0.5 | ONIX automated scene commands (agent-driven editing) | 📋 Planned | Jun 2026 |
| v1.0 | B2B client demo layer — first commercial use | 📋 Planned | Q3 2026 |

---

## Development

```bash
# Install
bun install

# Dev (hot reload all packages)
bun dev
# → http://localhost:3001

# Build
turbo build

# Lint
bun run lint

# Type check
bun run typecheck
```

---

## Contributing (Internal)

1. All PRs target `main` — reviewed by Mario or ONIX
2. Branch naming: `feat/`, `fix/`, `study/`, `chore/`
3. Commits follow Conventional Commits
4. Upstream Pascal changes go through `feat/pascal-sync-YYYY-MM-DD` branches
5. No direct push to `main` — always PR

---

## License

MIT — forked from [pascalorg/editor](https://github.com/pascalorg/editor)
Adaptations © 2026 ONOX Systems — mario@onoxsystems.com
