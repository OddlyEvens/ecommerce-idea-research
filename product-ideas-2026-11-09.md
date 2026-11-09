# Product Ideas — Week of 2026-11-09

**Evidence mode: B (WebSearch only).** WebFetch re-checked first: `example.com` and `en.wikipedia.org` both
returned `getaddrinfo ENOTFOUND` — blocked in all 17 runs, DNS form now 3 runs running. Every claim traces to a
search result actually seen; nothing here was read as a full page.

## Executive summary

- **One new validated idea, not four — stated plainly rather than padded.** Three further candidates were worked
  and died in one query each; two channels yielded grievance without a nameable gap.
- **The ceiling moved back DOWN to 13.** Week 16's first upward move in 16 runs lasted one week: **ID 025 re-scored
  14 → 13**, because **Xero itself shipped two of the three regions** that row covered.
- **The deep-dive slot resolved cleanly by rule for the first time in three runs** — no tie, no judgement call.
- **Method unlock: Reddit and Hacker News are reachable under Mode B via mirrors.** A five-week access escalation is
  withdrawn — and half-refuted, since having that voice produced no new row.
- **The first genuinely new vein in six runs is statute:** a legal deadline with a penalty cannot be undercut by a
  free tier — the wall that has killed almost everything else here.

## Deep Dive of the Week — ID 026: portable long service leave (PLSL) return generator for Xero (AU)

**The job.** Australian states run *portable* long service leave schemes: a worker accrues LSL across employers in
an industry, and every covered employer must lodge periodic service-and-wage returns to a state authority, with
penalties for late lodgement. Xero Payroll holds the data and produces no such return.

**Pre-dive cheap-tier check (mandatory) — for the first time in seven runs it did not kill the target.** The only
real incumbent feature is **Employment Hero's Portable Long Service Leave Report** (filters by pay category,
period, location, employee; a "Portable LSL employee" checkbox and membership ID per employee) — but it lives inside
its own payroll platform at **A$10/employee/month, ~A$100 minimum spend**: a payroll replacement, not a cheap
add-on. `paycat.com.au` sells a "portable LSL toolbox" — consultancy, not product. The free government portals are
the **destination, not the competitor**: QLeave and the Victorian PLSA both accept a spreadsheet, so producing a
validation-clean file from payroll data *is* the unpaid work.

**MVP — four features, one scheme first (Victoria):**
1. Xero OAuth2 connect; pull employees, pay items, ordinary hours and gross wages for a chosen quarter.
2. Per-employee PLSL fields the ledger cannot store — membership ID, covered/not-covered, start and end dates
   (precisely what Employment Hero keeps in its own employee profile).
3. Return-file builder with **validation mirroring the portal's own fault codes** — PLSA publishes a guide covering
   "Common Faults and Upload Codes".
4. Quarter-close checklist with statutory due dates plus **nil-return generation**: ACT and LeavePlus both require a
   return for quarters with no covered work, a classic penalty trigger.

**Stack Claude would build it with:** Next.js on Vercel; `xero-node` OAuth2 with `offline_access`; Postgres
(Supabase) for PLSL fields, scheme rules and lodgement history; **scheme rules as per-scheme JSON/TS config**, so
adding Queensland or the ACT is a config file, not a rewrite; SheetJS for XLSX/CSV; Zod for validation; Stripe for
billing. No queues, no ML, no infrastructure.

