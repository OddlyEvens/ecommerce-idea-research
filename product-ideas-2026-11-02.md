# Buildable Product Ideas — Week of 2026-11-02 (Week 16)

## Executive summary

- **Evidence mode: B** (WebSearch-only), **sixteenth consecutive blocked run.** Both Step 0 probes
  (`example.com`, `en.wikipedia.org`) failed with `getaddrinfo ENOTFOUND` — DNS resolution failure, the same
  mechanism as week 15, not the 403 of weeks 2–14. Not retried; no curl attempted.
- **One new validated idea — and it sets a new backlog ceiling of 14, the first upward move in 16 runs.**
  ID 025: a **leave-liability provision report + journal generator for Xero Payroll** (AU/NZ/UK). It is this
  week's Deep Dive.
- **The competitor-hunt method step got its sixth confirmation and then produced its first *favourable*
  nuance.** The author of the "Australian Leave Liability Playbook" (Finlert) is indeed the competitor in the
  channel — it sells **LeaveCal** — but LeaveCal's own FAQ states it *"will never retrieve any of your
  invoice, payment or salary data."* Valuing a leave liability **requires** salary data, so the incumbent has
  publicly disclaimed the data the wedge needs.
- **One bar-clearing candidate killed in-session** (Xero bank-statement PDF→CSV: nine-plus priced competitors
  from **$4.50/mo** plus free tiers) and **one recorded as a resolved-negative lead** (Xero wrong-bank-account
  transaction fixer).
- **ID 017 re-validation was attempted and is inconclusive** — two queries returned nothing on Ocean Pricing's
  status. Score holds at 13, unchanged. Housekeeping: **ID 018 retired**, **ID 022 marked Stale**.

## Deep Dive of the Week — ID 025

**Leave-liability provision report + one-click journal for Xero Payroll (AU/NZ/UK; accountants & bookkeepers)**

Xero Payroll accrues leave but never posts the resulting liability to the balance sheet. Xero has marked the
fix **"not in pipeline"** repeatedly and recently, and its own advice is to do it by hand.

**MVP (5 features)**
1. Connect a Xero org by OAuth2; pull employees, leave balances and pay rates.
2. **Leave liability valuation report** — per-employee hours × current rate, Annual Leave split from Long
   Service Leave, with a configurable on-cost % (super, payroll tax, workers comp) and AU state LSL
   vesting/pro-rata settings.
3. **One-click manual journal** — debit leave expense, credit leave provision, dated at period end, posted via
   the Accounting API, idempotent and reversible.
4. **Period-over-period movement view**, so the accountant can explain the delta at review.
5. **Multi-client dashboard** flagging which connected orgs have no provision posted.

**Stack Claude would build it with:** Next.js/TypeScript on Vercel; `xero-node` for OAuth2; Supabase Postgres
for tokens, settings and provision snapshots; Vercel Cron for the monthly refresh; server-rendered PDF/CSV
export. Entirely managed services — no infrastructure to run.

**First acquisition channel:** the Xero idea threads themselves — the AU provisions thread (**114 votes**) and
the AU Employee Payroll Details thread (**96 votes**), where the audience is self-identified and Xero has said
on the record it will not build it. This is precisely where Ocean Pricing (ID 017) and CancelCheck (ID 006)
recruited their beta users. Secondary: AU/NZ bookkeeper groups and the Xero advisor directory.

**Benchmarked price point (all figures observed, none invented):** LeaveCal, the nearest same-channel app,
lists **£10/mo for 6–20 employees, £14 for 21–50, £20 for 51–80** ex-tax on the Xero App Store UK, and
**AUD $15/mo for 10 team members (AUD $1.50/member)** on its own site. XO Report prices by *org count* —
**$9.90 (1 org) → $29.90 (10) → $49.90 (25)**. Price per connected org, not per employee: roughly
**A$19–29/mo single org**, **A$79–99/mo for a 10-client accountant tier**.

**Single biggest risk — unverified whitespace.** `apps.xero.com` is unreachable in this environment, so "no app
does accountant-facing leave-liability provisioning" rests on absence of evidence in search results, not on a
read of the marketplace. Finlert already owns the channel *and* the narrative. Its "never retrieve salary data"
line is a current privacy promise, not a moat — adding salary scope is a product decision, not a technical
barrier.

## This week's validated ideas

