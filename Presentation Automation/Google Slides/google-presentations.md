# Google Presentations — AI-Powered Slide Deck from Markdown

**Last updated:** April 17, 2026
**Skill level:** Beginner — no coding experience required
**What this covers:** How to write a presentation in Markdown, hand it to an AI agent to convert into a styled Google Slides deck, and publish it to Google Drive using Google Apps Script

---

## What This Process Is

Instead of manually building slides in Google Slides, you write the content of your presentation in a simple text format called Markdown — and then an AI agent converts that content into a fully designed, styled Google Slides presentation automatically.

A small script (written in Google Apps Script) runs inside Google's own tools to build the deck. You don't install anything. You don't write any code. The AI writes the script; you run it.

---

## Why This Approach

- **Separation of content and design** — You focus on what to say; the agent handles how it looks
- **Version-controlled** — Your content lives in GitHub as Markdown files, so every change is tracked
- **Reproducible** — Run the script again at any time to regenerate the deck
- **Editable** — If content changes, update the Markdown file and regenerate

---

## What You Need

- A GitHub account (free)
- A Google account (free)
- Access to an AI agent (your VonDoom Studios agent setup)
- That's it

---

## Step 1 — Write Your Content in Markdown

Markdown is a lightweight way to write formatted text. It uses simple symbols instead of clicking buttons in a word processor. Here's the key syntax:

```
# This is a large heading (H1)
## This is a medium heading (H2)
### This is a smaller heading (H3)

- This is a bullet point
- So is this

**This text is bold**
*This text is italic*
```

### How We Organized It

For the 24 Tattoos pitch dossier, each section of the presentation got its own Markdown file:

```
01-cover.md
02-logline.md
03-synopsis-short.md
04-synopsis-full.md
05-characters.md
06-themes.md
07-tone-and-comps.md
08-setting.md
09-market.md
10-writer-bio.md
```

Each file contained only the text content for that section — no design decisions, just words. The AI agent read all of them and understood what each slide needed to say.

> **Tip:** Numbering your files (01-, 02-, etc.) keeps them in order inside GitHub and makes it easy for both you and the agent to reference them.

### Where They Live

All content files were stored in a GitHub repository:
`github.com/Von-Doom-Studios/24-tattoos-dossier`

This makes the content version-controlled — every edit is tracked, and you can roll back to a previous version if something goes wrong.

---

## Step 2 — The AI Agent Reads the Content and Writes the Script

Once the Markdown files are in GitHub, you ask the AI agent to generate the Google Apps Script.

The agent:
1. Reads every Markdown file in order
2. Understands the structure — what's a title, what's body text, what's a list
3. Maps each section to a slide
4. Writes a `.gs` script that builds the entire presentation programmatically

### What the Script Does

The script uses Google's built-in `SlidesApp` API. This is a set of tools built into Google that lets code create and modify Google Slides — no external software needed.

The script:
- Creates a new Google Slides file in your Drive
- Adds slides one by one, each representing a section
- Places text boxes, shapes, colors, and lines in precise positions
- Applies fonts, sizes, and colors to match the design system
- Inserts image placeholder boxes where visuals are needed

---

## Step 3 — The Design System (How It Was Styled)

The agent didn't just dump text onto blank slides. It applied a full design system — a set of consistent rules for how everything looks.

### Color Palette

The 24 Tattoos dossier used a specific brand palette defined at the top of the script:

| Color Name | Hex Code | Used For |
|---|---|---|
| Black | `#0A0A0A` | Primary slide background |
| Charcoal | `#181818` | Card/panel backgrounds |
| Gold | `#C9A84C` | Primary accent — headings, rules, borders |
| Bone | `#F0EAD6` | Primary body text — warm off-white |
| Muted | `#9A9080` | Secondary text, captions |
| UV Purple | `#7B5CF0` | Used sparingly for reveal moments |
| Divider | `#2A2826` | Subtle horizontal rules between sections |

These were defined once at the top of the script as constants (`const C = { ... }`), so changing a color in one place updates it everywhere.

### Typography

Two font families were used throughout:

- **Playfair Display** — A serif display font used for large titles and headings. Gives the deck a cinematic, editorial feel.
- **Lato** — A clean sans-serif font used for body text, captions, and metadata. Readable at small sizes.

Fonts were also defined as constants at the top (`const F = { ... }`).

### Layout Elements

Every slide shared a set of recurring design elements that create visual consistency:

