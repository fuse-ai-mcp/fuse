<p align="center">
  <img src="assets/logo.svg" alt="Fuse" width="96" />
</p>

<h1 align="center">Fuse MCP server</h1>

<p align="center">
  Prospecting, enrichment, buying signals and outreach for your AI assistant.<br/>
  <a href="https://fuseai.com">fuseai.com</a> · <a href="https://docs.fuseai.com/mcp/connect">Docs</a> · <a href="https://docs.fuseai.com/mcp/tools">Tool reference</a>
</p>

---

[Fuse](https://fuseai.com) is a B2B sales platform used by more than 1,000 companies. The Fuse MCP server lets Claude, Cursor, VS Code and other MCP clients run the whole prospecting workflow from one request: find people and companies, enrich contact details, watch for buying signals, research accounts, and create email and LinkedIn campaigns.

It is a hosted server. There is nothing to install and no API key to copy. You sign in with your Fuse account, and every action runs in your own workspace.

| | |
|---|---|
| **URL** | `https://mcp.fuseai.com` |
| **Transport** | Streamable HTTP |
| **Auth** | OAuth 2.1 with dynamic client registration and PKCE, scope `mcp:tools` |
| **MCP Registry** | [`com.fuseai/fuse`](https://registry.modelcontextprotocol.io/v0/servers?search=com.fuseai) |

## Try it

```text
Find US SaaS companies that raised a Series A in the last 30 days, get the Head of Sales at each, and draft a congratulations email.

Build a list of 200 VPs of Marketing at London fintechs with 50-500 employees, with emails and phone numbers.

Alert me when a target account posts a RevOps or sales ops job.

Write a 3-step personalised email sequence for this list and schedule it to start Monday.

Prep me for my call with Sarah Chen at Acme: her background, company news and our past emails.
```

## Connect

You need a Fuse account. [Sign up free](https://fuseai.com), no waiting list.

### Claude (claude.ai and Claude Desktop)

Settings → Connectors → **Add custom connector**, then enter `https://mcp.fuseai.com` and sign in.

### Claude Code

```bash
claude mcp add --transport http fuse https://mcp.fuseai.com
```

Then run `/mcp` in Claude Code and choose **fuse** to sign in.

Or install the plugin, which adds the server plus a skill that teaches Claude how to use Fuse safely:

```text
/plugin marketplace add fuse-ai-mcp/fuse
/plugin install fuse@fuseai
```

### Cursor

Add to `~/.cursor/mcp.json` (or `.cursor/mcp.json` in a project):

```json
{
  "mcpServers": {
    "fuse": {
      "url": "https://mcp.fuseai.com"
    }
  }
}
```

Cursor will prompt you to sign in the first time a Fuse tool is used.

### VS Code (GitHub Copilot)

```bash
code --add-mcp '{"name":"fuse","type":"http","url":"https://mcp.fuseai.com"}'
```

Or add to `.vscode/mcp.json`:

```json
{
  "servers": {
    "fuse": {
      "type": "http",
      "url": "https://mcp.fuseai.com"
    }
  }
}
```

### Antigravity (App and CLI)

```bash
agy plugin install https://github.com/fuse-ai-mcp/fuse
```

The plugin adds the Fuse MCP server and skill. Sign in to Fuse in your browser when the server first connects.

### Gemini CLI

```bash
gemini extensions install https://github.com/fuse-ai-mcp/fuse
```

### Any other MCP client

Add a remote server with URL `https://mcp.fuseai.com` and transport Streamable HTTP. Leave authentication to OAuth: the client registers itself and opens a browser sign-in. Don't add an API key or `Authorization` header. Agents can follow [`llms-install.md`](llms-install.md).

## What it can do

- **Search** people and companies with natural-language or structured filters
- **Enrich** contacts with verified work emails and phone numbers from 40+ data providers
- **Lists**: build, import, filter, add AI research columns, export and sync to your CRM
- **Signals**: monitor job changes, hiring, funding, headcount growth, website visitors and LinkedIn activity
- **Research**: account and contact research, web search and meeting prep
- **Outreach**: generate and run multi-step email, LinkedIn and calling campaigns, and work your inbox

See the [tool reference](https://docs.fuseai.com/mcp/tools) for the full list.

## Safety

- Campaigns are created as drafts. Nothing is sent until you explicitly launch it.
- Searches, enrichment and research use your Fuse credits. Your assistant can check your balance and prices first.
- Access is scoped to your own Fuse workspace through OAuth.

## What's in this repo

This repo holds configuration only. The server itself is hosted by Fuse.

| File | For |
|---|---|
| `server.json` | Official MCP Registry entry |
| `.claude-plugin/`, `.mcp.json` | Claude Code plugin and marketplace |
| `.cursor-plugin/` | Cursor Marketplace plugin |
| `plugin.json`, `mcp.json` | Agent Plugins format (Cursor, Kiro, Copilot) |
| `.antigravity-plugin/`, `mcp_config.json` | Antigravity plugin (App and CLI) |
| `gemini-extension.json`, `GEMINI.md` | Gemini CLI extension |
| `skills/fuse/SKILL.md` | Skill that teaches agents how to use Fuse |
| `llms-install.md` | Install steps for agents such as Cline |

## Support

- Docs: https://docs.fuseai.com/mcp/connect
- Email: dev@tryfuse.ai
- [Privacy policy](https://fuseai.com/legal/privacy-policy) · [Terms of service](https://fuseai.com/legal/terms-of-service)

## License

The configuration files in this repo are released under the [MIT License](LICENSE). Use of the Fuse service is subject to the [Fuse terms of service](https://fuseai.com/legal/terms-of-service).
