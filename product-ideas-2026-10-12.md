# Product Ideas — Week of 2026-10-12 (Week 13)

## Executive summary

- **Evidence mode: B** (WebFetch UNAVAILABLE — thirteenth consecutive run). Step 0 failed *differently* this week:
  both control URLs returned `getaddrinfo ENOTFOUND` (DNS failure) rather than weeks 11–12's named
  `EGRESS_BLOCKED` proxy refusal. Same outcome, different mechanism. No retries, no curl.
- **Zero new validated ideas — third consecutive zero.** One vein was worked properly and closed hard: Xero
  invoice subtotals/grouping carried the **best raw demand signal this project has ever seen** (353 votes, vendor
  refusal, five clustered open requests) and died at a **$7.50/month incumbent**.
- **The top of the backlog came down.** ID 017 re-scored **15 → 14** (whitespace 3 → 2): a Xero App Store app
  (Qoblex) does offer per-customer price lists, and this week independently proved that user "I searched the app
  store and found nothing" claims are unreliable. ID 012 re-scored **13 → 12** (feasibility 3 → 2).
- **ID 006 strengthened on a materially expanded forcing function, and its composite still did not move** — the
  thirteenth straight week with zero upward composite revisions. It takes the deep-dive slot as a re-dive.
- **Methodological finding worth more than this week's ideas:** compound `site:A OR site:B` queries fail
  systematically under Mode B; single-`site:` queries worked perfectly in the same run.

---

## Deep Dive of the Week — ID 006: Auto-renewal ("click-to-cancel") cancel-flow compliance monitor + evidence archive

**Why this slot — a stated deviation.** The highest never-Deep-Dived row is **ID 021 (12)**, which week 12's
pre-dive check killed outright (verdict NO; AgencyComp at $39.95/mo occupies the tier). It is **marked Deep-Dived
this week** to close it out rather than manufacture a build plan for a dead idea. The depth goes to **ID 006** —
the only row at 13 carrying neither a NO verdict nor whitespace 1, and whose 2026-08-03 dive predates every dated
obligation below. Same handling as week 12's ID 017 re-dive; sixth week running the pre-dive check moved the target.

**What changed since the 2026-08-03 dive.** That dive rested on California AB 2863 and the vacated FTC rule. The
live map is now far larger, and every date below postdates it:

| Jurisdiction | Obligation | Effective |
|---|---|---|
| **New York City** | Cancel as easily as signup, same medium; no reason-survey before cancelling | **1 Oct 2026** |
| Virginia | Conspicuous online cancel; cancel as easy as signup | 1 Jul 2026 |
| Maryland | Alternative cancel path for consumers who can't cancel online | 1 Jun 2026 |
| Colorado (SB25-145) | One-step online cancel — **extended to B2B subscriptions** | 16 Feb 2026 |
| Maine | Separate consent to auto-renewal | 1 Jan 2026 |
| Louisiana | New regulatory requirements | Summer 2026 |
| FTC | Rulemaking **restarted** (ANPR 13 Mar 2026, comments closed 13 Apr 2026) | pending |