- **Top-left dash mark** — A small gold horizontal line in the upper-left corner of every slide
- **Top-right metadata block** — Two small label/value pairs (e.g., "Section · 01", "Written by · Q. Pradelle")
- **Section label** — A gold uppercase label near the top of each content slide, with a thin rule below it
- **Bottom page bar** — A dark strip at the bottom of every slide with the page number, a rule, and the presentation title
- **Gold orbs** — Layered semi-transparent ellipses positioned in corners or off-screen edges. These approximate a soft glowing light effect.
- **Circle arrow** — A small circular button with an arrow, used as a visual "next" indicator

### Slide Dimensions

All slides were sized at **720 × 405 points** — a standard 16:9 widescreen ratio. Every element was positioned using exact pixel coordinates (`x`, `y`, `width`, `height`) calculated relative to these dimensions.

### The Helper Function Pattern

To keep the code clean and non-repetitive, the agent wrote small helper functions for common actions:

```
txt()      → insert a text box with font, size, and color
rect()     → insert a colored rectangle
ellipse()  → insert a circle/oval shape
hline()    → insert a horizontal line
vline()    → insert a vertical line
imgBox()   → insert an image placeholder (a labeled box)
orb()      → place a gold orb at a named position
pageBar()  → add the bottom page bar with a slide number
topDash()  → add the top-left gold dash
topMeta()  → add the top-right metadata block
```

These functions were called on every slide, keeping each slide's code short and readable.

---

## Step 4 — Run the Script in Google Apps Script

Once the agent generates the `.gs` file, you run it through Google's built-in script editor. No installation required.

### Steps

1. Go to **[script.google.com](https://script.google.com)**
2. Click **"New Project"** (top left)
3. Delete all the default code in the editor (it will say `function myFunction() {}`)
4. Open the `.gs` file from the GitHub repo (e.g., `google-apps-script/create-dossier.gs`)
5. Copy the entire contents and **paste it into the Apps Script editor**
6. At the top of the editor, find the dropdown that says `Select function` — choose **`createDossier`** (or whatever the main function is named)
7. Click **▶ Run**
8. A dialog will appear asking for permissions — click **Review Permissions → Allow**
   - This gives the script permission to create files in your Google Drive
   - It only has access to files the script itself creates
9. Wait **15–30 seconds**
10. Open **Google Drive** — the presentation will be there, ready to open

> **Note:** The presentation is created under whichever Google account is logged into the browser. If you want it in a specific account, make sure you're logged in as that account before running.

---

## Step 5 — Add Images (Manual Step)

The script creates labeled placeholder boxes where images should go. These look like dark boxes with a description of what image belongs there (e.g., `[ COVER IMAGE — TATTOOED HANDS, PARIS RAIN ]`).

To add real images:
1. Generate or source the image (using Midjourney, Flux, or sourced photography)
2. In Google Slides, click on the placeholder box
3. Go to **Insert → Image → Upload from computer** (or paste a URL)
4. Position and resize the image to fill the placeholder

> **Tip:** The agent typically also writes an `image-prompts.md` file listing one prompt per image placeholder, so you know exactly what to generate.

---

## How to Update the Deck

If the content changes:

1. Edit the relevant Markdown file in GitHub
2. Ask the agent to regenerate the script (or update specific slide functions)
3. Paste the updated script into Apps Script and run it again
4. A new version of the presentation is created in Google Drive

You can also edit specific slide functions directly in the script without regenerating everything — each slide is its own function.

---

## File Structure Reference

Here's how the project was organized:

```
24-tattoos-dossier/
├── 01-cover.md                  ← Content for slide 1
├── 02-logline.md                ← Content for slide 2
├── ...                          ← One file per section
├── 10-writer-bio.md
├── google-apps-script/
│   ├── create-dossier.gs        ← The script that builds the deck
│   └── README.md                ← How to run it
└── visual-assets/
    └── (generated images)
```

---

## Common Questions

**Do I need to know how to code?**
No. You write the content in plain text (Markdown). The agent writes the code. You paste and click Run.

**What if the script errors out?**
Copy the error message and send it to the agent. It will fix the script and you try again.

**Can I change the colors or fonts?**
Yes — ask the agent to update the design constants at the top of the script, then re-run.

**Can I use this for any presentation?**
Yes. The workflow is the same regardless of the topic. Write the content in Markdown, tell the agent what style you want, and it generates the script.

**What if I want to add a slide?**
Ask the agent to add a new `buildSlide()` function and call it inside `createDossier()`. Then re-run.

---

## Quick Reference — The Workflow

```
1. Write content → Markdown files in GitHub
2. Ask AI agent → it reads the files and writes the .gs script
3. Go to script.google.com → New Project → paste the script
4. Select the main function → click Run → authorize
5. Open Google Drive → find your new presentation
6. Add real images to replace the placeholders
7. Done
```

---

*This guide covers the process used to build the 24 Tattoos pitch dossier for VonDoom Studios.*
*Last updated: April 17, 2026*
