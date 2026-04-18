# Component: Shop Page (`app/shop/page-client.tsx`)

The product listing page — used for `/shop` and all `/collections/[slug]` pages.

---

## Props

| Prop | Type | Default | Description |
|---|---|---|---|
| `initialProducts` | Product[] | — | Pre-fetched product list from Shopify |
| `defaultCategory` | string | "all" | Pre-selected category filter |
| `heroTitle` | string | "All products" | Title shown in hero and breadcrumb |
| `heroImage` | string | (forest green hanger) | Background image URL for hero |

---

## Categories

Defined in `CATEGORIES` constant:

| Label | Value (matches `product.category`) |
|---|---|
| Hangers | `"Hangers"` |
| African Pillows | `"African Pillows"` |
| Cases | `"Cases"` |

---

## Collection Pages

Each `/collections/[slug]` page maps to a config in `app/collections/[slug]/page.tsx`:

| Slug | Title | Category | Hero Image |
|---|---|---|---|
| `hangers` | Woven Hangers | Hangers | yellow-hanger-2.jpg |
| `pillows` | African Pillows | African Pillows | PillowCover_Nala.jpg |
| `sneaker-cases` | Sneaker Cases | Cases | Sneaker_Case_red-white-black.jpg |
| `all` | All Products | all | (Shopify CDN forest green hanger) |

To add a new collection: add an entry to `COLLECTION_CONFIG` in `app/collections/[slug]/page.tsx`.

---

## Body Background

On the shop page, `body` background is set to `#EA183C` (brand red) via a `<style>` tag in the component. This shows through the transparent hero area.

---

## Filter Toolbar — Locked Values

| Property | Value |
|---|---|
| Height | 80px |
| Button height | 60px |
| Button width | 180px |
| Button border | 2px solid #1a1a1a |
| Button border radius | 40px |
| Font size | 15px, weight 600 |
| No uppercase on buttons | confirmed |

---

## Product Grid

| Breakpoint | Columns |
|---|---|
| Desktop (>1200px) | 4 |
| Tablet (768–1200px) | 3 |
| Mobile (<768px) | 2 |

Grid gap: 32px

---

→ Back to [../README.md](../README.md)
