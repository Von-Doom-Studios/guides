# 04 - Automation Stack: Floki Brands

Every tool needed to run Floki sales operations with maximum automation. For each tool: what it does, pricing, API availability, why it was chosen, and how it connects to the rest of the stack.

**Related files:** [06-PIPELINE.md](./06-PIPELINE.md) | [14-ANALYTICS-AND-REPORTING.md](./14-ANALYTICS-AND-REPORTING.md) | [07-OUTREACH-STRATEGY.md](./07-OUTREACH-STRATEGY.md)

---

## Stack Architecture: Data Flow

```
[Shopify] Orders + B2B Wholesale
    |
    v
[HubSpot CRM] - Contact synced, deal created automatically
    |
    v
[Klaviyo] - Post-purchase email flow triggered
    |
    v
[GA4 + Polar Analytics] - Session, conversion, revenue tracking
    |
    v
[QuickBooks Online] - Invoice synced, revenue recorded
    |
    (all connected via)
[Make.com Webhooks] - Orchestrates all API-to-API data flows
    |
    v
[Discord] - Automated weekly sales report posted to #sales channel
```

**Supporting layers:**
- Apollo.io: Cold outreach sequences feeding leads into HubSpot
- GitHub: Document/asset versioning (this repo)
- Visualping: Competitor website monitoring alerts
- Google Trends API: Market demand tracking

---

## 1. CRM and Pipeline Management

### HubSpot Free CRM

**What it does:** Central contact database for all 52+ prospects. Tracks email opens, link clicks, deal stages, and notes. Connects natively to Gmail (shopflokibrands@gmail.com) for automatic email logging.

**Pricing:** Free (up to 1,000 contacts, unlimited deals, email tracking)  
**API:** Yes - https://developers.hubspot.com/docs/api/overview  
**Why chosen:** Best free CRM with full API access, native Shopify integration, email open tracking, and deal pipeline. No credit card required. HubSpot's free tier is genuinely powerful, not crippled.

**Setup steps:**
1. Create account at hubspot.com (free)
2. Connect Gmail account for email sync
3. Import prospects CSV from [05-PROSPECTS.md](./05-PROSPECTS.md)
4. Set up pipeline stages matching [06-PIPELINE.md](./06-PIPELINE.md)
5. Install HubSpot Shopify app when store is live

**Connects to:** Shopify (native app), Klaviyo (via Make.com), Apollo.io (CSV/API sync), Gmail (native)

---

## 2. Cold Email and Outreach Automation

### Apollo.io

**What it does:** B2B database of 275M+ contacts and 65M+ companies. Find and verify emails and phone numbers for hotel procurement managers, STR operations leads, FF&E directors, and boutique retail buyers. Run automated multi-touch email sequences with personalization. Free tier includes 50 email credits/month and 2 sequences.

**Pricing:**
- Free: 50 email credits/month, 2 sequences
- Basic: $49/month - 1,000 credits, unlimited sequences, intent data
- Professional: $99/month - 2,000 credits + AI features

**API:** Yes - https://apolloio.github.io/apollo-api-docs/  
**Why chosen:** Best B2B prospecting database available. Competitors like ZoomInfo cost $15K+/year. Apollo has email sequence automation built in, so you do not need a separate tool for Phase 1. Also has LinkedIn integration for multi-channel outreach.

**Key use cases for Floki:**
- Find hotel procurement manager emails (company name + title search)
- Find STR management operations leads
- Find boutique retail buyer contacts
- Run automated 3-touch and 5-touch follow-up sequences
- Track open rates and reply rates by template

**Connects to:** HubSpot (native sync), Gmail, LinkedIn

### Alternative: Saleshandy

**What it does:** Cold email platform focused on deliverability. Unlimited email warm-up, email sequence automation, A/B testing built in.

**Pricing:** $25/month (Outreach Basic)  
**API:** Yes - https://help.saleshandy.com/en/articles/api  
**Why use instead of Apollo:** If you already have a prospect list and just need email automation without the database, Saleshandy at $25/mo is cheaper. But Apollo includes both the database and the sequencing, making it the better default.

---

## 3. Email Marketing and Flows

### Klaviyo

**What it does:** Email marketing platform with deep Shopify integration. Runs automated flows: abandoned cart recovery, welcome series for new DTC subscribers, post-purchase follow-up, and reorder reminders for B2B accounts. Also runs manual campaigns (product launches, promotions, new color drops).

