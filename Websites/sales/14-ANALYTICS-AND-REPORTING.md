# 14 - Analytics and Reporting: Floki Brands

Sales-specific metrics, KPI tracking, and reporting cadence. Covers dashboard setup, automated reporting, and the specific numbers to track at each growth phase.

**Related files:** [04-AUTOMATION-STACK.md](./04-AUTOMATION-STACK.md) | [06-PIPELINE.md](./06-PIPELINE.md) | [02-SALES-STRATEGY.md](./02-SALES-STRATEGY.md)

---

## North Star Metrics

| Metric | Definition | Target (Year 1) |
|--------|-----------|-----------------|
| Total Revenue | All channels combined | $50,000-200,000 |
| B2B Revenue | Hotel, FF&E, STR, Retail wholesale | 70%+ of total |
| DTC Revenue | Shopify direct sales | 30% of total |
| Units Sold | Total units across all channels | 5,000-25,000 |
| Active Accounts | B2B accounts with at least 1 order | 15-30 |
| Reorder Rate | B2B accounts placing 2+ orders | 40%+ |

---

## KPIs by Channel

### B2B (Hotel / FF&E / STR)

| KPI | Benchmark | Frequency |
|-----|-----------|-----------|
| Outreach emails sent | 20-40/week | Weekly |
| Email open rate | 25-40% | Weekly |
| Email reply rate | 5-15% | Weekly |
| Meetings booked | 2-5/week | Weekly |
| Sample kits sent | 3-8/month | Monthly |
| Proposals sent | 4-10/month | Monthly |
| Close rate (proposal to order) | 20-35% | Monthly |
| Average order value | $250-2,500 | Monthly |
| Average deal cycle | 30-60 days | Monthly |
| Customer acquisition cost | Under $50/account | Quarterly |

### DTC (Shopify)

| KPI | Benchmark | Frequency |
|-----|-----------|-----------|
| Monthly sessions | Track growth rate | Monthly |
| Conversion rate | 2-3% | Weekly |
| Average order value | $25-45 | Weekly |
| Cart abandonment rate | Under 70% | Weekly |
| Return customer rate | 20%+ | Monthly |
| Revenue per visitor | Track trend | Monthly |
| Customer acquisition cost | Under $15 | Monthly |

### Wholesale Marketplaces (Faire, Tundra, etc.)

| KPI | Benchmark | Frequency |
|-----|-----------|-----------|
| Profile views | Track growth | Monthly |
| Inbound inquiries | Track volume | Weekly |
| Orders from marketplace | Track volume + AOV | Monthly |
| Conversion rate (view to order) | 2-5% | Monthly |

### Partnerships (Stylists, Designers, etc.)

| KPI | Benchmark | Frequency |
|-----|-----------|-----------|
| Active referral partners | 10-25 | Monthly |
| Referral revenue | Track % of total | Monthly |
| Revenue per partner per month | $50-200 | Monthly |
| New partners added | 2-5/month | Monthly |

---

## Dashboard Setup

### HubSpot CRM Dashboard (Pipeline)

Set up these dashboard widgets in HubSpot:

1. **Pipeline funnel** - deals by stage, value at each stage
2. **Deals won this month** - count and total value
3. **Deals by channel** - breakdown by FF&E, Hotel, STR, Retail, etc.
4. **Activity feed** - emails sent, meetings booked, calls logged
5. **Lead source breakdown** - cold outreach vs. trade show vs. directory vs. referral
6. **Average time in each stage** - identifies bottlenecks
7. **Forecast** - projected revenue based on pipeline weighted probability

### Shopify Dashboard (DTC + B2B)

Use Shopify's native analytics plus Polar Analytics for deeper cuts:

1. **Revenue by day/week/month** - trend line
2. **Top products** - units and revenue
3. **Traffic sources** - where buyers come from
4. **Conversion funnel** - sessions -> add to cart -> checkout -> purchase
5. **B2B orders** (once Shopify B2B is active) - separate from DTC
6. **Average order value** - track by channel (DTC vs. wholesale)

### Google Analytics 4 (Website Behavior)

1. **User acquisition** - channels driving traffic
2. **Engagement** - pages per session, time on site
3. **Conversion events** - purchase, add to cart, begin checkout
4. **Landing page performance** - which pages convert best
5. **Geographic breakdown** - where buyers are located

---

## Reporting Cadence

### Weekly Report (Every Friday)

Quick operational snapshot. Should take 15 minutes to compile.

**Template:**

```
## Weekly Sales Report - [Date]

### Pipeline
- Outreach emails sent: __
- Replies received: __
- Reply rate: __%
- Meetings booked: __
- Sample kits shipped: __
- Proposals sent: __
- Deals closed: __ ($__)

### DTC
- Shopify revenue: $__
- Orders: __
- AOV: $__
- Conversion rate: __%

### Hot Leads
- [Company] - [Stage] - [Next step] - [Expected value]

### This Week's Wins
-

### Next Week Priorities
1.
2.
3.

### Blockers
-
```

### Monthly Report (First Monday of each month)

Deeper analysis with trends and strategic adjustments.

**Template:**

