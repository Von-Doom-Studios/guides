# AI Agent System Guide — Machine-Readable Reference

**Last updated:** 2026-04-16  
**Scope:** VonDoom Studios · Floating Objects Studios · Floki Brands  
**Runtime:** OpenClaw (self-hosted)

---

## System Overview

6 persistent AI agents, each bound to a Discord channel, serving three companies. Each agent has a SOUL.md (role definition), AGENTS.md (team map), and MEMORY.md (session-persistent context). Sessions wipe nightly. Memory files are the only persistent context.

---

## Agent Roster

| Agent | Discord Channel | Role |
|-------|----------------|------|
| Ops | #ops | External comms, email, project coordination, cross-agent routing |
| Marketing | #marketing | Social media, content, campaigns — Floki + FOS |
| Creative | #creative | AI artwork, animation assets, prompt engineering, design |
| Dev | #dev | Websites, mobile apps, code, deployment |
| Finance | #finance | Accounting, invoicing, tax, credit strategy |
| Growth | #growth | Analytics, sales strategy, user acquisition |

---

## Companies

### Floki Brands
- **Products:** Luxury woven hangers, sneaker phone cases, African print accent pillows
- **Hanger inventory:** 1,000 units (200 each: red, green, blue, yellow, white)
- **COGS:** $2.00/unit (hangers)
- **DTC Pricing:** Single $9.99 / 4-pack $34.99 / 8-pack mixed $59.99
- **Email:** shopflokibrands@gmail.com (routed through Ops)
- **Status:** Website in development (blocked on Shopify credentials)

### VonDoom Studios
- **Type:** Full-service creative agency (design, animation, client work)
- **Email:** vondoomstudios@gmail.com (Ops sends/receives)
- **GitHub Org:** Von-Doom-Studios
- **Repos:** clients, finance, guides, 24-tattoos-dossier (archived)

### Floating Objects Studios
- **Type:** Animation studio (traditional + AI animation)
- **Agents:** fos-research, fos-visual, fos-worldbuilding, fos-writer (separate agent cluster)
- **Active project:** CFG (multi-season animated series in development)

---

## Agent Behavior Standards

### Memory Rules (all agents)
- **Real-time writes:** Write to MEMORY.md immediately on: new instructions, decisions, corrections, state changes
- **Session end:** MEMORY.md must be updated before session ends — non-negotiable
- **Format:** Daily notes in `memory/YYYY-MM-DD.md`; long-term context in `MEMORY.md`

### Cross-Agent Communication
- Agents cannot directly call each other's tools
- Cross-agent requests go through Anthony (human relay)
- Reference target agent by name and Discord channel
- Do NOT send status pings to other agents — only engage when delivering something actionable

### Cost Discipline
- **Images:** Max 2–3 per session; prefer text descriptions over image analysis
- **Browser:** Only when Anthony explicitly requests a specific URL
- **Scope first:** State what you're about to do before doing it if it involves images, browser, or extended research
- **No autonomous browsing**

### Reply Length (Dev agent only)
- 1–2 sentences max
- After `git push`: reply with ONLY the commit hash

---

## GitHub Conventions

- **Org:** Von-Doom-Studios
- **CLI:** `gh` (authenticated)
- **All significant changes:** PR-based
- **Task tracking:** GitHub Issues
- **CI/CD:** GitHub Actions → Vercel/Netlify

### Active Repos
| Repo | Visibility | Description |
|------|-----------|-------------|
| clients | public | Client work |
| finance | private | Financial records |
| guides | public | This document + human guide |
| 24-tattoos-dossier | public, archived | Quentin Pradelle pitch dossier |

---

## Active Projects

### Floki Website
- **Stack:** Next.js / React / Tailwind / Vercel
- **Blocker:** Shopify Storefront API token + store URL + logo file
- **Status:** Dev blocked; Marketing + Sales holding launch prep

### Floki Sales Pipeline
- 50 prospects built across 8 channels (see Growth MEMORY.md)
- Outreach on hold until website launches
- 7 email templates ready in EMAIL_TEMPLATES.md
- ~38 of 50 prospects still need contact info research

### Credit Repair — Anthony Emezu
- TransUnion: 574 / Equifax: 587 (as of 2026-03-23)
- Priority items: Velocity Investments double jeopardy, student loan rehabilitation, high utilization
- Finance agent owns: letter queue, bureau disputes, pay-for-delete negotiations
- Status: Strategy delivered, awaiting Anthony responses

### 2024 Tax Return
- **Status:** Filed by mail 2026-04-15
- Federal owed: $9,167 | NY+NYC owed: $3,087 | Total: $12,254
- Capital loss carryforward: -$10,083.30
- Payment plans needed: irs.gov/OPA (federal), tax.ny.gov (NY)

### CFG Animated Series
- FOS cluster: fos-research, fos-visual, fos-worldbuilding, fos-writer
- Characters: Ba Li, Phantom Doctor, Wanmei Lu
- Notion integration active (notion.sh scripts in each workspace)
- Season 1 episode structure in progress

---

## Tech Stack

| Layer | Tech |
|-------|------|
| Web | Next.js, React, Tailwind CSS |
| Deploy | Vercel / Netlify |
| Mobile | React Native / Expo |
| Backend | Node.js / Python |
| Database | PostgreSQL / Supabase |
| Runtime | OpenClaw (self-hosted, Mac mini) |
| Versioning | GitHub (Von-Doom-Studios org) |

---

## Key People

| Name | Role | Contact |
|------|------|---------|
| Anthony Emezu | Owner / Principal | Discord: aemezu (638133675439030272) |
| Quentin Pradelle | Screenwriter (24 Tattoos) | quentinpradelle@gmail.com / +33 674 898 937 |

---

## Sales Pricing Reference

### Floki Hangers — B2B Channels
| Channel | Price/unit | MOQ |
|---------|-----------|-----|
| FF&E Firms | $5.00–6.00 | 50 |
| Hotels Direct | $5.00–6.00 | 50 |
| STR Hosts | $7.00–7.50 | 12 |
| Boutique Retail | $7.50–8.00 | 24 |
| Fashion Brands | $7.50–8.00 | 24 |
| Personal Stylists | $10.00 + 15–20% referral | — |
| Corporate Gifting | $12–15 (packaged) | — |

---

## Finance Reference

### Home Office Deduction (2024)
- Office: 561 sq ft / Total: 1,020 sq ft = 55%
- Rent: $29,400 | Electric: $3,480 | Internet: $948

### Vehicle (2024)
- 2020 Porsche Cayenne, Affinity FCU
- Business use: 60%
- Deduction: $24,284 (actual expenses + MACRS depreciation)
- Interest paid 2024: $3,794

---

## Routing Rules

| Task Type | Owner |
|-----------|-------|
| Client email / external comms | Ops |
| Social media / content | Marketing |
| AI art / design / animation assets | Creative |
| Websites / apps / code | Dev |
| Invoices / books / tax / credit | Finance |
| Prospect research / sales strategy | Growth |
| Outreach execution | Growth / Ops (email relay) |
| GitHub Issues (task creation) | Ops → Dev |
| Creative briefs | Marketing → Creative |

---

## Agent File Structure (per workspace)

```
workspace/
├── SOUL.md          # Role definition — read every session
├── AGENTS.md        # Team map + cross-agent rules
├── MEMORY.md        # Long-term persistent context
├── HEARTBEAT.md     # Scheduled check tasks (leave blank = skip)
├── IDENTITY.md      # Agent persona
├── TOOLS.md         # Local tool/environment notes
├── USER.md          # About Anthony
└── memory/
    └── YYYY-MM-DD.md  # Daily session notes
```
