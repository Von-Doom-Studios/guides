# Reference System — Pinterest to Prompt

This is how we generate high-quality, on-brand images for the Floki website. The process starts with visual research, not prompting — we find images that are already styled the way we want, then use those as the creative foundation.

---

## Why This System Exists

AI image generators produce generic results without direction. Feeding them a specific visual reference — composition, lighting, color mood, set design — produces images that feel intentional and editorial rather than stock.

---

## Step 1 — Find References on Pinterest

Search Pinterest for images that match the **mood and styling** you want, not necessarily the product itself.

**What to look for:**
- Editorial product photography (clean, considered composition)
- Lifestyle images with the right color temperature and set design
- Fashion or home decor images with styling that fits Floki's aesthetic

**Good search terms for Floki:**
- `minimal luxury home editorial`
- `lifestyle product photography wardrobe`
- `sneaker editorial flat lay`
- `african print home decor editorial`
- `capsule wardrobe photography`
- `luxury lifestyle product photography white background`

**Criteria for a good reference:**
- Lighting is clear and intentional (not muddy or mixed)
- Composition has breathing room
- Color palette is compatible with Floki brand (or intentionally contrasting)
- The styling feels premium — not mass market

---

## Step 2 — Build a Reference Folder

Save selected images into a local reference folder organized by product or campaign:

```
references/
├── hangers/
│   ├── ref-01.jpg
│   ├── ref-02.jpg
│   └── ref-03.jpg
├── pillows/
│   ├── ref-01.jpg
│   └── ref-02.jpg
└── sneaker-cases/
    ├── ref-01.jpg
    └── ref-02.jpg
```

**Naming:** Keep it simple — `ref-01.jpg`, `ref-02.jpg`. The folder name carries the context.

**How many references:** 3–6 per product or campaign. More than that and you lose focus.

---

## Step 3 — Analyze the Reference

Before writing a prompt, break down what makes the reference work:

| Element | What to Note |
|---|---|
| **Lighting** | Soft/hard, direction, warm/cool, single or split |
| **Background** | Color, texture, depth of field |
| **Composition** | Angle, framing, negative space |
| **Color palette** | Dominant tones, accent colors |
| **Mood** | Editorial, intimate, aspirational, minimal |
| **Set elements** | Props, surfaces, fabrics |

Write this down — even a few words per element. This becomes your prompt skeleton.

---

## Step 4 — Write the Prompt

Use the reference analysis to write a prompt that combines **Floki's product** with the **reference's styling**.

**Prompt structure:**
```
[Product description], [lighting from reference], [composition/angle from reference], 
[background/setting from reference], [mood/color palette from reference], 
editorial product photography, 4K --ar [ratio]
```

**Example — Hangers:**
Reference: editorial shot of minimal wardrobe, soft north light, hanging garments, warm neutral tones

```
luxury woven rope hangers in canary yellow, soft north window light, 
hanging in a minimal open wardrobe, warm cream and white tones, 
editorial lifestyle photography, 4K --ar 3:2
```

**Example — Pillows:**
Reference: African textile editorial, flat surface, strong side light, rich saturated colors, architectural framing

```
African print accent pillow with Ankara geometric pattern, 
strong directional side light, placed on a linen surface, 
rich warm tones with architectural framing, editorial home decor photography, 
4K --ar 1:1
```

**Example — Sneaker Cases:**
Reference: fashion accessory close-up, marble countertop, cool daylight, minimal props

```
transparent sneaker phone case with Jordan 1 print, 
cool diffused daylight, marble surface, one prop (black pen), 
fashion accessory editorial, minimal composition, 4K --ar 4:5
```

---

## Step 5 — Midjourney with Image Reference

If you're uploading the Pinterest image directly to Midjourney as a style reference:

1. Upload the reference image to the Midjourney prompt field
2. Use `--sref` (style reference) or paste the image URL at the start of the prompt
3. Adjust `--sw` (style weight) — start at 100, increase for stronger reference influence

```
[image URL] luxury woven rope hangers, editorial lifestyle photography --ar 3:2 --sw 100
```

---

## Step 6 — Review and Save

Before handing off any image:
- Does it match the brand's color palette? (see Style Guide)
- Is the quality good enough — no artifacts, distortions, or obvious AI errors?
- Does it look like something Floki would actually publish?

Save accepted images to `public/images/products/` using the naming convention in the Style Guide.

---

→ See [03-AI-DESIGN-WORKFLOW.md](./03-AI-DESIGN-WORKFLOW.md) for full prompting templates  
→ See [05-VIDEO-WORKFLOW.md](./05-VIDEO-WORKFLOW.md) for applying this same approach to video