**Pricing:**
- Free: Up to 250 contacts, 500 emails/month
- Email ($45/month): Up to 1,001 contacts, unlimited sends
- Email + SMS ($60/month): Adds SMS automation

**API:** Yes - https://developers.klaviyo.com/en  
**Why chosen:** Industry standard for DTC brands on Shopify. Native Shopify integration means order data flows automatically. Flows are visual and drag-and-drop. Owned audience (email list) is the most valuable long-term asset.

**Flows to build:**
1. Welcome series (3 emails, 7 days) - triggered when someone subscribes or buys DTC
2. Abandoned cart (3 emails, 48 hours) - triggered when cart is abandoned
3. Post-purchase (2 emails, Day 7 + Day 30) - review request + reorder prompt
4. B2B reorder reminder (1 email, Day 60) - triggered after B2B order ships
5. Win-back (2 emails, Day 90 + Day 120) - for lapsed customers

**Connects to:** Shopify (native), HubSpot (via Make.com webhook), GA4 (via UTM tracking)

---

## 4. E-commerce Platform

### Shopify

**What it does:** DTC storefront, product catalog, checkout, B2B wholesale portal. As of April 2026, Shopify's native B2B features (price lists, payment terms, company accounts, draft orders) are available to all merchants on any paid plan, not just Shopify Plus.

**Pricing:**
- Basic: $39/month - full B2B features included
- Shopify: $105/month - better reporting, staff accounts

**API:** Yes - https://shopify.dev/docs/api  
**Why chosen:** Already chosen. The April 2026 B2B feature expansion means Floki can run wholesale pricing, Net-30 payment terms, and customer-specific price lists without upgrading to Plus ($2,000+/month).

**B2B setup steps:**
1. Create a "Company" in Shopify admin for each wholesale account
2. Assign a price list matching channel (hotel, STR, retail, etc.)
3. Set payment terms (Net-30)
4. Share the B2B portal link with each wholesale buyer

**Connects to:** HubSpot (native app), Klaviyo (native app), QuickBooks (native app), GA4 (native), Faire (integration)

---

## 5. Analytics and Reporting

### Polar Analytics

**What it does:** Shopify-native analytics dashboard aggregating all revenue, acquisition, and retention data. Shows blended CAC, LTV, ROAS across channels, cohort analysis. Pulls from Shopify, Meta Ads, Google Ads, Klaviyo.

**Pricing:** $300/month (starts at lower revenue tiers)  
**API:** Yes - https://help.polaranalytics.co  
**Why chosen over Triple Whale:** Better Shopify-native integration and cleaner interface for non-technical users. Triple Whale is an alternative at similar pricing.

**Note for Phase 1:** Polar Analytics is overkill at zero revenue. Use it starting Phase 2 when DTC is live and ad spend begins. In Phase 1, use Shopify built-in analytics + GA4.

### Google Analytics 4

**What it does:** Website traffic, conversion funnel, user behavior, source attribution. Free. Essential from Day 1.

**Pricing:** Free  
**API:** Yes - https://developers.google.com/analytics/devguides/reporting/data/v1  
**Setup:** Add GA4 tag to Shopify via Google & YouTube app. Set up conversion events: purchase, add-to-cart, form-submission (for B2B inquiry form).

---

## 6. Competitor Intelligence

### Visualping

**What it does:** Monitors competitor websites for changes. Set it to watch Braiform, Hangers.com, and any other hotel hanger supplier's pricing/product pages. Alerts you via email when pages change.

**Pricing:** Free tier (5 monitors, daily checks) / Paid from $10/month  
**API:** Yes - https://visualping.io/docs  
**URL to monitor:** https://www.hangers.com/hotel-hangers, https://braiform.com, and any direct competitor product pages

### SimilarWeb

**What it does:** Traffic estimates for competitor websites. See where they get their traffic (organic, referral, paid), their top referring sites, and keyword rankings.

**Pricing:** Free (limited views, 5 results per report) / Paid from $125/month  
**Why:** Understand which channels competitors are investing in and identify gaps to exploit.

---

## 7. Market Research

### Google Trends (API via SerpAPI)

**What it does:** Track search volume trends for keywords like "luxury hangers," "hotel hangers bulk," "woven hangers wholesale." Identify seasonal demand spikes (Q4 holiday = spike in corporate gifting searches).

