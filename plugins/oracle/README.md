# SaltCrate Oracle (plugin)

This plugin connects Claude Code to **Oracle by SaltCrate**, a remote MCP server that gives an agent
live web capabilities: `search`, `extract`, `fetch`, `verify`, `monitor`, `check_change`,
`check_link`, and `check_deps`. It ships an MCP server config plus the `oracle-web-tools` skill,
which tells the model when to reach for each tool.

**Setup: none.** The server runs at `https://oracle.saltcrate.com/mcp` and the free tier allows
200 calls per hour per IP with no API key and no signup. `extract` is paid-only ($0.01/call in
USDC, or a card pass at <https://oracle.saltcrate.com/buy> — $1 for 100 calls, $5 for 1,000).

Install in one step (Claude Code 2.1.275+):

```bash
/plugin install oracle --marketplace saltcrate/oracle-plugin
```

Or, in two steps: `/plugin marketplace add saltcrate/oracle-plugin`, then
`/plugin install oracle@saltcrate`.


After installing, ask Claude to "search the web for the latest US Mint silver quarter mintage
figures and extract them as a table" to confirm the tools are live.

Privacy policy: <https://saltcrate.com/privacy/>. The server does not store page content beyond the
calls needed to answer a request; `check_change` and `monitor` keep a hash and timestamps per URL.
