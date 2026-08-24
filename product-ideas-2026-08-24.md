# Product Ideas — Week of 2026-08-24

## Executive summary

- **Evidence mode: B** (WebFetch blocked for the **sixth consecutive run** — `EGRESS_BLOCKED` on both
  control URLs, identical structured envelope to weeks 4 and 5). No page has been read in six weeks.
- **Three ideas cleared the evidence bar against a 4–6 target, and all three are negative-leaning**
  (composites 11–12). Reported as three rather than padded to hit the target. This is the weakest
  *idea* week of the project — and the first week where every new row is a "do not build".
- **The week's real output is two channels and one closed lead.** `contractortalk.com` is confirmed as
  a deeply-indexed practitioner forum, opening the construction/home-services vertical that five prior
  weeks never touched. Public feature-request boards (`ideas.gohighlevel.com`, Canny) are indexed at
  the individual-request level — a genuinely new evidence class, but Mode-A-only. And the parked
  **Amazon FBA fee-change** lead is now resolved — as a kill.
- **Six kills at the pre-scoring check**: TTB COLA label pre-check, MoCRA cosmetics registration,
  short-term-rental permit renewal, Medicare call-recording retention, LSA lead disputes, and the
  Google/LSA agency suspension vein.
- **Deep dive: ID 003** (small-batch maker COGS tracker, composite 13). It is the highest-scoring
  non-deep-dived row, and the verdict is **conditional-no** — the deep dive below identifies the only
  wedge the evidence supports and names the one question that must be answered before any build.

---

## Deep Dive of the Week — ID 003, small-batch maker COGS / batch-cost tracker

Highest composite (13) not yet Deep-Dived. It ties with ID 011 (supplier PO chasing); the tie breaks
toward 003 because 011's note is a flat "do not build" with added platform risk (Shopify shipped native
purchase orders), whereas 003's leaves one door open: *"only a sharply differentiated wedge would
justify revisiting."* This deep dive tests whether that wedge exists. **It concludes that it probably
does not, and states the single check that would settle it.**

**The evidence, restated.** The Show HN author of *Craftplan* built his own because existing tools were
*"expensive, too generic, or both"*, and the Soapmaking Forum carries a standing *"Inventory and batch
tracking software"* thread. Demand was never the problem — it is that Craftybase (from $20/mo per its
own pricing page; one source said $49/mo Studio, **conflict still unresolved under Mode B**), Inventora
(free / $19 / $39), SoapMaker 3 (desktop, one-time) and Craftplan itself (free, open-source) occupy
every price point including zero.

**The only wedge the evidence supports** is the "too generic" half of that quote, not the "expensive"
half — a free tier makes price un-winnable. So: not a better general COGS tracker, but a **single-craft
batch record with lot→order traceability** — every finished unit carries a lot code, and the tool
answers backwards, "which customers received lot 2026-114?" A recall workflow, not an accounting one.

**MVP feature list (4 features):**
1. Recipe/formula version history with per-version unit cost, recalculated when an ingredient price changes.
2. Batch creation that consumes ingredient lots and mints an output lot code.
3. Lot → order linkage: assign lot codes at fulfilment, then reverse-lookup every order containing a lot.
4. One-page printable batch record (inputs, lots, yield, date, maker) as a PDF archive.

**Tech stack Claude would build it with:** Next.js on Vercel, Postgres via Supabase (relational
lot-genealogy is the whole product — do not use a spreadsheet-shaped store), Supabase Auth, Stripe
Billing, and a single Shopify/Etsy order-import job. No queues, no ML, no infrastructure. This is
comfortably inside a non-coder-plus-Claude scope; feasibility 4 stands.

**First acquisition channel:** the Soapmaking Forum thread that produced the original evidence, plus
maker Facebook groups — build-in-public, not ads. Etsy seller communities remain a valid *acquisition*
channel even though week 5 ruled Etsy dead as a *research* channel.

**Benchmarked price point: $15–19/mo** — below Craftybase's from-$20 entry, at or under Inventora's $19
tier. No room above that, and nothing to charge against a free open-source alternative except focus.

**The single biggest risk — and it is a go/no-go, not a caveat:** the wedge may already ship inside
Craftybase. Batch tracking is in its name; whether it does *lot → customer order* reverse traceability
is exactly the fact Mode B cannot establish, because it requires reading a feature page. **Do not write
a line of code before that page is read under Mode A.** If Craftybase has it, this idea is dead and the
backlog's existing "do not re-research" verdict stands unchanged.

Secondary risk: a related check this week weakened the regulatory tailwind a wedge like this might have
leaned on. MoCRA exempts businesses under $1M average annual cosmetic sales, and true soap is excluded
from FDA product listing entirely (regulated by CPSC instead) — so "you need this for FDA compliance"
is **not** an available claim for the soap segment. Marketing it as one would repeat the accessiBe
error catalogued under ID 001.

---

## This week's validated ideas

