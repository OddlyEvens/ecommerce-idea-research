# Product Ideas — Week of 2026-10-19 (Week 14)

## Executive summary

- **Evidence mode: B** (WebSearch only). WebFetch failed Step 0 for the **fourteenth consecutive run**, with the same DNS-level signature as last week (`getaddrinfo ENOTFOUND` for both `example.com` and `en.wikipedia.org`) — no proxy response at all. No retries, no curl.
- **Infrastructure finding, and it is the most urgent item in this report: last week's entire run was never pushed.** The 2026-10-12 commit existed only as an orphaned commit on a detached HEAD; `origin/main` still sat at 2026-10-05. It has been recovered and is included in this week's push. See *Risks*.
- **One new validated idea (ID 024)** — a customer "notify me when back in stock" waitlist for **Square Online**, scored **11**. It carries the **freshest demand signal this project has found** (a complaint **27 days old**) and a vendor-confirmed absence, and it is killed down to 11 by a price anchor of **free-to-$9/mo** in the comparable Shopify category.
- **Two downward re-scores, both well-evidenced.** **ID 017 → 13** (a direct competitor, *Ocean Pricing*, was found recruiting beta testers **inside the Xero complaint thread itself** — the second time in two weeks the competitor was hiding in the complaint channel). **ID 001 → 12** (the Shopify accessibility category now has **67+ apps**, including one that is ID 001's exact product with a free plan).
- **Fourteen weeks, still zero upward composite revisions.** The backlog's ceiling is now **13**.

## Deep Dive of the Week — ID 024: Back-in-stock waitlist for Square Online

Selected by rule as the highest-composite row never deep-dived (11). This finally **ends three consecutive weeks** in which no live never-dived row existed and the slot had to be spent as a re-dive.

**The gap.** Square has no customer-facing restock alert, and says so itself: *"this feature is not yet available for Square Online in any of our markets"* ([community.squareup.com](https://community.squareup.com/t5/Questions-How-To/Back-In-Stock-Email-Notification-Functionality/m-p/774894)). Square's Online plans page advertises only *low-stock alerts to the merchant*. At least six separate request threads exist across Square's two boards, Square has itself run a *"Feature Request Highlight: Notify When an Item is Back in Stock"* ([m-p/752264](https://community.squareup.com/t5/Online-Store/Feature-Request-Highlight-Notify-When-an-Item-is-Back-in-Stock/m-p/752264)), a moderator recorded *"no update or ETA"* ([sellercommunity.com](https://sellercommunity.com/t5/Square-Online/NOTIFY-WHEN-BACK-IN-STOCK/idi-p/285686)), one seller wrote they would *"likely have to switch to a different platform if this isn't added"*, and a request **27 days old** states it *"has been a feature request from countless users for many years and it's still being ignored"* ([idc-p/849718](https://community.squareup.com/t5/Feature-Requests/Notify-me-when-back-in-stock-feature/idc-p/849718)). Every mature Shopify equivalent is Shopify-locked, so Square merchants cannot buy their way out.

**MVP (4 features).** (1) A "Notify me" capture widget pasted into Square Online's embed-code block, recording email + item. (2) An inventory watcher on Square's Catalog/Inventory API webhooks, detecting a count moving from 0 to positive. (3) A deduplicated restock email per subscriber per restock. (4) **The differentiator — a merchant dashboard ranking waitlisted items by demand**, i.e. a *what-to-reorder* report. Features 1–3 are the commodity; feature 4 is the only reason to charge above the category floor.

**Stack Claude would build.** Node/TypeScript on a managed host (Railway or Render); Postgres via Supabase for subscriptions; Square OAuth plus the Catalog/Inventory APIs with an `inventory.count.updated` webhook; Postmark or Resend for transactional email; a dependency-free vanilla-JS widget served from a CDN so it survives being pasted into Square's embed block; Stripe for billing. Nothing here is beyond an AI-assisted solo builder.

**First acquisition channel.** The six request threads themselves — and this is a channel the project has now watched work **twice**: both *InvoicePolish* and *Ocean Pricing* were found by recruiting inside the vendor's own complaint thread. The 27-day-old thread is live and unanswered.

**Benchmarked price point: $12/mo with a free 50-alert tier.** Benchmarks actually seen: Zooomy **Pro $5.99/mo**, Premium $19.99 ([apps.shopify.com](https://apps.shopify.com/back-in-stock-zooomy)); Restocked **Pro $9/mo**, Business $20 ([apps.shopify.com](https://apps.shopify.com/restocked-1)); Digismoothie's Back in Stock Product Alerts **from $14.99/mo** ([digismoothie.com](https://www.digismoothie.com/app/back-in-stock-product-alerts)); Amp **$19/$49/$99** ([backinstock.org](https://backinstock.org/pricing)); and free tiers at 100 emails/mo from GrootApps and Crawlapps.

**The single biggest risk: Square ships it.** On **24 September 2026** Square released **preorders for sold-out items** ([release notes](https://squareup.com/us/en/release-notes)) — the same merchant problem solved from the other direction. A vendor that just shipped an adjacent sold-out-item feature has that area on its roadmap. Secondary: embedded code is **Plus and Premium only** and Square states it is *"unable to assist with custom code of any kind"* ([help article 6899](https://squareup.com/help/us/en/article/6899-add-external-content-and-widgets-with-embedded-code-in-square-online-store)), which caps reach and puts the widget on unsupported ground.

## This week's validated ideas

| ID | Idea | D | W | F | M | Comp | Mode | Key evidence |
|----|------|---|---|---|---|------|------|--------------|
| 024 | Back-in-stock waitlist + reorder-demand report for Square Online | 4 | 2 | 3 | 2 | **11** | B | Vendor-confirmed absence *"not yet available… in any of our markets"*; 6+ threads; one **27 days old**; Shopify analogues free–$9/mo and all Shopify-locked |

Demand is capped at 4, not 5, because **every source is a Square-operated domain** (`sellercommunity.com` and `community.squareup.com` are the same vendor): the brief's two-domain letter is met, its spirit is not.

## Re-scores

| ID | Was | Now | Why |
|----|-----|-----|-----|
| 017 | 14 | **13** | **Ocean Pricing** — a developer posted in the Xero thread that they built *"a customer price list solution… to create invoices in Xero"* and is recruiting beta testers at `oceanpricing.com` ([user page](https://productideas.xero.com/users/6468051653-mark-shields)). Dedicated, direct, unpriced. Whitespace 2 → 1. Demand *strengthened* (a second thread, [46911148](https://productideas.xero.com/forums/939198-for-small-businesses/suggestions/46911148-invoice-ability-to-add-a-price-list-to-a-custome), states the exact mechanism; a commenter notes *"Zoho, Sage, Freshbooks, and Quickbooks they all have the function"*) but demand was already 5. |
| 001 | 13 | **12** | Monetization 3 → 2. The honest-scanner tier is now **free**: **AccessRadar** scans WCAG 2.1, returns a prioritised fix list, re-scans weekly with email alerts, explicitly **no overlay**, **free plan** ([apps.shopify.com](https://apps.shopify.com/accessradar)) — ID 001's product, including its differentiator. Plus **HewnScan** and **AccessKit** (free plans), **Accessibility Manager Pro $9.99/mo**, **WCAG Guard $189/mo**, against **67+ accessibility apps** on the store ([testparty.ai](https://testparty.ai/blog/best-shopify-accessibility-apps-2026)). |
| 020 | 13 | **retired** | Verdict NO (2026-09-28), six-plus competitors spanning $45–299/mo. Retired so closed rows stop holding top-ten slots. |

## Top-10 backlog snapshot

| Rank | ID | Idea | Comp | Status |
|------|----|------|------|--------|
| 1 | 017 | Customer-specific price lists for QBO + Xero | 13 | Re-scored down |
| 2 | 006 | Click-to-cancel cancel-flow monitoring | 13 | Strengthened |
| 3 | 001 | Honest accessibility scan + fix pack | 12 | Re-scored down |
| 4 | 012 | Google review disappearance archive | 12 | Re-scored down |
| 5 | 010 | Prop 65 warning audit register | 12 | Re-scored down |
| 6 | 018 | Sub-$50 quoting calculator for job shops | 12 | Re-scored down |
| 7 | 021 | Carrier commission reconciliation | 12 | Deep-dived, NO |
| 8 | 003 | Small-batch maker COGS tracker | 12 | Deep-dived |
| 9 | 011 | Supplier PO chasing | 12 | Deep-dived |
| 10 | 024 | Square back-in-stock waitlist | 11 | **New** |

Rank 10 is a ten-way tie at 11; ID 024 is shown because it is the **only row at that score not marked Stale**. Ranks 3–9 are a seven-way tie at 12. After retiring ID 020 the backlog holds **23 active rows**, of which **9 sit at 12 or above and every one of those has already been deep-dived**.

## Risks and watch-outs

1. **The repo was silently losing work.** Week 13 committed onto a detached HEAD and never reached `origin/main`; had this container been reclaimed, that run would have been lost outright. Recovered and pushed this week. **Every future run must verify it is on `main` before committing.**
2. **The competitor hides in the complaint channel.** Two weeks running, the product that kills an idea was being advertised *inside the very thread that evidenced the demand* (InvoicePolish, now Ocean Pricing). Read the thread's own replies before scoring whitespace.
3. **A free tier is a harder kill than a cheap one.** ID 024's category and ID 001's category are both now anchored at $0. Neither is a pricing problem that a better product solves.
4. **No upward revision in fourteen weeks.** Strong enough to be a prior: an idea that survives first contact has not yet been searched hard enough. The ceiling is 13 and falling.
5. **No guarantees.** Nothing here is an income projection; every price and complaint traces to a cited link seen in a search result, not a fetched page.
