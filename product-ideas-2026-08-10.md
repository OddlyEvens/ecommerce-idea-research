# Product Ideas — Week of 2026-08-10

## Executive summary

- **Evidence mode: B** (WebFetch UNAVAILABLE — fourth consecutive run). Both STEP 0 control
  fetches were re-run fresh and failed: `example.com` and `en.wikipedia.org` both returned
  `EGRESS_BLOCKED` from the network egress proxy. Note the error *shape* changed this week —
  weeks 1–3 reported `HTTP 403 Forbidden`, this run returns a structured `EGRESS_BLOCKED`
  envelope. Same outcome, but it confirms an explicit egress allowlist rather than bot detection.
- **Two ideas cleared the bar, not the 4–6 target.** Reported honestly rather than padded. The
  headline find — **ID 010, Prop 65 warning determination + evidence tracker for online sellers**
  (composite **14**) — is the second-strongest idea in four weeks of backlog and gets this week's
  deep dive.
- **Five ideas were killed at the cheap-tier check**, which is the week-3 rule working as intended:
  WooCommerce box packing, EU Omnibus 30-day pricing, FDA nutrition labels, EU GPSR responsible
  person, and HTS/tariff-code classification. Each death is recorded so no future run re-walks it.
- **One new working channel: `wordpress.org/support/topic/` review titles are indexed verbatim**,
  including specific removed features. But it yields *quality* complaints ("poor support", "buggy"),
  not *gap* complaints — with ~60,000 plugins, WordPress rarely has a hole. Useful, lower-yield
  than the Shopify App Store channel found in week 3.
- **Three channels confirmed dead** (stop trying): Trustpilot, iOS/Android app-store review text,
  Atlassian and Notion marketplaces. All are intercepted by aggregator/SEO pages.

---

## Deep Dive of the Week — ID 010

**Prop 65 warning audit + per-SKU determination register + dated evidence archive for online sellers**

### Why this one

