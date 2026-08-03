# Product Ideas — Week of 2026-08-03

## Executive summary

- **Evidence mode: B** (third consecutive run). STEP 0 control fetches were re-run fresh:
  `https://example.com` → **HTTP 403**, `https://en.wikipedia.org/wiki/Main_Page` → **HTTP 403**.
  The egress block is now firmly persistent, not intermittent. No page was opened this week.
- **Methodological breakthrough: Shopify App Store review text *is* reachable through WebSearch.**
  Week 2 concluded 1-star review text was unreachable — that was true for the Chrome Web Store,
  but `apps.shopify.com/...\/reviews` pages surface verbatim merchant complaints in result text.
  This produced the strongest primary-source quotes in three runs, including exact dollar figures.
- **Four new ideas cleared the Mode B bar** (IDs 006–009), scoring 11–13. **None beats ID 001's 16.**
  Three of the four are recorded specifically because their whitespace is poor — the rows exist so
  week 4 does not re-research crowded ground.
- **Deep Dive of the Week: ID 006 — auto-renewal law ("click-to-cancel") flow monitoring.** Tied at
  composite 13 with ID 003, tie broken toward 006 because 003's own backlog note says its category
  is crowded and should not be pursued.
- **Honest caveat:** the regulatory vein keeps producing ideas whose demand evidence is enforcement
  actions and law-firm alerts, never a user saying "I need this." Every such idea is capped at
  Demand 3 for consistency with ID 002. Real merchant complaint text (IDs 008, 009) scored higher
  on demand but worse on whitespace. Nothing this week is a clear buy.

---

## Deep Dive of the Week — ID 006: ARL cancel-flow monitoring & evidence archive

