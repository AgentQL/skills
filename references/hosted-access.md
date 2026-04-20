# Hosted Access

This artifact preserves the hosted phase-1 contract for the installed skill.

## Portal Onboarding

1. Complete portal registration or pilot activation for the target account.
2. Open portal `Dashboard Keys` and create a `workspace_api_key`.
3. Store the issued key in the host environment variable used by your skill config, for example `AQL_WORKSPACE_API_KEY`.

## Hosted Access

- Gateway base URL: `https://gw-aql.tomo.services`
- Gateway WebSocket endpoint: `wss://gw-aql.tomo.services/v1/market/ws`
- Gateway REST asset profile route: `https://gw-aql.tomo.services/v1/market/asset-profile`
- Gateway REST market profile route: `https://gw-aql.tomo.services/v1/market/market-profile`
- Gateway REST price snapshot route: `https://gw-aql.tomo.services/v1/market/price-snapshot`
- Gateway REST OHLCV window route: `https://gw-aql.tomo.services/v1/market/ohlcv-window`
- BSC JSON-RPC endpoint: `https://gw-aql.tomo.services/rpc/bsc`
- Solana JSON-RPC endpoint: `https://gw-aql.tomo.services/rpc/solana`
- Hosted MCP server endpoint: `https://mcp-aql.tomo.services`
- Auth header: `Authorization: Bearer <workspace_api_key>`
- Gateway API inventory docs: repository `docs/standards/agent-api-inventory.md`
- Capability summary for the installed skill: `references/capabilities.md`
- Quick validation guide: `references/quickstart.md`

## Integration Rules

- Route request-response market reads through gateway `REST`.
- Route live market subscriptions through gateway `WebSocket`.
- Route raw chain compatibility through gateway `JSON-RPC`.
- Keep websocket target promises inside the current DEX-first realtime scope unless later contract docs widen that boundary.
- If the hosted MCP server is part of the workflow, keep it separate from gateway routes and configure it through the dedicated MCP URL.
- Do not treat `workspace_id` as the hosted source of truth for identity.
- Do not add host-local retries that mask gateway continuity or source-state events.
- Route all hosted traffic through product-owned surfaces only.
