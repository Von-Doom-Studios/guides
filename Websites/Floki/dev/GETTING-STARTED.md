# Getting Started — Floki Website

> **No coding experience required.** This guide is for anyone joining the team who needs to understand how the Floki website is built, maintained, and updated — using AI agents to do the heavy lifting.

---

## What You Need to Know First

The Floki website is a **Next.js** web application hosted on **Vercel**. All code lives on **GitHub**. You never need to write code yourself — an AI agent (VD-Dev) writes and manages it for you.

Your job is to:
1. Know what you want the site to do or look like
2. Describe it clearly to the agent
3. Review the result and give feedback

---

## What You'll Need Installed

| Tool | What it's for | Download |
|---|---|---|
| **GitHub Desktop** | Syncing code to/from GitHub | [desktop.github.com](https://desktop.github.com) |
| **Node.js (LTS)** | Running the site locally | [nodejs.org](https://nodejs.org) |
| A modern browser | Previewing the site | Chrome, Safari, Firefox |

---

## Step-by-Step: Run the Site Locally

1. Open **GitHub Desktop**
2. Clone the repo: `Floki-Brands/Floki-Website`
3. Click **Repository → Open in Terminal**
4. Run: `npm install` (first time only — waits a minute)
5. Run: `npm run dev`
6. Open your browser to **http://localhost:3000**

That's the live preview of the site running on your machine.

---

## How Changes Work

```
You describe a change → Agent writes the code → Agent asks to push → You approve → Agent pushes to GitHub → You pull in GitHub Desktop → You see it locally
```

The agent **always asks before pushing**. You are always in control.

---

## Where to Go Next

- 📖 [README.md](./README.md) — Project overview and links
- 🛠 [SETUP.md](./SETUP.md) — Detailed local setup
- 🤖 [ai-workflow/OVERVIEW.md](./ai-workflow/OVERVIEW.md) — How to work with the AI agent
- 🎨 [../design/STYLE-GUIDE.md](../design/STYLE-GUIDE.md) — Visual rules for the site