NYC is the sharpest instrument: **DCWP enforces**, penalties escalate **$525 / $1,050 / $3,500 per violation**,
restitution covers amounts charged after a consumer's first cancellation attempt, each omission may be a
**separate** violation, and the city opened a **public complaint portal** on day one
([nyc.gov](https://www.nyc.gov/main/click-to-cancel),
[Kelley Drye](https://www.kelleydrye.com/viewpoints/blogs/ad-law-access/summer-2026-autorenewal-roundup-nyc-and-louisiana-enact-new-regulatory-requirements),
[Mondaq](https://www.mondaq.com/unitedstates/consumer-law/1852544/nycs-click-to-cancel-rule-is-now-in-effect-what-subscription-businesses-need-to-know)).
The product thesis is stated by the sources themselves: **"a cancel flow that satisfies one state can breach
another"** ([Churnkey](https://churnkey.co/guides/state-automatic-renewal-laws),
[Zwillgen](https://www.zwillgen.com/general/subscription-state-law-patchwork-evolves-expands/)).

**MVP — 4 features, deliberately no legal engine**

1. **Jurisdiction rule table** — the ~10 live states plus NYC as a hand-maintained checklist keyed to (where the
   customer lives) × (how they signed up). Plain JSON, edited by hand.
2. **Guided self-audit** — the merchant walks their own cancel path, answers prompts, uploads screenshots; the
   tool names which jurisdiction each step fails. **Merchant-captured, not crawled.**
3. **Dated evidence archive** — timestamped screenshots plus a PDF of the signup disclosure and cancel path,
   re-captured quarterly. This is the recurring product, and the only asset worth anything when a complaint lands
   months later.
4. **Response packet generator** — one PDF: what the flow looked like on date X, which rule it satisfied.

**Stack:** Next.js on Vercel; Supabase Postgres for the rule table and audit records; Cloudflare R2 for the
archive; `pdf-lib` for packets; Stripe Billing; Resend for re-audit nudges. No scraper, no queue, no browser
automation in v1 — which is what keeps it inside this builder's reach.

**First acquisition channel.** Explicitly **not** merchant forums — the absence of merchant voices there is this
idea's central problem, not an untapped channel. Go to the subscription-app ecosystems whose merchants *are* the
covered population: **Loop already publishes an ARL compliance explainer**
([help.loopwork.co](https://help.loopwork.co/en/articles/12708349-united-states-automatic-renewal-laws-requirements-loop-compliance)),
making it a partner surface rather than a competitor. Same for Skio and Recharge agency networks.

**Benchmarked price: $39/month**, with the one-off audit sold first at $149. Anchors actually seen:
**RenewalTracker $49/mo Basic** (closest published adjacent tool,
[Capterra](https://www.capterra.com/p/10037627/RenewalTracker/)); **ProsperStack from $200/mo per 500 cancellation
sessions** (on file, a churn tool not a compliance monitor); and this week's Flippa anchors of
**≈$41/subscriber/month** ($17,753 MRR / 430 subscribers, [flippa.com/13365450](https://flippa.com/13365450)) and
≈$50/sub/mo from week 12. One third-strike NYC violation ($3,500) is roughly seven years of subscription.

**The single biggest risk — demand, not build.** Ten weeks and now **two independent dedicated attempts** have
failed to surface **a single merchant or founder voice** asking for this. Every source on file is a law firm, a
compliance vendor, or an enforcement action; this week's targeted query for founder "we had to rebuild our cancel
flow" stories returned **zero** HN or Indie Hackers threads. Separately, a direct search for cancel-flow
compliance auditors **found no vendor selling one at any price**. Both facts point the same way, and the brief's
yellow-flag rule applies: nobody sells it may mean nobody buys it. The buyer is compelled in theory but has never
been observed *shopping*. **Mitigation: sell the $149 one-off audit to ten merchants before building the
monitoring half.** If the audit will not sell, the subscription never would have.

---

## This week's candidate ideas

**No idea cleared the evidence bar this week.** One vein was worked to a conclusion and is reported as a
negative finding rather than padded into a row:

| Candidate | Demand evidence found | Why it did NOT earn a row |
|---|---|---|
| **Xero invoice subtotals / line-item grouping** | **The strongest raw demand signal in 13 weeks.** [Invoices — Add subtotals](https://productideas.xero.com/forums/967115-invoices-quotes/suggestions/44960377-invoices-add-subtotals): **353 votes**, status **"Not in pipeline"**, Xero community manager responding **13 Apr 2026** that the team has heard strong demand but will not commit — Xero's own words are *"no foreseeable plans for developing the ability to add subtotals in invoices."* **Four further clustered open requests** ([combine/hide lines](https://productideas.xero.com/forums/967115-invoices-quotes/suggestions/44960341-sales-invoices-combine-and-hide-line-items-for-c), [blank lines to group](https://productideas.xero.com/forums/967115-invoices-quotes/suggestions/47734688-invoicing-allow-blank-lines-to-make-groups-of-in), [group items](https://productideas.xero.com/forums/967139-purchase-orders-bills-inventory/suggestions/45215815-products-services-ability-to-group-items), [hide cost on quotes](https://productideas.xero.com/forums/967115-invoices-quotes/suggestions/46074502-quotes-hide-line-item-cost)). Xero's own workaround is *recurring* labour — type the maths into description-only lines, or **"export the invoice as a PDF and edit it externally"** — so it survives the free-workaround screen. | **RULED OUT at the cheap-tier check. [invoicepolish.com](https://invoicepolish.com/) — "Clean, Grouped Invoices for Xero"** — a dedicated incumbent doing exactly this: **Basic $90/yr (≈$7.50/mo**, 1 org, 40 invoices/mo), **Professional $268/yr (≈$22.33/mo**, 3 orgs, 200/mo), extra orgs $5–6/mo, 7-day trial, no card. **The cheapest incumbent this project has ever found.** Whitespace 1. Do not revisit. |

---

## Top-10 backlog snapshot (after this week's re-scores)

| # | ID | Idea | Composite | Status |
|---|----|------|-----------|--------|
| 1 | 017 | Customer-specific price lists bridge (QBO + Xero) | **14** ↓ | Re-scored down; Deep-Dived ×2 |
| 2 | 001 | Honest accessibility scan + fix pack for small e-commerce | 13 | Deep-Dived |
| 3 | 020 | CAM / NNN reconciliation for small commercial landlords | 13 | Deep-Dived — verdict NO |
| 4 | 006 | Auto-renewal cancel-flow monitoring + evidence archive | 13 | **Strengthened; Re-Deep-Dived** |
| 5 | 012 | Google review disappearance archive + appeal pack | **12** ↓ | Re-scored down; Deep-Dived |
| 6 | 010 | Prop 65 warning audit + per-SKU register | 12 | Closed |
| 7 | 018 | Sub-$50 quoting calculator for tiny machine shops | 12 | Deep-Dived |
| 8 | 021 | Carrier commission reconciliation (small insurance agencies) | 12 | **Deep-Dived — verdict NO, closed** |
| 9 | 003 | Small-batch maker COGS / batch-cost tracker | 12 | Deep-Dived |
| 10 | 011 | Supplier PO chasing for small e-commerce brands | 12 | Deep-Dived — verdict NO |

---

## Risks and watch-outs

- **Thirteen weeks, still zero upward composite revisions.** A settled prior, not an observation: every score
  that has ever moved in this project moved **down**. The screens are working, but the backlog is being pruned
  faster than replenished, and **nothing above 14 exists**.
- **The absence claim is now demonstrably unsafe, and it was load-bearing for ID 017.** InvoicePolish — a live
  $90/yr product in exactly its niche — stayed invisible across **four** queries before one topical query
  surfaced it. If this project's own targeted searching can miss that, a Xero user's casual *"I have been through
  the app store and cannot find an app"* carries little weight. ID 017's whitespace was cut accordingly, and
  should not be raised again on absence evidence alone.
- **ID 012's blocker is a human gate, not a code problem, and it got worse.** GBP API access is approved **per
  GCP project** (approval does not transfer), rejects API keys (OAuth 2.0 only), needs a verified profile active
  60+ days, and *"rejections are common for vague or thin applications"* — reported waits of 4 days to 6 weeks
  against a stated 7–10 business days. A developer reports the reviews endpoint still returning
  `PERMISSION_DENIED` — *"Service mybusiness.googleapis.com is not available to this consumer"* — with a possible
  **separate allowlist** unresolved
  ([discuss.google.dev](https://discuss.google.dev/t/business-profile-api-reviews-endpoint-mybusiness-googleapis-com-cant-be-enabled-basic-access-pending-10-business-days/389462),
  [mapsleads.co](https://www.mapsleads.co/blog/google-business-profile-api-quotas-limits),
  [xovionlabs.com](https://xovionlabs.com/blog/google-business-profile-api-hidden-gate/)). For a non-coder this is
  close to a hard stop. Feasibility 3 → 2.
- **Flippa/Acquire figures are asking prices and seller claims**, never verified earnings — use them only as
  willingness-to-pay anchors, which is how they are used above.
- **Mode B has been the only mode for 13 straight runs** and is carrying the work — this week's two best findings
  (a 353-vote vendor refusal, and a $90/yr competitor's full price card) both came through it cleanly. Prices are
  not the bottleneck; **self-qualified demand statements are**, which is exactly what the unreachable hosts supply.
