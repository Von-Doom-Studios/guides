# AI Design Workflow — Generating Site Content & Assets

This guide explains how to use external generative AI tools to create images, copy, and other content for the Floki website — and how to hand that off to the dev agent.

---

## Overview

The site needs several types of content that are generated or sourced externally:

| Content Type | Tool | Notes |
|---|---|---|
| Product photography | Real photography or AI (Midjourney, DALL·E) | Used in hero, carousel, collection pages |
| Hero background images | Midjourney or product photography | Must be high resolution (2000px+ wide) |
| Copy / marketing text | ChatGPT or Claude | Used in hero slides, product descriptions, About page |
| Brand assets (logos, icons) | Figma or Adobe | Managed separately by Creative team |

---

## Product Images

### File Requirements

- **Format:** JPG or PNG
- **Minimum size:** 1200×1200px (square products), 1200×1600px (tall products)
- **Background:** White or lifestyle setting (match existing product photos)
- **Naming convention:** `[color]-[product]-[number].jpg`
  - Examples: `yellow-hanger-2.jpg`, `PillowCover_Nala.jpg`, `Sneaker_Case_red-white-black.jpg`

### How to Add New Images

1. Add the image file to `public/images/products/` in the local repo
2. Tell the agent the filename
3. Agent references it in the code

### Generating with AI (Midjourney)

Good prompts for product images on white background:
```
luxury woven rope hanger, [color], white background, studio lighting, 4K, product photography --ar 1:1
```

For lifestyle shots:
```
luxury woven rope hanger hung in minimalist wardrobe, soft natural light, editorial style --ar 3:4
```

Always download at full resolution and rename according to the naming convention above.

---

## Hero Images

Hero images appear behind the large page titles on the shop and collection pages. They need:

- High contrast so white text is readable over them
- Landscape orientation (wider than tall)
- Dark subject matter or lifestyle context

The agent applies a 50% black overlay automatically — so the image doesn't need to be dark on its own.

---

## Marketing Copy

### Hero Slide Text

Each hero slide has a headline and a button. Keep headlines short and punchy:
- ✅ "Elevate Your Space"
- ✅ "Woven with Intention"
- ❌ "Our luxury woven rope hangers are crafted for those who appreciate fine living"

### Product Descriptions

Generated with Claude or ChatGPT. Pass the agent a description and it will update the Shopify product (if connected) or the site copy directly.

Template prompt for product copy:
```
Write a 2-sentence product description for [product name]. Brand voice: premium, confident, minimal. No filler phrases. Target customer: style-conscious homeowner aged 25–45.
```

---

## Handing Off to the Dev Agent

Once you have your asset or copy ready:

1. **Images:** Add to `public/images/products/` locally, then tell the agent the filename and where to use it
2. **Copy:** Paste the text directly into the Discord #dev channel and say where it goes
3. **Hero images:** Tell the agent the filename or URL and which page/section it's for

The agent handles all the implementation — you just provide the asset.

---

→ Back to [OVERVIEW.md](./OVERVIEW.md)
