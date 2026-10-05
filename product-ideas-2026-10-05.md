# Product Ideas — Week of 2026-10-05 (Week 12)

## Executive summary

- **Evidence mode: B** (WebFetch UNAVAILABLE — twelfth consecutive run). Step 0 ran first: both control URLs failed with a named
  `EGRESS_BLOCKED` proxy error. No retries, no curl. Every claim below comes from result text that itself carried a price, status,
  vote count or quoted complaint.
- **Zero new validated ideas — reported rather than padded, the second consecutive zero.** Three discovery veins were probed and
  all three closed: Airtable gaps (served at $29/mo), Xero's missing customer-PO field (free native workaround), and 2026–27
  software sunsets (nothing small-business-scale not already on file).
- **Re-validation again outperformed discovery — four score changes.** **ID 010 (Prop 65) fell 14 → 12**; **ID 014 (subcontractor
  COIs)** and **ID 009 (Shopify forecasting)** both fell to 11, each killed by an incumbent matching its feature list at or below
  its own target price. **ID 002 was retired on premise expiry**, the failure mode week 11 predicted.
- **ID 017 gained the best-evidenced claim in this project's history — and its score deliberately did not rise.** Xero's own board
  shows the gap refused with **128 votes** and a **May 2026** complaint; the composite stays **15** because no dimension honestly
  crossed a threshold. Twelve weeks, still no upward revision.
- **One new evidence class: Flippa / Acquire.com listing data.** Listing titles carry real revenue and asking prices under Mode B,
  which no other channel does — now the standing benchmark for deep-dive price points.

---

## Deep Dive of the Week — ID 017: customer-specific price lists for Xero (and QBO)