**Pricing:** SerpAPI from $50/month (500 searches). Direct Google Trends is free via web.  
**API:** Yes - https://serpapi.com/google-trends-api

### Exploding Topics

**What it does:** Identifies emerging trends before they peak. Useful for spotting new product categories (e.g., sustainable hangers, travel accessories).

**Pricing:** Free tier available / Pro from $39/month  
**URL:** https://explodingtopics.com

---

## 8. Accounting and Finance

### QuickBooks Online

**What it does:** Tracks all income, expenses, invoices, and taxes. Syncs natively with Shopify (orders become invoices automatically). Generates P&L, cash flow, and balance sheet for monthly review.

**Pricing:** Simple Start $35/month, Essentials $65/month  
**API:** Yes - https://developer.intuit.com/app/developer/qbo/docs/api/accounting/most-commonly-used/account  
**Shopify sync:** Native Shopify app available. Auto-maps orders to revenue, fees to expenses.

**Why chosen:** Industry standard for small business accounting. Has the Shopify sync that matters most. Accountant-friendly when tax season comes.

---

## 9. Workflow Automation

### Make.com (formerly Integromat)

**What it does:** Connects all tools via webhooks and API calls without custom code. Core automation scenarios for Floki:

- Scenario 1: New Shopify order -> Create HubSpot deal -> Tag contact in Klaviyo
- Scenario 2: HubSpot deal stage moves to "Closed Won" -> Add to QuickBooks as invoice -> Send onboarding email via Klaviyo
- Scenario 3: Every Sunday at 8am -> Pull HubSpot pipeline data -> Format weekly report -> Post to Discord #sales channel
- Scenario 4: New Apollo.io lead -> Create HubSpot contact -> Enroll in Klaviyo welcome sequence
- Scenario 5: New Faire order -> Create Shopify order -> Sync to QuickBooks

**Pricing:** Free (1,000 operations/month) / Core: $10.59/month (10,000 ops)  
**API:** Yes - native visual interface, all major tools have Make.com modules  
**Why chosen over Zapier:** More flexible, cheaper, more operations on free tier. Zapier is easier to set up but costs 2-3x more at scale.

---

## 10. Document and Asset Management

### GitHub

**What it does:** Version control for all sales documents, templates, and strategy files (this repo). Full audit trail of changes. Access for Anthony and all agents.

**Pricing:** Free for public repos, $4/month per user for private  
**Already in use.** All files in `/ecommerce-brands/Websites/sales/` are version-controlled here.

---

## 11. Communication

### Discord

**What it does:** Real-time communication across the Von Doom agent team. Automated reports from Make.com post directly to Discord channels.

**Already in use.** Key channels: #sales for pipeline updates, #main for Anthony direct comms.

**Automated Discord posting:**  
Make.com scenario posts weekly pipeline report to Discord #sales every Sunday at 8am ET. Format: plain text summary with key metrics and link to updated GitHub files.

---

## Phase 1 Stack Cost Summary

| Tool | Monthly Cost |
|------|-------------|
| HubSpot Free CRM | $0 |
| Apollo.io Basic | $49 |
| Klaviyo Free | $0 |
| Shopify Basic | $39 |
| Make.com Core | $10.59 |
| QuickBooks Simple Start | $35 |
| GA4 | $0 |
| Visualping Free | $0 |
| GitHub | $0 |
| Discord | $0 |
| **Total** | **$133.59/month** |

Phase 2 additions: Polar Analytics ($300/month), Klaviyo Email plan ($45/month) when email list exceeds 250 contacts.

---

## Implementation Order

1. **Day 1:** HubSpot CRM setup, import prospects, connect Gmail
2. **Day 2:** Apollo.io account, enrich top 20 contacts with emails
3. **Day 3:** Make.com setup, build Scenario 3 (weekly Discord report first)
4. **Day 4-7:** Email domain warm-up begins (see [07-OUTREACH-STRATEGY.md](./07-OUTREACH-STRATEGY.md))
5. **Week 2:** Apollo.io sequences built and loaded with templates from [08-EMAIL-TEMPLATES.md](./08-EMAIL-TEMPLATES.md)
6. **Week 3:** First outreach wave launches
7. **Phase 2:** Shopify live, Klaviyo flows built, Make.com Scenarios 1-2 built, QuickBooks synced

See [14-ANALYTICS-AND-REPORTING.md](./14-ANALYTICS-AND-REPORTING.md) for dashboard setup and KPI tracking.
