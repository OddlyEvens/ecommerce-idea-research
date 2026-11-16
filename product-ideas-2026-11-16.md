# Product Ideas — Week of 2026-11-16

**Evidence mode: B (WebFetch UNAVAILABLE).** Step 0 ran first: both `example.com` and
`en.wikipedia.org` failed with `getaddrinfo ENOTFOUND` — a DNS-level egress block, not a 403. Per
standing rule WebFetch was not retried and no curl was attempted. **Run 18, Mode B for the 18th
consecutive run.** Every claim below traces to WebSearch result text.

## Executive summary

- **One new validated idea (ID 027), not four** — reported short rather than padded. A CIS300
  pre-filing checker + nil-return watchdog for UK construction contractors on Xero scores
  **composite 14, the highest row in the backlog**, and takes the deep-dive slot cleanly: every
  other active row is already Deep-Dived or Stale, so no tie and no judgement call.
- **Last week's "clean competitor pass" on ID 026 was WRONG** — the run's most consequential
  finding. Week 17 recorded Pay Cat as *"a consultancy, not a product."* It is a product: **Pay Cat
  Toolbox**, a portable-LSL report covering **every state and territory scheme**, at **$2 per
  active employee per month**. ID 026 re-scored **12 → 11**.
- **The competitor-hunt-before-scoring step is 8-for-8 as a decision step.** It killed the week's
  other three candidates outright and demoted ID 026.
- **Week 17's headline recommendation — hunt dated statutory obligations — half-worked.** Four
  statute probes returned regulation *calendars* with no buyer voice. Statute produced a row only
  where it **intersected a documented vendor defect**. That intersection is the actual vein.
- **ID 025's evidence upgraded without moving its score**, and the correction favours it: Tanda's
  journal claim is confirmed from **Tanda's own docs**, but its **LSL liability does not post to
  the journal** — so the LSL half of the wedge survives.

## Deep Dive of the Week — ID 027

**CIS300 pre-filing checker + nil-return watchdog for UK construction contractors on Xero.**
Highest-composite row never deep-dived (14), selected by rule. The mandatory pre-dive cheap-tier
check ran first and **passed**: the only named alternatives are construction ERPs an order of
magnitude dearer.

**Why it exists.** Xero files CIS returns, but a documented defect under-reports them. On
AccountingWeb a contractor reports the return *"does not pull though this invoice value onto the
report"* for materials-only invoices, their workaround being **two offsetting £1 and −£1 lines** on
a CIS labour code. The matching Xero idea carries *"materials were not being reported via our
submissions on Xero"* and was still live in **May 2026**. A sibling idea sits at **Not in
pipeline**: Xero allows **only one labour and one materials code**, unworkable for a firm needing
one per trade.

**The statutory half.** CIS300 is due the **19th**, with an automatic **£100** penalty from day
one, **£200** at two months, then **£300 or 5%** of deductions at six and twelve. And from
**6 April 2026 nil returns are compulsory again** — contractors must file even in months they pay
no subcontractors (**CIPP**, plus BDO and several practices).

**MVP (4 features).**
1. Pull bills/credit notes for the tax month (6th–5th) with CIS codes and subcontractor contacts.
2. **Shadow CIS300**: recompute gross / materials / deduction per subcontractor and diff it
   against Xero's own CIS Monthly Return — flagging materials-only omissions by name.
3. **Nil-return watchdog**: detect a tax month with zero subcontractor payments and alert before
   the 19th that a nil return is still required.
4. **Dated evidence pack**: per-month CSV/PDF snapshot of what was filed and why, for enquiries.

**Stack Claude would build it with.** Next.js + TypeScript on Vercel; Xero OAuth 2.0 on the
Accounting API (Bills, Contacts, Tracking Categories); Postgres on Supabase for month snapshots;
Vercel Cron for 14th/18th reminders; Postmark; Stripe. **Read-only, no HMRC filing** — deliberately
avoiding HMRC recognition and keeping the build in solo scope.

**First acquisition channel.** UK bookkeepers serving construction, reached where the complaint
lives: AccountingWeb *Any Answers* CIS threads, the Xero idea thread, AAT/ICB groups. Content
target: *"CIS materials only not pulling through Xero."* One bookkeeper carries many contractor
clients, so a conversion lands several seats.

**Benchmarked price.** **£15–25/month** per contractor, ~£9/month/client in bookkeeper bundles.
Benchmarks seen: **Chalkstring** at **$49/user/month** (Capterra) or **$200/month** (Software
Advice); **Archdesk** at **£690/month** (Software Advice), **$420/$800** (SaaSWorthy). Against a
£100 day-one penalty a sub-£25 tool is an easy yes, and nothing cheap was found in the slot.

**Single biggest risk.** The materials-only idea is **open, not "Not in pipeline"** — so unlike
every recent row this wedge sits on a live defect the vendor is *most* likely to patch, which ID
025's perishability rule makes structurally fragile. Compounding it: **sources conflict on whether
materials-only subcontractors belong on the return at all** — one AccountingWeb thread reports the
CIS helpline saying such a subcontractor *need not appear*. If HMRC considers Xero already correct,
the wedge evaporates. **Verify HMRC's position before writing code.**

