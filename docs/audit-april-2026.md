# SwitchKart SEO / AEO Audit — April 2026 (extract)

> This is a structured summary of the source audit PDF, kept in this repo as the basis for sprint scope. The full PDF lives on the studio side.

## Headline scores

| Metric | Score | Change vs. Jan 2026 |
|---|---|---|
| SEO Health | 34 / 100 | +9 |
| AEO Readiness | 28 / 100 | +8 |

The site is on the right trajectory but executing at roughly **30–40%** of what the January strategy called for at this stage. Content quality is genuinely good; structural SEO/AEO gaps are what's blocking distribution.

## Progress scorecard vs. January strategy

| January recommendation | Status (Apr) | Notes |
|---|---|---|
| Launch blog content (10–12/month) | Partial | 10 posts in 3 months, not 10/month |
| Product Schema on all pages | Partial | Present, but no `aggregateRating`, wrong brand name |
| LocalBusiness Schema | Not done | No local schema anywhere |
| H1 tags on collection pages | Not done | All collection pages missing H1 |
| FAQ Schema on blog posts | Not done | FAQ content exists, no schema markup |
| Internal linking (blog → products) | Not done | Blog posts have 0 product/collection links |
| Image alt text on products | Not done | 17 images missing alt on checked product page |
| Google Business Profile | Unknown | Cannot verify externally |
| Local directory citations | Unknown | Cannot verify externally |
| Guest posting / HARO | Unknown | No external signals found |

## Critical technical SEO issues remaining

### Issue 1 — Collection pages have no H1
Every brand collection page (iPhone, Samsung, OnePlus, etc.) is missing an H1. **Fix:** edit `sections/main-collection-banner.liquid` in the Shopify theme to wrap `{{ collection.title }}` in `<h1>` tags.

### Issue 2 — Multiple H1 tags on homepage
Homepage renders at least three H1 elements: an empty logo H1, "Get to know SwitchKart", and "From Our Community. Voices of our users." Multiple competing H1s dilute topical focus. **Fix:** consolidate to a single H1, e.g. *"Buy & Sell Certified Refurbished Phones in India | SwitchKart"*.

### Issue 3 — Product schema: missing aggregateRating + wrong brand name
Product schema is present, but three errors on the Apple iPhone 14 Pro PDP (and likely all PDPs):
1. **No `aggregateRating`** — required for star-rating rich results.
2. **Brand set to "switchkart"** — should reflect the device manufacturer (Apple, Samsung, etc.).
3. **No `itemCondition`** — for refurbished products, `http://schema.org/RefurbishedCondition` should be explicit on the Offer object.

### Issue 4 — 17 of 22 product images missing alt text
On checked product page, 17 of 22 images had no alt text. Image filenames are also non-descriptive (e.g., `IMG_0065_225fdca6...`). Hurts image search + accessibility + contextual signals.

### Issue 5 — Dummy Blog 1 is indexed empty page
`/blogs/dummy-blog-1` is in the sitemap and actively indexed but has no content. Wastes crawl budget and sends thin-content signals. **Fix:** delete or `noindex`.

### Issue 6 — `sameAs` points to backend Shopify URL
Organization schema's `sameAs` array includes `https://qmvvde-qq.myshopify.com/` (the internal Shopify backend URL) as a brand-identity match. Should be only verified social/brand URLs.

## Blog content — real progress, execution gaps

10 posts published in a ~4-week window (March–April 2026). Strongest post: *"Refurbished vs New Phones: Complete 2026 Comparison Guide"* (2,000+ words, tables, FAQ, Article schema).

**Critical content gap:** zero internal links from blog posts to specific product or collection pages. Every reader who wants to buy has no guided path. Every post should link to 3–5 specific collection/product pages contextually.

