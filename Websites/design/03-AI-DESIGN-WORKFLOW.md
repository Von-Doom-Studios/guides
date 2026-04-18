# AI Design Workflow

How to use external generative AI tools to create images, copy, and design assets for the Floki website.

> For the full workflow including how to hand off assets to the dev agent, see [./ai-workflow/DESIGN-WORKFLOW.md](./ai-workflow/DESIGN-WORKFLOW.md).

---

## Tools We Use

| Tool | Purpose |
|---|---|
| **Midjourney** | Product and lifestyle photography |
| **DALL·E / ChatGPT** | Supplementary image generation |
| **Claude / ChatGPT** | Marketing copy, product descriptions |
| **Figma** | Brand assets, component mockups (Creative team) |

---

## Image Generation — Midjourney

### Product on White Background

```
[product description], white background, studio lighting, high resolution product photography, 4K --ar 1:1
```

Examples:
- `luxury woven rope hanger in canary yellow, white background, studio lighting, high resolution product photography, 4K --ar 1:1`
- `African print accent pillow with Ankara pattern, white background, soft natural light, 4K --ar 1:1`

### Lifestyle / Hero Images

```
[product] in [setting], editorial photography, soft natural light, minimal composition --ar 16:9
```

Examples:
- `luxury woven rope hangers in a minimalist walk-in wardrobe, editorial photography, soft natural light --ar 16:9`
- `sneaker phone case on a marble countertop, fashion lifestyle photography --ar 3:2`

---

## Copy Generation — Claude / ChatGPT

### Product Descriptions

```
Write a 2-sentence product description for [product name].
Brand voice: premium, confident, minimal. No filler phrases.
Target customer: style-conscious homeowner or fashion enthusiast, aged 25–45.
```

### Hero Slide Headlines

```
Write 3 short headline options for a hero slide featuring [product/theme].
Max 5 words each. Brand voice: luxury, editorial. No exclamation marks.
```

### Section Headings

```
Write a 3–5 word heading for a [section description].
Brand: Floki Brands — modern lifestyle. Tone: confident, minimal.
```

---

## Handing Off to the Agent

1. **Save images** to `public/images/products/` in the local repo, using the naming convention
2. **Tell VD-Dev in #dev:** "I've added [filename] to the products folder. Use it as the hero image for the hangers collection page."
3. **For copy:** paste the text in #dev and say where it goes

That's it — the agent handles all implementation.

---

## Design Review Process

1. Generate asset or copy with AI
2. Review it against the [Style Guide](./STYLE-GUIDE.md)
3. If it matches brand standards, hand off to agent
4. Agent implements and pushes
5. You pull and preview
6. Approve or iterate

---

→ Back to [STYLE-GUIDE.md](./STYLE-GUIDE.md)
