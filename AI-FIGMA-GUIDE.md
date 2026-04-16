# Figma Plugin Development — AI Agent Reference

**Last updated:** April 16, 2026  
**Scope:** Process for building Figma presentations via custom local plugins  
**Based on:** The working v3 plugin from the 24 Tattoos dossier build

---

## Overview

A Figma local plugin generates an entire presentation programmatically. The agent writes `code.js` and `ui.html`, which are imported and run inside the Figma desktop app. The plugin creates frames, text, shapes, and placeholders from scratch.

**Key constraint:** The plugin runs in Figma's sandbox. No DOM, no `fetch`, no Node.js APIs, no external image loading.

---

## Plugin File Structure

```
plugin-folder/
├── manifest.json
├── code.js
└── ui.html
```

**manifest.json:**
```json
{
  "name": "Plugin Name",
  "id": "unique-string",
  "api": "1.0.0",
  "main": "code.js",
  "ui": "ui.html",
  "editorType": ["figma"]
}
```

> **Required:** `editorType` must be present or Figma will refuse to import the plugin. Use `["figma"]` for standard Figma files. Other valid values: `"figjam"`, `"dev"`, `"slides"`, `"buzz"` — combine as needed, e.g. `["figma", "figjam"]`.

---

## The UI-Based Pattern (What Actually Worked)

The working plugin uses a UI panel with a button to trigger generation — not a headless run. This avoids timing issues with font loading and gives the user a clear control point.

**ui.html** (minimal working version):
```html
<!DOCTYPE html>
<html>
<head>
  <style>
    body { font-family: sans-serif; padding: 20px; }
    .btn { width: 100%; padding: 10px; cursor: pointer; }
  </style>
</head>
<body>
  <button class="btn" onclick="parent.postMessage({pluginMessage:{type:'generate'}},'*')">
    Generate Deck
  </button>
</body>
</html>
```

**code.js entry point:**
```js
figma.showUI(__html__, { width: 300, height: 200 });

figma.ui.onmessage = async function(msg) {
  if (msg.type !== 'generate') return;

  // 1. Load all fonts first
  // 2. Create a new page
  // 3. Build slides
  // 4. Zoom to fit
  // 5. Close plugin

  figma.closePlugin();
};
```

---

## Font Loading — The Pattern That Works

Load all fonts at the start, before any slides are created. Use a loop with try/catch so that unavailable fonts are skipped gracefully instead of crashing the plugin.

```js
var fonts = [
  { family: 'Playfair Display', style: 'Bold' },
  { family: 'Playfair Display', style: 'Bold Italic' },
  { family: 'Playfair Display', style: 'Regular' },
  { family: 'Inter', style: 'Regular' },
  { family: 'Inter', style: 'Medium' },
  { family: 'Inter', style: 'Bold' },
];

for (var i = 0; i < fonts.length; i++) {
  try {
    await figma.loadFontAsync(fonts[i]);
  } catch(e) {
    console.warn('Font skipped:', fonts[i].family, fonts[i].style);
  }
}
```

**Why try/catch:** If a font isn't installed on the machine, `loadFontAsync` throws. Without the catch, the entire plugin crashes. With it, the plugin continues and falls back gracefully.

---

## Page Creation

Create a new page rather than working on the current one. This prevents accidentally overwriting existing work.

```js
var page = figma.createPage();
page.name = 'Deck Name v1';
await figma.setCurrentPageAsync(page);
```

---

## Builder Class Pattern

The working plugin used a Builder class with prototype methods. This keeps slide code clean and avoids repeating low-level API calls.

