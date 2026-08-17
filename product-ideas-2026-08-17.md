# Product Ideas — Week of 2026-08-17

## Executive summary

- **Evidence mode: B** (WebFetch UNAVAILABLE — fifth consecutive run). Both STEP 0 control
  fetches returned `EGRESS_BLOCKED`. No page has been read in five weeks; every score in the
  backlog carries that caveat.
- **The run's most durable output is a new channel, not a new idea.**
  `support.google.com/business` community threads are indexed verbatim — titles *and* partial
  reply content — and so is `localsearchforum.com`. This is the first genuinely productive
  channel found since week 3's Shopify App Store discovery, and it opens the **local-business**
  category, which this project had never touched in four prior weeks of e-commerce work.
- **Two ideas cleared the bar against a 4–6 target; reported as two, not padded.** ID 012
  (Google review disappearance archive, composite **13**) and ID 013 (CIPA website-tracking
  scanner, composite **11** — recorded as a *negative* finding).
- **Five kills at the pre-scoring cheap-tier check**, the rule that keeps earning its place:
  CIPA scanners, FTC fake-review rule tooling, GBP suspension reinstatement, TCPA/SMS consent,
  and Shopify payout reconciliation (re-confirmed).
- **Deep Dive of the Week: ID 012.** It sits in a three-way tie at composite 13, and it is the
  only one of the three whose own backlog note does not already say *do not build*.

---

## Deep Dive of the Week — ID 012: Google review disappearance archive, alert + appeal evidence pack

**The pain.** Google does not notify a business when a review is removed, and reviews vanish
constantly — in silent waves, sometimes years after posting. Owners discover it by accident and
then cannot say *what* was lost, so they have nothing to appeal with.

**Evidence (two independent domains, verbatim thread titles).**

