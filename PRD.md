# PRD — Switchkart Shopify Theme Refresh + Search Visibility Sprint

| | |
|---|---|
| **Project** | Switchkart Shopify Theme Refresh + Search Visibility Sprint |
| **Client** | Switchkart (switchkart.com) — refurbished phones marketplace, Bangalore |
| **Studio** | Daily Web (a Daily Mark8ing studio · legal entity AKAARA SERVICES) |
| **Owner** | Piyush Mishra (Founder) |
| **Status** | Proposed — awaiting kickoff |
| **Invoice** | DW-2026-0001 — ₹50,000 + 18% GST = ₹59,000 |
| **Drafted** | 12 May 2026 |
| **Source audit** | `docs/audit-april-2026.md` (SwitchKart SEO/AEO Audit, April 2026) |

---

## 1. Why this sprint exists

Switchkart has two parallel problems that the April 2026 audit surfaced:

1. **Storefront problems** — the current theme isn't pulling its weight on mobile or desktop. Page speed is hurt by a desktop CLS issue. Layout polish is uneven across collection pages, product pages, and the homepage. The visual system isn't yet doing the work of convincing a first-time visitor that a refurbished phone is a safe, premium purchase.
2. **Search visibility problems** — the site scores 34/100 on SEO health and 28/100 on AEO readiness. Structural issues (missing H1s, broken product schema, no Merchant Center connection, no FAQ/Author/LocalBusiness schema, soft + hard 404s) are blocking organic distribution.

Doing the SEO/AEO fixes as patches on a tired theme is the wrong order. This sprint **refreshes the storefront and bakes the audit fixes into the new build at the same time** — one cohesive deploy, not a theme patch followed by a separate SEO patch.

The competitive context: Google AI Mode is live in India, AI Overviews suppress organic CTR from ~1.6% to ~0.6%, and Cashify is already shipping AEO-optimized content. Switchkart's content quality is genuinely good — the storefront polish + structural SEO/AEO gaps are what's holding back distribution.

This is a **fast theme refresh + sprint**, not a from-scratch custom-theme build. The approach is to ride on a clean, fast Shopify theme foundation, customize the high-leverage sections (home, collections, PDP), and bake all the audit fixes into that foundation as one deploy.

---

## 2. Goals & Success Metrics

### Primary goals
1. **Refresh the storefront** so mobile + desktop both feel current, fast, and trust-building.
2. **Unlock rich results** — every product page eligible for Google rich snippets.
3. **Activate Google Shopping** — Switchkart products live in Google Merchant Center with a clean feed.
4. **Make the site AEO-ready** — FAQPage, BlogPosting/Author and LocalBusiness schema deployed.
5. **Clear technical debt** — no soft/hard 404s, no desktop CLS warnings, no orphan indexed pages.

### Measurable success metrics (verified at handover and again 30 days post-deploy)

| Metric | Baseline (Apr 2026) | Target (handover) |
|---|---|---|
| Mobile usability (Google PSI) | mixed | passing on home + top-3 collections + sample PDP |
| Desktop Core Web Vitals (CLS / LCP / INP) | failing CLS | passing (CLS < 0.1, LCP < 2.5s, INP < 200ms) on home + top-3 collections |
| Collection pages with valid single H1 | 0 / 20 | 20 / 20 |
| Product pages passing Google Rich Results test | failing | passing |
| Soft 404s in Google Search Console (T+30) | present | 0 |
| Hard 404s | unknown | 0 (each mapped to redirect / 410) |
| Google Merchant Center feed status | not connected | connected, approved |
| Blog posts with FAQPage + BlogPosting + Author schema | 0 / 10 | 10 / 10 |
| Pages with LocalBusiness / MobilePhoneStore schema | 0 | Homepage + Contact |

