# PRD — Switchkart SEO + AEO Remediation Sprint

| | |
|---|---|
| **Project** | Switchkart Technical SEO + AEO Remediation Sprint |
| **Client** | Switchkart (switchkart.com) — refurbished phones marketplace, Bangalore |
| **Studio** | Daily Web (a Daily Mark8ing studio · legal entity AKAARA SERVICES) |
| **Owner** | Piyush Mishra (Founder) |
| **Status** | Proposed — awaiting kickoff |
| **Invoice** | DW-2026-0001 — ₹50,000 + 18% GST = ₹59,000 |
| **Drafted** | 12 May 2026 |
| **Source audit** | `docs/audit-april-2026.md` (SwitchKart SEO/AEO Audit, April 2026) |

---

## 1. Why this sprint exists

The April 2026 audit gave Switchkart a **SEO Health Score of 34/100** and an **AEO Readiness Score of 28/100**. Content fundamentals (blog, titles, meta) have improved since January, but structural execution is the bottleneck: collection pages have no H1, product schema is missing fields Google requires for rich results, the site is not connected to Google Merchant Center, blog posts and key pages lack FAQ/Author/LocalBusiness schema, and a desktop CLS issue is degrading page-speed signals.

The competitive context has also shifted: Google AI Mode is live in India, AI Overviews suppress organic CTR from ~1.6% to ~0.6%, and competitors (Cashify) are already publishing AEO-optimized content. Switchkart's content quality is genuinely good — the structural SEO/AEO gaps are what's blocking distribution.

This sprint **fixes the structural blockers** identified in the audit. It is execution-only, not strategy or content production.

---

## 2. Goals & Success Metrics

### Primary goals
1. **Unlock rich results** — every product page eligible for Google rich snippets (price, availability, condition, ratings once collected).
2. **Activate Google Shopping** — Switchkart products live in Google Merchant Center with a clean feed.
3. **Make the site AEO-ready** — FAQPage, BlogPosting/Author and LocalBusiness schema deployed so Switchkart can be cited in AI Overviews and AI Mode.
4. **Clear technical debt** — no soft/hard 404s, no CLS warnings on desktop, no orphan indexed pages.

### Measurable success metrics (verified 30 days post-deploy)

