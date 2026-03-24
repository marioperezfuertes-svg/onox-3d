# ONOX Systems — Automation Stack

> Complete guide to all automation tools, workflows, and techniques used by ONOX Systems. ONIX manages and expands this stack continuously.

---

## Automation Philosophy

**Automate everything that doesn't require Mario's judgment. Notify Mario on everything that does.**

Every automation must:
1. Be documented here with purpose and trigger
2. Have a fallback/alerting mechanism
3. Be monitorable by ONIX
4. Improve velocity, stability, or knowledge

---

## Stack Overview

| Tool | Role | Environment | Status |
|------|------|-------------|--------|
| GitHub Actions | CI/CD, sync, testing | Cloud | Active |
| N8N | Business automation, webhooks, integrations | Local + Cloud | Configuring |
| Vercel | Auto-deploy on push | Cloud | Active |
| Supabase Edge Functions | Serverless automation triggers | Cloud | Active |
| Tailscale | Private network automation, health checks | Private mesh | Active |
| Notion API | Documentation automation, briefings | Cloud | Planned |
| ONIX Agent | Meta-automation — manages all others | Both | Active |

---

## GitHub Actions Workflows

### 1. CI — Test & Lint on PR
**File:** `.github/workflows/ci.yml`
**Trigger:** Every PR to `main`
**Actions:**
- Install dependencies (bun install)
- Run TypeScript check
- Run linter (Biome)
- Run unit tests
- Comment results on PR

### 2. Deploy to Vercel on Push
**File:** `.github/workflows/deploy.yml`
**Trigger:** Push to `main`
**Actions:**
- Trigger Vercel deployment
- Wait for deployment URL
- Post deployment URL to commit status
- Notify ONIX via webhook

### 3. Sync from Upstream (Pascal)
**File:** `.github/workflows/sync-pascal-upstream.yml`
**Trigger:** Weekly schedule (Monday 09:00 UTC)
**Actions:**
- Fetch upstream changes from `pascalorg/editor`
- Create PR with upstream diff
- Label PR as `upstream-sync`
- ONIX reviews and decides to merge

### 4. ONIX Weekly Briefing
**File:** `.github/workflows/onix-briefing.yml` *(to create)*
**Trigger:** Every Friday 17:00 UTC
**Actions:**
- Collect git log from past week
- Collect open issues and PRs
- Generate briefing via ONIX
- Create GitHub issue tagged `onix-brief`
- Post to Notion workspace

### 5. Dependency Updates
**File:** `.github/workflows/deps-update.yml` *(to create)*
**Trigger:** Monthly (1st of month)
**Actions:**
- Run `bun update`
- Create PR with updated lock file
- Run CI checks
- Label as `deps-update`

---

## N8N Workflows

### Setup
```bash
# Local N8N (development)
docker run -it --rm -p 5678:5678 n8nio/n8n

# Access at http://localhost:5678
```

### Workflow 1 — GitHub → Notion Sync
**Trigger:** GitHub webhook (new issue, PR, commit)
**Flow:** GitHub → N8N → Notion database
**Purpose:** Keep Notion project board in sync with GitHub activity

### Workflow 2 — Vercel Deploy → Alert
**Trigger:** Vercel deployment webhook
**Flow:** Vercel → N8N → [Slack/Telegram/Email]
**Purpose:** Notify team of successful/failed deployments

### Workflow 3 — Research Aggregator
**Trigger:** Daily schedule (08:00)
**Flow:** RSS feeds → N8N → Filter by keywords → Notion page
**Keywords:** WebGPU, React Three Fiber, AI agents, spatial computing, Basque tech
**Purpose:** Feed STUDIES.md research pipeline

### Workflow 4 — Supabase Health Monitor
**Trigger:** Every 15 minutes
**Flow:** Supabase API ping → N8N → Alert if down
**Purpose:** Service health monitoring

### Workflow 5 — Weekly Revenue Report
**Trigger:** Every Monday 09:00
**Flow:** Stripe API → N8N → MRR calculation → Notion
**Purpose:** Track revenue metrics for INVESTMENT.md KPIs

---

## Vercel Automation

### Auto-Deploy Configuration
```json
// vercel.json
{
  "buildCommand": "bun run build",
  "outputDirectory": ".next",
  "framework": "nextjs",
  "git": {
    "deploymentEnabled": {
      "main": true
    }
  }
}
```

### Preview Deployments
- Every PR gets a preview URL automatically
- Preview URLs are posted as PR comments
- ONIX reviews preview before approving merge

### Environment Variables
Managed via Vercel dashboard. ONIX tracks required vars in `.env.example`.
Never commit secrets to git.

---

## Supabase Edge Functions

### Function: `onix-notify`
**Purpose:** Receive webhook from external services and notify ONIX
**Endpoint:** `https://[project].supabase.co/functions/v1/onix-notify`

### Function: `deploy-hook`
**Purpose:** Trigger Vercel deployment from external events
**Usage:** Called by N8N when conditions are met

### Function: `usage-tracker`
**Purpose:** Track API usage for billing/metrics
**Trigger:** Each 3D scene load via the viewer

---

## Tailscale Automation

### Network Topology
```
onoxsystems.com (Vercel Edge)
         ↓
    [Public traffic]
         ↓
Supabase (DB + Auth + Functions)
         ↓
    [Tailscale mesh]
         ↓
Dev machines (Vitoria-Gasteiz)
N8N instance
Local test environments
```

### Health Check Script
```bash
#!/bin/bash
# Run via cron every 5 minutes
tailscale status | grep -E "(online|offline)" | while read line; do
  if echo "$line" | grep -q "offline"; then
    curl -X POST $WEBHOOK_URL -d "{\"text\": \"ONOX Tailscale node offline: $line\"}"
  fi
done
```

---

## Automation Skills — Team Training

### Level 1 — Basic (All team members)
- [ ] Understand GitHub Actions YAML syntax
- [ ] Create simple N8N workflows
- [ ] Monitor Vercel deployments
- [ ] Use Supabase dashboard

### Level 2 — Intermediate (DevOps team)
- [ ] Write custom GitHub Actions
- [ ] N8N advanced flows (conditions, loops, error handling)
- [ ] Supabase Edge Functions (Deno/TypeScript)
- [ ] Tailscale ACL configuration

### Level 3 — Advanced (ONIX + Senior devs)
- [ ] Multi-step automation orchestration
- [ ] Webhook security and validation
- [ ] Rate limiting and cost optimization
- [ ] Automation testing and monitoring
- [ ] Custom ONIX integration patterns

---

## Automation Principles (Maximizar Resultados)

1. **Idempotency** — Running twice should produce same result
2. **Observability** — Every automation must log its actions
3. **Fail loudly** — Failures must alert, never silently fail
4. **Least privilege** — Each automation only has the access it needs
5. **Documentation first** — Document before you build
6. **ONIX awareness** — ONIX must know about every automation

---

## Accounts Required (Complete Stack)

| Service | Account | Purpose |
|---------|---------|--------|
| GitHub | marioperezfuertes-svg | Code + CI/CD |
| Vercel | ONOX account | Deployment |
| Supabase | ONOX project | DB + Auth + Functions |
| Tailscale | ONOX org | Private network |
| N8N | Self-hosted or n8n.cloud | Business automation |
| Stripe | ONOX account | Payments |
| Notion | ONOX workspace | Docs + PM |
| Anthropic | API key | ONIX LLM |
| Cloudflare | onoxsystems.com DNS | Domain + CDN |

---

*Maintained by ONIX. Extended by the DevOps team. All additions must be documented here before deployment.*