- `support.google.com/business` — at least seven distinct threads:
  *"Reviews disappeared after reinstatement – locked duplicate thread prevents follow-up"*
  ([thread/398337229](https://support.google.com/business/thread/398337229)),
  *"Listing Was Suspended + Reinstated. Lost visibility, and thousands of reviews are missing"*
  ([thread/4225597](https://support.google.com/business/thread/4225597)),
  *"Google My Business Profile Disappeared, 200+ Reviews lost"*
  ([thread/165274879](https://support.google.com/business/thread/165274879)), plus
  *"Disappearing Google reviews"*, *"Reviews Gradually Disappearing"*, *"All my reviews
  disappeared"*, *"All of our reviews have disappeared"*.
- `localsearchforum.com` — at least eight, including a five-page-plus running thread
  *"Missing Reviews/ Reviews Disappearing"*
  ([threads/59057](https://localsearchforum.com/threads/missing-reviews-reviews-disappearing.59057/)),
  *"Reviews From Years Ago Disappearing"*
  ([threads/61840](https://localsearchforum.com/threads/reviews-from-years-ago-disappearing.61840/)),
  and separately *"Review replies disappeared from Google"*
  ([threads/57011](https://localsearchforum.com/threads/review-replies-disappeared-from-google.57011/)).
  Search-result text carried a specific agency account: four client listings *"losing 3 reviews
  every day,"* consistently deleted at the same time.

**MVP feature list (5).**

1. Daily immutable snapshot of every review on each connected location — author, rating, full
   text, date, review ID.
2. Diff + alert: email the owner when a review disappears, quoting the full text of what
   vanished and when it was last seen.
3. **Appeal evidence pack** — one-click per-review PDF/CSV (text, first-seen and last-seen
   timestamps) to attach to a Google reinstatement or redressal submission. This is the wedge;
   nobody markets it.
4. Review-count-over-time chart with monthly export, for agencies reporting to clients.
5. Reply-disappearance detection — multiple forum threads report *replies* silently vanishing,
   and no competitor advertises this.

**Stack Claude would build it with.** Next.js on Vercel; Postgres (Supabase or Neon) for the
snapshot store; Google OAuth plus the Google Business Profile APIs (account/location management,
with reviews still served from the legacy `mybusiness.googleapis.com` v4 endpoint); a daily
scheduled job (Vercel Cron or `pg_cron`); Resend or Postmark for alerts; Stripe for billing;
server-side headless-Chrome rendering for the evidence-pack PDF.

**First acquisition channel.** Local Search Forum and the local-SEO agency community — the
running "Missing Reviews" thread is five-plus pages and the concentrated buyer is an agency
carrying dozens of client locations, not a single owner. Lead magnet: a free one-off "how many
of your reviews vanished last month" scan. Do **not** self-promote inside
`support.google.com` threads; it violates forum norms and would burn the channel.

**Benchmarked price point.** $9–15/mo for one location, $49–79/mo for an agency tier at 10–25
locations — deliberately under the cheapest incumbent tier actually observed. Benchmarks seen:
**Localo Single Business $39–49/mo**, **Localo Pro $149–169/mo**
([localo.com/pricing](https://localo.com/pricing)); **Reply Champion from $10/mo** (reply
automation, not archival).

**Single biggest risk — the Google API approval gate.** Google Business Profile API quota is
**0 until a separate manual access request is approved**; the review period is stated as 7–10
business days, and developers report worse. A Google Developer forum thread reads *"Business
Profile API — reviews endpoint (mybusiness.googleapis.com) can't be enabled; Basic Access
pending 10+ business days"*
([discuss.google.dev/t/389462](https://discuss.google.dev/t/business-profile-api-reviews-endpoint-mybusiness-googleapis-com-cant-be-enabled-basic-access-pending-10-business-days/389462)),
and a GBP community thread is titled *"Business Profile API quota increase request - no response
from Google"* ([thread/222003029](https://support.google.com/business/thread/222003029)).
Guidance also indicates requests are denied where a project does not consistently hit its QPM
limit. **A non-technical founder cannot code around this and the product is dead without it** —
so submit the access request on day one, against a verified GBP that is 60+ days old with a real
business website, *before* building. The gate is also the likely reason no $9 competitor exists;
it is simultaneously the risk and the moat.

---

## This week's validated ideas

| ID | Idea | Mode | Dem | White | Feas | Money | Comp | Evidence (2+ independent domains) | Competitive teardown |
|----|------|------|-----|-------|------|-------|------|-----------------------------------|----------------------|
| 012 | Google review disappearance archive + alert + appeal evidence pack | B | 4 | 2 | 3 | 4 | **13** | `support.google.com/business` (7+ threads) and `localsearchforum.com` (8+ threads), verbatim titles; agency report of 4 listings losing 3 reviews/day | Localo $39–49 single / $149–169 pro **already advertises removed-review tracking**; GMBapi monitors deleted reviews (agency-shaped); Reviewlee exports "forever"; Reply Champion from $10/mo. Feature exists inside suites — wedge is price, focus, and the appeal pack |
| 013 | CIPA / website-tracking wiretap risk scanner for small business | B | 3 | 1 | 4 | 3 | **11** | [designrush](https://news.designrush.com/cipa-demand-letters-small-business-cookiebot) *"CIPA Demand Letters Are Piling Up for Small and Local Businesses"*; [Ward and Smith](https://www.wardandsmith.com/article/the-cipa-demand-letter-wave-how-one-serial-litigant-is-turning-basic-websites-into-a-tsunami-of-lawsuits) *"…How One Serial Litigant Is Turning Basic Websites Into a Tsunami of Lawsuits"*; $5,000 statutory damages per violation | **Saturated.** PieEye $10–14/mo per site, CookieScript €8 basic / €19 full CIPA, Termly $10/site/mo, plus a free scanner at ciparisk.com and Enzuzo/Ketch/Usercentrics/ConsentPixel/Captain Compliance content-marketing the same buyer. **Do not build** |

---

## Top-10 backlog snapshot

| Rank | ID | Idea | Composite | Status |
|------|-----|------|-----------|--------|
| 1 | 001 | Honest accessibility scan + fix pack, small e-commerce | 16 | Deep-Dived |
| 2 | 010 | Prop 65 warning audit + determination register | 14 | Deep-Dived |
| 3 | 006 | Auto-renewal / click-to-cancel flow monitoring | 13 | Deep-Dived |
| 4 | 012 | **Google review disappearance archive + appeal pack** | **13** | **Deep-Dived (this week)** |
| 5 | 003 | Small-batch maker COGS / batch-cost tracker | 13 | New (category ruled out) |
| 6 | 011 | Supplier PO chasing for small e-commerce | 13 | New (negative finding) |
| 7 | 002 | EU AI Act Art. 50 transparency kit | 12 | New |
| 8 | 007 | US state packaging-EPR reporting assistant | 12 | New |
| 9 | 009 | Sub-$50 Shopify inventory forecasting | 12 | New (negative finding) |
| 10 | 004 | SMB-priced AI-visibility / AEO tracking | 11 | New (negative finding) |

_Also at 11: ID 008 (Shopify app-spend auditor), ID 013 (CIPA scanner). ID 005 (10) retired._

---

## Risks and watch-outs

- **Five weeks, no page read.** Mode B evidence is search-result text only. Nothing here is
  claimed as a full-page read, and the brief's preferred bar cannot be met until egress is
  opened.
- **ID 012's whitespace is the weak leg, not its demand.** Localo explicitly sells removed-review
  tracking today. The idea survives on price and on the appeal-evidence-pack angle; if Localo
  drops a $9 tier or Google ever ships native removal notifications, the wedge closes.
- **The API gate cuts both ways.** It is the moat *and* the single point of failure, and it is
  outside a solo founder's control. Treat approval as a go/no-go milestone before any build.
- **Fifth instance of the standing pattern.** ID 012's monitoring feature, like IDs 004/009/011
  before it, was already occupied by the time the complaint was found. The prior stands: *if a
  complaint is discoverable by searching "X is too expensive", the arbitrage has already
  happened.* The only reliable edge left is a gap that requires clearing a non-obvious barrier —
  here, Google's manual approval.
- **No income or profit claim is made anywhere above.** Market context (Flippa micro-SaaS at
  2.85× annual profit average, 6.13× top quartile) is background only, not a projection.
