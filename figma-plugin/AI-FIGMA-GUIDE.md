# Figma Plugin Development — AI Agent Reference

**Last updated:** April 16, 2026  
**Scope:** Building Figma presentation decks via custom local plugins (code.js + manifest.json)  
**Source:** Lessons from building the 24 Tattoos pitch dossier (April 2026)

---

## Plugin Architecture

A Figma local plugin consists of two files in the same directory:

```
figma-plugin/
├── manifest.json    # Plugin metadata
└── code.js          # Plugin logic — runs in Figma's sandbox
```

**manifest.json minimum structure:**
```json
{
  "name": "Plugin Name",
  "id": "unique-id-string",
  "api": "1.0.0",
  "main": "code.js"
}
```

**code.js** runs in Figma's plugin sandbox. It has access to the `figma` global object. It does NOT have access to the DOM, `fetch`, `fs`, or any Node.js APIs.

---

## Figma Plugin API — Core Methods

### Create a frame (slide)
```js
const frame = figma.createFrame();
frame.resize(W, H);
frame.name = "01 — Cover";
frame.fills = [{ type: 'SOLID', color: { r: 0.08, g: 0.05, b: 0.04 } }];
figma.currentPage.appendChild(frame);
```

### Create a text node
```js
const txt = figma.createText();
await figma.loadFontAsync({ family: "Inter", style: "Bold" });
txt.fontName = { family: "Inter", style: "Bold" };
txt.fontSize = 48;
txt.characters = "Your text here";
txt.fills = [{ type: 'SOLID', color: { r: 1, g: 0.84, b: 0.39 } }];
txt.x = 80;
txt.y = 200;
frame.appendChild(txt);
```

**Critical:** `figma.loadFontAsync()` must be awaited before setting `fontName` or `characters`. The entire plugin must be wrapped in an `async` IIFE or the main function must be async.

### Create a rectangle
```js
const rect = figma.createRectangle();
rect.resize(W * 0.42, H);
rect.x = 0;
rect.y = 0;
rect.fills = [{ type: 'SOLID', color: { r: 0.12, g: 0.08, b: 0.06 } }];
frame.appendChild(rect);
```

### Create an ellipse (for orbs/atmosphere)
```js
const orb = figma.createEllipse();
orb.resize(600, 600);
orb.x = W - 500;
orb.y = -100;
orb.fills = [{ type: 'SOLID', color: { r: 0.83, g: 0.32, b: 0.04 }, opacity: 0.15 }];
frame.appendChild(orb);
```

### Create an image placeholder
```js
const ph = figma.createRectangle();
ph.resize(W * 0.42, H);
ph.x = 0;
ph.y = 0;
ph.fills = [{ type: 'SOLID', color: { r: 0.2, g: 0.12, b: 0.08 } }];
ph.strokes = [{ type: 'SOLID', color: { r: 0.83, g: 0.64, b: 0.24 } }];
ph.strokeWeight = 2;
ph.dashPattern = [8, 6];
// Add label
const label = figma.createText();
await figma.loadFontAsync({ family: "Inter", style: "Regular" });
label.characters = "[Image: Description of what goes here]";
label.fontSize = 14;
label.fills = [{ type: 'SOLID', color: { r: 0.83, g: 0.64, b: 0.24 } }];
label.x = ph.x + 20;
label.y = ph.y + H/2;
frame.appendChild(ph);
frame.appendChild(label);
```

---

## Common Type Errors — Critical

These bugs cause Figma to throw errors during plugin execution:

### Error: Expected number, got object
**Cause:** Passing an object `{x, y}` where a number is expected, or passing a calculation result into an argument that expects a coordinate pair.

**Example of the bug:**
```js
// WRONG — passing W*0.68 as the content argument
addText(frame, W*0.68, someText, 20, 200);

// CORRECT — W*0.68 is the width, not the content
addText(frame, someText, W*0.68, 20, 200);
```

**Prevention:** Always check the argument order of any helper function before calling it. If you define `function addText(parent, content, width, x, y)`, content comes before width.

### Error: Cannot set property on read-only object
**Cause:** Trying to set properties on a node after it's been closed or on a native object.

### Error: Font not loaded
**Cause:** Setting `fontName` or `characters` before `loadFontAsync` resolves.

**Prevention:** Load all fonts at the top of the plugin before any slide creation:
```js
async function buildDeck() {
  await figma.loadFontAsync({ family: "Playfair Display", style: "Bold" });
  await figma.loadFontAsync({ family: "Inter", style: "Regular" });
  await figma.loadFontAsync({ family: "Inter", style: "Bold" });
  // ... build slides
  figma.closePlugin();
}
buildDeck();
```

---

## Slide Structure Pattern

Each slide should follow this pattern:

```js
// Slide N — Name
const slideN = figma.createFrame();
slideN.resize(W, H);
slideN.name = "NN — Slide Name";
figma.currentPage.appendChild(slideN);

// 1. Background fill (never leave black)
slideN.fills = [{ type: 'SOLID', color: { r: ..., g: ..., b: ... } }];

// 2. Atmospheric shapes (orbs, panels, dividers)

// 3. Image placeholder (if this slide has an image)

// 4. Text content
```

