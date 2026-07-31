# Product Ideas — Week of 2026-07-31 (Run 2)

*Week 2 research. Filed as `-run2` because the scheduler fired twice on 2026-07-31 and
`product-ideas-2026-07-31.md` (the week-1 zero-result report) already exists and was not
overwritten.*

## Executive Summary

- **Evidence Mode B applied.** WebFetch is still fully blocked: the STEP 0 control fetches
  against `example.com` and `en.wikipedia.org` both returned `403 Forbidden`. This is the
  second consecutive run with the same result — the block looks persistent, not intermittent.
  All evidence below comes from WebSearch titles and result text, never from a page I opened.
- **Four ideas cleared the Mode B evidence bar; only one is genuinely attractive.** The other
  three are recorded with honest low scores specifically so future weeks stop re-researching
  crowded ground.
- **The find of the week is a price chasm, not a missing feature.** Small e-commerce sites
  choose between $10–$59/mo accessibility *overlay* widgets that demonstrably do not work
  (the FTC fined accessiBe $1M over exactly this claim) and $1,250–$25,000 agency audits and
  remediation. There is nothing in between. That gap gets the Deep Dive.
- **Three parked leads from week 1 are now retired, not left dangling.** Etsy bulk-edit and
  small-batch maker inventory both resolved to crowded markets with named incumbents and real
  pricing — week 1's suspicion was correct. A PCI DSS angle I opened this week was killed by a
  2025 rule change before it earned a row.
- **No idea this week is backed by a page I read in full.** Treat every score as provisional
  until Mode A access returns.

---

## Deep Dive of the Week — ID 001: Honest accessibility remediation for small e-commerce

