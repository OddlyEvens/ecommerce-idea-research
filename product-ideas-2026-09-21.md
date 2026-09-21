# Product Ideas — Week of 2026-09-21 (Week 10)

## Executive summary

- **Evidence mode: B** (WebFetch UNAVAILABLE — tenth consecutive run). Both Step 0 probes
  returned `EGRESS_BLOCKED` from the network egress proxy. No retries, no curl fallback.
- **This was a cleanup week, not a discovery week, and that is the honest headline.** One new
  idea cleared the evidence bar (ID 023, composite 10 — recorded as a negative finding), but
  **five existing backlog rows were re-scored down on new evidence**, four of them to flat
  do-not-builds. The backlog is materially more accurate than it was seven days ago.
- **Last week's best lesson paid off immediately.** Week 9 found that questions deferred as
  "needs Mode A" often fall to a sharper Mode B query. Three such deferred questions were
  retried this week and **all three resolved** — two against the idea they gated (IDs 003, 021)
  and one in favour of an existing row's evidence quality (ID 017).
- **ID 017 is now the only row in the backlog whose demand evidence sits on the vendor's own
  domain.** Intuit's own community and help pages state that Price Levels is not a QuickBooks
  Online feature and that Price Rules is Plus/Advanced-only. Week 8's vendor-SEO caveat is
  retired. The score does not change (15), but confidence in it does.
- **No new idea cleared 13, so the deep dive went to the highest non-deep-dived row (ID 011)
  and closed it with a NO.** The backlog now contains no non-deep-dived row above 13, and the
  single row at 13 is a confirmed do-not-build. Next week's deep dive must come from new ground.

---

## Deep Dive of the Week — ID 011: Supplier PO chasing for small Shopify brands

Selected as the highest-composite row never marked Deep-Dived (13), with week 8's tie-break
(prefer higher Competitive Whitespace) selecting it over ID 020. Week 9's standing rule — re-run
the cheap-tier check *before* diving — was applied first, and it changed the verdict's basis.

**MVP (5 features).** (1) PO register synced from Shopify inventory: SKU, supplier, quantity
ordered, promised date. (2) An automated chase ladder — supplier email at T-7 / T-0 / T+3
carrying the open-line summary, with replies threaded back onto the PO. (3) A promised-vs-actual
supplier scorecard: on-time %, mean slip in days. (4) Partial-receipt reconciliation — receive
against a PO, flag short-ships and unit-price variances. (5) A weekly "what's late and what it
blocks" digest tied to stock cover.

**Stack Claude would build it with.** A Shopify embedded app: Remix/Node with App Bridge and
Polaris, Shopify Admin GraphQL API for products, locations and inventory levels, Postgres
(Supabase or Neon), a scheduled worker for the chase ladder, Postmark or Resend for outbound
and inbound email parsing, Shopify Billing API for subscriptions, hosted on Vercel or Fly.