**Rule: Every slide needs a non-black visual treatment.** A slide that is just dark + text is not a designed slide.

---

## Design System — 24 Tattoos Reference

**Slide dimensions:** 1920 × 1080px

**Color palette:**
| Name | Hex | RGB (0–1) |
|------|-----|-----------|
| Background dark | #140D0A | r:0.08, g:0.05, b:0.04 |
| Warm brown mid | #1E120C | r:0.12, g:0.07, b:0.05 |
| Accent burnt orange | #D4520A | r:0.83, g:0.32, b:0.04 |
| Gold | #D4A43E | r:0.83, g:0.64, b:0.24 |
| UV purple | #7B2DFF | r:0.48, g:0.18, b:1.0 |
| Text white | #F5F0E8 | r:0.96, g:0.94, b:0.91 |
| Text grey | #8A8178 | r:0.54, g:0.51, b:0.47 |

**Typography:**
- Display headings: Playfair Display Bold
- Body / labels: Inter Regular / Medium
- Small metadata: Inter Regular, 12–14px, grey

**Layout patterns used:**
- Full bleed (cover, key emotional slides): background fills entire frame
- Two-column (character slides): left 42% = image/portrait zone, right 58% = text
- Text-dominant: large typographic statement + atmospheric orbs
- Grid (market / comparable): 2×2 or 3×2 card layout

**Orb system:** Overlapping ellipses with 10–20% opacity, burnt orange or UV purple, placed off-frame (x < 0 or x > W) to bleed into the edge.

**Dash mark:** 30px horizontal line, gold color, top-left corner of every slide at y=40.

**Bottom bar:** Full-width rectangle, 48px height at y = H-48, dark fill, with text: `01 ——— TITLE · Subtitle`

---

## Image Prompt Standards

Every AI-generated image prompt must include, in this order:
1. **Camera + lens** — `ARRI Alexa 35 · Zeiss Master Prime [focal length]mm`
2. **Camera angle** — low angle, OTS, wide establishing, extreme close-up, etc.
3. **Scene subject** — specific to the slide content, NOT generic
4. **Single light source** — where it comes from, what quality
5. **Atmosphere** — grain, color grade, mood
6. **Constraint** — `no faces visible` / `no people` / `silhouette only`

**Bad prompt:**
> "A cyclist in Paris at night, cinematic, moody"

**Good prompt:**
> "ARRI Alexa 35 · Zeiss Master Prime 28mm — wide establishing shot from behind, lone cyclist seen from low angle on rain-slicked Rue de Rivoli, single sodium streetlamp casting warm amber shadow forward, rear Uber Eats bag barely visible, Parisian Haussman facades dark on both sides, grain-heavy night photography look, no face visible"

**Prompt-to-slide alignment rule:** The image prompt must connect to the TEXT on that specific slide, not just the general story. A slide about the synopsis needs an image that represents the mystery/central premise — not Pierre's bicycle because he's a cyclist.

---

## Placeholder ↔ Prompt Consistency

If the plugin creates a placeholder labeled `"Pierre cycling through rain-soaked Paris"`, the corresponding entry in `image-prompts.md` for that slide MUST describe that same scene. Mismatches cause confusion when placing final images.

Audit process:
1. Export or screenshot every slide from Figma
2. Read each placeholder label
3. Cross-reference against `image-prompts.md`
4. Any mismatch = fix both (or fix whichever is wrong)

---

## What the Plugin Cannot Do

| Limitation | Implication |
|-----------|-------------|
| Cannot load images from URLs | All image fills must be placed manually after plugin runs |
| Cannot use Figma blur API in basic builds | Blurred orbs require PNG assets placed manually |
| No network access (`fetch` blocked) | All data must be hardcoded into `code.js` |
| No file system access | Cannot read/write local files |
| Font must be loaded before use | Load all fonts at plugin startup |

---

## Testing Workflow

```
1. Edit code.js locally
2. In Figma: Plugins → Development → [plugin] → Run
   (Figma hot-reloads code.js changes automatically in most cases)
3. If error: read the exact message, identify the line, fix the type
4. If layout is wrong: add console.log statements — output appears in Figma's dev console
5. If fonts not rendering: confirm loadFontAsync is called for that exact family + style combo
6. Delete the generated page and re-run to test from scratch
```

---

## File Versioning

Always version `code.js` in GitHub. After each working build:
```
git add figma-plugin/code.js figma-plugin/image-prompts.md
git commit -m "figma: working v3 — visual treatments complete"
git push
```

Name versions clearly: v1, v2, v3 — or use git branches for major experiments. A working plugin that gets broken by edits can always be restored from git.

---

## Delivery

When delivering a plugin to a human:
1. Push the final `code.js` and `manifest.json` to GitHub
2. Link directly to the raw file (not the repo root)
3. Include instruction: "Download `code.js`, replace the one in your `figma-plugin-v3/` folder, re-import from manifest.json, run."
4. Do NOT paste the code in Discord — link to GitHub

Link format:
```
https://github.com/Von-Doom-Studios/[repo]/blob/main/figma-plugin-v3/code.js
```
