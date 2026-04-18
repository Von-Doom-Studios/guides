# Deployment

The Floki website is hosted on **Vercel** and deploys automatically from the `main` branch of the GitHub repo.

---

## How Deployment Works

```
Agent pushes code to GitHub (main branch)
    ↓
Vercel detects the push automatically
    ↓
Vercel builds the site (~1–2 minutes)
    ↓
Live site updates at floki-website.vercel.app
```

There is no manual deploy step. Every approved push goes live.

---

## Vercel Account

- **Plan:** Hobby (free) during development — upgrade to Pro ($20/month) before launch
- **Repo connected:** `Floki-Brands/Floki-Website`
- **Build command:** `next build` (set automatically)
- **Output directory:** `.next` (set automatically)

---

## Environment Variables

Set these in the Vercel dashboard under **Settings → Environment Variables**:

| Variable | Description |
|---|---|
| `SHOPIFY_STORE_DOMAIN` | Your Shopify store domain (e.g. `yourstore.myshopify.com`) |
| `SHOPIFY_STOREFRONT_ACCESS_TOKEN` | Public Storefront API token from Shopify admin |

These must also exist in `.env.local` for local development (not committed to GitHub).

---

## Custom Domain

When ready to go live on `flokibrands.com`:

1. Go to Vercel dashboard → project → **Domains**
2. Add `flokibrands.com` and `www.flokibrands.com`
3. Vercel provides DNS records — add them to your domain registrar
4. SSL certificate is provisioned automatically

---

## Preview Deployments

Every push to GitHub (even on non-main branches) creates a **preview URL** — a temporary link to that version of the site. Useful for reviewing changes without touching the live site.

---

## Limits (Hobby Plan)

| Limit | Value |
|---|---|
| Deployments per day | 100 |
| Build time per deploy | 45 minutes |
| Serverless function execution | Metered (covered by $0 free tier for low traffic) |

Upgrade to Pro before launch for unlimited deployments and team features.

---

→ Back to [README.md](./README.md)
