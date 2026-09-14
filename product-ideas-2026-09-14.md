# Product Ideas — Week of 2026-09-14 (Week 9)

**Evidence mode this run: B** (WebFetch UNAVAILABLE — ninth consecutive run). Both probe
fetches — `example.com` and `en.wikipedia.org` — returned
`EGRESS_BLOCKED: "Access to <domain> is blocked by the network egress proxy."` No curl
fallback attempted, per the brief. All evidence below is WebSearch result text.

---

## Executive summary

- **One new scored idea, honestly reported as thin** (ID 022, workers' comp premium-audit
  prep for small contractors, composite 13). Fifteen other candidates were tested and killed.
  No padding: this was the lowest-yield week of the project for *new* ideas.
- **The most valuable finding of the run is a retro-kill, not a new idea.** Last week's
  open question on **ID 020 (CAM/NNN reconciliation)** — is CapVeri's cheap tier a real
  reconciliation product? — resolved *against* the idea. Result text puts **CapVeri Starter
  at $20/mo**, **Pro $49/mo**, and states **"All CapVeri plans include CAM reconciliation"**,
  with **ManageCasa at $45/mo for up to 25 units** also doing CAM reconciliation and
  **CAMAudit at $79/audit** pay-per-use. ID 020 drops **Whitespace 2 → 1, composite 14 → 13**,
  and its "do not build until a Mode A check" note becomes a flat do-not-build.
- **ID 017 (QBO/Xero customer price lists) is re-scored down 16 → 15** on new platform-risk
  evidence: Intuit **shipped native sales orders into QuickBooks Online in January 2026**
  (Plus/Advanced, or the Inventory add-on on lower plans), with custom fields, bundles and
  convert-to-PO added through 2026. The Desktop-parity gap that ID 017 sits in is
  demonstrably being closed by Intuit itself.
- **The cheap-tier check killed 10 of ~13 candidates again** — and, for the first time, it
  killed a *backlog row* as well as new candidates. New standing rule adopted: re-run the
  price check on a row **before** deep-diving it, not only when first scoring it.
- **One genuinely new working channel:** the Square Seller Community
  (`sellercommunity.com` / `community.squareup.com`), a Khoros board that returns seller
  frustration text verbatim ("*Two+ years down now… no update available on this Feature
  Request*"; "*STILL no update on this??? This thread is over 2 years old!*").

---

## Deep Dive of the Week — ID 022: workers' comp premium-audit prep for small contractors

**Why this one.** After this week's re-scores, the highest-composite rows not yet deep-dived
are a four-way tie at 13 (IDs 011, 020, 021, 022). Week 5's tie-break (prefer the row whose
note is not already *do not build*) and week 8's tie-break (prefer higher Competitive
Whitespace) both point to **022** — it is the only one of the four not already a
do-not-build, and the only one at Whitespace 3.

