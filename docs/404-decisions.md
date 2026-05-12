# 404 Decisions Log

Per-URL decisions for soft/hard 404 remediation. Populated in W1 of the sprint after Search Console + Screaming Frog crawl.

## Decision codes
- `301` — permanent redirect to another URL
- `302` — temporary redirect (rare; only for limited-time campaigns)
- `410` — permanently gone, intentionally removed from index
- `noindex` — keep URL live but block from index
- `keep` — keep live with content fix (e.g., add "Notify me" UI to stocked-out collection)
- `restore` — content needs to be restored (was inadvertently removed)

## Soft 404s — stocked-out collections + frontpage

| URL | Type | Current state | Decision | Target / action |
|---|---|---|---|---|
| _(populated in W1)_ | | | | |

## Hard 404s — from Search Console + Screaming Frog

| URL | Source | Decision | Target / action | Date resolved |
|---|---|---|---|---|
| `/blogs/dummy-blog-1` | audit | `410` or `noindex` | confirm with client whether to delete or no-index | — |
| _(more populated in W1)_ | | | | |

## sameAs cleanup (Organization schema)

| Current entry | Decision | Replacement |
|---|---|---|
| `https://qmvvde-qq.myshopify.com/` | remove | — (backend admin URL, not a brand identity) |
| _(verified socials populated in W1)_ | | |
