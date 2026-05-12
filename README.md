# switchkart-storefront-sprint

Working repo for the **Switchkart Shopify Theme Refresh + Search Visibility Sprint** — delivered by **Daily Web**, a [Daily Mark8ing](https://dailymark8ing.com) studio (legal entity: AKAARA SERVICES) — May 2026.

A fast theme refresh on a clean Shopify foundation, with all the April-2026 audit fixes (SEO + AEO + Core Web Vitals + Merchant Center + schema) baked into the new build. One deploy, not a theme patch followed by a separate SEO patch.

> Daily Web is the Daily Mark8ing sub-brand for websites, landing pages, and technical-web work (SEO/AEO, schema, Core Web Vitals, Shopify/Next.js theme engineering). Tagline: *Built to ship.*

---

## How the sprint moves

```mermaid
flowchart LR
    classDef trig fill:#C5FF00,stroke:#0E0E0E,stroke-width:2px,color:#0E0E0E,font-weight:bold
    classDef wk   fill:#F2F0EA,stroke:#0E0E0E,stroke-width:1.5px,color:#0E0E0E
    classDef hand fill:#0E0E0E,stroke:#0E0E0E,color:#F2F0EA,font-weight:bold

    A([Advance · ₹29,500]):::trig --> W1
    W1[W1 — Setup<br/>Access · base theme · 404 strategy]:::wk --> W2
    W2[W2 — Home + Collections<br/>Templates live on staging]:::wk --> W3
    W3[W3 — PDP + Blog<br/>Schema · Rich Results passing]:::wk --> W4
    W4[W4 — Static pages + GMC<br/>Feed submitted · a11y pass]:::wk --> W5
    W5[W5 — Deploy + Soak<br/>Production · Search Console]:::wk --> H([Handover · ₹29,500]):::hand
```

## The deliverable bundle

Six audit findings + a storefront refresh, shipped as **one deploy**:

```mermaid
flowchart TD
    classDef audit fill:#F2F0EA,stroke:#0E0E0E,color:#0E0E0E
    classDef build fill:#C5FF00,stroke:#0E0E0E,color:#0E0E0E,font-weight:bold
    classDef ship  fill:#0E0E0E,stroke:#0E0E0E,color:#F2F0EA,font-weight:bold

    A1[Soft 404s on stocked-out collections]:::audit --> B
    A2[Hard 404 sweep]:::audit --> B
    A3[Google Merchant Center connection]:::audit --> B
    A4[Product schema · brand / itemCondition / aggregateRating]:::audit --> B
    A5[Desktop CLS · Core Web Vitals fix]:::audit --> B
    A6[FAQ · BlogPosting · Author · LocalBusiness schema]:::audit --> B

    R[Shopify theme refresh<br/>Home · 20 collections · PDP · Blog · Statics]:::build --> B

    B[New build on staging]:::build --> S([Production deploy · sign-off]):::ship
```

## 404 decision flow

Every non-200 from the W1 crawl resolves to one of these:

```mermaid
flowchart TD
    classDef q  fill:#F2F0EA,stroke:#0E0E0E,color:#0E0E0E
    classDef d1 fill:#C5FF00,stroke:#0E0E0E,color:#0E0E0E,font-weight:bold
    classDef d2 fill:#0E0E0E,stroke:#0E0E0E,color:#F2F0EA,font-weight:bold

    U[URL returns non-200]:::q --> Q1{Soft 404 on<br/>stocked-out collection?}:::q
    Q1 -- yes --> A1[Keep live with<br/>'Notify me' UI]:::d1
    Q1 -- no  --> Q2{Has a clear<br/>replacement URL?}:::q
    Q2 -- yes --> A2[301 redirect]:::d1
    Q2 -- no  --> Q3{Permanently retired<br/>or thin content?}:::q
    Q3 -- yes --> A3[410 Gone]:::d2
    Q3 -- no  --> Q4{Was it<br/>accidentally removed?}:::q
    Q4 -- yes --> A4[Restore content]:::d1
    Q4 -- no  --> A5[noindex + keep crawlable]:::d2
```

---

## What's here

| File | Purpose |
|---|---|
| `PRD.md` | The product requirements document — scope, goals, deliverables, timeline, acceptance criteria, risks, commercials. **Read this first.** |
| `docs/audit-april-2026.md` | Extract of the SwitchKart SEO/AEO audit (April 2026) — the basis for sprint scope. |
| `docs/changelog.md` | Running log of every change made to the Switchkart Shopify theme + schema. Filled in during execution. |
| `docs/404-decisions.md` | Per-URL decision log for soft/hard 404 remediation. Filled in W1. |

## Project state

- **Status:** Proposed → awaiting kickoff (advance receipt triggers W1)
- **Invoice:** DW-2026-0001 — ₹50,000 + 18% GST = ₹59,000
- **Duration:** 5 weeks from kickoff (+1 week buffer)
- **Single point of contact:** Piyush Mishra · dailymark8ing.com

## Repo conventions

- This repo holds **planning + documentation** for the sprint.
- Actual theme code edits land in the Switchkart Shopify theme repo (or via Shopify Admin theme editor) — every edit gets a one-line entry in `docs/changelog.md` with file path + summary.
- Decisions made during the sprint that affect scope or timeline are appended as dated addenda at the bottom of `PRD.md` — never edited inline.

## Sharing

Published openly so Switchkart can review the proposed scope, success metrics, and timeline directly. Audit findings referenced here are summarised from the source audit PDF held with the studio; reproduction of this document for commercial pitching by third parties is not permitted.
