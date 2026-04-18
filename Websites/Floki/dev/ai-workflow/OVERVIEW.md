# AI Workflow — Overview

The Floki website is built and maintained using **VD-Dev**, an AI coding agent that runs as part of the VonDoom Studios agent system. You don't write code — you direct the agent in plain English.

---

## How It Works

```
You describe what you want
    ↓
Agent writes the code on the Mac mini
    ↓
Agent asks: "Ready to push — confirm?"
    ↓
You say "push"
    ↓
Agent pushes to GitHub
    ↓
You pull in GitHub Desktop
    ↓
You preview at http://localhost:3000
    ↓
Give feedback or approve
```

The agent has access to the full codebase, can read and write files, and manages all git operations. You never touch the terminal for code changes.

---

## Where to Talk to the Agent

VD-Dev lives in the **#dev channel** on the Von Doom Discord server. Send your requests there.

---

## What the Agent Can Do

- Build new pages and sections
- Edit existing components (layout, spacing, color, animation)
- Fix bugs
- Add new features
- Push and manage GitHub commits
- Read Notion and GitHub for context

## What the Agent Cannot Do (Without Your Input)

- Push changes without asking you first
- Make design decisions without direction
- Add new external services without your approval

---

## The Push/Pull Cycle

This is the core of the workflow:

1. **You request a change** in #dev
2. **Agent makes the change** on the Mac mini
3. **Agent says "confirm to push?"** — you say "push"
4. **Agent pushes to GitHub**
5. **You open GitHub Desktop** → Fetch origin → Pull origin
6. **You refresh your browser** at http://localhost:3000 to see it

Always pull before reviewing. If you don't pull, you're looking at an old version.

---

## Sessions

Each conversation with the agent is a session. The agent remembers context within a session. When sessions restart (e.g. after a long break), the agent reloads its memory from saved files — so important decisions and design rules persist.

---

## Guides in This Section

- [PROMPTING.md](./PROMPTING.md) — How to write effective requests
- [DESIGN-WORKFLOW.md](./DESIGN-WORKFLOW.md) — Using AI to generate site assets and content

---

→ Back to [../README.md](../README.md)