```js
var W = 1920, H = 1080, GAP = 100, M = 80;

function B(page) {
  this.page = page;
  this.idx = 0;
}

// Create a slide frame
B.prototype.frame = function(name, bg) {
  var f = figma.createFrame();
  f.name = name;
  f.resize(W, H);
  f.x = this.idx * (W + GAP);  // space slides horizontally
  f.y = 0;
  f.fills = [{ type: 'SOLID', color: bg || { r: 0, g: 0, b: 0 } }];
  f.clipsContent = true;
  this.page.appendChild(f);
  this.idx++;
  return f;
};

// Create a rectangle
B.prototype.rect = function(f, x, y, w, h, col, opacity) {
  var r = figma.createRectangle();
  r.x = x; r.y = y;
  r.resize(Math.max(w, 1), Math.max(h, 1));  // Math.max prevents zero-size errors
  r.fills = [{ type: 'SOLID', color: col, opacity: opacity !== undefined ? opacity : 1 }];
  r.strokes = [];
  f.appendChild(r);
  return r;
};

// Create a text node — defensive pattern
B.prototype.txt = function(f, content, x, y, w, h, opts) {
  opts = opts || {};
  var t = figma.createText();
  t.x = x; t.y = y;
  t.resize(w, h);
  t.textAutoResize = 'HEIGHT';

  // Font selection
  var family = opts.font === 'display' ? 'Playfair Display'
             : opts.font === 'mono'    ? 'Roboto Mono'
             : 'Inter';
  var style = opts.bold ? 'Bold' : 'Regular';
  try {
    t.fontName = { family: family, style: style };
  } catch(e) {
    try { t.fontName = { family: 'Inter', style: 'Regular' }; } catch(e2) {}
  }

  t.fontSize = opts.size || 24;
  t.fills = [{ type: 'SOLID', color: opts.color || { r: 1, g: 1, b: 1 } }];
  t.textAlignHorizontal = opts.align || 'LEFT';

  // Set characters last — always wrap in try/catch
  try {
    t.characters = content;
  } catch(e) {
    try { t.characters = ''; } catch(e2) {}
  }

  f.appendChild(t);
  return t;
};

// Image placeholder — dashed border, labeled clearly
B.prototype.img = function(f, x, y, w, h, label) {
  var bg = figma.createRectangle();
  bg.x = x; bg.y = y;
  bg.resize(w, h);
  bg.fills = [{ type: 'SOLID', color: { r: 0.12, g: 0.10, b: 0.08 } }];
  bg.strokes = [{ type: 'SOLID', color: { r: 0.8, g: 0.7, b: 0.4 } }];
  bg.strokeWeight = 3;
  bg.dashPattern = [16, 8];
  f.appendChild(bg);
  this.txt(f, '[ ' + label + ' ]', x + 20, y + h / 2 - 12, w - 40, 28,
    { size: 16, color: { r: 0.8, g: 0.7, b: 0.4 } });
  return bg;
};
```

**Usage per slide:**
```js
var b = new B(page);
b.s01_cover();
b.s02_intro();
// etc.
```

---

## Viewport — Zoom to Fit at the End

```js
figma.viewport.scrollAndZoomIntoView(page.children);
```

Call this after all slides are built so Figma shows the full deck on completion.

---

## Error Handling — Wrap the Build

Wrap the entire build in a try/catch so Figma displays a readable error instead of silently failing:

```js
try {
  var b = new B(page);
  b.s01_cover();
  // ... all slides
  figma.viewport.scrollAndZoomIntoView(page.children);
  figma.notify('Done — N frames');
} catch(err) {
  figma.notify('Error: ' + err.message, { error: true, timeout: 12000 });
  console.error(err);
}
figma.closePlugin();
```

---

## Common Type Errors

### "Expected value of type number, got object"
**Cause:** Argument order mismatch in a helper function.

```js
// Helper: rect(f, x, y, w, h, col)
// WRONG — passing col where x is expected
b.rect(frame, COL.gold, 0, 400, 100);

// CORRECT
b.rect(frame, 0, 0, 400, 100, COL.gold);
```

**Prevention:** Before calling any helper, check the argument order matches the function signature. This was the most common error in the 24 Tattoos build.

### "Font not loaded" / characters silently empty
**Cause:** `t.characters` set before `loadFontAsync` resolves, or font not installed.

**Prevention:**
- Load all fonts at plugin startup in a loop with try/catch
- Always set `t.characters` last, after `fontName` and `fontSize`
- Wrap `t.characters` assignment in try/catch

