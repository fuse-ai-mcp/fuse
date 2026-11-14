# Installing the Fuse MCP server

Fuse is a hosted (remote) MCP server. There is nothing to download, build or run locally, and no API key to configure.

## Connection

- URL: `https://mcp.fuseai.com`
- Transport: Streamable HTTP
- Authentication: OAuth 2.1 with dynamic client registration and PKCE. The client registers itself automatically. Scope: `mcp:tools`.
- OAuth discovery: `https://mcp.fuseai.com/.well-known/oauth-protected-resource`

## Steps

1. Add a remote MCP server named `fuse` with the URL `https://mcp.fuseai.com` and transport Streamable HTTP. Example configuration:

   ```json
   {
     "mcpServers": {
       "fuse": {
         "type": "streamableHttp",
         "url": "https://mcp.fuseai.com"
       }
     }
   }
   ```

   Use whatever field name your client expects for the transport (for example `streamableHttp`, `streamable-http` or `http`).

2. Do not add any API key, token or `Authorization` header. The first request returns `401` with an OAuth challenge, which starts the sign-in flow.
3. The user signs in to Fuse in their browser (or creates a free account at https://fuseai.com) and approves access.
4. Once connected, call a read-only tool such as `get_credits_balance` or `get_user_info` to confirm the connection works.

## Troubleshooting

- **401 Unauthorized** before sign-in is expected. If it persists after sign-in, remove the server, re-add it and sign in again.
- **No tools listed** usually means sign-in did not complete. Reconnect and finish the browser flow.
- Docs: https://docs.fuseai.com/mcp/connect