**Topic coverage gaps still open** (not in sprint scope, flagged for follow-on work):
- Local Bangalore buying/selling guides (fastest conversion content)
- IMEI verification + phone grading guides (trust-building)
- Buying guides under specific price points (e.g., "under ₹20,000")
- Samsung / OnePlus / Xiaomi brand-specific guides
- Sustainability / e-waste angle (link-building hook)

## AEO readiness — the new critical dimension

Google AI Mode is now live in India. AI Overviews appear in ~13% of queries globally; CTR drops to 0.61% when AI Overviews are present (vs 1.62% without). Cashify is already publishing AEO-optimized content.

For Switchkart with under AS 20, AEO citation does not weight purely on domain authority — content extractability, answer quality, and schema accuracy matter more. This is where a new site can punch above its weight right now.

**Current AEO weaknesses:**
- No FAQPage schema (despite blog posts having explicit FAQ sections)
- Content is essay-structured, not answer-first (AEO content leads with a 40–80 word direct answer before expanding)
- No product-level Q&A / comparison content on PDPs
- No LocalBusiness schema (despite physical Bangalore address)
- robots.txt allows AI crawlers (GPTBot, ClaudeBot, PerplexityBot) implicitly via `User-agent: *` but doesn't name them — opportunity to signal AEO intent explicitly.

## E-E-A-T

**Positive signals:**
- Blancco-certified data erasure mentioned prominently
- 52-point QC inspection cited across blog + product pages
- 6-month warranty consistent across touchpoints
- GSTIN + CIN on Contact page

**Gaps:**
- No author attribution on blog posts (no bylines, bios, credentials)
- No external press mentions / backlinks
- Customer reviews on homepage not marked up with Review / AggregateRating schema

## Local SEO — not yet activated

The Bangalore local SEO opportunity — identified in January as the **fastest path to traffic** — shows no visible activation:
- No LocalBusiness schema implemented
- No Knowledge Panel for "SwitchKart Bangalore"
- No local content published
- No Justdial / Sulekha / local directory presence found in search results

Local keywords ("refurbished phones Bangalore", "sell old phone HRBR Layout", "buy refurbished iPhone Bangalore") are entirely uncontested by SwitchKart at this stage.

## Priority action plan — next 60 days

From the audit (consolidated; sprint scope is the *Critical* + most of *High Priority* items):

### Critical — this week
1. Fix H1 on all collection pages
2. Add internal links in all blog posts (3–5 per post)
3. Delete or noindex Dummy Blog 1
4. Fix product schema (brand, itemCondition, aggregateRating scaffold)
5. Add FAQ schema to all blog posts

### High priority — this month
6. Fix multiple H1 tags on homepage
7. Add LocalBusiness / MobilePhoneStore schema
8. Add image alt text on top 10 best-selling product pages
9. Add author bio to blog posts
10. Rewrite blog intros for answer-first structure

### Strategic — next 30–60 days (flagged out of sprint scope)
- Publish 6 missing pillar topics (Bangalore local, phone grading, IMEI, sub-₹20k, Samsung guide, sustainability)
- Launch Google Business Profile
- Begin review collection (target 20+ Google reviews in 60 days)
- Fix `sameAs` in Organization schema
- Explicitly allow AI crawlers in robots.txt

## Revised traffic projections

| Metric | Original Jan target (M6) | Revised target (M6 = Jul 2026) | Current (Apr 2026) |
|---|---|---|---|
| Organic monthly visitors | 2,000–5,000 | 800–2,000 | < 200 |
| Top-10 keyword rankings | 30–50 | 10–20 | 0–5 |
| Authority Score | 25–35 | 18–25 | 12–16 |
| Blog posts live | 80–100 | 25–35 | 9 substantive |
| Referring domains | 60–100 | 20–40 | < 10 |

If critical technical fixes happen in next 2 weeks: optimistic path reaches **1,500–3,000 visitors/month by Jul 2026**.

---

*Source: SwitchKart SEO/AEO Audit — April 2026 (Current State vs. January 2026 Strategy). Full PDF on file with studio. This extract is the canonical reference for sprint scope decisions.*
