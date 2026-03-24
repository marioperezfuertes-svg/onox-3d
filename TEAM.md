# ONOX 3D — Team, Skills & Meeting Protocol

> **ONOX Systems** · Bilbao, Euskadi · **onoxsystems.com**
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
  - AI/LLM orchestration (Claude, Gemini, Ollama, N8N)
  - Business strategy & B2B commercial (gestoras, autónomos, Bilbao)
  - RTX 4060 Ti local inference — €0/month AI stack
- **Multiplier techniques**:
  - Delegates execution to ONIX, retains decision
  - Uses "compile then decide" protocol — never decides without data
  - Reviews ONOX Learning Log weekly before any meeting
  - One rule: demo before budget — always

---

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
- **Target**: Gestoras, autónomos, pymes Bilbao/Euskadi
- **Skills stack**:
  - Personalized cold email sequences (5 emails/day max)
  - CRM via CSV + Notion (seguimiento_leads.csv)
  - Demo booking — triggers calendar slot
  - Objection handling scripts (3 standard objections mapped)
- **Manual**: `docs/agents/JAVIER_SDR_MANUAL.md`
- **Multiplier techniques**:
  - "Demo before budget" rule hard-coded
  - Max 3 touches per lead — no spam
  - Uses social proof from previous ONOX demos
  - Handoff to Mario when lead is warm (score ≥ 7/10)

#### Nexo — Coordination & Communications Hub
- **Role**: Internal routing, external communications, email management
- **Email**: nexo@onoxsystems.com
- **Skills stack**:
  - Routes inter-agent messages
  - Drafts and sends transactional emails via Resend
  - Slack/Telegram relay for ONIX alerts
  - Meeting scheduling and agenda compilation
- **Manual**: `docs/agents/NEXO_MANUAL.md`
- **Multiplier techniques**:
  - Zero inbox protocol — all emails triaged within 4h
  - Compresses multi-agent activity into single daily digest
  - Never sends without Mario approval for external comms

#### Laura — Legal & Compliance
- **Role**: Contract review, GDPR, terms, legal risk flags
- **Email**: laura@onoxsystems.com
- **Skills stack**:
  - GDPR compliance checks on data handling
  - Contract template library (NDA, SLA, MSA)
  - Risk flagging — escalates to Mario if severity ≥ medium
  - EU AI Act awareness (agent disclosure requirements)
- **Manual**: `docs/agents/LAURA_LEGAL_MANUAL.md`
- **Multiplier techniques**:
  - Proactive — reviews new features before deploy, not after
  - Maintains `docs/legal/COMPLIANCE_LOG.md`
  - Templates everything — zero custom legal work from scratch

#### Agora — Commercial Strategy
- **Role**: Pricing, positioning, market analysis, go-to-market
- **Email**: agora@onoxsystems.com
- **Skills stack**:
  - Competitive analysis (weekly scan of competitors)
  - Pricing models (fixed, retainer, success-based)
  - Proposal generation for B2B clients
  - Market segmentation (gestoras, constructoras, industriales)
- **Manual**: `docs/agents/AGORA_STRATEGY_MANUAL.md`
- **Multiplier techniques**:
  - "Minimum viable price" rule — price to close, not to impress
  - Builds comparison matrices before any pricing meeting
  - Tracks win/loss reasons in `data/ventas/win_loss_log.csv`

---

## Meeting Protocol

> Mario is **always present**. No decision is made without him in the room.
> ONIX prepares everything. Mario reviews and decides. Dates are committed in writing.

### Meeting Types

#### 1. Weekly Digest Meeting (Every Monday, 09:00 CET)
**Format**: Async-first — ONIX sends compiled digest by 08:30. Mario reviews and responds.
**Agenda** (ONIX compiles automatically):
- Upstream Pascal changes detected this week
- Open PRs and pending reviews
- Agent activity summary (Javier leads, Nexo emails, Agora proposals)
- Studies in progress — new findings
- Blockers requiring Mario decision
- Suggested actions for the week

**Output**: Mario approves/rejects each item. ONIX executes approved items same day.

#### 2. Decision Meeting (On-demand, triggered by ONIX)
**Trigger**: ONIX detects a decision needed (new cost, new scope, new risk, roadmap conflict)
**Format**: ONIX prepares a "Decision Packet":
```
DECISION PACKET — [date] — [topic]
├── Context: what happened
├── Options: A / B / C (with tradeoffs)
├── Recommendation: ONIX suggests option X because...
├── Required from Mario: decision + date commitment
└── Deadline: decision needed by [date] to stay on roadmap
```
**Output**: Mario decides. Date committed. ONIX logs to Notion + ROADMAP.md.

#### 3. Sprint Review (Every 2 weeks, Friday 17:00 CET)
**Format**: Live review of what shipped vs planned
**Agenda**:
- What shipped this sprint (demos ready)
- What didn't ship — honest post-mortem
- Studies completed — findings presented by ONIX
- Next sprint scope — Mario sets priorities
- Date commitments updated in ROADMAP.md

**Rule**: Every sprint ends with a working demo. No exceptions.

