# SaltCrate Oracle — Claude Code plugin

One-command install of [Oracle by SaltCrate](https://oracle.saltcrate.com/) — eight MCP tools for
live web work: `search`, `extract`, `fetch`, `verify`, `monitor`, `check_change`, `check_link`,
`check_deps`.

**Free tier: 100 calls, no API key, no signup.** When you exceed it, calls are $0.01 in USDC
(Tempo) or you can buy a card pass at <https://oracle.saltcrate.com/buy> — $1 for 100 calls,
$5 for 1,000. No subscription, no seat, no minimum.

## Install

```bash
# in Claude Code
/plugin marketplace add saltcrate/oracle-plugin
/plugin install oracle@saltcrate
```

Or from a shell:

```bash
claude plugin marketplace add saltcrate/oracle-plugin
claude plugin install oracle@saltcrate
```

Restart the session if the tools don't appear; `claude plugin details oracle` shows the MCP server
and the bundled skill.

## What you get

| Tool | Use it for |
|---|---|
| `search` | Live web results — `{title, url, snippet}` |
| `extract` | Schema-driven structured extraction: pass a JSON Schema, get typed entities |
| `fetch` | Clean page text, boilerplate stripped, plus title/status/length |
| `verify` | Heuristic claim-vs-source check with confidence + best excerpt |
| `monitor` | Recurring URL watch with first-seen/change counts |
| `check_change` | One-shot "did this page change since last check?" |
| `check_link` | HTTP status, redirect chain, latency |
| `check_deps` | Latest version + known advisories for npm/PyPI/crates.io/Go/RubyGems packages |

The plugin also ships the `oracle-web-tools` skill so the model knows which tool to reach for.

## Endpoint

`https://oracle.saltcrate.com/mcp` (Streamable HTTP, stateless). Discovery files:
[`/llms.txt`](https://oracle.saltcrate.com/llms.txt),
[`/openapi.json`](https://oracle.saltcrate.com/openapi.json),
[`/.well-known/mcp/server-card.json`](https://oracle.saltcrate.com/.well-known/mcp/server-card.json).

## No Claude Code?

Any MCP client can connect directly — see the [server card](https://oracle.saltcrate.com/.well-known/mcp/server-card.json)
for the config, or the plain-HTTP routes documented in `llms.txt`.

## License

MIT
