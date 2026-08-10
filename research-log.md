# Research Log

Narrative notes per week: sources and angles tried, honest read on signal quality,
and guidance for the next run.

---

## 2026-07-31 — Week 1

### Source types and categories attempted

Planned emphasis for a week-1 baseline: broad sweep across primary-complaint sources
(Reddit / HN / Indie Hackers), 1-2 star review mining (Chrome Web Store, G2, Capterra,
Shopify app store), and marketplace willingness-to-pay signals (Acquire.com, Flippa).

Categories probed: Etsy/Shopify seller operations, short-term-rental host tooling,
freelancer invoicing and payment chasing, nonprofit/church volunteer scheduling,
cleaning/field-service crew scheduling, small food-producer production planning,
and Make/Zapier long-tail automation gaps.

### Honest read on signal quality: **unusable this week**

This run failed to produce a single idea meeting the evidence bar, and the cause was
tooling access, not a shortage of opportunity. Documented precisely so future runs
don't repeat the same dead ends:

1. **WebFetch is fully blocked in this environment.** Every host returned `HTTP 403
   Forbidden` at the tool layer — including `example.com` and `wikipedia.org`, which
   rules out a site-level block or a bot-detection issue. Also 403'd:
   `news.ycombinator.com`, `community.etsy.com`, `apps.shopify.com`, `g2.com`,
   `blog.acquire.com`, `producthunt.com`.
2. **Reddit is explicitly off-limits to the crawler.** `WebSearch` with
   `allowed_domains: ["reddit.com"]` returns a hard API error: *"The following domains
   are not accessible to our user agent: ['reddit.com']."* Reddit content also does not
   appear organically in results, even with `site:reddit.com` in the query string.
3. **Direct HTTP is blocked by egress policy.** `curl` to `hn.algolia.com` and
   `www.reddit.com` both failed with `CONNECT tunnel failed, response 403`, confirmed
   against the agent proxy status endpoint (`kind: connect_rejected`). Per the proxy
   README, policy denials must be reported, not routed around — so no workaround was
   attempted.
4. **That leaves WebSearch alone**, which returns page titles, URLs, and an AI-written
   summary of pages I cannot open and cannot verify. The routine's own brief names this
   exact artifact as insufficient: *"A single generic search result summary is NOT
   sufficient evidence."*

