# ACCRUE MCP Server

[![Glama MCP Server](https://glama.ai/mcp/servers/ACCRUE1/mcp-server/badges/score.svg)](https://glama.ai/mcp/servers/ACCRUE1/mcp-server)

Non-custodial USDC yield platform. Live stablecoin yield data for AI agents, plus transaction tools that return unsigned payloads for the agent's own wallet to sign.

## Endpoint

https://accrue.cc/mcp

Protocol: JSON-RPC 2.0 · MCP spec 2024-11-05 · Streamable HTTP · No authentication, no API key, no rate limit

## What it does

Exposes the **[Stablecoin Yield Index (SYX)](https://accrue.cc/index)** — a TVL-weighted onchain benchmark computed directly from canonical contracts and updated every 15 minutes — and live USDC vault APYs across **[12 markets](https://accrue.cc/strategies) on Ethereum and Base**: the Aave v3 and Compound v3 USDC supply markets, and four curated Morpho v2 vaults from Steakhouse Financial and Gauntlet. The same six markets on each chain, plus six [model portfolios](https://accrue.cc/model-portfolios).

SYX separately tracks Ethereum, Base and Arbitrum. ACCRUE has no vaults on Arbitrum.

## Tools (19)

| Group | Tools | On the site |
|---|---|---|
| SYX index | `get_syx_value` `get_syx_methodology` `get_syx_components` `get_syx_history` | [SYX index](https://accrue.cc/index) |
| Vaults | `list_vaults` `get_vault_details` `compare_vaults` `search_vaults` | [All strategies](https://accrue.cc/strategies) · [Compare](https://accrue.cc/compare-strategies) |
| Portfolios | `list_model_portfolios` `get_portfolio_details` | [Model portfolios](https://accrue.cc/model-portfolios) · [Build your own](https://accrue.cc/create-portfolio) |
| Decisions | `recommend_strategy` `calculate_yield` `get_platform_info` `search` | [Yield calculator](https://accrue.cc/yield-calculator) · [Ask the assistant](https://accrue.cc/ask-ai) |
| Transactions | `list_vault_contracts` `prepare_transaction` `build_user_operation` `submit_user_operation` `get_transaction_status` | [For AI agents](https://accrue.cc/for-agents) |

Every tool is read-only except `submit_user_operation`, which relays an operation the agent has already signed. `prepare_transaction` and `build_user_operation` return **unsigned** transaction data for the agent's own wallet. ACCRUE never signs, never holds keys and never takes custody at any stage.

## Paying network fees in USDC

An agent can pay gas in USDC instead of ETH on both Ethereum and Base, through Circle's paymaster. One EIP-7702 authorization is enough and the agent keeps its own address, so no ETH balance is needed on either chain. The path runs `prepare_transaction` → `build_user_operation` → `submit_user_operation`.

The agent always pays its own network fee. ACCRUE does not sponsor, subsidise or absorb any part of it.

## Getting USDC on the right chain

Two tools on the platform, neither of which ACCRUE charges anything for:

- **[Bridge USDC](https://accrue.cc/bridge)** — moves USDC between Ethereum and Base over Circle's Cross-Chain Transfer Protocol. Burned on the source chain, minted natively on the destination by Circle. No fee, no spread, no markup.
- **[Swap to USDC](https://accrue.cc/swap)** — converts USDT, USDS, DAI, ETH or WETH into USDC on either chain, routed through 0x. No swap fee, no spread, no markup.

ACCRUE holds no key and operates no liquidity pool in either path.

## Quick start

```bash
curl -s -X POST https://accrue.cc/mcp \
  -H "Content-Type: application/json" \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/list"}'
```

Read the current index value:

```bash
curl -s -X POST https://accrue.cc/mcp \
  -H "Content-Type: application/json" \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"get_syx_value","arguments":{}}}'
```

## Status

The read surfaces — SYX, vault data, portfolios, the REST API and this server — are live and answer real requests today.

Deposits are not publicly open. The ACCRUE contracts are **not yet audited**; an independent audit is scheduled before public launch and deposits are restricted to allowlisted addresses until it completes. Public launch is targeted for Q1 2027. Yields are variable and not guaranteed, and principal is not guaranteed. See the [FAQ](https://accrue.cc/faq) and the [documentation](https://accrue.cc/docs).

## Links

**Platform**

- Home: https://accrue.cc
- SYX index: https://accrue.cc/index
- All strategies: https://accrue.cc/strategies
- Model portfolios: https://accrue.cc/model-portfolios
- Build a custom portfolio: https://accrue.cc/create-portfolio
- Compare strategies: https://accrue.cc/compare-strategies
- Yield calculator: https://accrue.cc/yield-calculator
- Bridge USDC: https://accrue.cc/bridge
- Swap to USDC: https://accrue.cc/swap
- Ask the assistant: https://accrue.cc/ask-ai

**Documentation**

- Documentation: https://accrue.cc/docs
- FAQ: https://accrue.cc/faq
- For AI agents: https://accrue.cc/for-agents
- MCP documentation: https://accrue.cc/mcp-docs
- Blog: https://accrue.cc/blog

**Machine-readable**

- OpenAPI 3.1 spec: https://accrue.cc/openapi.json
- Agent identity: https://accrue.cc/.well-known/agent.json
- Plain-text summary: https://accrue.cc/llms.txt
- Full plain-text reference: https://accrue.cc/llms-full.txt
- SYX value: https://accrue.cc/api/index
- SYX methodology: https://accrue.cc/api/index/methodology
- SYX history: https://accrue.cc/api/index/history
- Vault data: https://accrue.cc/api/vaults
- MCP Registry: cc.accrue/mcp (v2.0.0)
