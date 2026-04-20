# Agent Query Layer Skill Pack

Install globally with one command:

```bash
npx skills add AgentQL/skills -g -y
```

This repository publishes the installable skill bundle for Agent Query Layer.

Published files:

- `SKILL.md`
- `agents/openai.yaml`
- `references/capabilities.md`
- `references/hosted-access.md`
- `references/quickstart.md`

Current phase-1 scope stays inside DEX market-read workflows on `bsc` and `solana`, plus the live minimal symbol-first CEX query slice.
Hosted auth uses `Authorization: Bearer <workspace_api_key>` and should load the issued key from an environment variable such as `AQL_WORKSPACE_API_KEY`.
The installed skill should steer the agent toward the current hosted product surfaces: gateway `REST`, gateway `WebSocket`, and hosted `JSON-RPC`.
A private MCP companion may still exist as separately provisioned companion wiring, but it remains optional alongside the standard hosted surfaces.
For supported service names and routing guidance, read `references/capabilities.md` after install.
For copy-ready smoke checks against the active hosted surfaces, read `references/quickstart.md`.

## Hosted Production Endpoints

- Gateway base URL: `https://gw-aql.tomo.services`
- Gateway WebSocket URL: `wss://gw-aql.tomo.services/v1/market/ws`
- BSC JSON-RPC URL: `https://gw-aql.tomo.services/rpc/bsc`
- Solana JSON-RPC URL: `https://gw-aql.tomo.services/rpc/solana`
- Hosted MCP server URL: `https://mcp-aql.tomo.services`

Use the hosted production endpoints above for the default install and validation flow.