**The problem.** Workers' comp policies are written on *estimated* payroll and trued up by
an annual premium audit. Contractors lose at audit in three repeatable ways, all documented
on `contractortalk.com`: payroll not split by class code in the records ("*many instances
show auditors denying separation of payroll and lumping everything into the higher
category… because it wasn't done right*"); missing subcontractor COIs for the policy period
("*the auditor may decide coverage didn't exist and assess premiums*"); and vague
owner/officer and 1099 treatment. `lawnsite.com` confirms the mechanics on a second domain —
the auditor compares estimated vs actual payroll, wants payroll ledgers or tax-deposit
records, and increasingly audits remotely from PDFs.

**MVP (4 features).**
1. **Class-code payroll splitter** — import a payroll CSV, assign hours per employee per job
   to a class code, and hold the record that makes separation defensible.
2. **Sub COI vault with policy-period coverage map** — upload each sub's COI, extract
   effective/expiry dates, and show gaps *against the WC policy term* (not just "expired").
3. **Pre-audit gap report** — run before the auditor arrives: uncovered sub-days, unsplit
   payroll, missing owner/officer elections, cash/1099 labour with no COI.
4. **Auditor packet export** — one dated PDF/ZIP bundle in the order auditors ask for it.

**Stack Claude would build it with.** Next.js on Vercel + Postgres (Supabase) + Supabase
Storage for COI PDFs; Claude API for COI date/limit extraction with a human confirm step;
Stripe Billing; `pdf-lib` for the packet. No third-party API approval gate — the deliberate
contrast with ID 017 (Intuit review, 6 weeks–6+ months) and ID 012 (Google GBP quota gate).

**First acquisition channel.** `contractortalk.com` and `lawnsite.com` — the same two
domains that supply the evidence — posting an audit-prep checklist, not a product pitch
(the pattern the July 2026 Practical Machinist quoting-calculator post shows works). Second
channel: independent insurance agencies, who have a retention reason to hand it to insureds.

**Benchmarked price: $29/mo, annual only ($290/yr).** Benchmarks actually seen: certified-
payroll entry tools near **$49–50/mo** (ID 016), **myCOI ~$200–400/mo** with a 200-certificate
minimum and **TrustLayer free** at the bottom (ID 014), agency systems like **Xanatek IMS
~$200/mo** (ID 021). Annual-only matters because the pain is annual — a monthly plan gets
cancelled the day after the audit.

**Biggest risk — and it is the whole idea.** No dedicated competitor surfaced at all, which
this project treats as a **yellow flag, not good news**. The likeliest explanation is that
the job is already absorbed: payroll platforms (Gusto, Rippling) carry class codes, free COI
trackers cover the sub half, and **brokers prep the audit for free as a retention service** —
week 5's service-not-software kill. Verdict: **conditional-NO pending one demand test.** Before
any code, find a contractor asking for this tool rather than complaining about the outcome;
absent that, this is a pain without a purchase.

---

## This week's validated ideas

| ID | Idea | D | W | F | M | Comp | Mode | Evidence (two independent domains) |
|----|------|---|---|---|---|------|------|-----------------------------------|
| 022 | Workers' comp premium-audit prep (class-code payroll + sub-COI coverage map + auditor packet) for small contractors | 3 | 3 | 4 | 3 | **13** | B | `contractortalk.com` — [Workers Comp Class Codes & Separation of Payroll](https://www.contractortalk.com/threads/workers-comp-class-codes-separation-of-payroll.146555/), [Workers Comp Audit Mishap](https://www.contractortalk.com/f16/workers-comp-audit-mishap-84275/), [Workers Comp audit…](https://www.contractortalk.com/threads/workers-comp-audit.418879/); `lawnsite.com` — [workman's comp audits](https://www.lawnsite.com/threads/workmans-comp-audits.315775/), [Insurance audit?](https://www.lawnsite.com/threads/insurance-audit.283884/). Third, vendor-adjacent: [carolinariskpartners.com](https://carolinariskpartners.com/blog/workers-comp-audit-traps-in-north-carolina-why-payroll-class-codes-1099-labor-and-owner-pay-create-surprise-premium-bills-in-2026/) reports an insulation contractor with three employees going **$5,500 → $25,000** — an agency blog, treat as illustrative. |

**Re-scored rows:** ID 020 **14 → 13** (Whitespace 2 → 1; CapVeri Starter **$20/mo**, Pro
**$49/mo**, all plans include reconciliation; ManageCasa **$45/mo**/25 units; CAMAudit
**$79/audit**). ID 017 **16 → 15** (Whitespace 4 → 3; Intuit shipped QBO sales orders Jan 2026).

---

## Top-10 backlog snapshot

| Rank | ID | Idea | Comp | Status |
|------|----|------|------|--------|
| 1 | 001 | Honest accessibility scan + fix pack for small e-commerce | 16 | Deep-Dived |
| 2 | 017 | Customer price lists bridge for QBO + Xero | 15 | Deep-Dived (re-scored ↓) |
| 3 | 010 | Prop 65 warning audit + determination register | 14 | Deep-Dived |
| 4 | 018 | Sub-$50 quoting calculator for 1–5 person job shops | 14 | Deep-Dived |
| 5 | 003 | Small-batch maker COGS / batch tracker | 13 | Deep-Dived (conditional-NO) |
| 6 | 006 | Auto-renewal cancel-flow monitoring | 13 | Deep-Dived |
| 7 | 011 | Supplier PO chasing for small e-commerce | 13 | New (do not build) |
| 8 | 012 | Google review disappearance archive | 13 | Deep-Dived |
| 9 | 020 | CAM / NNN reconciliation generator | 13 | New (re-scored ↓, do not build) |
| 10 | 021 | Carrier commission reconciliation for agencies | 13 | New (do not build) |
| — | 022 | Workers' comp premium-audit prep | 13 | **Deep-Dived this week** |

---

## Risks and watch-outs

1. **Nine straight Mode B runs.** Four score-moving facts remain unreachable without page
   fetches. The allowlist escalation stands (see research log).
2. **Conflicting price text on CapVeri** — one query returned Starter $20 / Pro $49 /
   Business $99; another returned Reconcile $99 / Control $249 / Defend $499. Either reading
   puts a reconciliation-capable tier well under the $150–300/mo tier ID 020 assumed, and
   ManageCasa at $45/mo settles it independently. Recorded as approximate, conclusion
   unaffected.
3. **Vendor-SEO contamination, fourth consecutive week.** The $5,500 → $25,000 premium swing,
   the "40% of unexpected audit adjustments are subcontractor-related" figure, and every
   CAM price above come from parties selling the fix.
4. **The expired-premise screen fired twice more** (QBO sales orders; Square Appointments
   packages). Mode B's bias toward older indexed content remains the main source of false
   positives in this project.
5. **No income claim is made anywhere above.** Every price is a figure seen in result text
   and linked; nothing here is a projection of revenue.
