# Figma Plugin Guide — How to Build a Deck Using a Plugin

**Last updated:** April 16, 2026  
**What this covers:** The process for building a Figma presentation using a custom plugin — based on what actually worked

---

## What This Process Is

You write a plugin in JavaScript that builds an entire presentation inside Figma automatically — slides, text, layouts, colors, shapes, and image placeholders. You import it as a local plugin, click a button, and it generates the full deck.

Every change is made in code and re-run. It's reproducible and version-controlled.

---

## What You Need

Three files in the same folder on your computer:
- `manifest.json` — tells Figma the plugin name and where the files are
- `code.js` — the plugin logic that builds the deck
- `ui.html` — a simple panel with a button that triggers the generation

> **Note:** `manifest.json` must include two required fields or Figma will error on import:
> - `"editorType": ["figma"]` — required by Figma; without it you get "Missing editorType"
> - `"documentAccess": "dynamic-page"` — required when the plugin creates new pages; without it page creation fails silently at runtime

---

## Setup — First Time

### 1. Get the files
Download or clone the plugin folder from GitHub. All three files must be in the same directory.

### 2. Import into Figma
1. Open the **Figma desktop app** — local plugins do not work in the browser
2. Go to **Main Menu → Plugins → Development → Import plugin from manifest…**
3. Navigate to the plugin folder and select `manifest.json`
4. The plugin now appears under **Plugins → Development**

### 3. Run the plugin
1. Open or create a Figma file
2. **Plugins → Development → [your plugin name]**
3. A small panel appears with a button
4. Click **Generate** — the plugin builds the full deck on a new page

---

## The Build Workflow

```
1. Understand what slides are needed and what each one contains
2. Write code.js (one section per slide) and ui.html
3. Import from manifest.json → run in Figma → click Generate
4. Review output → fix any errors → re-run
5. Write image-prompts.md — one prompt per slide that needs an image
6. Generate images externally (Midjourney, Flux, etc.)
7. Place images into Figma by replacing the placeholder boxes the plugin created
8. Final check: does every image match the content on that slide?
```

---

## When There's an Error

Figma shows errors as a red notification bar at the bottom of the screen, or a message in the plugin panel.

**What to do:**
1. Note the exact error message
2. Fix `code.js` — the most common causes are argument order mistakes and font loading issues (see below)
3. Delete the page the plugin generated (so you're starting fresh)
4. Re-run the plugin

**Figma usually picks up changes to `code.js` automatically.** If it doesn't, re-import from manifest.

---

## The Most Common Errors

**"Expected value of type number, got object"**  
An argument is being passed in the wrong order to a helper function — something that should be a number is getting an object instead (or vice versa). The fix is checking which argument is wrong on the line the error points to.

**Font not working / text showing wrong**  
The font wasn't loaded before the text was created. All fonts need to be loaded at the very start of the plugin, before any slides are built. This is already handled in the working pattern — don't move font loading anywhere else.

**Plugin crashes silently / no output**  
A slide section has an error that's being swallowed. Check the Figma plugin dev console for details.

---

## Image Placeholders

The plugin creates placeholder rectangles with dashed borders and a label showing what image goes there. They're intentionally high-contrast so you can see exactly where each image sits.

**To place the final image:**
1. Select the placeholder rectangle in Figma
2. In the Fill panel on the right, click the fill and switch it to **Image**
3. Upload or select your generated image
4. Delete or hide the label text node above it

---

## Image Prompts

Keep an `image-prompts.md` file alongside the plugin. One entry per slide that needs an image.

**Each prompt must have:**
1. Camera and lens — stated first
2. Shot type and angle
3. What's in the scene — specific to that slide's content
4. Single light source
5. Atmosphere and mood
6. Constraint — no faces, no people, silhouette only, etc.

**The image must connect to the text on that slide** — not just the project theme in general.

Slides that need a real photo (not AI): mark them clearly as **REAL PHOTO — NOT AI**.

---

## Design Rules

These apply to every project, regardless of style:

- **Every slide needs a visual treatment.** Text on a plain dark background is not a finished slide.
- **Image placeholders must be visually obvious.** If the placeholder blends in, you won't know where the image goes.
- **Slide layouts should vary.** The same template on every slide reads as a document, not a presentation.
- **The image must match the text on that slide.** Check this after generating — it's easy to have a prompt that drifts from the slide content.
- **The placeholder label must match the image prompt.** If they diverge, you'll place the wrong image.

---

## Files to Keep and Version

| File | What It Is |
|------|------------|
| `manifest.json` | Plugin metadata |
| `code.js` | The plugin — all slide logic |
| `ui.html` | The plugin's button panel |
| `image-prompts.md` | One prompt per slide that needs an image |

**Version all of these in GitHub.** If you break a working build, you need to be able to roll back. Commit after every clean working run.

---

## Delivering to Someone Else

When sharing the plugin:
1. Push all files to GitHub
2. Send direct links to each file (not the folder — direct links to the files)
3. Instructions: "Download all three files into the same folder. In Figma desktop: Plugins → Development → Import plugin from manifest → select manifest.json → Run."