**A stated deviation, declared up front.** By rule the slot belonged to **ID 021** (insurance commission reconciliation, 12) as the
highest never-dived row — **no never-dived row sits at 13+ anywhere in the backlog**, exactly the break week 11 forecast. The
pre-dive check killed it in one query: **AgencyComp Pro is $39.95/mo for up to 500 clients**
([agencycomp.com/pricing](https://agencycomp.com/pricing/)), so a "sub-$50" tool has nothing to price against. **Verdict NO, no
build plan.** The depth went to ID 017 instead, whose original dive (2026-08-31) predates every fact below.

### Why it still stands

Xero's own product board, suggestion
[44960380](https://productideas.xero.com/forums/967139-purchase-orders-bills-inventory/suggestions/44960380-product-services-create-custom-tiered-price)
("Create custom (tiered) price lists for contacts"): **128 votes**, official status **"Not in pipeline"** — *"the Inventory team
reviewed the idea but does not have development planned"* for this, and it will *remain "not planned" unless there is a change*.
A **May 2026** comment states the pain precisely: the ability *"to assign a pricing level to Contacts so that customers charged at
different levels (e.g. distributor, wholesale or retail) don't need to have the item price manually overwritten on every invoice."*

On the QBO side the gap is real but closing: native **Price Rules** now documents customer-level targeting, is **Plus/Advanced
only**, and is still in beta after years — already known and scored around, so not a new kill. What is new is the **1 Aug 2026
repricing**: Plus ~$99 → **$140/mo**, Advanced ~$200 → **$340/mo**
([fourlane](https://www.fourlane.com/quickbooks-online-pricing-changes-2026-new-rates-and-fourlane-discounts/)), so an Essentials
user ($75–85) now faces a **$55–65/mo jump** to reach it.

**The whitespace caveat:** one result stated that *"a search through the app store did not find an app that offers this feature and
integrates with Xero"* — but a second query could **not** confirm that absence. Recorded as a single-source claim, which is why
Whitespace held at 3 rather than rising to 4.

### MVP — five features

1. **Price-list builder** — named tiers (Distributor / Wholesale / Retail), each a % off list or a fixed per-item price.
2. **Tier assignment per Xero contact**, with bulk CSV assignment so onboarding an existing ledger is one upload.
3. **Auto-apply on draft** — a webhook on invoice creation looks up the contact's tier and rewrites line-item unit amounts
   *before* approval. This is what the May 2026 comment literally asks for.
4. **Exception report** — a weekly list of invoices whose prices don't match the contact's tier; makes the product auditable
   rather than magic, and covers the race condition in feature 3.
5. **Quotes, not just invoices** — the same substitution on Xero quotes, where the pricing decision gets made.

### Stack Claude would build it with

Next.js (App Router, TypeScript) on Vercel; `xero-node` with **OAuth 2.0** against the Accounting API (Contacts, Items, Invoices,
Quotes); **Xero webhooks** for Invoice CREATE/UPDATE into a serverless handler with `x-xero-signature` HMAC verification; Postgres
on Supabase or Neon; Stripe Billing; Postmark or Resend for the exception email. No queues, no infrastructure to run.

### Benchmarked price point: **$29/month**

Inside the documented **$20–$100+/mo** band for Xero add-ons (A2X $19–300, Dext $24–90); matches the observed 2026 floor for
single-purpose B2B add-ons (**miniExtensions Basic $29**, **PaperBoss $29**); and undercuts the **$55–65/mo** QBO upgrade it
replaces. Flippa shows ~**$50 per subscriber per month** is achievable for a small tool
([flippa.com/12062722](https://flippa.com/12062722-44k-rev-8-5k-profit-in-10-mos-3-9k-mrr-77-subs-5-0-star-chrome-extension-ai-saas-with-strong-traction-and-big-growth-runway)),
so $29 is conservative, not aspirational.

### First acquisition channel

The 128-vote thread itself — a self-qualified queue of named buyers with a vendor refusal on the record, still live as of May
2026. Post once as a builder with a free tier, then the Xero community thread, then an App Store listing. Xero's free developer
tier allows **5 connections at $0**, so the first five customers cost nothing to serve — the cheapest honest validation available.

### The single biggest risk

**The platforms control the unit economics and both moved in 2026.** Xero replaced its 15% revenue share with **tiered developer
pricing effective 2 March 2026**: Starter **$0 (5 connections)**, Core **~$22 (50 connections, 10 GB egress)**, Plus **~$152
(1,000)**, overage **$2.40 AUD/GB** ([developer.xero.com/pricing](https://developer.xero.com/pricing),
[accountingtoday](https://www.accountingtoday.com/news/xero-shifts-to-tiered-pricing-model-for-developers)) — trade press called it
*"'All you can eat Xero data buffet' comes to abrupt end."* A flat fee beats 15% for a small app, but there is a hard **$22 → $152
cliff at the 51st customer**, and a platform that repriced once will do so again. Meanwhile **QBO's Price Rules leaving beta would
erase the QBO half outright.** Build the Xero half first; treat QBO as upside.

---

## This week's new validated ideas

**None.** Three veins were probed; each failed a screen:

| Probe | Real evidence found | Why it earned no row |
|---|---|---|
| Airtable feature gaps | Filtered "Link to record" fields are *"the #1 feature request from all Airtable users for the last 6+ years, but Airtable has refused to implement it"*; no native record locking | **miniExtensions ($29/mo)** already sells both, and an alternatives layer has formed on top. Marketplace density closed it in one query. |
| Xero customer-PO-number field | Xero: *"there are no plans for developing a field for a PO number in invoicing"*; a seller: *"no customer will pay an invoice without their purchase order number appearing on an invoice"* | **Killed at $0.** The free native fix is the **Reference field**, which *"prints on the invoice, and is also searchable"*, renamed in the template. |
| 2026–27 software sunsets | QBD 2023 ends 31 May 2026, 2024 ends 30 Sep 2027; Quip non-renewable after 1 Mar 2027 | Small-business cases already on file; the rest is enterprise/partner-led. A **sunset tracker already exists** ([sunsetproof.com](https://sunsetproof.com/tracker/)). |

## Top-10 backlog snapshot

| # | ID | Idea | Score | Status |
|---|---|---|---|---|
| 1 | 017 | Customer-specific price lists for QBO + Xero | **15** | Strengthened / Re-Deep-Dived 2026-10-05 |
| 2 | 001 | Honest accessibility scan + fix pack | 13 | Re-scored down (whitespace 1) |
| 3 | 020 | CAM/NNN reconciliation, small landlords | 13 | Deep-Dived — verdict NO |
| 4 | 012 | Google review archive + appeal pack | 13 | Deep-Dived |
| 5 | 006 | Auto-renewal cancel-flow monitoring | 13 | Deep-Dived |
| 6 | 010 | Prop 65 per-SKU register + archive | **12** ↓ | **Re-scored down 2026-10-05** |
| 7 | 018 | Sub-$50 job-shop quoting | 12 | Re-scored down |
| 8 | 021 | Insurance commission reconciliation | 12 | **Pre-dive: verdict NO 2026-10-05** |
| 9 | 003 | Small-batch maker COGS tracker | 12 | Deep-Dived — conditional NO |
| 10 | 011 | Supplier PO chasing | 12 | Deep-Dived — verdict NO |

Only **ID 017** is above 13, and **seven of the top ten carry an explicit do-not-build or verdict-NO note.** 

## Risks and watch-outs

- **The backlog is one idea deep, and twelve weeks have produced zero upward revisions.** ID 017 at 15 is the only row not leaning
  negative; everything at 13 is deep-dived or killed. Every revisited score has fallen or held — ID 017 had the best case for a
  rise this week and still did not get one. Treat un-rechecked scores as provisional and optimistic.
- **The deep-dive slot is structurally broken.** Five consecutive weeks the pre-dive check has moved or killed the scheduled
  target, and no never-dived row at 13+ remains.
- **Reddit and Hacker News — two of the brief's named priority sources — remain unavailable** under this backend; ClickUp's
  community joined them this week with zero domain results.
- **No claim here forecasts profit.** Flippa and Acquire figures are *asking prices and seller claims*, not verified earnings, and
  every price above was seen in result text, not invented.
