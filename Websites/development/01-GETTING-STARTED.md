# Getting Started — Floki Website Development

Welcome to the Floki website development system. This folder is the single source of truth for how the site is built, maintained, and updated — using an AI agent (VD-Dev) to write all the code.

---

## Who This Is For

Anyone involved in building or updating the Floki website — whether you're directing changes, reviewing the site, managing the project, or joining the team for the first time. You do not need to know how to code.

---

## Folder Map

| File / Folder | What It Covers |
|---|---|
| [02-README.md](./02-README.md) | Project overview — stack, live URLs, page inventory |
| [03-SETUP.md](./03-SETUP.md) | How to run the site on your own computer |
| [AI-WORKFLOW/](./AI-WORKFLOW/) | How to work with the AI agent to build and update the site |
| [05-ARCHITECTURE.md](./05-ARCHITECTURE.md) | How the codebase is structured |
| [06-DEPLOYMENT.md](./06-DEPLOYMENT.md) | How the site goes live and is hosted |
| [07-DECISIONS.md](./07-DECISIONS.md) | Why things were built the way they were |
| [COMPONENTS/](./COMPONENTS/) | Detailed specs for every major UI component |

---

## The Process in Brief

1. **Run the site locally** — clone the repo, install Node.js, run `npm run dev` (see `03-SETUP.md`)
2. **Request a change** — describe what you want in #dev on Discord
3. **Agent writes the code** — VD-Dev handles all implementation on the Mac mini
4. **Agent asks to push** — you approve with "push"
5. **Pull in GitHub Desktop** — sync the latest code to your machine
6. **Preview at localhost:3000** — review the change in your browser
7. **Repeat until approved**

---

## Ground Rules

- **The agent always asks before pushing.** You are always in control.
- **Pull before reviewing.** If you don't pull after a push, you're looking at an old version.
- **Locked values are locked.** Colors, spacing, and component specs in the Style Guide must not be changed without explicit approval.
- **One change at a time, batched clearly.** List all your changes in one message so the agent can address them in a single pass.

---

## Where to Talk to the Agent

VD-Dev lives in **#dev** on the Von Doom Discord server.

→ Start with [03-SETUP.md](./03-SETUP.md) to get the site running locally, then read [AI-WORKFLOW/01-OVERVIEW.md](./AI-WORKFLOW/01-OVERVIEW.md) to understand how to work with the agent.
