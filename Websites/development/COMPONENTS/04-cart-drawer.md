# Component: Cart Drawer (`components/cart-drawer.tsx`)

Slide-in cart panel, opened from the cart icon in the header.

---

## Props

| Prop | Type | Description |
|---|---|---|
| `open` | boolean | Whether the drawer is visible |
| `onClose` | function | Called when user closes the drawer |

---

## Layout — Locked Values

| Property | Value |
|---|---|
| Width | 560px max |
| Left corner radius | 40px (top and bottom left) |
| Horizontal padding | 50px |
| Vertical padding | 32px |
| Slide animation | `0.3s` (translate-x) |
| Close button | 63×63px circle, 1.5px solid #c9c9c9, no shadow |

---

## Empty Cart State

When cart is empty, shows:
- "Your cart is currently empty" (22px bold)
- Supporting text (15px)
- Three collection links styled as pill buttons

---

## Cart Context

Cart state is managed by `context/cart-context.tsx`. The drawer consumes:

- `lineItems` — array of cart items
- `cartTotal` — formatted total price
- `checkoutUrl` — Shopify hosted checkout URL
- `removeItem(lineId)` — removes an item
- `updateItemQuantity(lineId, quantity)` — updates quantity

---

## Status

Cart **add/remove/update** is wired to Shopify Storefront API. Checkout redirects to Shopify hosted checkout. Cart state persists in `localStorage`.

> **Note:** Cart functionality is connected but the Shopify mutations are pending full testing against a live store.

---

→ Back to [../README.md](../README.md)
