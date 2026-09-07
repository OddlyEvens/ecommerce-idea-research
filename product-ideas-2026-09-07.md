# Product Ideas — Week of 2026-09-07 (Week 8)

## Executive summary

- **Evidence mode: B.** WebFetch was re-checked fresh at the start of the run and is still blocked — `example.com` and `en.wikipedia.org` both returned `EGRESS_BLOCKED` from the network egress proxy. **Eighth consecutive run, zero variation.** No curl or direct-HTTP workaround attempted; WebFetch was not retried after the check.
- **Two new validated ideas, and both are near-misses rather than builds.** ID 020 (CAM/NNN reconciliation for small commercial landlords, composite **14**) and ID 021 (carrier commission reconciliation for small insurance agencies, **13**). Each has genuinely good demand evidence; each fails the cheap-tier check — at **$49/mo** and **$60/mo** respectively. Reported as two, not padded to five.
- **The most valuable result of the run was a re-score, not a discovery.** ID 017 (QBO/Xero customer price lists) rose **15 → 16** and is now the backlog's highest row: QuickBooks Desktop **has** price levels, QuickBooks Online **cannot import them**, and the Desktop sunset is forcing that exact buyer into that exact gap on a fixed clock.
- **ID 018 was revised down 15 → 14** on a direct competitor found during its own deep-dive prep. It still won the deep dive — on a tie-break rule this run changed deliberately.
- **Six kills**, five of them at the cheap-tier check, and one — Xero delivery notes — killed inside a single query by the expired-premise screen. **Four new working Mode B channels**: `biggerpockets.com` (forum 32), `insurance-forums.com`, `productideas.xero.com` (UserVoice), `flippa.com`.

---

## Deep Dive of the Week — ID 018: quoting calculator with quote memory for 1–5 person job shops

Chosen at composite 14 in a two-way tie with ID 020. Week 7 required this deep dive to **open on willingness-to-pay, not features**, so it does.

### Willingness to pay — the question that decides everything

