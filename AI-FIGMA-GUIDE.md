# Figma Plugin Development — AI Agent Reference

**Last updated:** April 16, 2026  
**Scope:** Process for building Figma presentations via custom local plugins

---

## Overview

A Figma local plugin generates an entire presentation programmatically. The agent writes `code.js`, which is imported and run inside the Figma desktop app. The plugin creates frames, text, shapes, and placeholders from scratch.

**Key constraint:** The plugin runs in Figma's sandbox. No DOM, no `fetch`, no Node.js APIs, no external image loading.

---

## Plugin File Structure

```
plugin-folder/
├── manifest.json
└── code.js
```

**manifest.json:**
```json
{
  "name": "Plugin Name",
  "id": "unique-string",
  "api": "1.0.0",
  "main": "code.js"
}
```

**code.js** has access to the `figma` global object only.

---

## Core API Reference

### Plugin entry point
```js
async function buildDeck() {
  // Load all fonts before any text operations
  await figma.loadFontAsync({ family: "Inter", style: "Regular" });
  await figma.loadFontAsync({ family: "Inter", style: "Bold" });

  // Build slides here

  figma.closePlugin();
}
buildDeck();
```

**Rule:** The main function must be `async`. All font loads must be awaited before any text node is created or modified.

---

### Create a frame (slide)
```js
const slide = figma.createFrame();
slide.resize(W, H);
slide.name = "01 — Slide Name";
slide.fills = [{ type: 'SOLID', color: { r: 0, g: 0, b: 0 } }];
figma.currentPage.appendChild(slide);
```

### Create a text node
```js
const txt = figma.createText();
txt.fontName = { family: "Inter", style: "Bold" };
txt.fontSize = 48;
txt.characters = "Heading text";
txt.fills = [{ type: 'SOLID', color: { r: 1, g: 1, b: 1 } }];
txt.x = 80;
txt.y = 120;
slide.appendChild(txt);
```

### Create a rectangle
```js
const rect = figma.createRectangle();
rect.resize(400, 300);
rect.x = 100;
rect.y = 200;
rect.fills = [{ type: 'SOLID', color: { r: 0.2, g: 0.2, b: 0.2 } }];
slide.appendChild(rect);
```

### Create an ellipse
```js
const ellipse = figma.createEllipse();
ellipse.resize(300, 300);
ellipse.x = 500;
ellipse.y = 100;
ellipse.fills = [{ type: 'SOLID', color: { r: 0.5, g: 0.2, b: 0.8 }, opacity: 0.2 }];
slide.appendChild(ellipse);
```

### Image placeholder pattern
```js
// Placeholder rectangle
const ph = figma.createRectangle();
ph.resize(placeholderW, placeholderH);
ph.x = placeholderX;
ph.y = placeholderY;
ph.fills = [{ type: 'SOLID', color: { r: 0.15, g: 0.15, b: 0.15 } }];
ph.strokes = [{ type: 'SOLID', color: { r: 0.8, g: 0.8, b: 0.8 } }];
ph.strokeWeight = 2;
ph.dashPattern = [8, 6];
slide.appendChild(ph);

// Label inside placeholder
const label = figma.createText();
label.fontName = { family: "Inter", style: "Regular" };
label.fontSize = 14;
label.characters = "[Image: description of what goes here]";
label.fills = [{ type: 'SOLID', color: { r: 0.8, g: 0.8, b: 0.8 } }];
label.x = ph.x + 16;
label.y = ph.y + placeholderH / 2 - 10;
slide.appendChild(label);
```

The placeholder label must exactly match the prompt in `image-prompts.md` for that slide.

---

## Common Type Errors

### "Expected value of type number, got object"
**Cause:** Argument order mismatch in a helper function — passing an object where a number is expected, or vice versa.

```js
// Helper defined as: addText(parent, content, x, y, fontSize)
// WRONG — passing width where content is expected
addText(slide, W * 0.5, "My text", 100, 48);

// CORRECT
addText(slide, "My text", 100, 200, 48);
```

**Prevention:** Before calling any helper, verify the argument order matches the function signature.

### "Font not loaded" / characters not setting
**Cause:** Setting `fontName` or `characters` before `loadFontAsync` resolves.

**Fix:** Load every font family + style combination used in the plugin at startup, before any slide creation.

### "Cannot read properties of undefined"
**Cause:** Referencing a node before it exists, or using the wrong variable name.

**Fix:** Check creation order — nodes must exist before being appended or modified.

---

## Slide Code Structure

Each slide follows this pattern:

```js
// --- Slide N: Name ---
const slideN = figma.createFrame();
slideN.resize(W, H);
slideN.name = "NN — Name";
figma.currentPage.appendChild(slideN);

// 1. Background
slideN.fills = [{ type: 'SOLID', color: { r: ..., g: ..., b: ... } }];

// 2. Structural shapes (panels, dividers, decorative elements)

// 3. Image placeholder (if this slide has an image)

// 4. Text content — headings, body, labels
```

---

## What the Plugin Can and Cannot Do

| Can Do | Cannot Do |
|--------|-----------|
| Create frames, text, rectangles, ellipses, lines | Load images from URLs into fills |
| Set solid and gradient fills | Apply blur effects (without advanced API usage) |
| Set font, size, weight, color, alignment | Read/write files |
| Set opacity, corner radius, stroke | Make network requests |
| Group and nest nodes | Use fonts not installed on the machine |

**Implication for images:** All image fills must be placed manually in Figma after the plugin runs. The plugin creates placeholder rectangles that the human replaces with real images.

---

## Image Prompt Standards

Every AI-generated image prompt must be written in this order:

1. **Camera + lens** — specific equipment (e.g., `ARRI Alexa 35 · Zeiss Master Prime 35mm`)
2. **Shot type and angle** — wide establishing, close-up, OTS, low angle, etc.
3. **Scene subject** — what's specifically in the frame, tied to the slide content
4. **Light source** — single source, where it comes from, what quality
5. **Atmosphere** — grain, color grade, mood
6. **Constraint** — `no faces`, `no people`, `silhouette only`, etc.

**The prompt must match the content of that specific slide — not the project in general.**

For slides requiring real photos (actors, real people, specific locations): mark explicitly as `REAL PHOTO — NOT AI`. Do not write an AI prompt for these.

---

## image-prompts.md Format

```markdown
## Slide 01 — [Slide Name]
**Aspect ratio:** [ratio]
**Placement:** [full bleed / left panel / right panel / etc.]
**Type:** AI generated / REAL PHOTO — NOT AI / No image needed

[Full prompt text here, or "N/A"]

---

## Slide 02 — [Slide Name]
...
```

---

## Testing and Iteration

```
1. Write code.js
2. In Figma: Plugins → Development → [plugin] → Run
3. Figma hot-reloads code.js on re-run in most cases
4. If error: read the exact message → find the line → fix the type mismatch or load order
5. Delete the generated page before re-running to test clean
6. Use console.log() for debugging — output appears in Figma's plugin dev console
```

---

## Delivery Format

When delivering a plugin to a human:
1. Push `code.js`, `manifest.json`, and `image-prompts.md` to GitHub
2. Send a direct link to `code.js` on GitHub
3. Instructions: "Download `code.js`, replace the file in your plugin folder, re-import from `manifest.json` if needed, run."
4. Never paste code in Discord — always link to GitHub

---

## Versioning

After each working build:
```
git add code.js manifest.json image-prompts.md
git commit -m "figma: [what changed]"
git push
```

Name versions clearly in commit messages. A broken build can always be rolled back if the working version was committed.
