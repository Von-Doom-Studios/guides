# Component: Header (`components/header.tsx`)

The sticky navigation bar at the top of every page.

---

## Features

- **Sticky** — stays at the top on scroll
- **Transparent hero mode** — on the `/shop` route before scrolling, the nav is transparent with white text/logo
- **Shop dropdown** — hover "Shop" to open the category panel
- **Explore dropdown** — hover "Explore" to open the page links panel
- **Cart button** — opens the cart drawer
- **Mobile menu** — hamburger nav for small screens

---

## Props

| Prop | Type | Default | Description |
|---|---|---|---|
| `cartCount` | number | 0 | Number shown on cart icon badge |
| `onCartOpen` | function | — | Called when cart button is clicked |

---

## Shop Dropdown — Locked Values

| Property | Value |
|---|---|
| Card height | 496px |
| Card gap | 26px |
| Side/bottom padding | 60px |
| Top padding | 0 |
| Card border radius | 16px (via `clip-path`) |
| Drop animation (open) | `1.4s cubic-bezier(0.16,1,0.2,1) 0.15s` |
| Drop animation (close) | `0.25s ease-in` |
| Card stagger animation | `1s cubic-bezier(0.16,1,0.2,1)` — staggered left to right |
| Image hover zoom | `scale(1.075)` — 280ms |
| Title font size | 30px, weight 800 |
| Supporting text font size | 16px, weight 400 |

## Explore Dropdown — Locked Values (commit fe55338)

| Property | Value |
|---|---|
| Width | 252px |
| Border radius | 18px (bottom corners only) |
| Padding | 28px top/bottom, 22px gap between links |
| Animation | fade + translateY, 0.22s ease |
| Link font size | 14px, medium weight |

---

## Transparent Hero Logic

- `usePathname()` detects `/shop`
- `heroPage = pathname === "/shop"`
- When `heroPage && !scrolled && !shopOpen && !exploreOpen`: header transparent, logo white, nav links white
- When scrolled OR dropdown open: header white, logo primary, nav links dark

**Critical:** Never wrap `AnnouncementBar` + `Header` in a `div` with `position: relative` — breaks sticky positioning.

---

→ Back to [../README.md](../README.md)
