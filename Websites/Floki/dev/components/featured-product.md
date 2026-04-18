# Component: FeaturedProduct (`components/featured-product.tsx`)

The main product showcase on the home page — full gallery with color variants, lightbox, and add-to-cart.

---

## Gallery / Color Swatch Architecture — PERMANENT RULE

This is a critical rule that must never be violated:

| Data field | Purpose |
|---|---|
| `colorVariant.images[]` | Multi-angle shots for that color → drives gallery thumbnails + main image |
| `colorVariant.image` | Single swatch thumbnail shown in the color selector ONLY |
| `images` prop | Fallback gallery when no active color variant has `images[]` |

- Clicking a color swatch: sets `activeColor` + resets gallery index to 0
- Gallery thumbnails and color swatches are **always independent** — never share state

---

## Grid Layout — Locked Values

| Property | Value |
|---|---|
| Grid template | `76px 1fr minmax(0,578px)` |
| Column gap | 12px |
| Row gap | 16px (gap-y-4) |
| Gallery max size | 946×946px |
| Gallery background | #fafafa |
| Gallery aspect ratio | 1:1 |
| Info panel max-width | 578px |
| Info panel sticky top | 140px |
| Thumbnail size | 72×72px |
| Thumbnail scroll | up/down arrows when >4 images |

---

## Info Panel Typography — Locked Values

| Element | Size | Weight | Notes |
|---|---|---|---|
| "Featured" label | 15px | normal | no uppercase |
| Product title | clamp(30px→38px) | bold | |
| Price | 23px | semibold | |
| Color label / in-stock / description | 15px | normal | |
| Description | 20px | normal | |
| Add to Cart button | 15px | semibold | |
| Trust badge text | 15px | normal | |

---

## Lightbox — Locked Values

| Element | Value |
|---|---|
| All buttons | 63×63px, 1.5px solid #c9c9c9, white bg, no shadow |
| Arrow icons | 26×26px SVG, strokeWidth 1.5 |
| Close X icon | 23×23px SVG, strokeWidth 1.8 |
| Counter pill | Same border, height 63px, font 18px |
| Prev button position | left: 24px |
| Next + Close position | right: 24px |
| Open animation | 0.28s cubic-bezier(0.22,1,0.36,1) |

---

## Animations

| Animation | Duration | Easing |
|---|---|---|
| Slide in/out | 0.4s | ease-out |
| Lightbox open | 0.28s | cubic-bezier(0.22,1,0.36,1) |
| Images preloaded | on mount + color change | useEffect |

---

→ Back to [../README.md](../README.md)
