# Local Development Setup

This guide walks you through running the Floki website on your own computer so you can preview changes before they go live.

---

## Prerequisites

Install these once:

1. **Node.js (LTS)** — [nodejs.org](https://nodejs.org) → download and install the LTS version
2. **GitHub Desktop** — [desktop.github.com](https://desktop.github.com)

---

## First-Time Setup

### 1. Clone the Repository

1. Open **GitHub Desktop**
2. Click **File → Clone Repository**
3. Search for `Floki-Brands/Floki-Website`
4. Choose a local folder (e.g. your Documents or an SSD)
5. Click **Clone**

### 2. Install Dependencies

1. In GitHub Desktop, select the Floki-Website repo
2. Click **Repository → Open in Terminal**
3. Type the following and hit Enter:
   ```
   npm install
   ```
4. Wait for it to finish (takes 1–2 minutes the first time)

### 3. Start the Dev Server

In the same Terminal window:
```
npm run dev
```

Open your browser and go to **http://localhost:3000** — you should see the Floki site.

---

## Daily Workflow

Every time you sit down to work:

1. Open **GitHub Desktop**
2. Click **Fetch origin** → then **Pull origin** (gets latest changes from the agent)
3. Open Terminal: **Repository → Open in Terminal**
4. Run `npm run dev`
5. Open http://localhost:3000

The dev server hot-reloads — any changes the agent makes will appear in your browser automatically without restarting.

---

## Environment Variables

The site needs a Shopify API key to load products. The agent manages this via a `.env.local` file in the project root. This file is **not committed to GitHub** (it's in `.gitignore`). If you're setting up fresh:

1. Ask the agent or project lead for the `.env.local` contents
2. Create the file in the project root with those values

Variables needed:
```
SHOPIFY_STORE_DOMAIN=...
SHOPIFY_STOREFRONT_ACCESS_TOKEN=...
```

---

## Troubleshooting

| Problem | Fix |
|---|---|
| `npm: command not found` | Node.js isn't installed — go to [nodejs.org](https://nodejs.org) |
| Port 3000 taken by another site | Try http://localhost:3001 |
| Products not loading | Check `.env.local` exists with correct Shopify keys |
| Changes not showing | Hard refresh: `Cmd+Shift+R` (Mac) or `Ctrl+Shift+R` (Windows) |

---

→ Next: [ARCHITECTURE.md](./ARCHITECTURE.md)