California Prop 65 enforcement is a private bounty system running at industrial scale, and the
enforcement mechanic is *specifically* a web-page scan. In 2024, **5,398 60-day notices** were filed
with the CA AG by roughly **40 private enforcers**, up from 4,142 in 2023, with **5,000+ again in
2025** — averaging close to three notices a day
([National Law Review, 2025 trends](https://natlawreview.com/article/2025-california-proposition-65-trends);
[Intertek notice analyses](https://www.intertek.com/products-retail/insight-bulletins/2025/1487-june-2025-california-proposition-65-analysis/)).
Settlement volume went from **890 settlements / $26M in 2022 to 1,300+ / just over $101M in 2024**.
For Amazon-sold consumer products, attorney-negotiated settlements typically land **$10,000–$20,000**,
rising to **$40,000–$90,000** once litigation starts
([LA Law Group](https://www.bizlawpro.com/proposition-65-for-amazon-sellers/)). Statutory penalties
run to **$2,500 per day per violation** plus the plaintiff's attorney fees.

Sellers are visibly getting hit, in their own words, on two independent seller forums:
Amazon Seller Central threads titled *"I'm getting sued for Prop Proposition 65. Anyone else? What
did you do?"*
([link](https://sellercentral.amazon.com/seller-forums/discussions/t/baa7ead7872f21ac57736143885b1ebf))
and *"Sixty day notice of intent to sue Proposition 65"*
([link](https://sellercentral.amazon.com/seller-forums/discussions/t/ceccfcf2cff811fbb368c1fc926f3cac)),
plus a Shopify Community thread on implementing the warning
([link](https://community.shopify.com/c/shopify-apps/california-prop-65-warning-billing-and-shipping-address-are/td-p/1285267)).

And there is a **dated forcing function with an operational clock in it.** OEHHA's short-form
warning amendments took effect **1 Jan 2025** with an enforcement date of **1 Jan 2028**, and now
require naming **at least one listed chemical**. Critically for e-commerce: the warning must appear
on the product display page, or via a hyperlink marked "WARNING" / "CA WARNING" / "CALIFORNIA
WARNING", or otherwise be shown before purchase completes — and **internet retailers get only a
60-day grace period from receiving notice that a product's warning content has changed** to update
their listings
([Kelley Drye](https://www.kelleydrye.com/viewpoints/blogs/kelley-green-law/prop-65-update-big-changes-to-the-short-form-and-internet-warnings);
[Foley & Lardner](https://www.foley.com/insights/publications/2025/04/prop-65-changes-to-short-form-warnings-will-cause-long-term-impacts/)).
That 60-day clock, per SKU, is a tracking job no one is selling to small brands.

### MVP — 4 features

1. **Store scan + warning audit.** Crawl the merchant's own product pages and classify each against
   the three permitted internet-warning methods; flag every page with no compliant path.
2. **Per-SKU warning register.** Which chemical is named, which warning version (pre- or post-2025
   short form), what the determination rests on (uploaded supplier declaration or test report), and
   effective dates.
3. **60-day grace clock.** Log the date a supplier notice of changed warning content arrived per SKU,
   count down 60 days, alert before expiry.
4. **Dated evidence archive.** Timestamped snapshots of each product page as actually displayed,
   exportable as a PDF pack — the artifact you hand counsel the day a 60-day notice lands.

### Stack Claude would build it with

Next.js + TypeScript on Vercel; Supabase for Postgres, auth and snapshot storage; the official
Shopify app template with Admin GraphQL for catalog reads; Playwright on a scheduled job for page
rendering and screenshot capture; the public OEHHA chemical list ingested as a versioned table;
Shopify Billing API for subscriptions. A plain TypeScript rules engine — no ML anywhere.

### First acquisition channel

The CA AG publishes every 60-day notice ([oag.ca.gov/prop65](https://oag.ca.gov/prop65)), and
Prop 65 Clearinghouse publishes settlements
([link](https://www.prop65clearinghouse.com/settlements)). Both name the noticed company and product
category. Cold outreach to brands in categories **being noticed this month** who have not yet been
noticed themselves, leading with a free scan of their own store. Secondary: the Amazon and Shopify
seller threads above, where sellers surface at the moment of maximum urgency.

### Benchmarked price point

The commodity floor is real: Shopify apps that bolt a blanket Prop 65 warning onto every product run
**around $10/month** (e.g. Warn / Warnify, [apps.shopify.com/product-notes](https://apps.shopify.com/product-notes)).
The enterprise tier — Source Intelligence, Regilient, Sustalium, Assent — is quote-only with no
public pricing. **Price at $49/month**, roughly 5× the display-only app, and trivially below a single
$10,000 settlement. Reuse the ID 006 precedent: free one-off audit as the lead magnet, charge for the
recurring register and archive.

### The single biggest risk

**The software cannot make the determination.** Knowing *which* listed chemical is in a product
requires supplier declarations or lab work — **$150–$300 per sample** for heavy-metals screening,
**$500–$2,000** for multi-group panels, and **up to $10,000 per product** for a toxicologist exposure
assessment ([Compliance Gate](https://www.compliancegate.com/california-proposition-65-product-lab-testing/)).
So this tool can honestly audit *whether a compliant warning is displayed and documented* — it cannot
tell a merchant *whether they need one*. Marketed as the latter, it recreates ID 001's exact exposure:
accessiBe was fined **$1M by the FTC** for claiming a widget delivered compliance. Secondary risk:
businesses with **9 or fewer employees are statutorily exempt**
([Payne & Fears](https://www.paynefears.com/small-business-guide-proposition-65)), so the buyer is a
10–200 employee brand, not a hobbyist — a smaller pool than the enforcement numbers suggest.

---

## This week's validated ideas

| ID | Idea | Mode | Dem | White | Feas | Money | Composite | Key evidence |
|----|------|------|-----|-------|------|-------|-----------|--------------|
| 010 | Prop 65 warning audit + determination register + evidence archive | B | 4 | 3 | 3 | 4 | **14** | 5,398 notices (2024) / 5,000+ (2025) from ~40 private enforcers; 1,300+ settlements totalling $101M in 2024 vs 890/$26M in 2022; Amazon settlements $10–20K, $40–90K post-litigation; two Amazon Seller Central distress threads; 60-day internet-retailer grace period, enforcement date 1 Jan 2028 |
| 011 | Supplier PO chasing / follow-up for small brands (parked lead, now scored) | B | 4 | 2 | 4 | 3 | **13** | Three Shopify Community threads: "Purchase order app – what are you using?" (/t/213283), "When will Shopify add a vendor or supplier list just like customers" (/t/70705), and "chasing suppliers for POs" named in /t/652975. **But cheap tier already occupied:** Auto Purchase Orders Essential **$24.99/mo** (50 POs), Replenishly Pro **$299/yr**, Prediko from $49/mo, Precoro reported at both **$499/mo Core** and **$35/user/mo** (conflict unresolved) |

ID 011 is recorded primarily as a **negative finding**: the demand is well-evidenced across three
independent threads, and the $10–50 tier is already arbitraged. Same arc as IDs 004 and 009. Do not
build; do not re-research the category.

---

## Top-10 backlog snapshot

| Rank | ID | Idea | Composite | Status |
|------|----|------|-----------|--------|
| 1 | 001 | Honest accessibility scan + fix pack for small e-commerce | 16 | Deep-Dived |
| 2 | 010 | Prop 65 warning audit + determination register + evidence archive | 14 | **Deep-Dived (this week)** |
| 3 | 006 | Auto-renewal / click-to-cancel flow monitoring + evidence archive | 13 | Deep-Dived |
| 4 | 003 | Small-batch maker COGS / batch-cost tracker | 13 | New |
| 5 | 011 | Supplier PO chasing / follow-up for small brands | 13 | New |
| 6 | 002 | EU AI Act Art. 50 transparency kit for SMEs | 12 | New |
| 7 | 007 | US state packaging-EPR reporting assistant | 12 | New |
| 8 | 009 | Sub-$50 inventory forecasting for small Shopify stores | 12 | New |
| 9 | 004 | SMB-priced AI-visibility / AEO tracking | 11 | New |
| 10 | 008 | Shopify app-subscription spend auditor | 11 | New |

(ID 005, Etsy bulk-edit, composite 10, is retired.)

---

## Risks and watch-outs

- **Every score in this backlog is Mode B.** Four runs, zero pages read in full. Prices and quotes
  come from search-result text, which is verbatim but unverified in context. One live conflict:
  Precoro at $499/mo vs $35/user/mo. Recorded, not resolved.
- **ID 010's marketing claims are the real hazard, not the build.** Automated auditing cannot
  establish whether a warning is *required*. Any copy implying "Prop 65 compliant" invites the
  accessiBe outcome. The honest product is a documentation-and-evidence tool.
- **The 9-employee exemption caps ID 010's market** and is easy to overlook when the enforcement
  statistics look so large.
- **Marketplace-mediated demand is fragile.** ID 011 sits inside Shopify's ecosystem, where Shopify
  shipped native purchase orders into the admin — a platform feature release can erase the category.
- **Market context (not idea-specific), refreshed from Flippa:** micro-SaaS under $1M ARR sells at an
  average **2.85× annual profit**, top quartile **6.13×**; Chrome extensions at **24–40× monthly
  revenue**; SaaS transactions on Flippa up **73.5% in 2025**
  ([Flippa multiples](https://flippa.com/blog/saas-multiples/)). Useful as a willingness-to-pay floor,
  not as validation of anything above.
- No income or profit outcome is claimed or implied anywhere in this report.
