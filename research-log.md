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
