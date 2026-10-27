<p align="center"><img src="logo.png" width="96" alt="InternetVitals logo"></p>

# InternetVitals MCP Server

Real-time health of the internet's backbone, for AI agents. Ask "is AWS down?", "what broke in the last hour?" or "how healthy is the internet right now?" and get live answers from [InternetVitals](https://internetvitals.com), which checks 41 major services every 5 minutes and rolls them into a single Internet Health Score.

- **Endpoint:** `https://internetvitals.com/mcp`
- **Transport:** Streamable HTTP (remote, hosted)
- **Auth:** none — no API key, no sign-up
- **Cost:** free

## Tools

| Tool | What it does | Arguments |
|---|---|---|
| `get_internet_health` | Current global health score and vital signs (pulse, temperature, blood pressure, SpO2) | — |
| `list_services` | All 41 monitored services with current status | `category` (cdn, cloud, consumer, developer, payments, communication, dns, ai), `status` (operational, degraded, major, outage, unknown) — both optional |
| `get_service_status` | Status, uptime and recent incidents for one service | `slug`, e.g. `cloudflare`, `aws`, `github` |
| `get_recent_incidents` | Recent outages and incidents, optionally for one service | `slug` (optional), `limit` 1–100 (default 10) |
| `get_vitals_history` | Health score history | `period`: `24h`, `7d` or `30d` (default `24h`) |

All tools are read-only and only query public status data.

## Monitored services

**CDN:** Cloudflare, Akamai, Fastly · **Cloud:** AWS, Azure, Google Cloud, DigitalOcean · **Consumer:** Google Search, YouTube, Gmail, Meta (Facebook + Instagram), WhatsApp, TikTok, X, Microsoft 365, Apple Services · **Developer:** GitHub, npm, Docker Hub, Vercel, GitLab, Datadog · **Payments & commerce:** Stripe, PayPal, Shopify · **Communication:** Zoom, Slack, Discord, Twilio, SendGrid · **Business:** Okta / Auth0, HubSpot, Salesforce · **DNS:** Google DNS, Cloudflare DNS · **AI:** OpenAI, Anthropic, Google Gemini, Meta AI, Mistral AI, Hugging Face

## Connect

**Claude (claude.ai / Desktop):** Settings → Connectors → Add custom connector → `https://internetvitals.com/mcp`

**Claude Code:**

```sh
claude mcp add --transport http internetvitals https://internetvitals.com/mcp
```

**Cursor** (`~/.cursor/mcp.json`):

```json
{
  "mcpServers": {
    "internetvitals": { "url": "https://internetvitals.com/mcp" }
  }
}
```

**VS Code** (`.vscode/mcp.json`):

```json
{
  "servers": {
    "internetvitals": { "type": "http", "url": "https://internetvitals.com/mcp" }
  }
}
```

**Clients that only speak stdio** (via [mcp-remote](https://www.npmjs.com/package/mcp-remote)):

```json
{
  "mcpServers": {
    "internetvitals": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://internetvitals.com/mcp"]
    }
  }
}
```

## Example prompts

- "Is anything major down right now?"
- "Is GitHub having problems? Show recent incidents."
- "Which AI providers are degraded at the moment?"
- "How has the internet health score changed over the last 7 days?"

## Also available

- REST API (JSON, no auth, CORS `*`): [internetvitals.com/developers](https://internetvitals.com/developers)
- JavaScript SDK: [internetvitals/sdk-js](https://github.com/internetvitals/sdk-js)

## About this repository

This repo holds the public listing for the hosted InternetVitals MCP server: the registry manifest ([`server.json`](server.json)), docs and logo. The server itself runs at `internetvitals.com/mcp`. Issues and feature requests are welcome here.

## License

MIT — see [LICENSE](LICENSE).