### "Cannot read properties of undefined"
**Cause:** Referencing a variable or node before it exists.

**Prevention:** Check creation order — create before referencing.

### Zero-size frame error
**Cause:** Passing 0 as width or height to `resize()`.

**Prevention:** Use `Math.max(value, 1)` on any dimension that could be zero.

---

## What the Plugin Can and Cannot Do

| Can Do | Cannot Do |
|--------|-----------|
| Create frames, text, rectangles, ellipses | Load images from URLs |
| Solid fills, gradient fills | Apply blur effects (basic API) |
| Radial gradient fills (for orb effects) | Read/write files |
| Set font, size, weight, color, alignment | Make network requests |
| Set opacity, corner radius, stroke, dash pattern | Use fonts not installed on the machine |
| Create a new page and set it as current | |
| Group nodes | |

**Implication for images:** All image fills must be placed manually in Figma after the plugin runs. The plugin creates placeholder rectangles.

---

## Full Working Plugin Structure

```js
figma.showUI(__html__, { width: 300, height: 200 });

figma.ui.onmessage = async function(msg) {
  if (msg.type !== 'generate') return;
  figma.notify('Loading fonts…');

  // Step 1: Load all fonts
  var fonts = [
    { family: 'Inter', style: 'Regular' },
    { family: 'Inter', style: 'Bold' },
    // add all fonts used
  ];
  for (var i = 0; i < fonts.length; i++) {
    try { await figma.loadFontAsync(fonts[i]); }
    catch(e) { console.warn('Font skipped:', fonts[i].family, fonts[i].style); }
  }

  figma.notify('Building deck…');

  // Step 2: Create a new page
  var page = figma.createPage();
  page.name = 'Deck Name';
  await figma.setCurrentPageAsync(page);

  // Step 3: Build slides
  try {
    var b = new B(page);
    b.s01();
    b.s02();
    // ... all slides

    // Step 4: Zoom to fit
    figma.viewport.scrollAndZoomIntoView(page.children);
    figma.notify('Done');
  } catch(err) {
    figma.notify('Error: ' + err.message, { error: true, timeout: 12000 });
    console.error(err);
  }

  figma.closePlugin();
};

// Builder class and prototype methods here
```

---

## Image Prompt Standards

Every AI-generated image prompt must be written in this order:

1. **Camera + lens** — specific equipment (e.g., `ARRI Alexa 35 · Zeiss Master Prime 35mm`)
2. **Shot type and angle** — wide establishing, close-up, OTS, low angle, etc.
3. **Scene subject** — specific to the slide content, not the project in general
4. **Light source** — single source, where it comes from, what quality
5. **Atmosphere** — grain, color grade, mood
6. **Constraint** — `no faces`, `no people`, `silhouette only`, etc.

The prompt must match the content of that specific slide. For slides requiring real photos: mark as `REAL PHOTO — NOT AI`.

---

## image-prompts.md Format

```markdown
## Slide 01 — [Name]
**Aspect ratio:** 16:9
**Placement:** Full bleed / Left panel / Right panel
**Type:** AI generated / REAL PHOTO — NOT AI / No image needed

[Full prompt or N/A]
```

---

## Testing

```
1. Write/edit code.js
2. Figma: Plugins → Development → [plugin] → Run
3. Click the Generate button in the UI panel
4. Figma hot-reloads code.js on re-run in most cases
5. If error: read the exact message → find the line → fix type or load order
6. Delete the generated page before re-running to start clean
7. console.log() output appears in Figma's plugin dev console
```

---

## Delivery

1. Push `code.js`, `ui.html`, `manifest.json`, and `image-prompts.md` to GitHub
2. Send a direct link to each file
3. Instructions: "Download all three files into the same folder. In Figma desktop: Plugins → Development → Import plugin from manifest → select manifest.json → Run."
4. Never paste code in Discord — link to GitHub

---

## Versioning

```
git add code.js ui.html manifest.json image-prompts.md
git commit -m "figma: [what changed or what version]"
git push
```