```
## Monthly Sales Report - [Month Year]

### Revenue Summary
- Total revenue: $__
- B2B revenue: $__ (__%)
- DTC revenue: $__ (__%)
- Marketplace revenue: $__ (__%)
- Partnership/referral revenue: $__ (__%)

### Pipeline Health
- Total pipeline value: $__
- New deals added: __
- Deals closed: __ ($__)
- Deals lost: __ ($__)
- Win rate: __%
- Average deal size: $__
- Average sales cycle: __ days

### Channel Performance
- FF&E: __ deals, $__ revenue
- Hotel Direct: __ deals, $__ revenue
- STR Management: __ deals, $__ revenue
- Boutique Retail: __ deals, $__ revenue
- Other B2B: __ deals, $__ revenue
- DTC: __ orders, $__ revenue

### Unit Economics
- Total units sold: __
- COGS: $__
- Gross margin: __%
- Blended average price per unit: $__

### Inventory
- Units remaining: __
- Reorder needed by: [date]
- Reorder quantity recommended: __

### What Worked
-

### What Didn't
-

### Adjustments for Next Month
1.
2.
3.
```

### Quarterly Review (End of each quarter)

Strategic review against phase targets from [02-SALES-STRATEGY.md](./02-SALES-STRATEGY.md).

- Revenue vs. target by phase
- Channel mix vs. plan
- Customer acquisition cost by channel
- Reorder rate analysis
- Partnership program performance
- Grant/funding application status
- Trade show ROI (if applicable)
- Competitive landscape changes
- Pricing strategy review
- Inventory planning for next quarter

---

## Automated Reporting via Make.com

Set up these automations once the stack is live (see [04-AUTOMATION-STACK.md](./04-AUTOMATION-STACK.md)):

### Automation 1: Daily Sales Summary to Discord
- **Trigger:** Scheduled (daily at 8:00 AM ET)
- **Source:** Shopify API - pull yesterday's orders
- **Action:** Post summary to Discord #sales channel
- **Format:** "Yesterday: [X] orders, $[Y] revenue, [Z] units sold. MTD: $[total]"

### Automation 2: New Deal Alert to Discord
- **Trigger:** HubSpot webhook - deal stage changes to "Closed Won"
- **Action:** Post to Discord #sales channel
- **Format:** "[Company Name] - DEAL CLOSED - $[value] - [channel] - [units]"

### Automation 3: Weekly Pipeline Digest
- **Trigger:** Scheduled (every Friday at 5:00 PM ET)
- **Source:** HubSpot API - pull pipeline summary
- **Action:** Post to Discord #sales channel
- **Format:** Pipeline snapshot with deals by stage, total value, meetings next week

### Automation 4: Low Inventory Alert
- **Trigger:** Shopify webhook - inventory drops below threshold (100 units)
- **Action:** Post to Discord #sales channel + DM to Anthony
- **Format:** "INVENTORY ALERT: [X] units remaining. Reorder needed."

### Automation 5: Monthly Revenue Report to Email
- **Trigger:** Scheduled (1st of each month at 9:00 AM ET)
- **Source:** Shopify API + HubSpot API
- **Action:** Compile and email monthly report to Anthony (shopflokibrands@gmail.com)

---

## Conversion Rate Benchmarks by Channel

Use these to evaluate whether outreach is performing well or needs adjustment:

| Channel | Cold Email Open Rate | Reply Rate | Meeting Rate | Close Rate |
|---------|---------------------|------------|-------------|------------|
| FF&E Procurement | 30-40% | 8-15% | 30-50% of replies | 20-30% |
| Hotel Direct | 25-35% | 5-12% | 25-40% of replies | 15-25% |
| STR Management | 25-35% | 8-15% | 30-45% of replies | 20-30% |
| Boutique Retail | 20-30% | 5-10% | 20-35% of replies | 25-40% |
| Fashion Brands | 20-30% | 5-10% | 25-35% of replies | 15-25% |
| Personal Stylists | 30-40% | 10-20% | N/A (direct sign-up) | 40-60% |
| Corporate Gifting | 20-30% | 5-10% | 20-30% of replies | 15-25% |

If actual rates fall below these benchmarks for 2+ weeks, review email templates in [08-EMAIL-TEMPLATES.md](./08-EMAIL-TEMPLATES.md) and outreach strategy in [07-OUTREACH-STRATEGY.md](./07-OUTREACH-STRATEGY.md).

---

## Tools for Analytics

| Tool | Purpose | Cost | Setup |
|------|---------|------|-------|
| HubSpot CRM | Pipeline tracking and deal analytics | Free tier | See [04-AUTOMATION-STACK.md](./04-AUTOMATION-STACK.md) |
| Shopify Analytics | DTC and B2B order data | Included with Shopify plan | Built-in |
| Google Analytics 4 | Website behavior and traffic sources | Free | Install tracking code on Shopify |
| Polar Analytics | Advanced Shopify analytics dashboards | $100/mo (optional) | Connect to Shopify |
| Make.com | Automated reporting to Discord | Free tier (1,000 ops/mo) | Build scenarios per above |
| Google Sheets | Manual tracking and ad-hoc analysis | Free | Use for custom reports |