## This week's validated ideas

| ID | Idea | D | W | F | M | Comp | Evidence (Mode B) |
|----|------|---|---|---|---|------|-------------------|
| **027** | CIS300 pre-filing checker + nil-return watchdog, Xero (UK construction) | 4 | 3 | 3 | 4 | **14** | `accountingweb.co.uk`: return *"does not pull though this invoice value"*; fix is *"two offsetting £1 and −£1 lines"*. `productideas.xero.com`: *"materials were not being reported via our submissions on Xero"*; sibling idea **Not in pipeline**, *"only one labour and one materials code."* `cipp.org.uk`: nil returns compulsory from **6 Apr 2026**; £100 day-one penalty. |

### Re-scored / strengthened

| ID | Change | Why |
|----|--------|-----|
| **026** PLSL return generator | **12 → 11** (Whitespace 3→2) | **Pay Cat Toolbox is a real product** covering *"every state and territory scheme"* at **$2/active employee/month** — week 17's clean pass was wrong. A Xero commenter has also already built a *"browser-based tool"* from Xero exports. And **LeavePlus does not accept file upload** (*"can only enter data manually"*), putting VIC construction out of MVP scope; PLSA and QLeave do take spreadsheets. |
| **025** Leave-liability report + journal | **13, unchanged** — evidence upgraded | Tanda's claim verified from **Tanda's own help docs**: liability = accrued hours × hourly rate × leave loading, posted in the payroll journal. **But Tanda's LSL (calculated) does not post** — tracked in a separate LSL Liability Report. Annual-leave half taken; **LSL half survives.** |

### Killed this week (cheap, and recorded so they are not retried)

- **Xero fixed assets / depreciation** — **AssetAccountant** on the Xero App Store does multi-country
  tax depreciation **and one-click journal posting**, at **$6–$12 per 100 assets** (+$4/loan).
  Whitespace 1.
- **EU multi-country VAT / OSS** (Xero does UK VAT only, *"not in its development pipeline"*) —
  **hellotax** OSS Reports **from €41/month**, filings **from €75/month**. Cheap tier occupied.
- **HubSpot scheduled report → Google Sheets** — real complaints, but **Coefficient** fills it at
  **$49/month** with a free tier; threads 400–3,400 days old.
- **MTD joint-ownership gap — premise refuted.** **Hammock** already ships per-owner quarterly
  submissions.

## Top-10 backlog snapshot

| Rank | ID | Idea | Comp | Status |
|------|----|------|------|--------|
| 1 | **027** | CIS300 checker + nil-return watchdog (Xero, UK) | **14** | **New + Deep-Dived** |
| 2 | 025 | Leave-liability report + journal generator (Xero AU) | 13 | Strengthened |
| 3 | 017 | Customer-specific price lists bridge (QBO/Xero) | 13 | Re-Deep-Dived |
| 4 | 026 | Portable LSL return generator (Xero AU) | **11** | Re-scored down |
| 5 | 006 | Auto-renewal cancel-flow monitoring | 12 | Re-Deep-Dived |
| 6 | 001 | Accessibility scan + fix pack | 12 | Deep-Dived |
| 7 | 012 | Google review disappearance archive | 12 | Deep-Dived |
| 8 | 003 | Small-batch maker COGS tracker | 12 | Deep-Dived |
| 9 | 002 | EU AI Act Art. 50 kit | 11 | Stale |
| 10 | 022 | Workers' comp premium-audit prep | 11 | Stale |

**Housekeeping:** **ID 011 retired** on week 17's standing nomination (composite 12, deep-dive
verdict NO, Whitespace 1, platform risk). **Active rows: 22** (+027, −011). **Ceiling: 14**, up
from 13 — its first move in seventeen runs.

## Risks and watch-outs

1. **ID 027's wedge is a live vendor defect — the most perishable kind.** Two of ID 025's three
   regions reversed inside a quarter, and an *open* idea is likelier patched than a "not in
   pipeline" one. Verify HMRC's position on materials-only subcontractors first.
2. **The week-17 statute recommendation needs narrowing, not repeating.** Statute alone yields
   calendars — packaging EPR, pay transparency and paid-leave filings all returned facts, no voice.
   Hunt statute **only where a vendor board already shows a defect**.
3. **Guaranteed-hours (UK, 2027) is parked, not scored** — deliberately. The reference period,
   mean-vs-median and the 8–20h threshold are **still in consultation**; building on unsettled
   regulations is a bad bet. Revisit when the regulations fix the method.
4. **Absence of alternatives is still a yellow flag.** No cheap CIS add-on was found. That reads
   as an unoccupied slot because complaint voice exists independently — but if a build starts and
   no one pays, this is the reason why.
5. **No income claims.** Every price above is a listed figure seen in search result text, several
   from aggregator pages that conflict, none verified under Mode A.
