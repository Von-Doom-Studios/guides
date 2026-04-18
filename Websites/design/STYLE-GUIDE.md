# Floki Website — Style Guide

This is the single source of truth for all visual design decisions on the Floki website. All locked values here must be matched exactly in code.

---

## Brand Colors

| Name | Hex | Usage |
|---|---|---|
| Brand Red | `#EA183C` | Primary accent, footer background, body bg on shop page |
| Foreground | `#171717` | All body text, icons, dark UI |
| Background | `#FFFFFF` | Page background, nav, cards |
| Hero Dark 1 | `#1a1a1a` | Hero slide backgrounds |
| Hero Dark 2 | `#111111` | Carousel dark cards, All Products card |
| Hero Dark 3 | `#0d0d0d` | Deepest dark backgrounds |
| Footer Bottom Bar | `#c41533` | 100px bottom section of footer |

---

## Typography

**Font Family:** Inter (all weights)

| Element | Size | Weight | Notes |
|---|---|---|---|
| Hero headline | clamp(3rem, 5.5vw, 4.5rem) | 800 | Uppercase |
| Shop page H1 | clamp(4rem, 10vw, 8rem) | 800 | Not uppercase |
| "Curating the extraordinary" | clamp(3rem, 5.5vw, 4.5rem) | 800 | Not uppercase |
| Body / blurb text | 24px | 400 | |
| Navbar links | 18px | 500 | |
| Announcement bar message | 15px | 500 | |
| Carousel panel headline | 30px | 700 | |
| Carousel panel subtitle | 15px | 500 | |
| Footer column headings | 20px | 700 | White |
| Footer nav links | 17px | normal | White, underline on hover |
| Footer contact email | 28px | 600 | Underlined |

---

## Pill Button Standard

All pill-style CTA buttons site-wide:

| Property | Value |
|---|---|
| Height | 60px |
| Padding | 28px left / 20px right |
| Border | 2px solid |
| Font size | 15px |
| Font weight | 600 (semibold) |
| Text transform | Uppercase |
| Letter spacing | 0.12em |
| Hover | Background fills (black or brand), text + arrow invert to white |

**Component:** `<PillButton>` — use this component for all pill buttons. Do not create custom pill buttons.

**Note:** PillButton text is NOT uppercase. Use sentence case or title case only.

---

## Circle Button Standard

All circular icon buttons site-wide (gallery arrows, lightbox, cart close, etc.):

| Property | Value |
|---|---|
| Size | 63×63px |
| Shape | 50% border-radius |
| Background | #FFFFFF |
| Border | 1.5px solid #c9c9c9 |
| Box shadow | None |
| Hover | rgba(0,0,0,0.05) background |
| Icon color | #171717 |
| Arrow icon | 22×22px, strokeWidth 1.5 |
| Close X icon | 21×21px, strokeWidth 1.8 |

---

## Spacing & Sizing

| Element | Value |
|---|---|
| Navbar height | 120px desktop |
| Navbar top corner radius | 28px |
| Announcement bar height | 56px |
| Hero slider height | 750px desktop / 620px tablet / 520px mobile |
| Hero slide border radius | 18px |
| Carousel panel width | clamp(280px, 30vw, 440px) |
| Carousel panel height | clamp(360px, 40vw, 560px) |
| Carousel panel border radius | 24px |
| Cart drawer width | 560px |
| Cart drawer left radius | 40px |
| Footer top padding | 56px |

---

## Animations

| Animation | Value |
|---|---|
| Primary easing | cubic-bezier(0.4, 0, 0.2, 1) |
| Hero slider transition | 900ms cubic-bezier(0.4, 0, 0.2, 1) |
| Hero auto-advance | Every 8 seconds |
| Carousel hover zoom | scale(1.15), 280ms |
| Shop dropdown open | 1.4s cubic-bezier(0.16,1,0.2,1), 0.15s delay |
| Shop dropdown close | 0.25s ease-in |
| Shop card stagger | 1s cubic-bezier(0.16,1,0.2,1), 90ms per card |

---

## Footer

| Property | Value |
|---|---|
| Background | #EA183C |
| Bottom bar | #c41533, 100px tall |
| Logo | /floki-logo-white.svg, 80px wide |
| Newsletter heading | clamp(2.125rem, 2.5rem) |
| Email field | #f85261 background, border-radius 10px, no border, white placeholder |
| Social icons | 24px, white |
| Separator | 1px, rgba(255,255,255,0.25), vertical desktop / horizontal mobile |

---

## Asset Naming Convention

Product images in `public/images/products/`:
```
[color]-[product]-[number].jpg
```
Examples:
- `yellow-hanger-2.jpg`
- `PillowCover_Nala.jpg`
- `Sneaker_Case_red-white-black.jpg`

---

→ See [AI Design Workflow](./AI-DESIGN-WORKFLOW.md) for generating new assets
