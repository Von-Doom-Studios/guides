# Video Workflow — Floki Website

How we create, source, and prepare video content for the Floki website.

---

## Where Video Is Used

| Location | Type | Format |
|---|---|---|
| Hero section | Looping background or product reel | MP4, autoplay, muted |
| Product pages | Product showcase / lifestyle clip | MP4, plays on click or scroll |
| Campaign sections | Mood/editorial clip | MP4 or WebM |

---

## Types of Video We Produce

### 1. AI-Generated Video (Runway / Kling / Luma)

Use for: hero backgrounds, mood clips, abstract lifestyle content where showing a real product isn't required.

**Tools:**
- **Runway Gen-3** — best for cinematic motion, lighting effects, abstract scenes
- **Kling** — strong for product and lifestyle motion, realistic movement
- **Luma Dream Machine** — good for object-focused motion

**Process:**
1. Follow the Reference System (see `04-REFERENCE-SYSTEM.md`) to find a reference clip or image
2. Use either an image-to-video or text-to-video prompt
3. Keep clips short — **4–6 seconds** for loops, **8–15 seconds** for showcase clips

**Prompt structure (text-to-video):**
```
[Scene description], [camera motion], [lighting], [mood], cinematic, 4K
```

Example:
```
luxury woven rope hangers swaying gently in a minimal wardrobe, 
slow push-in camera move, soft north window light, warm tones, 
cinematic lifestyle, 4K
```

**Image-to-video:**
- Use a strong Midjourney still as the starting frame
- Apply subtle motion — avoid fast cuts or chaotic movement for brand content
- Camera moves: slow push-in, gentle pan, slight zoom — nothing aggressive

---

### 2. Real Product Footage

Use for: product showcase on product pages, collection pages.

**Shot list per product:**
- 360° turntable or hand-held orbit
- Close-up texture/detail shot
- Lifestyle context shot (product in use or in environment)

**Capture specs:**
- Shoot in **4K minimum**
- Frame rate: **24fps** for cinematic feel, **60fps** if slow-motion is needed
- Lighting: match the style guide's editorial aesthetic — soft, directional, no harsh shadows

**Review before using:** apply the same reference analysis from `04-REFERENCE-SYSTEM.md` — does the lighting, color, and composition match the brand?

---

## File Specs for Web

| Property | Value |
|---|---|
| Format | MP4 (H.264 or H.265) |
| Resolution | 1920×1080 minimum for hero; 1280×720 acceptable for small sections |
| File size | Under 10MB for loops; under 25MB for showcase clips |
| Audio | Strip audio from all autoplay video |
| Compression | Use HandBrake or ffmpeg to compress before publishing |

**ffmpeg compression command:**
```bash
ffmpeg -i input.mp4 -vcodec h264 -acodec aac -crf 23 output.mp4
```

---

## Naming Convention

```
[section]-[product]-[type]-[number].mp4
```

Examples:
- `hero-hangers-loop-01.mp4`
- `product-pillows-showcase-01.mp4`
- `campaign-sneaker-mood-01.mp4`

---

## Handing Off to Dev

1. Compress and rename the file using the convention above
2. Drop it in the `public/videos/` folder in the repo
3. Post in #dev: "Added `[filename]` to `/public/videos/`. Use as [hero loop / product showcase / etc.] on [page]."

---

→ See [04-REFERENCE-SYSTEM.md](./04-REFERENCE-SYSTEM.md) for the reference-based approach that feeds into video prompts