The incumbent is a free spreadsheet, the July 2026 Practical Machinist poster is giving his own calculator away, and this run found that **QuoteBuddy** (Therness) now sells "Machine Shop Quoting Software with AI" to exactly this segment with a **free tier of 3 quotes/month**. Three free options. That looks fatal until you find the counter-evidence: **this audience demonstrably buys calculators.** CNCCookbook sells G-Wizard, a speeds-and-feeds calculator, to these same shops — **2 seats for 1 year at $79.99 (list $99), lifetime $215.99** ([cnccookbook.com](https://www.cnccookbook.com/g-wizard-calculator-pricing/)). Machinists will pay roughly **$50–100/year for a single-purpose calculator that does not touch revenue.** A quoting calculator does touch revenue.

So the honest read is: **willingness to pay exists but is capped near $100–150/year, not $300+.** Any plan that assumes $29/mo is assuming this audience is something it has never been.

### MVP — five features, nothing else

1. **Rate library** — machine rates, labour rates and outside-process minimums (plating, heat treat, anodize) stored once, applied every time. Directly answers "inconsistent numbers depending on their mood."
2. **Parametric quote calculator** — material (stock size, drop/scrap %) + setup × setup rate + cycle time × machine rate + handling + outside processes **with their minimum lot charges** + margin. The minimum-lot-charge line is the specific error the 2 July 2026 poster named.
3. **Quantity-break table**, auto-generated at 1/10/50/100 from one input set, amortising setup correctly — the calculation hand-built spreadsheets most often get wrong.
4. **Searchable quote memory** by part number, customer and material, diffed against the last similar quote. The feature no spreadsheet has, and the one the evidence names most directly.
5. **Branded PDF quote**, with expiry date and terms.

Out of scope: CAD/geometry auto-quoting, scheduling, job tracking, invoicing, ERP — those turn a feasibility 4 into a 1.

### Stack, channel, price

**Stack:** Next.js (App Router) on Vercel; Supabase for Postgres + auth; Stripe for billing; server-side PDF generation via a React-to-PDF renderer. All arithmetic server-side and unit-tested — a quoting tool that is wrong once is uninstalled. No CAD libraries, no queues, no API approval gates. Deliberately the most boring stack available, because the risk here is commercial, not technical.

**First acquisition channel:** the **"Shop Management and Owner Issues"** subforum on `practicalmachinist.com`, worked the way the 2 July 2026 thread was worked — build in public, post the tool, ask to have it torn apart. That exact motion already earned engagement in this niche from someone with no audience. Second: CNCCookbook's readership, the demonstrated population of machinists who pay for calculators. Cold outreach is wrong at this price; the economics only close if acquisition is organic.

**Benchmarked price:** **$15/month, or $149/year** — above G-Wizard's ~$50–100/year (this touches money, not feeds and speeds) and roughly an order of magnitude below the chasm floor: **JobBOSS² from $199/mo for one user**, **Fulcrum $43/user/mo with a 5-user minimum (~$215/mo)**, **Paperless Parts from $300/mo**. Annual billing preferred — it matches how this audience already buys, and front-loads the only validation that matters.

### The single biggest risk

**Not competition — willingness to pay.** A shop owner who has run a homemade spreadsheet for fifteen years has already revealed a preference for spending hours over dollars, and now has three free alternatives including one venture-shaped product with an AI story. The mitigation is also the kill signal: **pre-sell ten annual licences at $149 before writing any code.** If ten shops will not pay in advance, the correct outcome is not a cheaper price — it is not building it. Verdict: **conditional-YES, gated on a paid pre-sale.**

---

## This week's validated ideas

| ID | Idea | D | W | F | M | Total | Evidence (Mode B) |
|----|------|---|---|---|---|-------|-------------------|
| 020 | CAM/NNN annual reconciliation statements for small commercial landlords (3–20 tenants) | 4 | 2 | 4 | 4 | **14** | `biggerpockets.com` forum 32: *"Best PM software for a small commercial portfolio (under 20 units) — nobody has answe[red]"* (Apr 2026), *"NNN Lease Reconciliation methods"*; result text *"A spreadsheet plus QuickBooks combo works until CAM reconciliation season, at which point it turns into a nightmare."* Second domain confirms the structural gap: **"Buildium, Entrata, and RentRedi do not offer native CAM modules"** (re-leased.com). **Killed by price:** CapVeri Pro **$49/mo**, STRATAFOLIO **$150–210/mo**, Plazee **$299/mo**, PigJet. |
| 021 | Carrier commission-statement reconciliation for small insurance agencies | 4 | 2 | 3 | 4 | **13** | `insurance-forums.com`: *"Commissions Reconciliation and Monthly Census"*, *"Commissions: Do You Trust Your Carriers?"*; agents *"still reconciling commissions by hand on spreadsheets"*; an agency moved off Applied/WinTAM (*"breaking their budget"*) to **Xanatek IMS at ~$200/mo, one-tenth** the cost. **Killed by price:** Commission Tracker **$67–72/mo**, CommissionTrac **$60/mo**, plus AgencyBloc and six others. |

**Revisited with score-changing evidence:** **ID 017 → 16** (QBD price levels do not migrate to QBO; Desktop 2023 lost support 31 May 2026, Desktop 2024 goes 30 Sept 2027). **ID 018 → 14** (QuoteBuddy occupies the wedge with a free tier; demand simultaneously broadened to woodworking, welding/fab and print).

**Killed:** print-shop MIS (Morning Flight free, $145 one-time) · self-managed HOA (PayHOA free under 31 homes) · law-firm IOLTA (TrustBooks $39/mo) · Squarespace request-a-quote (QuotePlugin $17/mo, Elfsight free) · Xero delivery notes (**expired premise — Xero shipped packing slips**) · Xero multi-entity consolidation (Joiin $23/mo) · SaaS price-hike tracker (three free ones already exist).

---

## Top-10 backlog snapshot

| Rank | ID | Idea | Total | Status |
|------|-----|------|-------|--------|
| 1 | 017 | Customer price lists for QBO + Xero | 16 | Strengthened / Deep-Dived |
| 1 | 001 | Honest accessibility scan + fix pack | 16 | Deep-Dived |
| 3 | 018 | Job-shop quoting calculator + quote memory | 14 | **Deep-Dived this week** |
| 3 | 020 | CAM/NNN reconciliation for small commercial landlords | 14 | New |
| 3 | 010 | Prop 65 warning audit + evidence archive | 14 | Deep-Dived |
| 6 | 021 | Insurance carrier commission reconciliation | 13 | New |
| 6 | 012 | Google review disappearance archive | 13 | Deep-Dived |
| 6 | 006 | Auto-renewal cancel-flow monitoring | 13 | Deep-Dived |
| 6 | 003 | Small-batch maker COGS tracker | 13 | Deep-Dived (conditional-NO) |
| 6 | 011 | Supplier PO chasing | 13 | Do not build |

---

## Risks and watch-outs

- **Eight weeks without WebFetch is now the defining constraint on this project's quality, not a temporary annoyance.** Three of this week's most consequential facts — CapVeri's $49 tier, QuoteBuddy's paid prices, and whether Intuit's own pages confirm the price-level migration gap — are one page-fetch away and unreachable. Allowlisting egress remains the highest-leverage change available.
- **Vendor-SEO contamination, third consecutive week, worse this run.** The QBD migration claim rests on three conversion-vendor blogs; the CAM error rate and the insurance underpayment figures come from vendors selling the fix. All recorded as approximate; the forum quotes are the only clean evidence here.
- **A vendor name inside a forum thread is not a neutral recommendation.** The April 2026 BiggerPockets post praising PigJet reads like it could be seeded. Flagged in the backlog, not treated as validation.
- **The cheap-tier check is doing most of the work now, which is itself a finding.** Five of six kills were price, not demand — including two (Squarespace quotes, HOA) whose demand evidence was excellent. Finding an open request is not finding an open market.
- **No income or profit claim is made here.** Every price, date and quotation traces to a linked source seen in a search result this run; none was read on the page itself, because Mode B does not permit that.
