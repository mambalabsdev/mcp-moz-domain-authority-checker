# Moz Domain Authority Checker MCP Server

[![MCP Registry](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fregistry.modelcontextprotocol.io%2Fv0%2Fservers%3Fsearch%3Dcom.mambabuilt%252Fmcp-moz-domain-authority-checker%26limit%3D1&query=%24.servers%5B0%5D._meta%5B%22io.modelcontextprotocol.registry%2Fofficial%22%5D.status&label=mcp%20registry&color=blue)](https://registry.modelcontextprotocol.io/v0/servers?search=com.mambabuilt/mcp-moz-domain-authority-checker&limit=1) [![npm version](https://img.shields.io/npm/v/@mambalabsdev/mcp-moz-domain-authority-checker)](https://www.npmjs.com/package/@mambalabsdev/mcp-moz-domain-authority-checker) [![npm downloads](https://img.shields.io/npm/dm/@mambalabsdev/mcp-moz-domain-authority-checker)](https://www.npmjs.com/package/@mambalabsdev/mcp-moz-domain-authority-checker) [![license](https://img.shields.io/github/license/mambalabsdev/mcp-moz-domain-authority-checker)](https://github.com/mambalabsdev/mcp-moz-domain-authority-checker/blob/main/LICENSE)

An MCP server for the Mamba Labs Moz Domain Authority Checker actor on Apify. Moz Domain Authority for a list of domains, on your own Moz key.

## What's Inside

- [What it does](#what-it-does)
- [Quick start](#quick-start)
- [Prerequisites](#prerequisites)
- [Example prompts](#example-prompts)
- [Tool](#tool)
- [Inputs](#inputs)
- [Pricing](#pricing)
- [Full actor documentation](#full-actor-documentation)
- [License](#license)

## What it does

Give a list of domains or URLs and your own Moz API token. The actor sends them to the official Moz API in groups of 25 and returns one row per target with Domain Authority, Page Authority, Spam Score, linking root domains, link counts, and the date Moz last crawled the page. Each target uses your Moz plan quota.

All of the work runs on Apify. This package is a thin client that starts the actor run, waits for it, and hands back the dataset rows.

## Quick start

You need Node.js 18 or newer and an Apify account with an API token.

Add this to your Claude Desktop config (`claude_desktop_config.json`), Cursor, or any MCP client:

```json
{
  "mcpServers": {
    "mamba-moz-domain-authority-checker": {
      "command": "npx",
      "args": [
        "-y",
        "@mambalabsdev/mcp-moz-domain-authority-checker"
      ],
      "env": {
        "APIFY_TOKEN": "your-apify-token"
      }
    }
  }
}
```

Restart the client. The `get_moz_domain_authority` tool appears.

## Prerequisites

- Node.js 18 or newer.
- An Apify API token from [console.apify.com/account/integrations](https://console.apify.com/account/integrations), set as `APIFY_TOKEN`. The server lists its tool without a token; a call needs one.

## Example prompts

- "Get the Moz Domain Authority of these 20 domains on my Moz key."
- "Which of these sites has the highest Spam Score?"
- "Compare linking root domains for moz.com and ahrefs.com."

## Tool

`get_moz_domain_authority`. One tool. Example arguments:

```json
{
  "targets": [
    "moz.com",
    "apify.com"
  ]
}
```

## Inputs

Every buyer facing input of the actor. Omitted inputs take the actor's own defaults.

| Input | Type | Required | Description |
|---|---|---|---|
| `api_key` | string | no | Your own Moz API token from the Moz API dashboard (moz.com/api; a free trial plan exists). It is stored encrypted by Apify, sent only to api.moz.com in the x-moz-token header, and never written to a row or a log. With no token the run writes one free row and reads nothing. |
| `targets` | array | no | Domains or URLs to check, for example moz.com or https://moz.com/blog. Repeats are read once. In Clay, put the column inside a one item list. |
| `scope` | string | no | How Moz reads each target: domain (default; moz.com/blog reads as moz.com), subdomain, subfolder, or url (the exact page). |
| `max_targets` | number | no | Number, default 1000, at most 100000. Targets past this count are not read. |
| `max_charge_usd` | string | no | Optional. The run stops before a charge that would pass this amount. Summary rows are always returned. |

## Pricing

Pay per event on Apify, billed to your Apify account. Prices in USD.

| Event | Free plan | Bronze | Silver | Gold |
|---|---|---|---|---|
| `domain-row`, one domain or URL with Moz metrics | $0.006 | $0.0057 | $0.0054 | $0.0051 |
| `apify-actor-start`, per run start | $0.002 | $0.002 | $0.002 | $0.002 |

A missing or refused token, used up Moz quota, targets Moz has no data for, API errors, and refused input are free. Mamba Labs pays the platform costs of the run. Mamba Labs pays the platform costs of the run, Apify proxy traffic included.

## Full actor documentation

[apify.com/mambalabs/moz-domain-authority-checker](https://apify.com/mambalabs/moz-domain-authority-checker)

## License

MIT. See [LICENSE](LICENSE).