| ID | Idea | D | W | F | M | Composite | Evidence (two independent domains minimum) |
|----|------|---|---|---|---|-----------|--------------------------------------------|
| **025** | Leave-liability provision report + journal generator for Xero Payroll (AU/NZ/UK) | 4 | 3 | 3 | 4 | **14** | **Mode B.** `productideas.xero.com`: *AU Payroll – Provisions for Annual and Long Service Leave* (**114 votes**, Nov 2025, Not in pipeline, *"isn't on its foreseeable roadmap"*); *AU Payroll – Unpaid leave report* (*"leave reporting isn't in the roadmap for the near term"*); *UK Payroll – Leave Transactions report* (*"not currently set in our roadmap"*); *Custom payroll reports* (Not in pipeline, **14 Jan 2026**); *AU Employee Payroll Details Report* (**96 votes**, 7 Jan 2026). Xero's own workaround: raise expense + liability accounts and *"use the journal function to debit the expense and credit the liability"*, figures from the Leave Balances report. Independent: `finlert.com` playbook — *"the associated liability is not automatically posted to the balance sheet"*, **over 43%** of surveyed respondents *"never post Leave Liability to the Balance Sheet in Xero"* (**vendor-sourced stat — discount accordingly**); `inspire.accountants`, `benkorp.com`, `livingbusiness.co.nz` carry the same manual process. Users: reports *"miss Leave Taken Column"*. |

**Competitive teardown (ID 025).** **LeaveCal by Finlert** — £10/£14/£20 per month by headcount band on the Xero
App Store UK, AUD $15/mo for 10 members on its own site, price rise from 1 Aug 2025; leave *visibility*, and its
FAQ disclaims invoice, payment and **salary** data, which the valuation needs. **XO Report** — $9.90–$99.90/mo
Excel add-in for Xero data; payroll coverage unconfirmed. **Employment Hero / RosterElf / Deputy** — HR and
rostering platforms that bundle leave management at roughly **AUD $3–14 per employee per month**, a different
tier and a different buyer. The specific accountant-facing provisioning wedge has no confirmed direct app —
**contingent on an `apps.xero.com` read that this environment cannot perform.**

**Whitespace is 3, not higher:** incumbent in the channel, marketplace unverified. **Not lower:** the
disclaimer is explicit and the HR platforms sell a different thing to a different buyer at 5–10× the price.

## Current top-10 backlog snapshot

| Rank | ID | Idea (abbreviated) | Composite | Status |
|------|----|--------------------|-----------|--------|
| 1 | **025** | Xero Payroll leave-liability provision + journal | **14** | **New + Deep-Dived** |
| 2 | 017 | Customer-specific price lists bridge (QBO + Xero) | 13 | Deep-Dived (re-validation inconclusive) |
| 3 | 006 | Click-to-cancel cancel-flow monitoring + archive | 12 | Deep-Dived, closed |
| 4 | 001 | Honest accessibility scan + platform fix pack | 12 | Deep-Dived, closed |
| 5 | 012 | Google review disappearance archive + appeal pack | 12 | Deep-Dived |
| 6 | 010 | Prop 65 per-SKU register + evidence archive | 12 | Deep-Dived (next retirement candidate) |
| 7 | 003 | Small-batch maker COGS / batch-cost tracker | 12 | Deep-Dived |
| 8 | 011 | Supplier PO chasing for small e-commerce | 12 | Deep-Dived |
| 9 | 002 | EU AI Act Art. 50 transparency kit | 11 | Stale |
| 10 | 014 | Subcontractor COI / cert expiry tracking | 11 | Stale |

*(ID 018 retired this week — QuoteBuddy sells the exact MVP at $29–59/mo with a free tier. ID 022 marked Stale.)*

## Risks and watch-outs

- **The new ceiling rests on an unverifiable negative.** ID 025's whitespace score depends on no
  marketplace app existing. `apps.xero.com` is unreachable here. **Treat 14 as provisional** and re-score the
  moment Mode A returns. This is now the second row (with ID 017) blocked on the same single host.
- **Sensitive personal data from day one.** Xero's developer docs state the Payroll API *"does not filter or
  redact sensitive leave category data — including Family and Domestic Violence Leave — from API responses."*
  Not a licence regime, but a solo founder would be ingesting sensitive employee records. Budget for it.
- **AU Long Service Leave is state-by-state**, with differing vesting periods and pro-rata thresholds, and the
  output lands on a balance sheet a reviewer may test. This is the same accuracy-risk shape that killed week
  15's BAS candidate — lighter here only because the hours come straight from Xero's own report rather than
  being recomputed.
- **API ergonomics are mediocre.** AU leave balances arrive only via `GET /Employees/{id}` — one call per
  employee, so rate limits bite on large clients. The UK has a dedicated endpoint.
- **Vendor-sourced demand stat.** The 43% figure is Finlert's own marketing survey. It is the single most
  quotable number behind this row and it belongs to the competitor.
- **The offline-first-trades pivot failed on its first run.** Week 15's recommended new search space returned
  the same free-incumbent wall (Roll-Off Amigo *"free forever for owner-operators"*; Dumpster Controls free for
  a whole team). Do not read ID 025 as vindication of that pivot — it came from the old vein.
