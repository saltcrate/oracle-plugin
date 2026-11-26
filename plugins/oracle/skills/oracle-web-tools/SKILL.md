---
name: oracle-web-tools
description: Use the SaltCrate Oracle MCP server for live web data — web search, schema-driven extraction, clean page fetch, link liveness, page-change detection, recurring monitoring, claim-vs-source verification, and dependency freshness/vulnerability checks.
---

# SaltCrate Oracle — when to reach for which tool

Oracle is already connected as the `oracle` MCP server. Prefer it over guessing from memory
whenever the answer depends on what a page says *right now*.

| Need | Tool | Notes |
|---|---|---|
| Find pages on a topic | `search` | `{query}` → `{title, url, snippet}` list |
| Read a page as text | `fetch` | `{url}` → clean text + title/status/length |
| Pull typed data out of a page | `extract` | `{url, schema}` — pass a JSON Schema string; returns entities matching it |
| Is this URL alive? | `check_link` | status, redirect chain, final URL, latency |
| Did the page change since last check? | `check_change` | `{url}` → `new` / `changed` / `unchanged` |
| Watch a page over time | `monitor` | same states plus `changes_since_first_seen` |
| Does this source support this claim? | `verify` | `{claim, source_url}` → confidence, matched terms, best excerpt (heuristic) |
| Is this package current / vulnerable? | `check_deps` | `{package}` e.g. `requests==2.19.0`, `lodash@4.17.20`, `pypi:fastapi`, `cargo:serde` |

## Rules of thumb

1. **Search before fetching.** `search` returns URLs; `fetch` a specific result rather than
   crawling a site blindly.
2. **`extract` needs a schema.** Write the JSON Schema for exactly the fields you want
   (`{"type":"object","properties":{...}}`). A vague schema returns vague entities.
3. **`verify` is heuristic**, not semantic fact-checking — treat its confidence as a signal,
   not a verdict. Quote the excerpt it returns when you report a result.
4. **`monitor` is stateful.** The first call for a URL reports `new`; call it again later for
   `changed`/`unchanged`. Do not expect history from a single call.
5. **Do not fabricate a result if a tool errors.** Report the error and try a different URL.

## Quota and cost

- **Free tier:** 100 calls per IP (30 days), no key, no signup. All tools except `extract`.
- **Paid:** $0.05/call in USDC via Tempo (or $1.00 card on `extract`/`monitor`); card passes at
  https://oracle.saltcrate.com/buy ($1 / 100 calls, $5 / 1,000 calls).
- If you hit a payment challenge, stop and tell the user what it would cost rather than
  retrying in a loop.
