# 06 - Pipeline: Floki Brands

Live deal tracker with lead scoring criteria, conversion rate benchmarks by channel, and automated stage transitions via HubSpot CRM.

**Pipeline owner:** VD-Sales  
**CRM:** HubSpot Free  
**Related files:** [05-PROSPECTS.md](./05-PROSPECTS.md) | [07-OUTREACH-STRATEGY.md](./07-OUTREACH-STRATEGY.md) | [14-ANALYTICS-AND-REPORTING.md](./14-ANALYTICS-AND-REPORTING.md)

---

## Pipeline Stages

| Stage | Definition | Action Required | HubSpot Stage Name |
|-------|-----------|----------------|--------------------|
| 1. Not Contacted | Identified, no outreach yet | Schedule outreach | Prospect |
| 2. Outreach Sent | Initial email sent (Day 1) | None - wait for Day 5 | Outreach Sent |
| 3. Followed Up | Day 5 follow-up sent | None - wait for Day 12 | Follow-Up 1 |
| 4. Final Follow-Up | Day 12 final follow-up sent | Move to Nurture if no reply by Day 19 | Follow-Up 2 |
| 5. Warm | Responded, in active conversation | Reply within 24h, send samples if A-tier | Qualified |
| 6. Meeting Scheduled | Call or demo booked | Prep with product specs, pricing, sample | Meeting Set |
| 7. Proposal Sent | Pricing/line sheet/sample kit sent | Follow up in 5 business days | Proposal Sent |
| 8. Negotiation | Terms being discussed | Escalate to Anthony if deal > $2,000 | Negotiation |
| 9. Closed Won | Deal signed/PO received | Process order, update QuickBooks, trigger Klaviyo onboarding | Closed Won |
| 10. Closed Lost | Not moving forward | Document reason, schedule Nurture re-touch in 90 days | Closed Lost |
| 11. Nurture | Long-term, revisit later | Schedule 60-90 day re-contact in HubSpot sequence | Nurture |

---

## Lead Scoring Criteria

Each prospect gets a score from 1-10 based on these factors. Scores 7-10 = A-tier. Scores 4-6 = B-tier. Scores 1-3 = C-tier.

| Factor | Weight | Scoring Notes |
|--------|--------|--------------|
| Estimated deal size | 30% | $10K+ = 10 pts, $5K-10K = 7 pts, $1K-5K = 4 pts, <$1K = 1 pt |
| Decision-maker contact available | 20% | Direct email known = 10, LinkedIn findable = 6, Only general contact = 2 |
| Product/aesthetic fit | 20% | Perfect match = 10, Good fit = 7, Possible = 4, Stretch = 1 |
| Sales cycle speed | 15% | Under 30 days = 10, 30-90 days = 7, 90-180 days = 4, 180+ days = 1 |
| Strategic value (brand) | 15% | Logo account/press value = 10, Good reorder potential = 7, Standard = 3 |

### A-Tier Triggers (automatic score 8+)
- Any STR company with 500+ properties
- Any hotel group with 20+ properties
- Any GPO (Avendra, Entegra) - preferred vendor status
- Any hotel with opening in next 90 days (time-sensitive)
- Any corporate gifting platform with 1M+ annual transactions

---

## Conversion Rate Benchmarks by Channel

These are realistic benchmarks based on cold B2B outreach. Track your own actuals against these and adjust outreach if underperforming.

| Channel | Open Rate Target | Reply Rate Target | Call-to-Close Rate | Avg. Deal Size |
|---------|----------------|------------------|--------------------|---------------|
| FF&E Procurement | 40% | 8-12% | 30% | $3,000-$10,000 |
| Hotel Direct | 35% | 5-8% | 25% | $500-$3,000 |
| STR Management | 40% | 10-15% | 35% | $1,000-$50,000 |
| Boutique Retail | 45% | 12-18% | 40% | $180-$500 |
| Fashion Brands | 35% | 8-12% | 30% | $180-$500 |
| Personal Stylists | 50% | 20-30% | 60% | $90-$300 |
| Corporate Gifting | 30% | 5-8% | 20% | $2,000-$15,000 |

**If open rates are below benchmark:** Subject line is the problem. Run A/B tests (see [08-EMAIL-TEMPLATES.md](./08-EMAIL-TEMPLATES.md)).  
**If reply rates are below benchmark:** Email body is the problem. Too long, too generic, or wrong audience.  
**If call-to-close rate is below benchmark:** Pricing or product fit issue. Review offer with Anthony.

---

## Automated Stage Transitions (HubSpot + Make.com)

Set up these automations in HubSpot Workflows (free tier supports basic workflows):

| Trigger | Action | Tool |
|---------|--------|------|
| Contact replies to outreach email | Move to "Warm" stage | HubSpot email tracking (native) |
| Deal stage = "Closed Won" | Create invoice in QuickBooks | Make.com Scenario 2 |
| Deal stage = "Closed Won" | Enroll contact in Klaviyo B2B onboarding flow | Make.com Scenario 2 |
| Deal stage = "Closed Won" | Post notification to Discord #sales | Make.com Scenario 3 |
| 5 days since Outreach Sent with no reply | Send Day 5 follow-up email | Apollo.io sequence (automated) |
| 12 days since Outreach Sent with no reply | Send Day 12 final follow-up | Apollo.io sequence (automated) |
| 19 days since Outreach Sent with no reply | Move to "Nurture," schedule re-contact in 60 days | HubSpot workflow |
| Deal stage = "Nurture" for 60 days | Re-enroll in outreach sequence | HubSpot workflow |

---

## Current Pipeline Status

**Last updated:** 2026-04-18

| Metric | Value |
|--------|-------|
| Total prospects | 52 |
| Not Contacted | 52 |
| Warm | 0 |
| Meeting Scheduled | 0 |
| Proposal Sent | 0 |
| Closed Won | 0 |
| Revenue (YTD) | $0 |
| A-Tier prospects | 15 |

**Status:** Outreach on hold pending Anthony's go-ahead. Website live at https://floki-website.vercel.app. Shopify cart = Phase 2.

---

## Active Deals

_None yet. Outreach pending._

---

## Closed Won

_None yet._

---

## Closed Lost

_None yet._

---

## Nurture Queue

_None yet._

---

## Pipeline Rules

1. Update pipeline within 24 hours of any touchpoint
2. All outreach routes through shopflokibrands@gmail.com
3. Deals above $2,000 escalate to Anthony for negotiation sign-off
4. A-tier prospects get a phone call attempt after Day 5 email follow-up (see [07-OUTREACH-STRATEGY.md](./07-OUTREACH-STRATEGY.md))
5. Never let a warm lead go more than 24 hours without a response
6. Document every "Closed Lost" with a reason - patterns reveal pricing or positioning issues

---

## Weekly Pipeline Review (Every Monday)

Answer these questions every Monday morning:
- How many new prospects added last week?
- How many moved from Outreach Sent to Warm?
- How many deals in Proposal or Negotiation?
- What was the total value of Closed Won this month?
- What is the projected close for next 30 days?

Post results to Discord #sales via automated Make.com report. See [14-ANALYTICS-AND-REPORTING.md](./14-ANALYTICS-AND-REPORTING.md).