**First acquisition channel:** the Xero Product Ideas thread itself — *AU Payroll – Add portable long service leave
report* ([47693666](https://productideas.xero.com/forums/967118-payroll-expenses/suggestions/47693666-au-payroll-add-portable-long-service-leave-repor)),
three-plus pages of self-identified prospects asking for this output. Secondary: the regulators' own
**bookkeeper-and-accountant pages** (QLeave maintains them for contract cleaning and community services).

**Benchmarked price point — per connected employer per month, not per employee.** Comparables seen this week: Joiin
**$23/mo** (1–2 companies), LeaveCal **AUD $18/mo** (6–20 employees), Leave Balance **$10/mo flat unlimited**,
Employment Hero **A$10/employee/mo**. Defensible shape: **~A$29/mo single employer, ~A$99/mo multi-client practice
tier**, or ~A$49 per lodgement — between the flat-rate leave tools and Employment Hero's per-employee floor.

**Single biggest risk — Xero ships the report itself, and this is not hypothetical.** The request sits open on
Xero's public board, and **this run's ID 025 re-score is the proof**: Xero shipped NZ leave liability as a dollar
amount and accepted the UK leave balances report, same product area, in one quarter. Secondary: fragmentation is
worse than it looks — **Victoria alone runs two authorities** (LeavePlus for construction; PLSA for community
services, cleaning, security) against Queensland's three QLeave schemes on different cadences (QLD construction
**annual, due 31 July**; most others quarterly), plus ACT, NSW, SA, TAS, NT.

**Verdict: conditional-GO on a single-scheme MVP**, gated on two checks Mode B could not settle — whether
**LeavePlus** (as distinct from PLSA, where it is confirmed) accepts a spreadsheet upload at all, and whether any
`apps.xero.com` app already ships it.

## This week's scored ideas

| ID | Idea | D | W | F | M | Composite | Status | Evidence (Mode B) |
|----|------|---|---|---|---|-----------|--------|-------------------|
| 026 | Portable LSL scheme return generator from Xero payroll data (AU) | 4 | 3 | 2 | 3 | **12** | New + Deep-Dived | Xero board, verbatim: *"need a quarterly report that meets the Victorian Portable Long Service Leave requirements… to report each quarter to LeavePlus"*. `community.reckon.com` carries the **same gap on a different ledger**. Regulators: QLeave return *"by 31 July each year"*, bulk spreadsheet import, penalties *"for each month, or part of a month, the return isn't lodged"*; PLSA quarterly *"uploaded as a spreadsheet, or entered directly"*; ACT nil returns mandatory, *"the expanded scheme will commence on 1 July 2026"*. D held at 4 not 5: **no bookkeeper complaint voice found**, and QLeave's complaints register is tiny. |
| 025 | Leave-liability provision report + journal generator, Xero Payroll | 4 | 3→**2** | 3 | 4 | **14→13** | Re-scored down + Strengthened | **Demand strengthened**: Xero staff — *"Currently Xero does not automatically include leave liabilities on the Balance Sheet… workarounds such as… creating Manual Journals"*; AU provisions **Not in pipeline**; new LSL thread **Gaining Support** (*"LSL liability calculations are currently handled externally to Xero"*). **Whitespace cut**: NZ now shows *"the total leave liability as a dollar amount"*; UK **accepted**; **Tanda** reportedly posts liability journals at current hourly rate (*competitor-published, discounted*). **LeaveCal still not a liability valuer** (AUD $18/mo); new adjacent Leave Balance at **$10/mo flat unlimited**. |

**Worked and killed** (full detail in the backlog's leads table): **consolidated/multi-org Xero reporting** — 264
board votes, but **Joiin** holds the slot from ~**$23/mo**; **Reddit pain-point tooling** — **$79–199/mo** rivals,
moat is Reddit's API; **QBO as a discovery channel** — no public board with statuses or votes.

## Top-10 backlog snapshot (22 active rows; ceiling 13)

| # | ID | Idea | Composite | Status |
|---|----|------|-----------|--------|
| 1 | 025 | Leave-liability provision report + journal generator, Xero (AU) | 13 | Re-scored down + Strengthened |
| 2 | 017 | Customer-specific price lists bridge, QBO + Xero | 13 | Deep-Dived, re-scored down twice |
| 3 | 026 | Portable LSL scheme return generator, Xero (AU) | 12 | **New + Deep-Dived** |
| 4 | 006 | Click-to-cancel cancel-flow monitoring + archive | 12 | Deep-Dived, re-scored down |
| 5 | 001 | Accessibility scan + fix pack, small e-commerce | 12 | Deep-Dived, re-scored down |
| 6 | 012 | Google review disappearance archive + appeal pack | 12 | Deep-Dived, re-scored down |
| 7 | 003 | Small-batch maker COGS / batch-cost tracker | 12 | Deep-Dived, re-scored down |
| 8 | 011 | Supplier PO chasing, small e-commerce | 12 | Deep-Dived — NO *(next retirement)* |
| 9 | 002 | EU AI Act Art. 50 transparency kit | 11 | Stale, premise expired |
| 10 | 014 | Subcontractor COI / cert expiry tracking | 11 | Stale |

**Housekeeping:** ID 010 (Prop 65) **retired** on last week's nomination; ID 024 marked **Stale** as predicted.

## Risks and watch-outs

- **"The vendor has no plans" is perishable.** ID 025's whitespace rested on three regions of vendor inaction and
  **two reversed inside one quarter.** New rule: score region-by-region, never as a bloc, and treat any
  single-report wedge on a public vendor board as structurally fragile. ID 026 carries that exposure.
- **A vote count measures demand and nothing else** — seventh firing: 264 votes atop a $23/mo incumbent.
- **Mirror-sourced quotes are secondhand** (`reddit.sentinel-team.org`, `hn.svelte.dev`) and must never be cited as
  a page read. Relatedly, **three consecutive access escalations proved to be mis-diagnoses** — Indie Hackers
  (week 15), Reddit and HN (now); the next must first prove a host unreachable via WebSearch `site:`.
- **ID 026's Feasibility 2 is the honest constraint, not pessimism:** seven-plus schemes, two authorities in
  Victoria alone, and Xero's Payroll API returning leave balances only per employee — a developer reports having to
  *"get all employee objects one by one"* and hitting rate limits. A single-scheme MVP would score 3–4.
- **Unverifiable negatives remain Mode B's hard limit.** ID 026's Whitespace 3 rests on "no app found" — absence of
  evidence; `apps.xero.com` is reachable only by product-name query, never by `site:`.
- No income or profit claims are made or implied. Prices are vendor-published figures seen in search results;
  Flippa figures are seller-stated asking prices, not closed deals.