**First acquisition channel.** The Shopify App Store listing, seeded from the three community
threads the original demand came from ([/t/213283](https://community.shopify.com/t/purchase-order-app-what-are-you-using/213283),
[/t/70705](https://community.shopify.com/t/when-will-shopify-add-a-vendor-or-supplier-list-just-like-customers/70705)),
plus — new this week — search demand from the **Stocky shutdown in August 2026**.

**Benchmarked price point.** $19–29/mo. Benchmarks actually seen in result text this run:
**Ultimate Purchase Orders from $9.99/mo** ([apps.shopify.com/purchase-orders-pro](https://apps.shopify.com/purchase-orders-pro)),
**Auto Purchase Orders from $19.99/mo** (week 4 recorded $24.99 — the tier has moved *down*),
against Replenishly Pro $299/yr and Prediko from $49/mo.

**Biggest risk, and the verdict: NO.** The risk is the platform, and it is no longer
speculative. Shopify now documents **purchase orders and supplier management inside its own
admin** ([help.shopify.com/.../purchase-orders](https://help.shopify.com/en/manual/products/inventory/purchase-orders),
[.../managing-suppliers](https://help.shopify.com/en/manual/products/inventory/purchase-orders/managing-suppliers))
and is publicly soliciting merchant feedback on extending them
([community.shopify.com/t/.../683937](https://community.shopify.com/t/merchant-feedback-wanted-native-purchase-orders-in-supplier-specific-csv-formats/683937)).
A solo builder would be selling a feature the platform is absorbing, into a paid tier whose
floor has fallen to $9.99/mo. **Whitespace 2 → 1, composite 13 → 12, marked Deep-Dived.** Its
value now is that it stops consuming tie-break attention, which it has done in three of the
last five weeks. *(One conflict noted and unresolved: a changelog entry describes a new Stocky
purchase-orders extension, while a vendor blog says Stocky shuts down in August 2026.)*

---

## This week's validated ideas

| ID | Idea | D | W | F | M | Composite | Evidence (Mode B — search result text only) |
|----|------|---|---|---|---|-----------|---------------------------------------------|
| 023 | Job-costing / project-profitability layer for Wave accounting | 3 | 3 | 2 | 2 | **10** | **Recorded as a negative finding.** Domain 1 — `community.waveapps.com`, verbatim Wave staff refusals: *"this looks great but at this time we have no plans to add those features to wave as most of our customers dont require such features"* (project accounting), *"Adding recurring bills isn't currently on our roadmap"*, *"There are currently no plans to implement"* (cash-flow forecasting). Domain 2 — [techrepublic.com](https://www.techrepublic.com/article/wave-accounting-review/) and [work-management.org](https://work-management.org/accounting/wave-review/): *"Wave has no job costing or class tracking, so businesses that need to track profitability by project, location, or department hit a wall quickly"*, and *"Wave doesn't offer any native integrations with third-party apps"* — the only app it syncs with is Wave Payroll. **Feasibility 2 kills it: the public API cannot do the job.** Wave's GraphQL API is invoice-centric; per three integration-vendor sources you **cannot read any report, post journal entries, create or pay bills, or query transaction history** (money transactions in beta), and since **26 May 2025 third-party apps require the connected business to hold a Wave Pro subscription**. Monetization 2: the remedy every source recommends is *leave Wave for QuickBooks*. |

Only one idea cleared the bar this week. Per the brief, fewer and honest beats padded: eight
further candidates were researched and killed, listed in `research-log.md`.

---

## Backlog re-scores (the week's real output)

| ID | Change | Why |
|----|--------|-----|
| 003 | W 2→1, **13 → 12**, door closed | The single Mode-A-gated fact that ID 003's deep dive turned on — does Craftybase already ship lot→customer reverse traceability — **resolved against it in one query**. Craftybase result text: it can *"show you exactly which batches, orders, and customers are impacted"* and *"identify which order was shipped a product manufactured using a specific lot number"* ([craftybase.com/lot-tracking-software](https://craftybase.com/lot-tracking-software), [help.craftybase.com/article/1174](https://help.craftybase.com/article/1174-introduction-to-traceability)). The only wedge the evidence supported is gone. Flat do-not-build. |
| 021 | W 2→1, **13 → 12** | Week 8's gate ("revisit only if the sub-$50 single-producer tier is genuinely empty") resolved against it. **Insurstein** is described doing the exact MVP — *"import statements, auto-match to policies, spot missing commissions, and calculate producer splits by carrier and line of business"* — and **AgencyComp** markets precisely the intended wedge: *"affordable… for insurance agents and brokerage general agents that does not require you to purchase an expensive CRM"*, three plans, no long-term contracts. The $59–72 floor was also reconfirmed on a second domain (CommissionTrac $60/mo; Commission Tracker $72/mo small agency; AgencyBloc Standard $59/user/mo). |
| 022 | W 3→1, **13 → 11** | Both halves of last week's conditional-NO failed. The demand test (a contractor asking for *audit-prep software*) returned nothing in two query shapes. And the "no dedicated competitor exists" finding — which week 9 already flagged as a yellow flag — was wrong: **[workerscompauditprep.com](https://www.workerscompauditprep.com/products/construction-audit-prep-kit)** sells a Construction Audit Prep Kit (payroll reconciliation, COI tracking, packet index) **plus an Audit Packet Builder subscription** that uploads files, extracts values and generates the packet. That is the ID 022 MVP, already shipped. Price not surfaced. |
| 007 | W 3→2, **12 → 11** | Two problems. The buyer is largely **statutorily exempt**: Oregon exempts producers at ≤$5M global revenue, Colorado under $5M, California under $1M in-state (exemption applications were due to CalRecycle 1 Jun 2026). And the cheap tier is occupied inside the intended distribution channel — **EPR Insights is a Shopify app at $15/mo Basic, $29/mo Advanced** ([apps.shopify.com/epr-insights](https://apps.shopify.com/epr-insights)); **Repax starts free**, Growth €29/mo. The remaining money is in *fee-pathway optimisation* (rePurpose reports saving low-volume clients ~$3,750, one brand paying $360 instead of $4,400) — which is consulting, i.e. week 5's service-not-software kill. |
| 017 | No score change (**15**), evidence upgraded | Week 8's caveat was that Demand 5 rested on three conversion-vendor blogs. Intuit's own domain now carries it: Price Levels *"is not an available feature in QuickBooks Online"*, the official workaround is duplicating items, and **Price Rules is Plus/Advanced-only, not Essentials or Simple Start** ([/00/1270959](https://quickbooks.intuit.com/learn-support/en-uk/do-more-with-quickbooks/can-you-use-a-price-level-list-for-products-on-qb-online-like/00/1270959), [/00/492598](https://quickbooks.intuit.com/learn-support/en-us/reports-and-accounting/can-i-add-price-levels-for-different-customers-on-quickbooks/00/492598), [L5jI9VwXt](https://quickbooks.intuit.com/learn-support/en-us/help-article/mobile-apps/set-price-rules-quickbooks-online/L5jI9VwXt_US_en_US)). Status: Strengthened. |

---

## Top-10 backlog snapshot (after this week's re-scores)

| Rank | ID | Idea | Composite | Status |
|------|----|------|-----------|--------|
| 1 | 001 | Honest accessibility scan + fix pack, small e-commerce | 16 | Deep-Dived |
| 2 | 017 | Customer price lists bridge for QBO + Xero | 15 | Strengthened |
| 3 | 018 | Sub-$50 quoting calculator, 1–5 person job shops | 14 | Deep-Dived |
| 4 | 010 | Prop 65 warning audit + determination register | 14 | Deep-Dived |
| 5 | 012 | Google review disappearance archive + appeal pack | 13 | Deep-Dived |
| 6 | 006 | Auto-renewal cancel-flow monitoring + evidence archive | 13 | Deep-Dived |
| 7 | 020 | CAM / NNN reconciliation, small commercial landlords | 13 | Do-not-build |
| 8 | 003 | Small-batch maker COGS / batch tracker | 12 | Re-scored down |
| 9 | 011 | Supplier PO chasing, small Shopify brands | 12 | **Deep-Dived** |
| 10 | 021 | Carrier commission reconciliation, small agencies | 12 | Re-scored down |

---

## Risks and watch-outs

1. **The backlog's top is now fully deep-dived.** No non-deep-dived row sits above 13, and the
   single 13 (ID 020) is a confirmed do-not-build. Next week either finds a new row clearing 13
   or the deep-dive slot should go to **re-validating ID 001 (16)**, whose deep dive is eight
   weeks old and whose evidence has never been re-checked.
2. **Eleven of this backlog's kills are now "gap already filled"; still none is "nobody would
   have paid."** Week 8's tie-break rule (whitespace breaks composite ties) keeps being
   vindicated. Four of this week's five re-scores were whitespace cuts.
3. **Absence of a competitor remains a yellow flag, and ID 022 proves it twice over.** Week 9
   recorded "no dedicated competitor found" as a warning rather than an opening; this week the
   competitor turned up. The correct reading of an empty cheap-tier check is *search harder*,
   not *build*.
4. **Vendor-SEO contamination, fifth consecutive week.** Every Wave API limitation above comes
   from integration vendors (Knit, Merge, Apideck, ClonePartner); every EPR fee figure comes
   from parties selling EPR services. Directionally useful, individually unverified.
5. **No income or profit claim is made anywhere in this document.** Every price and quotation
   above appeared in search result text this run and is linked to its source.

*Evidence mode B throughout: search result text only. No page was fetched or read in full.*
