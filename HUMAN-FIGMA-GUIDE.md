# Figma Plugin Guide — How to Build a Deck in Figma with a Plugin

**Last updated:** April 16, 2026  
**What this covers:** How to build a Figma presentation deck using a custom plugin (code.js + manifest.json)

---

## What This Process Is

You write a plugin in JavaScript (`code.js`) that builds an entire presentation inside Figma automatically — slides, text, layouts, colors, shapes, image placeholders. You import it as a local plugin and run it. The plugin creates everything from scratch.

This is how the 24 Tattoos pitch dossier was built.

---

## Setup — First Time Only

### 1. Get the plugin files
You need two files in the same folder on your computer:
- `manifest.json` — tells Figma the plugin name and where the code is
- `code.js` — the actual plugin logic

The folder can be named anything. Put it somewhere easy to find.

### 2. Import into Figma
1. Open Figma (desktop app, not browser — required for local plugins)
2. Go to **Main Menu → Plugins → Development → Import plugin from manifest…**
3. Navigate to your folder and select `manifest.json`
4. The plugin now appears under **Plugins → Development**

### 3. Run the plugin
1. Open a Figma file (or create a new one)
2. Go to **Plugins → Development → [your plugin name]**
3. Click Run — it builds everything automatically

---

## When the Plugin Has a Bug

This is the most common issue. Figma will show an error like:

```
Expected value of type "number", got "object"
```

or just a red error bar at the bottom of the screen.

**What to do:**
1. Note the exact error message
2. Fix `code.js` — the bug is almost always a mismatched data type (passing an object where a number is expected, or vice versa)
3. Re-import: **Plugins → Development → [your plugin] → Edit** — it usually hot-reloads automatically
4. If it doesn't, re-import from manifest again
5. Run again

**Common bugs that came up:**
- Passing `W*0.68` (a calculation result that's already a number) as content — happens when you confuse positional arguments in a helper function
- Passing an object `{x: ..., y: ...}` where the API expects a plain number
- Layout functions where `x` and `y` are swapped

---

## How the Code is Structured

The plugin typically has:
- **A size constant** — the slide dimensions (e.g., `const W = 1920; const H = 1080;`)
- **A slide creation function** — creates a frame for each slide
- **Slide-specific sections** — one block of code per slide that adds elements to it
- **Helper functions** — for text, shapes, image placeholders

**Slide order in the code = slide order in Figma.** If slide 4 in the code says "Synopsis" but you see something different in Figma, check what content you actually wrote into that slide's code block.

---

## Image Placeholders

Because you can't insert real images programmatically in Figma, the plugin creates placeholder boxes with:
- A colored border (e.g., gold dashed)
- A label inside (e.g., "Pierre cycling through rain-soaked Paris")
- Dimensions matching where the final image will sit

**These placeholders must match the actual image prompt.** If the placeholder says one thing and the prompt document says something else, there's a disconnect. Always keep them in sync.

### Placing real images later
1. Generate the image using Midjourney, Flux, or another tool
2. In Figma, select the placeholder box
3. Right-click → **Replace with image** (or use the Fill panel to swap the fill)
4. Delete or hide the label text

---

## Image Prompts Document

Keep a separate `image-prompts.md` file that lists every prompt, slide by slide. Format:

```
## Slide 04 — Synopsis
**Aspect ratio:** 16:9 horizontal
**Placement:** Full bleed background

ARRI Alexa 35 · Zeiss Master Prime 28mm — [scene description] — [camera angle] — [light source] — [atmosphere] — [no faces]
```

**Rules that matter:**
- Camera and lens go first — before the scene description
- Every prompt needs: camera angle, one clear light source, specific narrative detail tied to what's on that slide
- No character faces — hands, silhouettes, necks OK
- Slides with real actor photos: mark them explicitly as "REAL PHOTO — NOT AI"
- The prompt must connect to the text on that slide, not just the general story

---

## Design Constraints — What Figma Plugins Can and Can't Do

**Can do:**
- Create frames, text, rectangles, ellipses, lines
- Set fill colors (solid, gradients)
- Set font, size, weight, color, alignment
- Create groups and nested frames
- Set opacity and corner radius
- Add image fill placeholders (solid color fill with label)

**Cannot do:**
- Load external images from a URL into a fill
- Use blur effects or drop shadows without specific API calls
- Create complex vector shapes beyond basic geometry
- Import fonts that aren't already installed on the machine

**Implication:** If your design calls for blurred gradient orbs, the plugin can approximate them using overlapping ellipses with low opacity — but for the real effect, you need to place PNG assets manually after the plugin runs.

---

## Slide Design Rules (Learned from 24 Tattoos)

These are the things that make a deck look professional vs. amateur:

1. **No slide should have a pure black background with just text.** Every slide needs a visual treatment — color fill, gradient, atmospheric shape, or image.
2. **Full bleed slides** (cover, key emotional beats) need a background color or image fill approximated with a gradient. Label it clearly.
3. **Every slide should look different.** Same template on every slide = amateur. Use 4–6 distinct layout types.
4. **Image placeholders must be visually dominant.** A placeholder that blends into the background tells you nothing. Make it a contrasting color so you can see where the image will go.
5. **Text-only slides should still be visually intentional.** Use typographic scale, color accents, dividers.
6. **Match the image to the text on the slide.** The image on the synopsis slide should reflect the synopsis — not a random establishing shot.

---

## Full Workflow Summary

```
1. Design the deck on paper or in your head first — how many slides, what each one contains
2. Write code.js with one section per slide
3. Import from manifest.json into Figma desktop
4. Run — review output
5. Fix bugs → re-run (repeat until clean)
6. Update image-prompts.md to match every slide exactly
7. Generate images externally (Midjourney / Flux / etc.)
8. Place images into Figma manually by replacing placeholders
9. Final review: does every image match the text on that slide?
```

---

## Files to Keep

| File | What It Is |
|------|------------|
| `manifest.json` | Plugin metadata — don't modify unless renaming |
| `code.js` | The plugin — all the slide-building logic |
| `image-prompts.md` | Prompts for every AI-generated image, slide by slide |
| `visual-guide.md` | Color palette, typography, design system |

Version all of these in GitHub. If code.js produces a good result and you then break it with edits, you need the last working version.
