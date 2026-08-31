# Product Ideas — Week of 2026-08-31 (Week 7)

## Executive summary

- **Evidence mode: B** (WebFetch UNAVAILABLE — seventh consecutive run). Both STEP 0 control
  fetches returned `EGRESS_BLOCKED`. No curl or direct-HTTP workaround attempted, per the brief.
- **Three validated ideas against a 4–6 target, reported as three rather than padded** — but unlike
  last week, **two of them are genuine build candidates** (composite **15** each, the highest new
  scores since week 2 and the first Whitespace-4 ratings in five weeks). The third is a clean kill.
- **The methodological find of the run corrects last week's guidance.** Week 6 parked public
  feature-request boards as a "Mode-A-only" evidence class. That is wrong for
  **Lithium/Khoros-hosted vendor communities**: `community.hubspot.com` and `community.xero.com`
  return **status labels *and* vote counts in search result text** ("Not Currently Planned",
  428 upvotes). This channel produced the week's top idea. Canny-hosted boards
  (`ideas.gohighlevel.com`) still do not work.
- **Two new trade-forum channels opened**, both productive on first contact:
  `practicalmachinist.com` (manufacturing / job shops) and `signs101.com` (sign & print).
  Week 6's "prefer the office/admin subforum" rule held exactly — Practical Machinist's
  *Shop Management and Owner Issues* subforum carried nearly all the signal.
- **Eight kills**, including the **expired-premise screen's first solo kill** (see risks).

---

## Deep Dive of the Week — ID 017: customer-specific price lists for QuickBooks Online + Xero