### Out-of-scope outcomes (explicitly not promised)
- Specific organic traffic numbers (depend on content velocity + external factors).
- Specific keyword rankings (depend on backlinks, competitor activity, query volume).
- AI Overview citations (depend on Google's selection — we can only make Switchkart eligible).

---

## 3. Scope — what's in

Bundled into one ₹50,000 sprint:

### 3.1 — Shopify theme refresh (lead deliverable)
**Approach:** Adopt or refresh a clean, fast Shopify theme as the foundation (Dawn-derivative or equivalent — final choice during W1 audit). Customize the high-leverage sections; reuse theme-native components elsewhere. **Not** a from-scratch custom-theme build.

- **Homepage** — refreshed hero, trust strip (Blancco / 52-point QC / 6-month warranty), category quick-links, featured collections grid, refurbished-vs-new explainer block, testimonials, blog teaser.
- **Collection pages (20 brand collections)** — single H1, filter UI (RAM / storage / price / condition), card layout with price + warranty + condition badge, stocked-out states with "Notify me" / waitlist.
- **Product detail page (PDP)** — gallery with proper alt text pattern, condition + warranty badges, trust strip (Blancco, 52-point QC), buy box, short FAQ block (3–5 product-specific Q&As), schema-rich.
- **Blog template + posts** — single H1, author byline, reading time, in-article CTAs to collection/product pages, FAQ block at the foot.
- **Static pages refreshed** — Contact, FAQ, Terms, Warranty, Shipping — consistent type scale, mobile-readable.
- **Header / footer / nav** — mobile-first menu, sticky add-to-cart on PDP, footer with trust + legal links + LocalBusiness data.
- **Mobile + desktop responsive polish** — verified on iPhone, Android, tablet, 1280 / 1440 / 1920 desktop breakpoints.

### 3.2 — 404 audit & remediation
Baked into the new theme deploy, not handled as a patch:
- **Soft 404 fixes** on stocked-out collections + frontpage collection — handled via the new "Notify me" / waitlist UI on collection cards.
- **Hard 404 sweep** via Google Search Console + Screaming Frog. Each non-200 mapped to: redirect, restore, or intentional 410. Captured in `docs/404-decisions.md`.
- **Dummy Blog 1** (`/blogs/dummy-blog-1`) — deleted or `noindex`'d at deploy.
- **`sameAs` cleanup** in Organization schema — remove the Shopify backend URL, keep only verified social/brand URLs.

### 3.3 — Google Shopping / Merchant Center connection
- Create or verify Google Merchant Center account.
- Install Google & YouTube Shopify channel + connect to GMC.
- Map Shopify product taxonomy → GMC categories.
- Set `condition = refurbished` on the feed (not `new`).
- Verify GTIN / MPN handling for refurbished SKUs.
- Submit feed; resolve initial feed errors until **status = active**.
- **Excluded:** Google Ads / Performance Max setup, ad spend, ongoing feed management beyond initial submission.

### 3.4 — Merchant listings + product schema upgrade
Built into the new PDP template:
1. **`brand.name`** → actual device manufacturer (Apple, Samsung, OnePlus, Xiaomi…), driven from Shopify product vendor / metafield.
2. **`itemCondition`** → explicit `"http://schema.org/RefurbishedCondition"` on the Offer object.
3. **`aggregateRating`** scaffold — schema structure deployed; values populate once reviews exist on a product.
4. Merchant-listing fields: `availability`, `price`, `priceValidUntil`, `priceCurrency`, `seller.name`.

### 3.5 — Desktop + mobile CLS / Core Web Vitals
- Diagnose CLS source on existing site (baseline measurement) so the new theme doesn't repeat it.
- New theme built with explicit `width`/`height` (or aspect-ratio) on hero, product images, above-the-fold elements.
- Preloaded critical webfonts; `font-display: swap`.
- Lazy-loading without layout shift; reserved space for late-loading blocks.
- **Goal:** homepage + top-3 collections pass Core Web Vitals on desktop **and** mobile (lab data acceptable for sign-off; field data verified at T+30).

### 3.6 — Schema additions (full list)
| Schema | Where | Notes |
|---|---|---|
| `Product` (upgraded) | All ~47 product pages | brand, itemCondition, aggregateRating scaffold, full merchant fields |
| `FAQPage` | All 10 blog posts with FAQ sections + new PDP FAQ blocks | JSON-LD |
| `BlogPosting` | All blog posts | `headline`, `datePublished`, `dateModified`, `image`, `mainEntityOfPage` |
| `Author` (Person) | All blog posts | byline + bio + URL |
| `LocalBusiness` / `MobilePhoneStore` | Homepage + Contact | Bangalore address, phone, opening hours, `areaServed`, `priceRange` |
| `Organization` (cleaned) | Site-wide | `sameAs` fixed — backend Shopify URL removed |
| `Review` / `AggregateRating` (on testimonials) | Homepage testimonials block | Once review source is confirmed |

### 3.7 — Light supporting fixes (bundled — no separate charge)
- Image alt text on top-10 best-selling product pages — pattern: `"{Brand} {Model} {Storage} {Color} — Certified Refurbished | SwitchKart"`. Full-catalog alt-text remediation if requested as separate scope.
- Single canonical H1 on homepage (consolidating the existing multiple-H1 issue).
- robots.txt update — explicitly allow GPTBot / ClaudeBot / PerplexityBot (AEO signal).

---

## 4. Out of scope

Explicitly **not** included in this sprint (separate scope + invoice if requested):

- **From-scratch custom theme** — this is a refresh, not a Figma-up theme build.
- **Backend / Shopify Plus / headless migration** — staying on standard Shopify with the existing plan.
- **New content production** (blog posts, buyer guides, local Bangalore content, video).
- **Copy rewriting** beyond what's needed for the refreshed page templates (existing copy is reused / re-laid-out, not re-written).
- **HARO / guest posting / link-building outreach.**
- **Google Business Profile setup & optimization** (recommended separately — fastest path to local pack rankings).
- **Review collection workflow build-out** (schema scaffold is in scope; the email/WhatsApp follow-up tooling and UX is not).
- **Google Ads / Performance Max / paid social campaigns.**
- **Ongoing SEO retainer / monthly reporting** beyond a single T+30 verification.
- **Full-catalog image alt-text remediation** (top-10 PDPs included; remaining ~37 PDPs separate).
- **Mobile app SEO / app store optimisation.**

---

## 5. Timeline

**Sprint duration:** 5 calendar weeks from advance receipt.

| Week | Block | Output |
|---|---|---|
| W1 | Access setup · base theme selected · audit confirmed · 404 strategy locked · staging environment ready | `404-decisions.md`, dev theme + staging URL, base-theme decision logged |
| W2 | Homepage + collection-page templates rebuilt on staging · brand schema + LocalBusiness drafted | Home + collection templates live on staging, mobile + desktop pass |
| W3 | PDP rebuilt with product schema + FAQ block · blog template with Author/BlogPosting schema · CLS pass | PDP + blog live on staging, Rich Results test passing |
| W4 | Merchant Center feed setup + submission · static pages refreshed · accessibility pass | GMC feed pending approval, all static pages updated |
| W5 | Production deploy · Search Console verification · 7-day soak · documentation · walkthrough call | Production live, sign-off doc |

Buffer: +1 week for Merchant Center feed approval (Google-side latency outside our control) and any client review cycles.

---

## 6. Acceptance criteria

Sign-off requires **all** of:

1. ✅ Google Rich Results Test passes for: homepage, one collection per device family, three sample PDPs, two blog posts.
2. ✅ PSI desktop **and** mobile pass on homepage + top-3 collections + sample PDP (CLS < 0.1, LCP < 2.5s, INP < 200ms — lab data).
3. ✅ Google Search Console — "Crawled, currently not indexed" and "Soft 404" reports show zero new entries 14 days post-deploy.
4. ✅ Google Merchant Center feed status = **Active**, no critical errors.
5. ✅ Visual QA on iPhone, Android, tablet, 1280 / 1440 / 1920 desktop — no horizontal scroll, no overlap, no text < 14px outside meta/legal copy.
6. ✅ All schema additions traceable in git, documented in `docs/changelog.md`.
7. ✅ One walkthrough call (≤ 60 min) explaining what was built and how to maintain it.

---

## 7. Access & dependencies

**From Switchkart (required before W1 can start):**

- Shopify Admin (Staff account) — `Manage theme`, `View / edit products`, `Edit themes`, `Manage settings` permissions.
- Google Search Console — owner or full user access to `switchkart.com` property.
- Google Analytics 4 — read access for baseline + post-deploy verification.
- Google Merchant Center — admin access (or invite to create on Switchkart's behalf).
- Shopify theme repo if version-controlled outside Shopify (GitHub / Theme Kit) — read/write.
- Domain registrar / DNS — read access for any verification step.
- Authorised contact for go/no-go decisions on 404 strategy, copy edits, base-theme choice.

**From client (decisions needed early in W1):**

- 404 handling preference per stocked-out collection (waitlist UI vs redirect vs 410).
- Author identity for blog posts (single house byline vs multi-author + bios).
- LocalBusiness opening hours, service area, contact phone.
- Base-theme preference, if any (else studio chooses + justifies).
- Brand colour / type direction for the refresh — keep current, or update?

---

## 8. Risks & mitigations

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Base-theme choice constrains a custom UI block | Medium | Forces section override | Decision locked in W1 with client; section-level customisation budgeted |
| Merchant Center flagged for refurbished item-condition rules | Medium | Delay on W4 deliverable | Submit early; refurbished policy reviewed in advance |
| Existing copy doesn't slot cleanly into new templates | Medium | Slows W2/W3 | First pass uses existing copy as-is; copy rewrite flagged as separate scope |
| Client review cycles slow approvals | Medium | Pushes past W5 | 48-hour decision SLA captured in shared doc; staging URL always live for review |
| Search Console takes 14+ days to re-crawl | Medium | Sign-off delayed | URL Inspection re-index requests submitted on each critical page post-deploy |
| Shopify theme update overwrites custom schema | Low | Schema disappears | All edits committed to git; `docs/changelog.md` lists touched files for restore |
| Scope creep ("can we also add X") | High | Sprint slips | Out-of-scope items flagged within 24h with quote — no silent expansion |

---

## 9. Commercials

- **Fee:** ₹50,000 + 18% GST (₹4,500 CGST + ₹4,500 SGST) = **₹59,000 total**.
- **Payment terms:** 50% advance (₹29,500) on receipt of invoice — kickoff trigger. 50% balance (₹29,500) on delivery / pre-handover.
- **Invoice:** DW-2026-0001 (issued 12 May 2026, from Daily Web · AKAARA SERVICES).
- **Bank:** AKAARA SERVICES · Kotak Mahindra · Koramangala · A/C 4246915159 · IFSC KKBK0000424.
- **GST treatment:** Intra-state (Karnataka → Karnataka). If Switchkart's place of supply is outside Karnataka, IGST 18% replaces the CGST+SGST split — invoice will be reissued.
- **Pricing note:** This rate reflects a *fast theme refresh* approach (clean Shopify theme as foundation, high-leverage section customisation) bundled with the SEO/AEO sprint. A full from-scratch custom theme would be quoted separately at studio standard rates.
- **Out-of-scope work:** quoted separately. No retroactive billing.

---

## 10. Open questions (to close before kickoff)

1. **Place of supply** — confirm Switchkart's registered GSTIN state (affects CGST/SGST vs IGST on the invoice).
2. **Switchkart GSTIN** — for the invoice "Bill to" block, if available.
3. **Authorised contact** — single point of contact at Switchkart for sprint decisions.
4. **Existing GMC** — does Switchkart already have a Merchant Center account, or do we create fresh?
5. **Author identity** — single house byline or named contributors for blog posts?
6. **Theme version control** — is the Shopify theme version-controlled (GitHub / Theme Kit), or live-edit only?
7. **Base-theme preference** — any opinion on the foundation theme (Dawn / Impulse / Empire / other), or studio choice?
8. **Brand visual direction** — keep current colour/type, or open to a refresh?

---

*This PRD is a working document. Any change to scope, fee, or timeline will be captured as a dated addendum at the bottom of this file and acknowledged by both parties before being acted on.*