#### 4. Monthly Strategy Meeting (Last Friday of month, 16:00 CET)
**Format**: 60 min max. ONIX prepares full monthly report.
**Agenda**:
- Revenue & pipeline update (Javier + Agora)
- Technical health (Nexo + ONIX)
- Legal risks (Laura)
- Studies review — which ST-XX to act on
- Roadmap version bump — Mario confirms next milestone dates
- New agent/tool proposals — approve/reject

**Output**: Updated ROADMAP.md version committed same day.

---

## Skills Multiplication Framework

> Every agent and every human on this team follows the ONOX Skills Multiplier:
> **Learn → Document → Systemize → Automate → Teach**

| Level | Action | Output |
|---|---|---|
| 1. Learn | Agent or Mario encounters new technique/tool | Raw notes in `docs/learning/` |
| 2. Document | ONIX formalizes into structured doc | Entry in STUDIES.md |
| 3. Systemize | Pattern extracted into reusable template/script | File in `docs/templates/` or `scripts/` |
| 4. Automate | Pattern becomes N8N workflow or GitHub Action | Workflow in `.github/workflows/` or `n8n/` |
| 5. Teach | Other agents use it autonomously | Added to agent manual |

**Multiplier rule**: Nothing learned stays in one brain. Everything flows up the chain.

---

## Agent Manuals Index

All manuals live in `docs/agents/`. Each manual contains:
- Purpose and scope
- Input/output specification
- Prompt templates
- Edge cases and fallbacks
- Known limitations
- Version history

| Manual | Agent | Last updated |
|---|---|---|
| `ONIX_ORCHESTRATOR_MANUAL.md` | ONIX | Auto-updated on each sprint |
| `JAVIER_SDR_MANUAL.md` | Javier | Updated after each lead campaign |
| `NEXO_MANUAL.md` | Nexo | Updated on protocol changes |
| `LAURA_LEGAL_MANUAL.md` | Laura | Updated on legal changes/EU AI Act |
| `AGORA_STRATEGY_MANUAL.md` | Agora | Updated after each strategy meeting |

---

## Accounts & Automations Master Table

| Service | Account | Owner | 2FA | Purpose | Automation |
|---|---|---|---|---|---|
| GitHub | marioperezfuertes-svg | Mario | ✓ | All ONOX repos | Actions: CI/CD, upstream sync |
| Vercel | onoxsystems@gmail.com | Mario | ✓ | onoxsystems.com + 3d.onoxsystems.com | Auto-deploy main |
| Supabase | onoxsystems@gmail.com | Mario | ✓ | Auth + DB shared platform | Row-level security |
| Cloudflare | onoxsystems@gmail.com | Mario | ✓ | DNS onoxsystems.com | Tunnel for MCP |
| Notion | mario@onoxsystems.com | Mario | ✓ | Docs, meetings, logs | ONIX webhook updates |
| Resend | mario@onoxsystems.com | Mario | ✓ | nexo@onoxsystems.com transactional | N8N send via API |
| npm | onoxsystems | Mario | ✓ | @onox/scene-core, @onox/scene-viewer | GH Action publish |
| Telegram | ONIX_bot | ONIX | Token | Alerts + daily digest | N8N → Telegram API |
| N8N | Local Docker (onox_n8n) | Mario | Basic | Automation hub | 12+ workflows active |
| Langfuse | Local Docker | Mario | Basic | LLM tracing + scoring | Auto-log all agent calls |
| Ollama | Local RTX 4060 Ti | Mario | — | Local inference €0/month | Auto-pull models |
| Qdrant | Local Docker | Mario | — | Vector DB for agent memory | Auto-embed on new docs |
| Redis | Local Docker | Mario | — | Cache + queue | TTL 24h default |
| OpenWebUI | Local Docker | Mario | Basic | LLM interface | MCP client |
| Sentry | onoxsystems@gmail.com | Mario | ✓ | Error tracking | Auto-capture exceptions |
| Uptime Robot | onoxsystems@gmail.com | Mario | ✓ | onoxsystems.com monitoring | Alert to Telegram if down |
| Cal.com | mario@onoxsystems.com | Mario | ✓ | Demo booking (Javier) | Webhook to N8N on booking |

### Critical Automations

| Automation | Trigger | Action | Owner |
|---|---|---|---|
| Upstream Pascal Sync | Monday 08:00 CET (cron) | Check diff, notify ONIX if changes | GitHub Actions |
| Daily Digest | Daily 08:30 CET | Compile agent activity → Telegram Mario | N8N + ONIX |
| Deploy to Prod | Push to main | Build + deploy onoxsystems.com | Vercel |
| Learning Log Update | ONIX detects new pattern | Append to ONOX_LEARNING_LOG.md | ONIX agent |
| Lead Score Update | Javier email response | Update seguimiento_leads.csv | N8N |
| Error Alert | Sentry exception | Post to Telegram #alerts | Sentry webhook |
| Downtime Alert | Site down >3 min | Post to Telegram + SMS Mario | Uptime Robot |
| Demo Booking | Cal.com event | Create Notion page + remind Mario 1h before | N8N |

---

*Last updated: 2026-03-24 · ONOX Systems · mario@onoxsystems.com · onoxsystems.com*