**The gap.** Small wholesalers, distributors and trade suppliers need to charge different customers
different prices for the same item. QuickBooks Online's Price Rules is **still in beta after years**,
is **Plus/Advanced only**, and was **pulled from the new invoice experience with "no specific
timeframe" for its return** ([dancingnumbers.com](https://www.dancingnumbers.com/price-rules-in-quickbooks-online/)).
Intuit's own community answer is to go find a third-party app, while declining to name one
([/00/1464772](https://quickbooks.intuit.com/learn-support/en-us/do-more-with-quickbooks/3rd-party-app-for-customer-price-rules-and-inventory-management/00/1464772)).
Xero never built it at all: the tiered price-list request has been **open since 2012**
([community.xero.com/business/discussion/129501](https://community.xero.com/business/discussion/129501)).

**MVP — five features.**
1. OAuth connect to QBO (Xero second); sync customers and items.
2. Price-list builder: named lists ("Wholesale Tier A"), per-item price or % off list, customers
   assigned to a list, **bulk CSV import** of the price sheet they already keep in Excel.
3. Invoice/estimate builder: pick a customer → app applies their list → **pushes a finished draft
   invoice or estimate into QBO/Xero**. (It cannot intercept the native invoice form, so it must
   own the build step — this is the core design constraint.)
4. Effective-dated price history and audit trail: *what price did this customer get, on what date,
   under which list.* Wholesale price disputes are the recurring pain underneath the complaints.
5. Customer price-sheet PDF export.

**Stack Claude would build it with.** Next.js on Vercel; Supabase (Postgres + auth); Intuit OAuth 2.0
against the QuickBooks Online Accounting API v3 (Customer, Item, Invoice, Estimate entities); Xero
OAuth 2.0 + Accounting API for phase two; Stripe for billing. No queues, no heavy infrastructure —
on-demand sync is sufficient at this scale.

**First acquisition channel.** The QBO community threads above already rank organically and keep
ranking for years. Publish a genuinely useful answer page for each named workaround thread
("QuickBooks Online price levels", "Xero customer price list") and let the existing search demand
land on it. Listing on the QuickBooks App Store is the *second* channel, not the first, because it
is gated (below).

**Benchmarked price point: $29/mo.** Benchmarks actually seen this run: Orderwerks **$60/user/mo**,
Now Commerce **$200/mo**, and the native path is a QBO **Plus $115/mo → Advanced $275/mo** upgrade
after Intuit's August 2026 price increase. $29 sits under half the cheapest per-user incumbent.

**Biggest risk: platform dependency.** Intuit finishing Price Rules for the new invoice experience —
already in beta — would erase the QBO half of this market with no warning. The mitigation is that
**Xero is the durable half**: a request Xero has declined to build for fourteen years is a far safer
foundation than a feature Intuit is actively mid-rollout on. Build QBO first for volume; treat Xero
as the moat. Secondary risk: Intuit's app-store review runs **6 weeks to 6+ months** (technical,
security and marketing stages). That is a real delay, but it is also the week-6 gate criterion
working *for* the builder — a wait a solo founder can absorb and a competitor chasing a $29/mo
product will not bother with.

---

## This week's validated ideas

| ID | Idea | D | W | F | M | Composite | Key evidence (Mode B) |
|----|------|---|---|---|---|-----------|------------------------|
| **017** | Customer-specific price lists for QBO + Xero | 4 | 4 | 3 | 4 | **15** | QBO threads *"Has anyone found a workaround for the price rules going away in new invoice EXPERIENCE (more like NIGHTMARE)?"*, *"Workaround for the ommission of price rules"*, *"Can i add Price Levels for different customers... It is crucial to my business i do so."* + Xero's 2012-open tiered-price-list request. Incumbents: Orderwerks $60/user/mo, Now Commerce $200/mo. |
| **018** | Sub-$50 quoting calculator + quote memory for 1–5 person job shops | 4 | 4 | 4 | 3 | **15** | Practical Machinist, **2 Jul 2026**: quoting off a homemade spreadsheet gives *"inconsistent numbers depending on their mood... no memory of what they quoted a similar part for last time."* *"What should a basic job shop quoting software have?"* names the gap between spreadsheets and E2/JobBOSS. [CNCCookbook survey](https://www.cnccookbook.com/job-quote-cost-estimation-survey-results/): *"nobody is happy with any of the available solutions."* Chasm: free → **JobBOSS² $199/mo (1 user)**, Paperless Parts $300/mo, DigiFabster $290/mo, Fulcrum $43/user/mo with a 5-user floor. |
| **019** | Sign-shop management for shopVOX price refugees | 4 | 1 | 2 | 3 | **10** | **Negative finding.** shopVOX **$215 → $366/mo**; Capterra: *"The sudden price increase, 350% to be specific... I was told if I don't like the increase to just leave and go find something else."* But SignTracker **$49/mo** and QuoteIQ **$29.99/mo** already catch every refugee. Whitespace 1. |

**Kills this run (8):** QBO invoice feature-restoration (expired premise — Intuit re-shipped subtotals
and time grouping); Xero custom reporting (Syft free, G-Accon $50/mo); farm/grain/spray records
(KernelAg free, Harvest Profit, Bushel); lawn care (Yardbook free); trucking paperwork (Transflo,
CamScanner); crop-share landlord statements (no complaint exists to find); `community.spiceworks.com`
(channel dead, plus free open-source ITFlow); Airtable/Notion boards (no status vocabulary indexed).

---

## Top-10 backlog snapshot

| Rank | ID | Idea | Composite | Status |
|------|----|------|-----------|--------|
| 1 | 001 | Honest accessibility scan + fix pack (e-commerce) | 16 | Deep-Dived |
| 2 | **017** | **Customer price lists for QBO + Xero** | **15** | **Deep-Dived (this week)** |
| 2 | **018** | **Sub-$50 job-shop quoting + quote memory** | **15** | **New — next week's deep dive** |
| 4 | 010 | Prop 65 warning audit + evidence archive | 14 | Deep-Dived |
| 5 | 012 | Google review disappearance archive + appeal pack | 13 | Deep-Dived |
| 5 | 006 | Auto-renewal / click-to-cancel flow monitoring | 13 | Deep-Dived |
| 5 | 003 | Small-batch maker COGS tracker | 13 | Deep-Dived (conditional-NO) |
| 5 | 011 | Supplier PO chasing | 13 | New (do not build) |
| 9 | 002 | EU AI Act Art. 50 transparency kit | 12 | New |
| 9 | 007 | US state packaging-EPR reporting | 12 | New |
| 9 | 014 | Subcontractor COI / cert expiry tracking | 12 | New (leans negative) |

No new Stale marks this run. ID 013 (composite 11, first seen 2026-08-17) crosses the three-week
threshold next week and should be marked Stale then unless fresh evidence moves it.

---

## Risks and watch-outs

1. **ID 017's whole thesis rests on Intuit not finishing a feature it has in beta.** This is the
   sharpest platform-dependency risk the backlog has carried. The Xero half is the hedge, and any
   build should start with a data model that treats the accounting platform as swappable.
2. **ID 018's competitor is free, and the free version is being built in public by the customer.**
   The 2 July 2026 Practical Machinist thread is a shop owner giving his quoting calculator away.
   ID 003 died on exactly this. Monetization 3 is not a rounding error — it is the whole question,
   and it is what the deep dive next week must attack first.
3. **The expired-premise screen earned its place immediately.** Week 6 added it; this week it killed
   an idea that looked like the strongest wedge shape this project knows (feature *loss*, not price).
   The QBO subtotal and time-grouping complaints are real, loud, and **stale** — Intuit restored the
   functionality. Mode B skews toward older indexed content, so every demand signal now needs a
   "does this still exist in 2026?" date check before it is scored, not after.
4. **Eighth consecutive instance of "loud verifiable complaint → gap already filled"** (ID 019).
   The prior is now essentially without exception. The two ideas that scored 15 both cleared it the
   same way: the gap is not *unnoticed*, it is **guarded** — by a slow app-store review in 017's
   case, by a market too small for a VC-backed vendor in 018's.
5. **Seven runs without WebFetch.** The block is now clearly the binding constraint on evidence
   quality, not merely an inconvenience — though this week partly rebuts the fatalism, since the
   channel week 6 wrote off as unreachable turned out to work and produced the top idea.
   Allowlisting the domains listed in the research log remains the single highest-leverage change.

*No claim above is a projection of income. Every price and quotation traces to a linked source seen
in search result text this run; none was read as a full page, and none is invented.*
