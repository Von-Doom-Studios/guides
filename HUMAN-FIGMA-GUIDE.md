# Figma Plugin Guide — How to Build a Deck in Figma with a Plugin

**Last updated:** April 16, 2026  
**What this covers:** The process of building a Figma presentation using a custom plugin

---

## What This Process Is

You write a plugin in JavaScript (`code.js`) that builds an entire presentation inside Figma automatically — slides, text, layouts, colors, shapes, image placeholders. You import it as a local plugin and run it once. The plugin creates everything from scratch.

This is faster and more reproducible than building slides manually. Every change is made in code and re-run.

---

## What You Need

Two files in the same folder on your computer:
- `manifest.json` — tells Figma the plugin name and where the code lives
- `code.js` — the plugin logic that builds the deck

The folder can be named anything.

---

## Setup — First Time

### 1. Create the manifest
Minimum `manifest.json`:
```json
{
  "name": "Your Plugin Name",
  "id": "any-unique-string",
  "api": "1.0.0",
  "main": "code.js"
}
```

### 2. Import into Figma
1. Open the **Figma desktop app** (required — local plugins don't work in browser)
2. Go to **Main Menu → Plugins → Development → Import plugin from manifest…**
3. Select your `manifest.json`
4. Plugin now appears under **Plugins → Development**

### 3. Run the plugin
1. Open or create a Figma file
2. **Plugins → Development → [your plugin name]**
3. Click Run — it builds the deck automatically

---

## The Build Workflow

```
1. Brief: understand what slides are needed and what each one contains
2. Write code.js — one section per slide
3. Import from manifest.json → run in Figma
4. Review output → fix bugs → re-run
5. Write image-prompts.md with a prompt for every slide that needs an image
6. Generate images externally (Midjourney, Flux, etc.)
7. Place images into Figma manually by replacing the placeholders the plugin created
8. Final check: does every image connect to the content on that slide?
```

---

## When the Plugin Has a Bug

Figma shows errors as a red bar or console message. Common ones:

**"Expected value of type number, got object"**
- You passed an object where a number was expected, or mixed up argument order in a helper function
- Fix: check the exact line, verify argument types match the function signature

**"Cannot read properties of undefined"**
- You referenced a node or variable before it was created
- Fix: check the order of operations in your code

**"Font not loaded"**
- You tried to set text before loading the font
- Fix: always `await figma.loadFontAsync(...)` before setting `fontName` or `characters`

**Re-running after a fix:**
Figma usually hot-reloads `code.js` — just click Run again. If it doesn't pick up changes, re-import from manifest. Delete the previously generated page before re-running to start clean.

---

## Image Placeholders

The plugin can't insert real images. Instead, create placeholder rectangles with:
- A contrasting border so they're visually obvious
- A label inside describing exactly what image goes there

When you generate the final images, replace them manually in Figma:
1. Select the placeholder rectangle
2. In the Fill panel, swap the solid fill for an image fill
3. Delete or hide the label text

---

## Image Prompts Document

Keep a separate `image-prompts.md` alongside your plugin files. One prompt per slide that needs an image.

**Each prompt must include:**
1. Camera and lens (leads the prompt)
2. Camera angle and composition
3. Scene subject — specific to what's on that slide, not generic
4. Single light source (where it comes from)
5. Atmosphere / mood
6. Constraint (no faces, no people, silhouette only, etc.)

**The prompt must match the text on the slide.** If the slide is about a specific character or moment, the image should reflect that — not something tangentially related.

**Also flag clearly:**
- Slides that need a real photo (not AI-generated) — mark them as `REAL PHOTO — NO AI`
- Slides that need no image at all

---

## Design Rules (Process, Not Style)

These apply regardless of the project:

- **Every slide needs a visual treatment.** A slide that is just background + text with no color, shape, or image is not finished.
- **Image placeholders must be visually distinct.** If the placeholder blends into the background, you won't know where the image goes.
- **Slides should vary in layout.** Using the same template for every slide reads as a document, not a presentation.
- **The image must connect to the text on that specific slide.** Don't reuse a thematically related image across slides where it doesn't fit the content.
- **Placeholder labels must match the image prompts.** If they diverge, you'll place the wrong image.

---

## Files to Keep and Version

| File | What It Is |
|------|------------|
| `manifest.json` | Plugin metadata |
| `code.js` | The plugin — all slide logic |
| `image-prompts.md` | One prompt per slide that needs an image |

Version all of these in GitHub. If you break a working build with edits, you need the last good version.

**Commit after every working build:**
```
git add manifest.json code.js image-prompts.md
git commit -m "figma: working build — [brief description]"
git push
```
