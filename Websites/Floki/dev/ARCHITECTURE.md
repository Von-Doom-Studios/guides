# Architecture

How the Floki website codebase is structured and how data flows through it.

---

## Folder Structure

```
Floki-Website/
├── app/                        # Next.js App Router pages
│   ├── layout.tsx              # Root layout — wraps every page (header, footer, cart)
│   ├── page.tsx                # Home page
│   ├── shop/
│   │   ├── page.tsx            # Fetches products server-side, passes to client
│   │   └── page-client.tsx     # Shop UI: hero, filter toolbar, product grid
│   ├── collections/
│   │   └── [slug]/page.tsx     # Dynamic collection pages (hangers, pillows, etc.)
│   ├── products/
│   │   └── [handle]/page.tsx   # Individual product detail page
│   ├── explore/page.tsx        # Our Story page
│   ├── faq/page.tsx
│   ├── contact/page.tsx
│   └── globals.css             # Global styles
│
├── components/                 # Reusable UI components
│   ├── header.tsx              # Sticky navbar, shop dropdown, explore dropdown
│   ├── announcement-bar.tsx    # Top bar with rotating messages
│   ├── hero-slider.tsx         # Home page carousel
│   ├── featured-product.tsx    # Product showcase with gallery + variants
│   ├── product-carousel.tsx    # Horizontal scroll carousel
│   ├── cart-drawer.tsx         # Slide-in cart panel
│   ├── pill-button.tsx         # Standard CTA button component
│   └── footer.tsx              # Footer with parallax effect
│
├── context/
│   └── cart-context.tsx        # Cart state — add, remove, update, checkout
│
├── lib/
│   └── shopify.ts              # Shopify Storefront API calls
│
├── public/
│   └── images/
│       └── products/           # Product images used on the site
│
└── .env.local                  # API keys (NOT committed to GitHub)
```

---

## Routing

Next.js App Router — each folder in `app/` is a route.

| Route | File |
|---|---|
| `/` | `app/page.tsx` |
| `/shop` | `app/shop/page.tsx` |
| `/collections/hangers` | `app/collections/[slug]/page.tsx` (slug = "hangers") |
| `/products/luxury-woven-hanger` | `app/products/[handle]/page.tsx` |

---

## Data Flow

```
Shopify Store
    ↓
lib/shopify.ts (Storefront API)
    ↓
Server Component (e.g. app/shop/page.tsx)
    ↓ passes data as props
Client Component (e.g. app/shop/page-client.tsx)
    ↓
UI rendered in browser
```

Products are fetched **server-side** at request time (no stale data). Cart state is managed **client-side** via React Context and persisted to `localStorage`.

---

## Key Patterns

### Server vs. Client Components

- Files without `"use client"` = Server Components (fetch data, no interactivity)
- Files with `"use client"` at the top = Client Components (useState, useEffect, event handlers)

### Styling Approach

- **Tailwind CSS** for utility classes (spacing, flex, grid, responsive)
- **Inline styles** for precise pixel values that must never drift (locked design values)
- **globals.css** for site-wide resets and custom CSS classes

### Locked Values

Certain pixel values in the codebase are **locked** — they must not be changed without explicit approval. These are documented in [../design/STYLE-GUIDE.md](../design/STYLE-GUIDE.md) and in each [component doc](./components/).

---

→ Next: [DEPLOYMENT.md](./DEPLOYMENT.md)
