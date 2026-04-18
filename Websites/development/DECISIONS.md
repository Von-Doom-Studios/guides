# Design & Technical Decisions

A log of *why* things were built the way they were. Saves confusion when someone asks "why is this done like that?" six months later.

---

## Footer: Fixed Position with Parallax Scroll

**Decision:** The footer uses `position: fixed` at the bottom of the page. The white content wrapper scrolls over it.

**Why:** Creates a premium parallax reveal effect as the user scrolls — the footer appears to emerge from behind the content. This matches the high-end brand feel.

**Implementation note:** `marginBottom` on the content wrapper is set via DOM ref (not React state) to avoid scroll jump on resize. The outer wrapper does NOT have `overflow: hidden` so modals and overlays can escape it correctly.

---

## Shop Dropdown: Clip-Path Instead of overflow:hidden + border-radius

**Decision:** Shop nav dropdown cards use `clip-path: inset(0 round 16px)` instead of `border-radius` + `overflow: hidden`.

**Why:** `overflow: hidden` + `border-radius` + CSS `scale` transform causes dark rendering artifacts on the card edges in Chrome (GPU compositing issue). `clip-path` clips cleanly without the artifact.

---

## Product Images: `unoptimized` on Local Assets

**Decision:** Product images added locally use the `unoptimized` prop on Next.js `<Image>`.

**Why:** Next.js image optimization runs on the server. Local images not yet pushed to the CDN need `unoptimized` to render at full resolution in local dev.

---

## Shopify Storefront API (not Admin API)

**Decision:** All Shopify data is fetched via the public Storefront API.

**Why:** The Storefront API is designed for storefronts — it's public-safe, supports cart operations, and doesn't expose sensitive business data. The Admin API is overkill and a security risk for frontend use.

---

## Cart: localStorage Persistence

**Decision:** Cart state is persisted to `localStorage` on every change.

**Why:** Without persistence, refreshing the page empties the cart. LocalStorage keeps cart state across sessions without requiring a user account.

---

## Collection Pages: Shared ShopPageClient

**Decision:** `/collections/[slug]` pages reuse `ShopPageClient` from the shop page with props for `defaultCategory`, `heroTitle`, and `heroImage`.

**Why:** Avoids duplicating hundreds of lines of UI code. The collection pages are identical in structure to the shop page — only the hero content and pre-selected filter differ.

---

## Transparent Nav on Shop Page

**Decision:** The header and announcement bar are transparent (not red/white) when on the `/shop` route and the user hasn't scrolled.

**Why:** The shop page has a full-bleed hero image. A transparent nav lets the hero breathe. Once scrolled, the nav returns to white.

**Implementation note:** Never wrap `AnnouncementBar` + `Header` in a `div` with `position: relative` — it breaks sticky positioning.

---

## No Server-Side Cart

**Decision:** Cart is entirely client-side until checkout.

**Why:** Shopify Storefront API carts are session-based. We don't need a server-side cart — Shopify handles checkout state on their end once the user reaches the checkout URL.

---

→ Back to [README.md](./README.md)