| Metric | Baseline (Apr 2026) | Target (T+30 days) |
|---|---|---|
| Collection pages with valid H1 | 0 / 20 | 20 / 20 |
| Product pages passing Google Rich Results test | failing (no aggregateRating, wrong brand) | passing — schema valid |
| Soft 404s in Google Search Console | present on stocked-out collections | 0 |
| Hard 404s in Google Search Console | unknown | 0 (or all redirected/410'd) |
| Google Merchant Center feed status | not connected | connected, feed approved |
| Desktop CLS (Core Web Vitals — homepage + top 3 collections) | failing | passing (< 0.1) |
| Blog posts with FAQPage schema | 0 / 10 | 10 / 10 |
| Pages with LocalBusiness/MobilePhoneStore schema | 0 | Homepage + Contact |
| Author bio + schema on blog posts | 0 | 10 / 10 |

### Out-of-scope outcomes (explicitly not promised)
- Specific organic traffic numbers (depend on content velocity + external factors).
- Keyword rankings (depend on backlinks, competitor activity, query volume).
- AI Overview citations (depend on Google's selection — we can only make Switchkart eligible).

---

## 3. Scope — what's in

The six deliverable areas billed under invoice **DW-2026-0001**:

### 3.1 — 404 audit & remediation
- **Soft 404 fixes** on stocked-out collections and the front-page collection. Options: (a) keep the collection live with "Notify me" / waitlist UI; (b) 301 to a parent category; (c) 410 the URL if permanently retired. Decision per URL, documented in `docs/404-decisions.md`.
- **Hard 404 sweep** via Google Search Console + Screaming Frog. Each non-200 mapped to: redirect, restore, or intentional 404/410.
- **Dummy Blog 1** (`/blogs/dummy-blog-1`) — deleted or `noindex`'d (per audit Issue 5).
- **`sameAs` cleanup** in Organization schema — remove the Shopify backend URL (`qmvvde-qq.myshopify.com`), keep only verified social/brand URLs (per audit Issue 6).

### 3.2 — Google Shopping / Merchant Center connection
- Create / verify Google Merchant Center account for Switchkart.
- Install Google & YouTube Shopify channel + connect to GMC.
- Map Shopify product taxonomy → GMC categories (focus: refurbished electronics).
- Set product condition correctly (`refurbished` — not `new`).
- Verify GTIN / MPN handling for refurbished SKUs.
- Submit feed; resolve initial feed errors / warnings until **status = active**.
- **Excluded:** Google Ads / Performance Max campaign setup, ad spend, ongoing feed management beyond initial submission.

### 3.3 — Merchant listings + product schema upgrade
Three corrections on every product page (per audit Issue 3):
1. **`brand.name`** → actual device manufacturer (Apple, Samsung, OnePlus, Xiaomi, etc.), driven from Shopify product vendor / metafield. Currently hardcoded "switchkart" — semantically wrong.
2. **`itemCondition`** → explicitly set `"http://schema.org/RefurbishedCondition"` on the Offer object. This is the key differentiator for refurbished marketplaces in search.
3. **`aggregateRating`** scaffold — schema structure deployed; values populate once review collection (see §3.6) is live. Until then, the property is included only on products with ≥3 verified reviews.
- Additional merchant-listing fields per Google's product schema requirements: `availability`, `price`, `priceValidUntil`, `priceCurrency`, `seller.name`.

### 3.4 — Desktop CLS / page-speed fix
- Diagnose CLS source (PageSpeed Insights → field + lab data → element identification).
- Fix likely culprits: unsized images/hero banners, late-loading webfonts, lazy-loaded blocks shifting layout, popup/banner injection.
- Set explicit `width`/`height` or aspect-ratio on hero, product images, and above-the-fold elements.
- Preload critical webfonts; add `font-display: swap` if missing.
- Re-test until **homepage + top-3 collection pages pass Core Web Vitals on desktop** (CLS < 0.1, LCP < 2.5s, INP < 200ms).
- **Excluded:** mobile CLS deep-dive if separate from desktop fix; image compression / WebP migration if requires bulk re-upload of product assets (will be flagged with quote if needed).

### 3.5 — Schema additions
| Schema | Where | Notes |
|---|---|---|
| `FAQPage` | All 10 blog posts that have FAQ sections | JSON-LD, per audit Issue (AEO weaknesses) |
| `BlogPosting` (meta details) | All 10 blog posts | Includes `headline`, `datePublished`, `dateModified`, `image`, `mainEntityOfPage` |
| `Author` (Person) | All blog posts | Includes `name`, `jobTitle`, `url` (author bio page if exists, else homepage) |
| `LocalBusiness` / `MobilePhoneStore` | Homepage + Contact page | Bangalore address, phone, opening hours, `areaServed`, `priceRange` |

### 3.6 — Light supporting fixes (bundled — no separate charge)
- Fix multiple H1s on homepage (Issue 2) — consolidate to one canonical H1.
- Add H1 to all 20 collection pages (Issue 1) — edit `sections/main-collection-banner.liquid`.
- Image alt text on top-10 product pages (Issue 4) — pattern: `"{Brand} {Model} {Storage} {Color} — Certified Refurbished | SwitchKart"`. Full catalog alt-text remediation if requested as separate scope.

---

## 4. Out of scope

Explicitly **not** included in this sprint (will require separate scope + invoice if requested):

- New content production (blog posts, buyer guides, local Bangalore content).
- HARO / guest posting / link-building outreach.
- Google Business Profile setup & optimization (recommended separately).
- Review collection workflow build-out (the *schema* scaffold is in scope; the email/WhatsApp follow-up tooling is not).
- Google Ads / Performance Max / paid social campaigns.
- Ongoing SEO retainer / monthly reporting beyond a single post-deploy verification.
- Theme redesign or UI changes beyond what's needed to fix CLS.
- Mobile app SEO / app store optimisation.

---

## 5. Timeline

**Sprint duration:** 4 calendar weeks from advance receipt.

| Week | Block | Output |
|---|---|---|
| W1 | Access setup · 404 audit · schema staging environment · CLS diagnosis | `404-decisions.md`, theme dev environment ready, GMC account created |
| W2 | Schema upgrades (product + FAQ + BlogPosting + Author) · H1 fixes · `sameAs` cleanup | All schema live in staging |
| W3 | LocalBusiness + Merchant Center feed setup + CLS fix push | GMC feed submitted; CLS fix deployed to staging |
| W4 | Production deploy · Search Console + GMC verification · 7-day soak · documentation | Production live; sign-off doc |

Buffer: +1 week for Merchant Center feed approval (Google-side latency, outside our control) and any client review cycles.

---

## 6. Acceptance criteria

Sign-off requires **all** of:

1. ✅ Google Rich Results Test passes for: homepage, one collection page per device family, three sample product pages, two blog posts.
2. ✅ Google Search Console — "Crawled, currently not indexed" and "Soft 404" reports show zero new entries 14 days post-deploy.
3. ✅ Google Merchant Center feed status = **Active**, no critical errors.
4. ✅ PageSpeed Insights desktop — CLS < 0.1 on homepage + top-3 collections (verified via field data after 28-day rolling window if available; lab data acceptable for sign-off if field data sparse).
5. ✅ Visual diff of theme code — all schema additions traceable in git, documented in `docs/changelog.md`.
6. ✅ One walkthrough call (≤ 60 min) explaining what was changed and how to maintain it.

---

## 7. Access & dependencies

**From Switchkart (required before W1 can start):**

- Shopify Admin (Staff account) — `Manage theme`, `View products`, `Edit themes` permissions.
- Google Search Console — owner or full user access to `switchkart.com` property.
- Google Analytics 4 — read access for traffic baseline + post-deploy verification.
- Google Merchant Center — admin access (or invite to create on Switchkart's behalf).
- GitHub / Shopify theme repo (if theme is version-controlled outside Shopify) — read/write.
- Domain registrar / DNS — read access for DNS verification if GMC requires.
- Authorised contact for go/no-go decisions on 404 strategy + content edits.

**From client (decisions needed early in W1):**

- 404 handling preference per stocked-out collection (waitlist UI vs redirect vs 410).
- Author identity for blog posts (single byline vs multi-author) + bio copy.
- LocalBusiness opening hours + service area copy.

---

## 8. Risks & mitigations

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Merchant Center feed flagged for refurbished item-condition rules | Medium | Could delay W3 deliverable | Submit early in W3 to leave 1-week buffer; refurbished policy reviewed in advance |
| CLS root cause is in a paid theme block we can't modify | Low | Forces theme-customisation workaround | Diagnose in W1; if blocker, flag immediately and propose theme-section override |
| Client review cycles slow approval on 404 decisions / copy | Medium | Pushes timeline beyond W4 | Decisions captured in W1 with explicit 48-hour SLAs documented in shared doc |
| Google Search Console takes 14+ days to re-crawl post-deploy | Medium | Sign-off delayed | Submit URL Inspection re-index requests on each critical page after deploy |
| Theme update from Shopify overwrites custom schema | Low | Schema disappears | All theme edits committed to git; `docs/changelog.md` lists touched files for restore |

---

## 9. Commercials

- **Fee:** ₹50,000 + 18% GST (₹4,500 CGST + ₹4,500 SGST) = **₹59,000 total**.
- **Payment terms:** 50% advance (₹29,500) on receipt of invoice — kickoff trigger. 50% balance (₹29,500) on delivery / pre-handover.
- **Invoice:** DW-2026-0001 (issued 12 May 2026, from Daily Web · AKAARA SERVICES).
- **Bank:** AKAARA SERVICES · Kotak Mahindra · Koramangala · A/C 4246915159 · IFSC KKBK0000424.
- **GST treatment:** Intra-state (Karnataka → Karnataka). If Switchkart's place of supply is outside Karnataka, IGST 18% replaces the CGST+SGST split — invoice will be reissued.
- **Out-of-scope work:** quoted separately. No retroactive billing.

---

## 10. Open questions (to close before kickoff)

1. **Place of supply** — confirm Switchkart's registered GSTIN state (affects CGST/SGST vs IGST on the invoice).
2. **Switchkart GSTIN** — for the invoice "Bill to" block, if available.
3. **Authorised contact** — single point of contact at Switchkart for sprint decisions.
4. **Existing GMC** — does Switchkart already have a Merchant Center account, or do we create fresh?
5. **Author identity** — single house byline or named contributors for blog posts?
6. **Theme version control** — is the Shopify theme version-controlled (GitHub, Shopify Theme Kit), or live-edit only?

---

*This PRD is a working document. Any change to scope, fee, or timeline will be captured as a dated addendum at the bottom of this file and acknowledged by both parties before being acted on.*
