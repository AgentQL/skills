# Quickstart

Use this file when you want to validate the skill against the active hosted production deployment without reverse-engineering the gateway flow first.

## Current Endpoints

- Gateway base URL: `https://gw-aql.tomo.services`
- Gateway WebSocket URL: `wss://gw-aql.tomo.services/v1/market/ws`
- BSC JSON-RPC URL: `https://gw-aql.tomo.services/rpc/bsc`
- Solana JSON-RPC URL: `https://gw-aql.tomo.services/rpc/solana`
- Hosted MCP server URL: `https://mcp-aql.tomo.services`

## Prerequisite

Export the issued key before running any validation:

```bash
export AQL_WORKSPACE_API_KEY="<workspace_api_key>"
```

## Fast Health Check

```bash
curl -sS https://gw-aql.tomo.services/healthz
```

Expected:

- returns `{"service":"gateway","status":"ok"}`

## Gateway REST Price Snapshot

```bash
curl -sS -G "https://gw-aql.tomo.services/v1/market/price-snapshot" \
  -H "Authorization: Bearer $AQL_WORKSPACE_API_KEY" \
  --data-urlencode "market_kind=dex" \
  --data-urlencode "chain=bsc" \
  --data-urlencode "address=0xbb4CdB9CBd36B01bD1cBaEBF2De08d9173bc095c"
```

## Gateway REST CEX Market Profile

```bash
curl -sS -G "https://gw-aql.tomo.services/v1/market/market-profile" \
  -H "Authorization: Bearer $AQL_WORKSPACE_API_KEY" \
  --data-urlencode "market_kind=cex" \
  --data-urlencode "symbol=BTCUSDT"
```

## Gateway WebSocket Subscribe

Use a websocket client such as `wscat` from the same machine where the skill is installed:

```bash
npx -y wscat -c "wss://gw-aql.tomo.services/v1/market/ws" \
  -H "Authorization: Bearer $AQL_WORKSPACE_API_KEY"
```

Then send this subscribe frame:

```json
{"action":"subscribe","profile":"standard","targets":[{"market_kind":"dex","target_id":"0xbb4CdB9CBd36B01bD1cBaEBF2De08d9173bc095c","chain":"bsc","event_family":"price","base_asset":"BNB","quote_asset":"USDT"}]}
```

Expected websocket behavior:

- first event is `SESSION_READY`
- later events include `MARKET_PRICE` for the subscribed DEX target

## Gateway JSON-RPC Check

```bash
cat >/tmp/aql-rpc-bsc.json <<'JSON'
{"jsonrpc":"2.0","id":11,"method":"eth_blockNumber","params":[]}
JSON

curl -sS \
  -X POST https://gw-aql.tomo.services/rpc/bsc \
  -H "Authorization: Bearer $AQL_WORKSPACE_API_KEY" \
  -H "Content-Type: application/json" \
  --data-binary @/tmp/aql-rpc-bsc.json
```

## Hosted MCP Server

- Use `https://mcp-aql.tomo.services` when your workflow explicitly needs the hosted MCP surface.
- Keep the hosted MCP server URL separate from the gateway base URL and raw gateway routes.

## How To Use These Checks

- Use the hosted production endpoints above for the default install and validation flow.
- If a live call fails, report the actual transport or auth failure instead of answering from memory.