Compounding the access problem, WebSearch result sets for "user complains about X"
queries were dominated by SEO listicles ("7 Best cleaning business software tools in
2026"), vendor marketing pages, and Gumroad template spam. Queries aimed at 1-star
review text returned product *landing* pages, never review text. The search tool itself
repeatedly volunteered that it could not find the requested primary discussions.

Rather than pad the backlog with plausible-sounding ideas backed by unverifiable
summaries, this week reports zero — per the brief's explicit instruction to report
fewer honestly. A fabricated evidence trail would poison the persistent backlog for
every subsequent week, which is a far worse outcome than an empty week 1.

### What *was* established (market-level context only — NOT per-idea demand evidence)

These are real, linkable, and useful as background, but none validates a specific idea:

- Acquire.com's biannual multiples report (Jan 2026) puts the median SaaS sale at a
  **3.9x profit multiple** across 2024 and 2025 —
  https://blog.acquire.com/acquire-com-biannual-acquisition-multiples-report-jan-2026/
- Live Flippa listings show real small-SaaS businesses transacting at this scale:
  an AI SaaS at **$1.9K MRR, 74% gross margin, 230+ Stripe-verified subscribers**
  (https://flippa.com/11936046), and an e-commerce product-research SaaS at **$3K MRR**
  (https://flippa.com/12021962). Useful as a general willingness-to-pay floor.
- Indie Hackers solo-founder traction posts exist and are indexed (Zigpoll at ~$125K MRR
  solo; Habit Pixel $0 to $1K MRR in eight months) — these are *reachable by search but
  not readable*, so they remain unusable as quoted evidence.

### Guidance for next week

**Blocking issue to resolve first — this is the whole ballgame.** Nothing about the
research method needs changing; the access does. Ask the environment owner to either
enable WebFetch, or extend the egress allowlist to `reddit.com`, `news.ycombinator.com`,
`hn.algolia.com`, `www.indiehackers.com`, `chromewebstore.google.com`, `g2.com`,
`capterra.com`, `producthunt.com`, `apps.shopify.com`, and `app.acquire.com`.
Until one of those lands, every weekly run will terminate here for the same reason and
burn a scheduled slot for nothing.

**If access is restored**, start from the four parked leads in `idea-backlog.md` rather
than a cold sweep — the Etsy bulk-edit and cottage-food-production leads are the two
worth attacking first, and both need a competitive teardown before scoring (Etsy tooling
in particular smells crowded, and should probably score 1-2 on whitespace).

**If access is NOT restored**, do not re-run the same sweep — it is now known to be a
dead end. Better fallback uses of the slot, in priority order:
1. Mine *marketplace listings* (Flippa/Acquire listing titles surface real MRR figures
   directly in search results, without needing to open the page) to reverse-engineer
   which micro-SaaS categories are actually transacting.
2. ~~Mine public GitHub issue trackers via the GitHub MCP tools.~~ **Ruled out — do not
   attempt.** The GitHub MCP tools are present and unaffected by the WebFetch block, but
   this session's repository scope is restricted to `oddlyevens/ecommerce-idea-research`,
   and the scope rules explicitly prohibit using search tools that don't take a repo
   argument (such as `search_issues`) to reach outside it. Public-repo issue mining would
   require the environment owner to widen repository scope first. Noting this here so a
   future run doesn't rediscover it and waste the slot.

**Angles now considered saturated / low-yield — deprioritize:** generic "best X software
2026" queries (pure SEO farm), Shopify order-export tooling (many incumbents), and
freelancer invoice-chasing (crowded, and searches returned only vendor blogs).

---

## 2026-07-31 — Week 2 (Run 2, same calendar day as week 1)

**Note on filing:** the scheduler fired twice on 2026-07-31. Week 1's report
(`product-ideas-2026-07-31.md`) documents a zero-result run and was **not** overwritten;
this run is filed as `product-ideas-2026-07-31-run2.md`.

### Evidence mode: **B** (WebFetch UNAVAILABLE — second consecutive run)

STEP 0 control fetches were run fresh, not assumed from last week:

- `https://example.com` → **HTTP 403 Forbidden**
- `https://en.wikipedia.org/wiki/Main_Page` → **HTTP 403 Forbidden**

Both trivial hosts failing rules out site-level bot detection; this is the same
environment-level egress block week 1 documented. **The block now looks persistent rather
than intermittent.** Per the brief, WebFetch was not retried after the STEP 0 check and no
curl/direct-HTTP workaround was attempted.

### What worked this run — the method change that unblocked it

Week 1 concluded WebSearch alone was unusable. That was too pessimistic, and the fix was
narrow: **WebSearch returns result *titles* verbatim, and titles can themselves carry hard
evidence.** The AI-written summary is the untrustworthy part, not the whole output. Query
patterns that made titles do the work:

1. **Competitor + price in the query** → titles come back containing real list prices.
   Best single hit of the run: `"Profound Alternatives: 5 AI Visibility Tools That Don't
   Cost $499/Month"` — a competitor name, a real price, and a positioning complaint, all in
   a verbatim title.
2. **Marketplace listing mining** (week 1's own suggestion — it worked). Flippa listing
   titles embed real metrics: `"$44K rev, $8.5K profit in 10 mos, $3.9K MRR, 77 subs,
   5.0-star Chrome extension"`. Numbers straight from the title, no page open needed.
3. **Forum-thread-title targeting.** Searching the *shape of a thread title* rather than the
   topic surfaced e.g. Soapmaking Forum's "Inventory and batch tracking software" and the
   AppleVis thread "Website widget overlays (accessiBe, Userway, etc) are not accesible."
4. **Regulatory forcing functions** turned out to be the richest vein by far — real dates,
   real fines, real enforcement actions, all indexed and quotable without opening a page.
   This is what produced ID 001 (composite 16), the only strong idea in two runs.

### What did NOT work

- Generic "I wish there was an app that" / "is there a tool that" exact-phrase queries →
  still pure SEO listicle farm (`bigideasdb.com`, `appnatively.com`, "40 App Ideas Backed by
  1M+ Complaints"). Week 1 said this; confirmed again. **Stop using these.**
- `site:` operators and Reddit remain unavailable — Reddit is hard-blocked to the user agent.
- Chrome Web Store 1-star review text is not reachable by search; queries return platform
  docs and Google Groups threads about the review system being broken, never review text.
- Asking for HN *comment* content returns only the submission title. Comments need Mode A.

### Honest read on signal quality: **usable but soft**

Four ideas cleared the Mode B bar, versus zero last week — a real improvement, and the method
above is the reason. But calibrate down: no page was read in full, and one direct conflict
went unresolved (Craftybase entry price reported as both $20/mo and $49/mo Studio by
different sources). Where sources conflicted I recorded the conflict rather than picking.

Three of the four new ideas score poorly on whitespace (1–2). That is not padding — those
rows exist so week 3 does not re-research crowded ground. The genuine finding is ID 001, and
it came from asking "where does regulation force a purchase?" rather than "what are people
complaining about?"

**Negative findings recorded deliberately** (each one saves a future slot):
- PCI DSS 6.4.3/11.6.1 → killed by a 2025 SAQ A change; obligation no longer reaches small
  merchants. Ruled out.
- Etsy bulk-edit → crowded (Evlista, eRank, Sale Samurai, Alura). Retired.
- Maker inventory → crowded (Craftybase, Inventora, SoapMaker 3, plus free open-source
  Craftplan). Recorded but capped at whitespace 2.

### Guidance for next week

1. **If WebFetch is restored, drop everything and fetch
   [news.ycombinator.com/item?id=48045237](https://news.ycombinator.com/item?id=48045237)
   first** — "Ask HN: What do you still do manually in 2026 that should be automated?" Its
   stated criteria (5+ times a week, looked for a tool and nothing good exists, would pay
   $10–20/month) match this project's brief almost exactly. Hundreds of self-qualified demand
   statements on one page. This is the single highest-value target identified in two runs.
   Second priority under Mode A: re-validate ID 001 by opening the FTC order PDF and the
   TestParty lawsuit research directly.
2. **If still Mode B, lead with regulatory forcing functions** — the vein that actually
   produced this week's only strong idea. Untried candidates: EU Digital Product Passport
   (textiles/batteries, 2027 — check whether prep demand exists *now*), state-level US privacy
   laws hitting small e-commerce, EU packaging waste regulation, and the EAA's national
   implementations diverging by member state. Pair each with a price-anchored competitor query
   to force list prices into result titles.
3. **Also still Mode B: keep mining marketplace listing titles** (Flippa, Acquire) — verbatim
   MRR figures with no page access required. Useful for reverse-engineering which micro-SaaS
   categories actually transact.
4. **Escalation, unchanged from week 1 and now more warranted:** two consecutive runs blocked.
   Ask the environment owner to enable WebFetch or extend the egress allowlist to at least
   `news.ycombinator.com`, `hn.algolia.com`, `reddit.com`, `chromewebstore.google.com`,
   `apps.shopify.com`, `g2.com`, `capterra.com`, and `producthunt.com`. Mode B works, but it
   yields provisional evidence and caps confidence on every score in the backlog.
5. **Do not re-research:** generic wish-phrase queries, Etsy seller tooling, maker/craft
   inventory, AI-visibility tracking, PCI DSS client-side scripts, freelancer invoice chasing,
   Shopify order export, "best X software 2026" queries.

---

## 2026-08-03 — Week 3

### Evidence mode: **B** (WebFetch UNAVAILABLE — third consecutive run)

STEP 0 control fetches re-run fresh, not assumed:

- `https://example.com` → **HTTP 403 Forbidden**
- `https://en.wikipedia.org/wiki/Main_Page` → **HTTP 403 Forbidden**

Identical to weeks 1 and 2. Three consecutive runs, both trivial control hosts failing, no variation:
**the block is persistent, not intermittent.** Per the brief, WebFetch was not retried after STEP 0 and
no curl/direct-HTTP workaround was attempted.

### The methodological breakthrough this week — Shopify App Store review text is searchable

Week 2 concluded that 1-star review text was unreachable. That conclusion was **correct for the Chrome
Web Store and wrong as a generalisation**. `apps.shopify.com/<app>/reviews` pages are indexed and their
verbatim review text comes back in search-result text. This is the first channel in three runs that
yields *actual user complaints with dollar figures*, not law-firm summaries.

Query shape that works:

```
apps.shopify.com reviews <category> "<complaint phrase>" merchant 1 star
```

It produced, verbatim: *"it became so expensive that it put the app out of the question for us"* and
*"Held hostage on a 12 month contract… was paying about $300/month and they jacked it up over
$600/month."* That is exactly the evidence class the brief asks for, obtained under Mode B.

**Second new channel: `community.shopify.com` threads are indexed, titles *and* partial reply content.**
Search surfaced not just the thread title but merchants' actual answers ("reordering stock before it runs
out, reconciling inventory across locations, chasing suppliers for POs"). Four high-value threads are now
parked in `idea-backlog.md`. This partially defeats the week-2 finding that forum *comments* need Mode A —
Shopify's forum is more indexable than HN's.

### What did NOT work (each of these saves a future slot)

- **Acquire.com listing mining** — unlike Flippa, returns only SEO listicles and Acquire's own marketing
  pages, never listing titles with metrics. **Flippa listing mining still works** (a `$44K rev, $8.5K
  profit, $3.9K MRR, 77 subs` title came back again). Use Flippa, skip Acquire.
- **G2 / Capterra review text** — still unreachable. Queries return platform-comparison content about G2
  and Capterra themselves. The search tool explicitly said the reviews "require searching within the
  review platforms themselves." Confirmed twice now; **stop trying**.
- **Generic price-hike backlash queries** — surfaced real numbers (QuickBooks +25% in 2026, Plus $85→$99,
  Desktop Pro Plus $1,149/yr) but only for categories far too large to build against. Low yield for a
  solo builder; the wedge is always "replace an accounting suite."
- Attempts to surface the `/t/577348` "$100/month problem" thread's replies failed — only the title and
  the opening post came back. Title-shaped queries get the thread; content-word queries get the replies.
  Use content words.

### Honest read on signal quality: **best channels yet, weakest ideas yet**

A genuine tension this week. The evidence *channels* improved materially (real merchant quotes for the
first time), but the ideas those channels produced scored **11–13** — worse than week 2's ID 001 at 16.
That is not a failure of method; it is what the evidence said, and it is recorded rather than inflated.

Two structural findings worth carrying forward:

1. **The regulatory vein has a hard ceiling of Demand 3.** It reliably produces deadlines, fines and price
   anchors — and it produced the backlog's only 16 — but it never produces a person saying they want to
   buy something. IDs 002, 006 and 007 are all capped at 3 for this reason, consistently.
2. **Obvious price chasms are already arbitraged.** ID 004 (AI visibility) and now ID 009 (inventory
   forecasting) followed the identical arc: a loud, verifiable "too expensive" complaint, and a $10–49/mo
   competitor already sitting in the gap by the time it was found. **New rule for week 4: check the cheap
   tier before scoring demand, not after.** A "too expensive" complaint is a lagging indicator.

Also recorded: the ID 008 kill. Merchant fury about Shopify app costs is loud and quotable, but **only
1.8% of stores spend over $100/mo on apps** — the complaints are real and the paying pool is thin. Finding
the datum that kills an idea is the week's second-most useful output.

### Guidance for next week

1. **If WebFetch is restored, the target order is unchanged at the top:**
   [news.ycombinator.com/item?id=48045237](https://news.ycombinator.com/item?id=48045237) first, then the
   four `community.shopify.com` threads now parked in the backlog, then re-validate ID 001 (FTC/accessiBe
   order) and ID 006 (ProsperStack pricing page, state ARL texts) under Mode A.
2. **If still Mode B, lead with marketplace review mining — it is now the highest-yield channel.** Extend
   the `apps.shopify.com reviews "<phrase>"` pattern to other indexed marketplaces not yet tested:
   WordPress.org plugin reviews, Atlassian Marketplace, Zapier app reviews, Notion template marketplaces,
   Squarespace/Wix extensions. Prioritise categories with **few** competing apps — this week's failures
   (wholesale, returns, forecasting) all had 9+ incumbents visible on a single results page.
3. **Pair every review-mined complaint with an immediate cheap-tier check** before writing it up. Two of
   four ideas this week died at that step, and both deaths were only discovered after the demand work.
4. **Regulatory vein — remaining untried:** state-level ARL expansion beyond CA/NY/MN/VA, NY algorithmic
   pricing disclosure, FTC junk-fee rule for lodging/ticketing. Expect Demand 3 ceilings; only pursue if
   paired with a real price chasm as ID 001 was.
5. **Escalation, third consecutive run.** Mode B is now genuinely productive — this run disproved two of
   week 2's "unreachable" verdicts — so the block is no longer fatal. But no page has been read in three
   runs and every score carries that caveat. Enabling WebFetch, or allowlisting
   `news.ycombinator.com`, `hn.algolia.com`, `reddit.com`, `community.shopify.com`, `apps.shopify.com`,
   `g2.com`, `capterra.com` and `producthunt.com`, would raise confidence across the entire backlog.
6. **Do not re-research** (additions this week): local-food/farm ordering, cookie/GPC scanners, Shopify
   B2B wholesale, Shopify inventory forecasting, Shopify app-spend auditing, EU PPWR, EU DPP, and
   Acquire.com listing mining — plus everything on week 2's list.

---

## 2026-08-10 — Week 4

### Evidence mode: **B** (WebFetch UNAVAILABLE — fourth consecutive run)

STEP 0 control fetches re-run fresh, not assumed:

- `https://example.com` → **`EGRESS_BLOCKED`** — "Access to example.com is blocked by the network egress proxy."
- `https://en.wikipedia.org/wiki/Main_Page` → **`EGRESS_BLOCKED`** — same message.

**The error shape changed this week and it is diagnostically useful.** Weeks 1–3 all reported a bare
`HTTP 403 Forbidden`; this run returns a structured `{"error_type":"EGRESS_BLOCKED","domain":...}`
envelope naming the egress proxy explicitly. Same outcome, but it settles the open question from week 1:
this is a **deliberate egress allowlist**, not bot detection, not a site-level block, and not a transient
fault. Four runs, zero variation. Per the brief, WebFetch was not retried after STEP 0 and no
curl/direct-HTTP workaround was attempted.

### Channels tested this week — two new, one confirmed, four dead

**NEW and working: `wordpress.org/support/topic/` review titles are indexed verbatim.** WordPress.org
files plugin reviews as support topics, and the title comes back in full, e.g. *"I wish we'd never
started using WooCommerce"*, *"Extremely Poor Support, Beware — [Wholesale Suite]"*, *"Buyer Beware —
Support Now Gone for 12 Days — WTF? — [WP Compress]"*, *"Don't buy this plugin and don't fall for the
fake reviews — [Eventin]"*. Best hit of the run went further and surfaced **specific removed features**:
*"WAIT BEFORE 'UPGRADING'! [REVISED] — [WooCommerce Shipping]"* naming the lost box-packing algorithm,
label re-purchasing, and address auto-validation.

**But calibrate the channel down.** It yields *quality* complaints — poor support, bugs, fake reviews —
far more than *gap* complaints, and with roughly 60,000 plugins WordPress almost never has a hole. Every
lead it produced this week died at the cheap-tier check (box packing → Octolize; salon booking → the
1-star reviewer *names Amelia as the working alternative* in the review itself). Treat it as a
secondary channel behind the Shopify App Store, not a replacement.

**Confirmed still working:** Flippa listing-title mining (refreshed multiples: micro-SaaS <$1M ARR at
**2.85× annual profit** average, **6.13×** top quartile; Chrome extensions **24–40× monthly revenue**;
freemium extensions at $500–2K MRR selling for $15–60K; Flippa SaaS transactions **+73.5% in 2025**),
and `community.shopify.com` thread + partial-reply indexing.

**Dead — stop trying (each confirmed this run):**
- **Trustpilot review text** — aggregator/SEO pages (softwareadvice, G2, Capterra, GetApp) intercept
  every query. Same failure mode as G2/Capterra in week 3.
- **iOS / Google Play review text** — not indexed. Queries return ASO-industry blog posts about review
  management. This closes out the last unexplored item on the brief's suggested source list.
- **Atlassian Marketplace** — returns Atlassian's own developer docs and marketplace-policy pages.
- **Notion template marketplace** — returns Notion's help-centre refund policy and Gumroad spam.

### Honest read on signal quality: **narrow but the best single idea since week 2**

Two ideas cleared the bar against a 4–6 target. Reported as two. The compensation is that one of them,
**ID 010 (Prop 65, composite 14)**, is the second-strongest row in the backlog and the first regulatory
idea in four weeks to **break the Demand-3 ceiling** that week 3 identified as structural. The reason it
broke is worth recording as a rule:

> **The regulatory vein produces Demand 4+ only when the enforcement mechanism is a private bounty,
> not a state agency.** Agency enforcement produces law-firm advisories and nobody complaining. Prop 65's
> ~40 private enforcers filing ~3 notices a day produce *victims who post on seller forums* — which is
> exactly the primary-source evidence class the brief asks for. Look for other private-right-of-action /
> bounty statutes: that is where regulation and real complaints overlap.

**Five kills this week**, all at the pre-scoring cheap-tier check — the rule week 3 introduced, now
clearly earning its place, since four of the five would otherwise have consumed full write-ups:
WooCommerce box packing (Octolize), EU Omnibus 30-day pricing (five-plus apps at $14.90–14.99/mo), FDA
nutrition labels (KitchenSync $14.99, Food Label Maker $49), EU GPSR (seven-plus vendors, and the core
deliverable is a legal service not software), HTS/tariff codes (Tariff HS Code Compliance already ships
the exact described feature).

**Also recorded honestly:** ID 011 (supplier PO chasing) graduated from parked lead to a scored row of
13, but as a *negative* finding — three independent Shopify threads confirm the pain, and Auto Purchase
Orders at $24.99/mo plus Replenishly at $299/yr already occupy the tier. This is the **fourth** instance
of the arc "loud verifiable complaint → gap already filled" (004, 009, 011, and box packing). The
pattern is now strong enough to state as a prior: *if a complaint is discoverable by searching "X is too
expensive", the arbitrage has already happened, because every other builder runs that same query.*

**Staleness check:** no row qualifies yet. The oldest ideas date to 2026-07-31, ten days ago, so nothing
has reached the 3-week threshold. ID 005 (composite 10) is the first candidate and is already retired.

### Guidance for next week

1. **If WebFetch is restored, target order is unchanged and now four weeks old:**
   [news.ycombinator.com/item?id=48045237](https://news.ycombinator.com/item?id=48045237) first, then the
   four `community.shopify.com` threads, then re-validate under Mode A in composite order — ID 001
   (FTC/accessiBe order), then **ID 010** (the OEHHA Article 6 regulation text and the CA AG's 60-day
   notice register at [oag.ca.gov/prop65](https://oag.ca.gov/prop65), which would convert ID 010's
   demand evidence from forum titles to primary records and plausibly move it to 5).
2. **If still Mode B, hunt private-right-of-action statutes** — the rule derived above is the most
   actionable finding of this run. Untried candidates with bounty or private-suit mechanics: ADA website
   suits by state (feeds ID 001), TCPA/telemarketing consent, BIPA-style biometric laws beyond Illinois,
   state wiretap claims against session-replay and chat widgets (an active plaintiff industry against
   e-commerce sites, and *directly* adjacent to ID 001's scan-and-fix shape), and FDCPA-style consumer
   statutes. Pair each with a cheap-tier check *before* any demand work.
3. **Do not spend another slot on:** Trustpilot, iOS/Android app-store reviews, Atlassian Marketplace,
   Notion Marketplace, Acquire.com, G2/Capterra, generic wish-phrase queries. The brief's suggested
   source list is now fully explored under Mode B; Reddit, HN comments, Chrome Web Store and Product Hunt
   comments require Mode A and nothing else remains untested.
4. **Do not re-research** (additions this week): WooCommerce box packing and WooCommerce shipping
   generally, EU Omnibus price history, FDA nutrition labels, EU GPSR, HTS/tariff codes, supplier PO
   tooling — plus everything on weeks 2 and 3 lists.
5. **Escalation, fourth consecutive run.** Mode B is genuinely productive and produced a 14 this week, so
   the block is not fatal — but the brief's own evidence bar (Mode A preferred, "do not rely on
   WebSearch's summary alone when WebFetch is available") cannot be met at all, and **no page has been
   read in four runs**. Every composite in the backlog carries that caveat. The single highest-leverage
   change available to this project remains allowlisting `news.ycombinator.com`, `hn.algolia.com`,
   `reddit.com`, `community.shopify.com`, `apps.shopify.com`, `wordpress.org`, `sellercentral.amazon.com`,
   `oag.ca.gov`, `g2.com` and `producthunt.com` for egress.