| ID | Idea | D | W | F | M | Composite | Evidence (Mode B — snippets, no page read) |
|----|------|---|---|---|---|-----------|--------------------------------------------|
| 014 | Subcontractor compliance-document expiry tracking (COIs + trade certs) for small GCs | 3 | 2 | 4 | 3 | **12** | [contractortalk.com](https://www.contractortalk.com/threads/software-for-managing-subcontractor-certs-of-insurance-associated-sub-data.264865/) — *"Software for managing Subcontractor Certs of Insurance & associated sub data"*; result text carries a specific failure (a sub's supervisor RRP certificates expired because *"the company renewed but the supervisors didn't take renewal courses"*) and a feature request: flag expiring dates, track X-Mod, OSHA 300A, incident rates. Second domain, price detail: myCOI ~**$200–400/mo** with a **200-certificate minimum**, self-service **$3–10/vendor/year**, TrustLayer a **free Starter tier** ([billyforinsurance.com](https://billyforinsurance.com/resources/billy-vs-jones-vs-trustlayer-vs-mycoi-coi-tracking-software/), [illumend.ai](https://www.illumend.ai/evaluation-buying/the-7-best-software-options-for-contractor-insurance-compliance-in-2026)). **Caveat: that pricing domain is a competitor comparing itself to rivals.** Whitespace 2 — a free tier already exists. |
| 015 | Per-ASIN Amazon FBA fee-change detection | 4 | 1 | 3 | 3 | **11** | **Resolves the week-5 parked lead — as a kill.** TheStreet: *"Amazon quietly introduces new fee sellers didn't see coming"*; [sellerlabs.com](https://www.sellerlabs.com/blog/amazon-fba-fees-2026-margin-impact/): *"most sellers are paying 8-10% more in fees, not the 0.5% Amazon announced"*, and the mechanism — Amazon *"does not send per-ASIN notifications when your specific product is reclassified… no email, no Seller Central notice per listing"*; plus a `community.ebay.com` thread *"Again rising the fees without even email warning"*. **Whitespace 1**: [Bindwise](https://bindwise.threecolts.com/alerts/track-fba-fee-overcharge) and [SentryKit](https://sentrykit.com/alerts/fba-fee-change-alert/) sell exactly this, plus tool4seller and ylishi.tools. |
| 016 | Certified payroll / prevailing-wage reporting for small subcontractors | 3 | 2 | 2 | 4 | **11** | [contractortalk.com](https://www.contractortalk.com/threads/prevailing-wage-davis-bacon-act-california.43576/) prevailing-wage threads: contractors certify payroll every two weeks, are audited at project end, and *"if an error is made, they will be fined with no exceptions."* Price chasm in a second domain: entry tools near **$49–50/mo**; Points North/LCPtracker/eBacon quote-based at ~**$175–300/mo with $995–$4,995 setup**; managed service **$1,000–5,000/mo** ([certifiedpayrollpro.com](https://www.certifiedpayrollpro.com/blog/ebacon-reviews-pricing-2026)) — **also vendor SEO.** **Feasibility 2**: state-specific forms, fringe-benefit math, mandated uploads into LCPtracker/DIR eCPR portals. The $49 tier holds the bottom. |

Demand evidence here is thread-title and result-text level. Nothing was read. No idea this week is a
build recommendation.

---

## Top-10 backlog snapshot

| Rank | ID | Idea | Composite | Status |
|------|-----|------|-----------|--------|
| 1 | 001 | Honest accessibility scan + fix pack for small e-commerce | 16 | Deep-Dived |
| 2 | 010 | Prop 65 warning audit + determination register | 14 | Deep-Dived |
| 3 | 012 | Google review disappearance archive + appeal pack | 13 | Deep-Dived |
| 4 | 006 | Auto-renewal / click-to-cancel flow monitoring | 13 | Deep-Dived |
| 5 | 003 | Small-batch maker COGS / batch-cost tracker | 13 | **Deep-Dived (this week)** |
| 6 | 011 | Supplier PO chasing for small e-commerce | 13 | New (do not build) |
| 7 | 002 | EU AI Act Art. 50 transparency kit | 12 | New |
| 8 | 007 | US state packaging-EPR reporting assistant | 12 | New |
| 9 | 009 | Sub-$50 Shopify inventory forecasting | 12 | New (do not build) |
| 10 | 014 | Subcontractor compliance-document expiry tracking | 12 | New (this week) |

**First Stale marks of the project**, as week 5 predicted: IDs **004** (11), **005** (10) and **008**
(11) have all passed three weeks below composite 12.

---

## Risks and watch-outs

1. **Six runs, zero pages read.** Every composite in this backlog rests on search-result text. The
   brief's preferred bar has been unmeetable since week 1 — now the project's dominant risk.
2. **The backlog is converging on "already served."** Week 4's prior keeps holding without exception:
   if a complaint is discoverable by searching *"X is too expensive"*, the arbitrage already happened.
3. **Vendor-SEO domains are contaminating the second-source leg.** Two of three rows this week lean on
   pricing from a competitor's own comparison page — legitimate signal under the Mode B rule, but
   marketing; treat any price quoted about a rival as approximate.
4. **A new failure mode: the expired premise.** Two kills this week (LSA disputes, partly TTB COLA)
   addressed pain that no longer exists. Mode B skews toward older indexed content, so this is
   systematically likelier here — a currency check now runs alongside the cheap-tier check.
5. **The deep dive is gated on a fact Mode B cannot reach.** Treat it as a conditional plan, not a
   green light. No claim here is a projection of income; every price and complaint traces to a linked
   source seen in a search result this run — none fabricated, none fetched.
