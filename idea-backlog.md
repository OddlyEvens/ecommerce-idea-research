# Idea Backlog

Persistent memory across weekly research runs. Every idea that clears the evidence bar
(REAL evidence from **two or more independent primary sources**) gets a row here.

**Scoring:** each dimension 1-5. Composite = sum, out of 20.

- **Demand Evidence (1-5)** — strength/specificity of real user complaints found
- **Competitive Whitespace (1-5)** — 5 = clear unmet gap; 1 = crowded, well-served
- **AI-Build Feasibility (1-5)** — 5 = trivially small for a non-coder + Claude; 1 = large/complex
- **Monetization Clarity (1-5)** — 5 = obvious who pays, how much, and why

**Status values:** New | Strengthened | Stale | Deep-Dived

**Evidence mode:** A = pages actually fetched and read (strong). B = WebSearch titles/result
text only, page never opened (weaker — re-validate under Mode A when access returns).

---

## Active Ideas

| ID | Idea | Category | First Seen | Demand Evidence | Competitive Whitespace | AI-Build Feasibility | Monetization Clarity | Composite | Status | Notes |
|----|------|----------|-----------|-----------------|------------------------|----------------------|----------------------|-----------|--------|-------|
| 001 | Honest accessibility scan + platform-specific "fix pack" for small e-commerce (explicitly not an overlay) | Small SaaS / web app | 2026-07-31 (run 2) | 4 | 4 | 4 | 4 | **16** | **Deep-Dived** (2026-07-31 run 2) | **Mode B.** The gap is a price chasm, not a missing feature: overlays $10–$59/mo that demonstrably don't work vs. $1,250–$25,000 agency audit + remediation, nothing between. FTC fined accessiBe $1M (Apr 2025) for claiming a widget = WCAG compliance. TestParty: >1,000 businesses sued *despite* an overlay; 22.6% of 2025 suits hit overlay users. AppleVis thread title: overlays "are not accesible". EAA enforced since 28 Jun 2025. Biggest risk is marketing-claims exposure (see deep dive) — automated scanning catches only ~30–40% of WCAG issues, so "compliant" can never be claimed. |
| 003 | Small-batch maker COGS / batch-cost tracker (soap, candle, bakery, micro-manufacture) | Small SaaS | 2026-07-31 (run 2) | 4 | 2 | 4 | 3 | **13** | New | **Mode B.** Demand is real and repeatedly evidenced — Show HN "Craftplan" author built his own because existing tools were "expensive, too generic, or both"; Soapmaking Forum thread "Inventory and batch tracking software". But whitespace is genuinely poor: Craftybase (from $20/mo per its own pricing page; one source said $49/mo Studio — **conflict unresolved**), Inventora (free/$19/$39), SoapMaker 3 (desktop, one-time), and Craftplan itself is free + open-source. Do not re-research the general category; only a sharply differentiated wedge would justify revisiting. |
| 002 | EU AI Act Article 50 transparency compliance kit for SMEs (chatbot disclosure, AI-content labelling) | Template pack / micro-tool | 2026-07-31 (run 2) | 3 | 3 | 4 | 2 | **12** | New | **Mode B.** Hard deadline: Art. 50 applies **2 Aug 2026** (two days after this run — urgency is largely spent). Obligations are concrete and light: disclose chatbots as AI, label AI-generated content, mark deepfakes. Fines to €15M or 3% worldwide turnover. Demand scored 3 not 4 because every source is an advisory/SEO explainer, **not** a user complaint — no primary evidence anyone is trying and failing to buy this. Monetization 2: one-time template sale, no recurring hook. |
| 004 | SMB-priced AI-visibility / AEO tracking (brand mentions in ChatGPT, Perplexity, etc.) | Small SaaS | 2026-07-31 (run 2) | 3 | 1 | 4 | 3 | **11** | New | **Mode B.** Real price signal in a verbatim title: "Profound Alternatives: 5 AI Visibility Tools That Don't Cost $499/Month". But the cheap tier this idea would have occupied is already taken — Otterly at $29/mo, Peec €89–199, Profound ~$499. Category filled in faster than the gap. **Deprioritize; do not re-research** unless a specific vertical wedge appears. |
| 005 | Etsy bulk-edit / bulk-listing tool | Browser extension / small SaaS | 2026-07-31 (run 1, parked) → scored run 2 | 3 | 1 | 4 | 2 | **10** | New | **Mode B.** Week-1 parked lead, now resolved — and week 1's suspicion was right. Etsy forums carry 277 discussions tagged "bulk edit" (real pain), but Evlista already sells exactly this, alongside eRank ($5.99–$29.99/mo), Sale Samurai ($99.99/yr), Alura ($9.99–$29/mo). Crowded. **Lead retired — do not revisit.** |

---

## Unvalidated Leads (NOT scored — do not treat as ideas)

| Lead | Why it looked interesting | What must be verified before it earns a backlog row |
|------|---------------------------|------------------------------------------------------|
| **Ask HN: "What do you still do manually in 2026 that should be automated?"** — [news.ycombinator.com/item?id=48045237](https://news.ycombinator.com/item?id=48045237) | Highest-value *source* found in two runs, not an idea itself. Thread criteria are almost exactly this project's brief: you do it 5+ times a week, you've looked for a tool and nothing good exists, and you'd pay $10–20/month. Hundreds of self-qualified demand statements in one page. | **Requires Mode A.** The moment WebFetch works, fetch this thread first, before any other research. Under Mode B the comments are unreachable — search returns the thread title only. |
| Make.com / Zapier long-tail connector gaps | Carried from week 1, still untouched. Reported pattern of "Sorry, app not found" for less-prominent apps and community connectors of uneven reliability with no quality signal. | Find forum posts naming *specific* missing integrations. Monetization remains unclear — a directory monetizes badly. Low priority. |
| Shopify order-export / payout reconciliation gaps | Carried from week 1. | Week 1 flagged this as likely already well-served (Smart Order Export, HubApp, CONA). Still unverified. Low priority. |
| ~~PCI DSS 4.0 client-side script monitoring for small merchants~~ | Looked like a strong 2026 forcing function (reqs 6.4.3 / 11.6.1: inventory every payment-page script, alert on unauthorized change). | **RULED OUT 2026-07-31 run 2 — do not revisit.** A 2025 change removed both requirements from SAQ A, which is the tier small merchants file under. The small-merchant obligation this idea depended on no longer exists. |
| ~~Small food producer / cottage-bakery production planning~~ | Week-1 lead. | **Resolved into ID 003.** No longer a separate lead. |
| ~~Etsy bulk-listing / bulk-edit pain~~ | Week-1 lead. | **Resolved into ID 005 and retired.** Crowded market confirmed. |

---

## Deep Dive History

| Date | Idea Deep-Dived | ID |
|------|-----------------|-----|
| 2026-07-31 (run 1) | _None — backlog empty, nothing eligible to deep dive._ | — |
| 2026-07-31 (run 2) | Honest accessibility scan + fix pack for small e-commerce | 001 |
