# ACCRUE MCP Server

[![Glama MCP Server](https://glama.ai/mcp/servers/ACCRUE1/mcp-server/badges/score.svg)](https://glama.ai/mcp/servers/ACCRUE1/mcp-server)

Non-custodial USDC yield platform. Live stablecoin yield data for AI agents.

## Endpoint

https://accrue.cc/mcp

Protocol: JSON-RPC 2.0 · MCP spec 2024-11-05 · No authentication required

## What it does

Exposes the **Stablecoin Yield Index (SYX)** — a TVL-weighted onchain benchmark updated every 15 minutes — and live USDC vault APYs across 12 strategies on Ethereum, Base, and Arbitrum (Aave v3, Compound v3, Morpho v2 curated vaults from Steakhouse Financial and Gauntlet).

## Tools (14 read-only)

| Group | Tools |
|---|---|
| SYX Index | `get_syx_value` `get_syx_methodology` `get_syx_components` `get_syx_history` |
| Vaults | `list_vaults` `get_vault_details` `compare_vaults` `search_vaults` |
| Portfolios | `list_model_portfolios` `get_portfolio_details` |
| Decisions | `recommend_strategy` `calculate_yield` `get_platform_info` `search` |

## Quick start

```bash
curl -s -X POST https://accrue.cc/mcp \
  -H "Content-Type: application/json" \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/list"}'
```

## Links

- Platform: https://accrue.cc
- Agent docs: https://accrue.cc/docs/agents
- OpenAPI spec: https://accrue.cc/openapi.json
- Agent identity: https://accrue.cc/.well-known/agent.json
- MCP Registry: cc.accrue/mcp (v2.0.0)
