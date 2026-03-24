# ONOX 3D — Team, Skills & Meeting Protocol

> **ONOX Systems** · Vitoria-Gasteiz, Araba · **onoxsystems.com**
> Mario Pérez Fuertes — CEO & Product Lead — **always present in every decision meeting**.
> ONIX compiles, presents and proposes. Mario decides. Dates are committed.

---

## Team Structure

### Humans

#### Mario Pérez Fuertes — CEO & Product Lead
- **Role**: Final decision authority on all product, dates, scope and strategy
- **Contact**: mario@onoxsystems.com
- **GitHub**: marioperezfuertes-svg
- **Presence**: Required in all Decision Meetings and Sprint Reviews
- **Skills equipped**:
    - Full-stack architecture (Next.js, Node, Docker, Postgres, Neo4j)
    - DevOps & containerization (Docker Compose, Vercel, Cloudflare)
    - **Tailscale (Mesh Networking & Remote Mando)** — secure PC/Mobile tunnel
    - AI/LLM orchestration (Claude, Gemini, Ollama, N8N)
    - Business strategy & B2B commercial (gestoras, autónomos, Vitoria-Gasteiz)
    - RTX 4060 Ti local inference — €0/month AI stack
- **Multiplier techniques**:
    - Delegates execution to ONIX, retains decision
    - Uses "compile then decide" protocol — never decides without data
    - Reviews ONOX Learning Log weekly before any meeting
    - One rule: demo before budget — always

#### Equipo de Apoyo — Infra & Logistics (Support Team)
- **Role**: Infrastructure provisioning, physical/digital workspace preparation, and operational assistance.
- **Location**: Vitoria-Gasteiz, Araba.
- **Responsibilities**:
  - **Workspace "Mise en Place"**: Setting up the environment (digital and physical) before every Decision Meeting.
  - **Hybrid Infra Management**: Maintaining the **Tailscale Mesh Network** (PC & Mobile) to ensure Mario has "Mando" (Remote Command) anywhere.
  - **Hardware Support**: Maintaining the local RTX 4060 Ti inference nodes and the local Docker stack (`onox_n8n`, `onox_postgres`, etc.).
  - **Asset Preparation**: Ensuring all 3D assets and scene data are loaded and ready for ONIX to present.
  - **Real-time Assistance**: Assisting Mario during "Level 0" operations to maximize autonomy.

### Internal AI Agents (ONIX Squad)

#### ONIX — Internal Orchestrator & Chief of Staff
- **Role**: Orchestrates all agents, compiles research, presents findings, executes approved decisions
- **Email**: nexo@onoxsystems.com (external facing)
- **Capabilities**:
    - Full read/write access to scene state via ONIXSceneBridge
    - Monitors all GitHub repos (commits, PRs, upstream changes)
    - Weekly digest to Mario: what changed, what needs a decision
    - Triggers N8N workflows on scene events
    - Maintains ONOX_LEARNING_LOG.md autonomously
- **Skills stack**:
    - MCP (Model Context Protocol) — connects to GitHub, Notion, Vercel, Supabase
    - Zustand store direct access via `useScene.getState()`
    - Event bus subscriber (`emitter.on('*', ...)`)
    - Upstream diff analysis — classifies Pascal changes as: merge/adapt/discard
    - Langfuse tracing — all agent calls logged and scored
- **Multiplier techniques**:
    - Batches findings — never interrupts Mario with single items
    - Prepares "decision packets": context + options + recommendation
    - Auto-executes pre-approved patterns without asking
    - Escalates only when: new cost, new risk, new scope

#### Javier — SDR Agent (Commercial)
- **Role**: Lead generation, cold outreach, follow-up cadence
- **Email**: javier@onoxsystems.com
- **Target**: Gestoras, autónomos, pymes Vitoria-Gasteiz/Euskadi
- **Skills stack**:
    - Personalized cold email sequences (5 emails/day max)
    - CRM via CSV + Notion (seguimiento_leads.csv)
    - Demo booking — triggers calendar slot
    - Objection handling scripts (3 standard objections mapped)
- **Manual**: `docs/agents/JAVIER_SDR_MANUAL.md`

---

## Meeting Protocol (Mando Protocol)

1. **Compilation Phase**: Agents (ONIX) gather data from Vercel, logs, and socials.
2. **Proposal Phase**: ONIX drafts a summary of findings and proposed actions.
3. **Decision Phase**: Mario reviews the proposal (Presence Required).
4. **Execution Phase**: Mario gives the "Mando" (Command), ONIX executes across all layers.

---

*Maintained by ONOX Internal Team in Vitoria-Gasteiz.*
- One rule: demo before budget — always