**The forcing function.** The FTC's federal click-to-cancel rule was vacated by the Eighth Circuit in
July 2025, so obligations now come state by state — and they attach to *where the customer lives, not
where the company sits* ([Traverse Legal](https://www.traverselegal.com/blog/automatic-renewal-law-compliance-subscriptions/)).
California's AB 2863 took effect 1 July 2025 and requires cancellation in the *same medium* used to
sign up ([ProsperStack](https://prosperstack.com/blog/california-automatic-renewal-law/),
[Davis Wright Tremaine](https://www.dwt.com/insights/2024/10/ab-2863-updates-california-automatic-renewal-law)).
The money is real and already moving: settlements of **$4.7M (JustAnswer), $2.3M (New York Times),
$2.3M (Potpourri)**, with actions pending against HelloFresh, UFC and NBC (ProsperStack, via
[Capterra](https://www.capterra.com/p/204618/ProsperStack/)).

**The gap.** The advice everyone gives is manual: *"Map out every step a customer takes from clicking
cancel to confirmation, count the clicks, compare it to your sign-up flow"*
([toslawyer.com](https://toslawyer.com/auto-renewal-and-subscription-compliance-what-saas-and-e-commerce-companies-must-fix-in-2026/)).
Nobody sells *continuous* verification. A flow audited in March silently breaks when the theme,
checkout or portal changes in June — and the merchant finds out via a demand letter.

**MVP (5 features).**
1. **Flow walker** — merchant supplies signup + cancel URLs and test credentials; a headless browser
   walks both paths, screenshotting every step and counting clicks-to-cancel vs clicks-to-subscribe.
2. **State rules matrix** — CA / NY / MN / VA checks: renewal-terms disclosure present and *proximate*
   to the purchase button, no pre-checked consent boxes, same-medium cancellation available, advance
   renewal reminder for annual terms.
3. **Findings report** — per-state pass/fail with the screenshot that proves each finding, plus
   ready-to-paste remediation copy blocks.
4. **Weekly re-run + drift alerts** — diffs against the last run and emails the merchant when a site
   change breaks a previously-passing disclosure. *This is the actual product; the audit is the demo.*
5. **Evidence archive** — timestamped, exportable PDF history. The artifact counsel wants on day one
   of a demand letter.

**Stack Claude would build it with.** Next.js on Vercel for the app; Playwright on a scheduled
container (Fly.io or Railway) for the flow walk; Supabase Postgres + object storage for screenshots
and run history; Stripe for billing; Resend for alerts. The Claude API reads each captured step's text
and judges disclosure presence and proximity against a per-state rules prompt — that is the defensible
AI angle: rules plus dated evidence, not a chat box.

**First acquisition channel.** Publish a free public *ARL scorecard* rating the cancel flows of 30
well-known consumer subscription brands, with screenshots. It is link-bait aimed precisely at the
subscription-ops and in-house-counsel readers who buy, and it doubles as a live product demo. Second
channel: referral relationships with the subscription-law practices already publishing on ARL
(Traverse Legal, toslawyer) — they want the monitoring layer they cannot staff.

**Benchmarked price point.** ProsperStack — the adjacent incumbent — starts at **$200/mo for up to 500
cancellation sessions** ([Capterra](https://www.capterra.com/p/204618/ProsperStack/)), and it is a
churn-deflection tool, not a compliance monitor. Commodity compliance scanners sit at $10–30/mo
(CookieYes from $10/mo, CookieScript $6.99/mo). Position at **$49/mo single brand / $149/mo agency
(5–10 brands)** — clearly under the ProsperStack floor, clearly above scanner-commodity pricing.

**Single biggest risk — over-claiming.** ProsperStack already gives a **free compliance audit** away as
a lead magnet, which caps what a one-off audit can ever charge, and a law-firm review is what a nervous
GC actually buys. That pushes the product toward monitoring, where the real trap lives: this tool can
honestly claim only *"we detect and document these specific flow attributes on these dates."* Claiming
"ARL compliant" would be a deceptive-claims exposure in its own right — the identical trap that cost
accessiBe a $1M FTC penalty in the ID 001 research. The marketing copy is the risk surface, not the code.

---

## This week's validated ideas

| ID | Idea | D | W | F | M | Comp | Key evidence (Mode B — result text, no page opened) |
|----|------|---|---|---|---|------|------------------------------------------------------|
| 006 | ARL / click-to-cancel flow monitoring + evidence archive | 3 | 3 | 4 | 3 | **13** | Settlements $4.7M JustAnswer / $2.3M NYT / $2.3M Potpourri; pending vs HelloFresh, UFC, NBC. ProsperStack from **$200/mo per 500 sessions** — churn tool, not compliance. [Skio](https://help.skio.com/docs/complying-with-california-new-york-state-ftc-clicktocancel-rules) ships a merchant-facing ARL doc. |
| 007 | US state packaging-EPR reporting assistant for small brands | 3 | 3 | 3 | 3 | **12** | CA SB 54 effective 1 May 2026; registration deadline 1 Jun 2026; **5,700+ producers**; penalties **to $50,000/day**; program start 1 Jan 2027 ([Mayer Brown](https://www.mayerbrown.com/en/insights/publications/2026/06/californias-sb-54-epr-regulations-take-effect-key-deadlines-and-compliance-obligations-for-producers)). Pathway choice is worth real money: one brand **paid $360 instead of $4,400** ([Ecoveritas](https://www.ecoveritas.com/powerful-epr-software)). Vendor pricing is not public. |
| 009 | Sub-$50 inventory forecasting for small Shopify stores | 4 | 2 | 3 | 3 | **12** | Verbatim merchant reviews: *"the best app for inventory forecasting I found on Shopify by far (I tested them all), but unfortunately it's extremely expensive… it became so expensive that it put the app out of the question for us"*; *"Held hostage on a 12 month contract… was paying about $300/month and they jacked it up over $600/month"* ([Inventory Planner reviews](https://reputon.com/shopify/apps/inventory-management/inventory-planner)). **But the gap is already filled** — [Godfrey](https://apps.shopify.com/godfrey) from $10/mo, Prediko from $49/mo. |
| 008 | Shopify app-subscription spend auditor | 3 | 2 | 4 | 2 | **11** | Loud merchant forum threads: *"Apps Have Become Worse Than the Mafia"*, *"The Price of Apps is Completely Out of Control"* ([Shopify Community](https://community.shopify.com/t/apps-have-become-worse-than-the-mafia/388157)); merchants describe reaching **~$400/mo on plugins**. **Counter-evidence that sinks it: only 1.8% of stores spend over $100/mo on apps** ([Eightx](https://eightx.co/blog/shopify-app-bloat-report-2026)) — the complaints are loud but the paying pool is thin, and the technical half is taken (ScriptSweep, Store Health, Store Auditor). |

D = Demand · W = Whitespace · F = AI-Build Feasibility · M = Monetization Clarity

---

## Backlog snapshot — top 10 (all 9 active ideas)

| Rank | ID | Idea | Composite | Status |
|------|-----|------|-----------|--------|
| 1 | 001 | Honest accessibility scan + fix pack for small e-commerce | 16 | Deep-Dived |
| 2 | 003 | Small-batch maker COGS / batch-cost tracker | 13 | New (category crowded — do not pursue) |
| 2 | 006 | ARL / click-to-cancel flow monitoring | 13 | **Deep-Dived (this week)** |
| 4 | 002 | EU AI Act Art. 50 transparency kit for SMEs | 12 | New |
| 4 | 007 | US state packaging-EPR reporting assistant | 12 | New |
| 4 | 009 | Sub-$50 Shopify inventory forecasting | 12 | New |
| 7 | 004 | SMB-priced AI-visibility / AEO tracking | 11 | New (deprioritized) |
| 7 | 008 | Shopify app-spend auditor | 11 | New |
| 9 | 005 | Etsy bulk-edit tool | 10 | Retired |

Nothing is old enough to mark Stale (the backlog is three days old).

---

## Risks and watch-outs

- **Three runs, zero pages read.** Every score in this backlog rests on search-result text. Where a
  claim is a real merchant quote it is quoted verbatim above; where it is a law-firm summary, treat it
  as background, not demand. This is why no idea this week scored above 13.
- **The regulatory vein has a ceiling.** It reliably surfaces deadlines, fines and price anchors, and
  it produced the only 16 in the backlog — but it never produces a person saying they want to buy
  something. Ideas 002, 006 and 007 all sit at Demand 3 for exactly this reason.
- **Whitespace is closing faster than gaps open.** ID 004 (AI visibility) and now ID 009 (inventory
  forecasting) both show the same pattern: a real price chasm that a cheap competitor had already
  filled by the time it was found. Assume any obvious "too expensive" complaint is already being
  arbitraged; check the cheap tier *before* scoring demand.
- **Free lead-magnet audits cap audit pricing.** ProsperStack gives an ARL audit away free. Any
  audit-shaped product should assume the audit itself is worth $0 and must monetize the recurring
  layer.
- **Over-claiming is the recurring failure mode.** ID 001 and ID 006 are both compliance-adjacent
  scanners where the legally dangerous surface is the marketing copy, not the software.
- No income or profit claim is made anywhere above; every price and figure traces to a linked source
  seen in search-result text this session.