**The gap.** Overlay widgets (accessiBe, UserWay, AudioEye, EqualWeb, plus a dozen Shopify
apps) sell for [$49–$349/month and "800+ users were sued"](https://testparty.ai/blog/shopify-apps-automatic-ada-compliance-honest-review);
TestParty's research puts >1,000 businesses — more than 25% of all digital accessibility
lawsuits — as having been sued *despite* having an overlay installed, and 22.6% of 2025
lawsuits targeted overlay-using sites. The FTC finalized a
[$1 million order against accessiBe in April 2025](https://www.ftc.gov/system/files/ftc_gov/pdf/ferguson-holyoak-statement-re-accessibe.pdf)
for deceptively claiming its widget could make any site WCAG compliant. The disability
community is blunt about it — an AppleVis forum thread is titled
["Website widget overlays (accessiBe, Userway, etc) are not accesible"](https://www.applevis.com/forum/assistive-technology/website-widget-overlays-accessibe-userway-etc-are-not-accesible).
At the other end, a real audit runs [$1,250–$2,750](https://www.digitala11y.com/how-much-does-a-web-accessibility-audit-cost/)
and remediation $250–$550 per page, with
[$5,000–$25,000 year one](https://a11yproof.com/resources/guides/accessibility-compliance-cost-small-business)
for a typical small business site. EAA enforcement started 28 June 2025 and 2026 is the first
full supervised year.

**MVP features (5).**
1. Template-aware scan: crawl the handful of pages that matter for a store (home, collection,
   product, cart, account) with axe-core, then dedupe findings by *theme template* rather than
   by page, so the owner sees "12 issues" not "1,400."
2. Platform-specific remediation output — for each violation, the actual Liquid/theme file,
   selector, and corrected markup, generated from the axe node HTML rather than a generic WCAG
   rule ID.
3. "Fix pack" export: one prioritized markdown file a non-technical owner hands to an AI coding
   assistant or a $60/hr freelancer. This is the whole value proposition — it converts a
   $250–$550/page job into a cheap one.
4. Evidence-backed accessibility statement that records what was scanned, what was fixed, what
   remains, and when — a dated paper trail, never an unconditional compliance claim.
5. Monthly re-scan with regression alerts (theme and app updates silently re-break things —
   TestParty documents third-party Shopify apps doing exactly this).

**Stack Claude would build it with.** Next.js on Vercel for app and marketing site; Playwright
+ `@axe-core/playwright` in a *separate* background worker (Railway or Render) because scans
outlive a request handler; Supabase for auth, Postgres, and stored scan history; the Claude API
for remediation generation (Opus for the fix synthesis, Haiku 4.5 for cheap dedup and
classification); Stripe for billing; Resend for the monthly regression email. Deliberately
**not** a Shopify App Store listing in v1 — app review adds weeks; ship a plain web app that
takes a URL.

**First acquisition channel.** Agency and freelancer resale, not direct-to-merchant. Web shops
already field "are we ADA compliant?" from clients, already know overlays are a liability, and
have no cheap middle option to sell. Supporting channel: comparison content in the
"overlay vs. real remediation" keyword space — TestParty and Accessibility.Works already rank
there, which proves the traffic exists — with a free single-template scan as the lead magnet.

**Benchmarked price.** $49/mo, at deliberate parity with
[UserWay's $49/mo small-site tier](https://softwarefinder.com/artificial-intelligence/userway-accessibility-widget)
and just under [accessiBe's $59/mo accessWidget entry](https://accessibe.com/pricing/accesswidget),
plus a one-time $199 "audit + fix pack" for owners who won't subscribe. The competing
alternative is a $1,250+ audit, so the anchor is favourable.

**Biggest risk — and it is a serious one.** The honest positioning is simultaneously the
differentiator and the commercial handicap. Automated scanning catches only ~30–40% of real
WCAG violations, so this product can never say "compliant" — and saying it is precisely what
drew the FTC's $1M order. Meanwhile competitors *do* say it, and that claim is likely what a
scared store owner actually wants to buy. Selling "materially fewer real barriers plus a
defensible paper trail" against rivals selling "you're covered" is a harder pitch, and it is
unproven that SMB owners will pay for the honest version. Mitigation: sell the documented
remediation trail as the legal-defence artifact, and refer the manual-testing 60–70% to a named
partner auditor rather than pretending to cover it.

---

## This week's validated ideas

| ID | Idea | Dem | Whit | Feas | Mon | Comp | Key evidence (Mode B) |
|----|------|-----|------|------|-----|------|----------------------|
| 001 | Honest a11y scan + platform-specific fix pack for small e-commerce | 4 | 4 | 4 | 4 | **16** | [FTC $1M order re accessiBe](https://www.ftc.gov/system/files/ftc_gov/pdf/ferguson-holyoak-statement-re-accessibe.pdf); [overlays $49–$349/mo, 800+ sued](https://testparty.ai/blog/shopify-apps-automatic-ada-compliance-honest-review); [AppleVis: overlays "are not accesible"](https://www.applevis.com/forum/assistive-technology/website-widget-overlays-accessibe-userway-etc-are-not-accesible); [audit $1,250–$2,750](https://www.digitala11y.com/how-much-does-a-web-accessibility-audit-cost/) |
| 002 | EU AI Act Art. 50 transparency kit for SMEs (chatbot/AI-content disclosure) | 3 | 3 | 4 | 2 | **12** | [Art. 50 applies 2 Aug 2026](https://artificialintelligenceact.eu/transparency-rules-article-50/); [deadlines/Digital Omnibus](https://www.lw.com/en/insights/ai-act-update-eu-resolves-to-change-rules-and-extend-deadlines); [SME-specific read](https://www.castaldosolutions.it/articles/en/blog/ai-act-2-agosto-2026-cosa-cambia). Fines to €15M/3% turnover |
| 003 | Small-batch maker COGS / batch-cost tracker (soap, candle, bakery) | 4 | 2 | 4 | 3 | **13** | [Show HN Craftplan — built it because existing tools were "expensive, too generic, or both"](https://news.ycombinator.com/item?id=46847690); [Soapmaking Forum: "Inventory and batch tracking software"](https://www.soapmakingforum.com/threads/inventory-and-batch-tracking-software.72366/); [Craftybase from $20/mo](https://craftybase.com/pricing) |
| 004 | SMB-priced AI-visibility (AEO) tracking | 3 | 1 | 4 | 3 | **11** | Title verbatim: ["Profound Alternatives: 5 AI Visibility Tools That Don't Cost $499/Month"](https://maxaeo.ai/blog/profound-alternatives-5-ai-visibility-tools-that-dont-cost-499-month/); [Otterly $29/mo, Peec €89–199](https://zapier.com/blog/best-ai-visibility-tool/) |
| 005 | Etsy bulk-edit / bulk-listing tool *(retired week-1 lead)* | 3 | 1 | 4 | 2 | **10** | [Etsy forum "bulk-edit" tag, 277 discussions](https://www.etsy.com/forums/tag/21704228046/bulk-edit); [Evlista already does this](https://www.evlista.com/); [eRank $5.99–$29.99/mo](https://printify.com/blog/etsy-keyword-tool/) |

*Dem = Demand Evidence, Whit = Competitive Whitespace, Feas = AI-Build Feasibility, Mon = Monetization Clarity.*

**Why 003 scores 2 on whitespace despite strong demand:** named incumbents at every price point
— Craftybase ($20/mo up), Inventora (free/$19/$39), SoapMaker 3 (desktop), and Craftplan itself
is free and open-source. Real pain, no room.

**Why 004 scores 1:** Otterly already occupies the $29/mo floor this idea would have targeted.
The category filled in faster than the gap.

---

## Top-10 backlog snapshot

Backlog holds five scored ideas; all are listed above in rank order (001 → 005). Nothing else
has cleared the evidence bar across two runs. ID 001 is now marked Deep-Dived.

---

## Risks and watch-outs

- **Mode B evidence is soft and should be treated that way.** WebSearch returns titles, URLs and
  an AI-written summary of pages I cannot open. Where a number appears above, it appears in a
  result title or result text — but I could not verify it against the live page. Two sources
  gave conflicting Craftybase entry pricing ($20/mo vs $49/mo Studio); that conflict is
  unresolved and is itself a caution about all figures here.
- **Idea 001's core risk is legal-claims exposure**, detailed in the deep dive. It is not a
  build risk; it is a marketing-copy risk with an FTC precedent attached.
- **Idea 002 is close to a dead deadline.** Article 50 applies 2 August 2026 — two days from
  this run. A compliance-kit product arriving after the date sells into relief, not urgency,
  and monetization is one-time template sales with no recurring hook. Scored 2 on monetization
  for that reason.
- **A PCI DSS 4.0 client-side script monitor was investigated and dropped.** Requirements 6.4.3
  and 11.6.1 looked like a forcing function for small merchants until search surfaced that a
  2025 change [removed them from SAQ A](https://cside.com/blog/pci-dss-4-0-1-requirements-6-4-3-11-6-1-client-side-compliance-guide),
  which removes the small-merchant obligation this idea depended on. Recording the negative so
  it is not rediscovered.
- **No income or profit claim is made anywhere above.** Prices cited are competitors' list
  prices, not projected revenue.
