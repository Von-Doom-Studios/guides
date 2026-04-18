# Floki Website — Project Overview

## What It Is

The Floki website is the official e-commerce and brand presence for **Floki Brands** — a modern lifestyle brand selling luxury woven hangers, African print accent pillows, and sneaker phone cases.

## Live URLs

| Environment | URL |
|---|---|
| Production | https://flokibrands.com *(pending domain)* |
| Vercel preview | https://floki-website.vercel.app |
| Local dev | http://localhost:3000 |

## Repository

**GitHub:** [Floki-Brands/Floki-Website](https://github.com/Floki-Brands/Floki-Website)

## Tech Stack

| Layer | Tool |
|---|---|
| Framework | [Next.js 14](https://nextjs.org) (App Router) |
| Language | TypeScript |
| Styling | Tailwind CSS + inline styles |
| E-commerce | Shopify Storefront API |
| Hosting | Vercel |
| Version Control | GitHub |
| Package Manager | npm |

## Agent

The site is maintained by **VD-Dev** — an AI coding agent on the VonDoom Studios team. VD-Dev writes all code, manages commits, and pushes changes to GitHub. Humans direct, review, and approve.

→ See [ai-workflow/OVERVIEW.md](./ai-workflow/OVERVIEW.md) for how to work with the agent.

## Pages Built

| Page | Route | Status |
|---|---|---|
| Home | `/` | ✅ Live |
| Shop (All Products) | `/shop` | ✅ Live |
| Collection — Hangers | `/collections/hangers` | ✅ Live |
| Collection — Pillows | `/collections/pillows` | ✅ Live |
| Collection — Sneaker Cases | `/collections/sneaker-cases` | ✅ Live |
| Collection — All | `/collections/all` | ✅ Live |
| Product Detail | `/products/[handle]` | ✅ Live |
| Our Story | `/explore` | ✅ Live |
| FAQ | `/faq` | ✅ Live |
| Contact | `/contact` | ✅ Live |
| Terms of Service | `/terms-of-service` | ✅ Live |
| Privacy Policy | `/privacy-policy` | ✅ Live |
| Refund Policy | `/refund-policy` | ✅ Live |

## Key Docs

- [GETTING-STARTED.md](./GETTING-STARTED.md) — New to the project? Start here
- [SETUP.md](./SETUP.md) — Local development setup
- [ARCHITECTURE.md](./ARCHITECTURE.md) — How the codebase is structured
- [DEPLOYMENT.md](./DEPLOYMENT.md) — Vercel deployment and environment variables
- [DECISIONS.md](./DECISIONS.md) — Why things were built the way they were
- [ai-workflow/OVERVIEW.md](./ai-workflow/OVERVIEW.md) — Working with the AI agent
- [../design/STYLE-GUIDE.md](../design/STYLE-GUIDE.md) — Visual design system
