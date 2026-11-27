# Installing the CookieYes MCP Server

These instructions are for AI agents (such as Cline) setting up the CookieYes MCP Server for a user.

## What this server is

CookieYes is a **hosted, remote** MCP server. There is nothing to clone, build, install or run locally: no npm
package, no Docker image, no API key and no environment variables. You only add the endpoint to the client's MCP
configuration, and the user signs in with OAuth.

- **Endpoint:** `https://app.cookieyes.com/mcp`
- **Transport:** Streamable HTTP
- **Authentication:** OAuth 2.1 (the client registers itself automatically and opens a browser sign-in)

## Before you start

Tell the user they need:

1. A CookieYes account. The Free plan works: https://www.cookieyes.com
2. MCP access turned on for that account. The account owner opens https://app.cookieyes.com/settings/mcp-access and
   switches on **Enable OAuth-based access**. Without this, sign-in fails.

## Setup for Cline

Configure **Cline's own MCP settings only**. Do not edit the configuration of any other client (for example
`~/.claude/settings.json`, `~/.claude.json`, `.vscode/mcp.json`, Cursor or Windsurf files), and do not tell the user
to run another client's commands (such as `claude mcp login`).

Cline's MCP settings file is:

- **Cline 4.x (VS Code extension and CLI):** `~/.cline/data/settings/cline_mcp_settings.json`, or the path in the
  `CLINE_MCP_SETTINGS_PATH` environment variable if it is set. Use this file. Cline creates it with
  `{"mcpServers": {}}` on first start, so if it exists, it is the right one.
- **Older Cline (3.x) only:** the extension's global storage, for example
  `~/Library/Application Support/Code/User/globalStorage/saoudrizwan.claude-dev/settings/cline_mcp_settings.json` on
  macOS. Use this only if `~/.cline/data/settings/cline_mcp_settings.json` does not exist. Never create this folder.

If unsure, ask the user to open the file from the Cline panel (**MCP Servers** → **Configure** → **Configure MCP
Servers**); that always opens the file Cline actually reads.

Add this entry under `mcpServers` in that file, keeping any servers already there:

```json
{
  "mcpServers": {
    "cookieyes": {
      "type": "streamableHttp",
      "url": "https://app.cookieyes.com/mcp"
    }
  }
}
```

- Set `"type": "streamableHttp"` explicitly. Without it, Cline falls back to the legacy SSE transport, which
  this server does not use.
- Do not add a `headers` or `Authorization` entry. Authentication is OAuth, not a token.

The user can also add it from the Cline panel: **MCP Servers** → **Remote Servers**, with Server URL
`https://app.cookieyes.com/mcp` and Transport Type **Streamable HTTP**.

## Sign-in

Cline handles the OAuth sign-in itself; you do not need to complete it from the chat. After the server is added (if
Cline does not prompt automatically, the user clicks **Authenticate** next to `cookieyes` in the **MCP Servers** panel),
Cline opens a browser window to CookieYes. Ask the user to log in, review the permissions
and click **Allow**. When the page says **Your CookieYes account is now connected**, they can return to Cline. With the
Cline CLI, run `cline mcp` and choose **Authorize OAuth** for `cookieyes`.

## Check that it works

Call the `list_domains` tool. It should return the websites in the user's CookieYes account.

## Troubleshooting

- **Sign-in fails or shows an access error:** MCP access is not turned on. See "Before you start".
- **Connection fails straight away:** check that `type` is `streamableHttp` and the URL is exactly
  `https://app.cookieyes.com/mcp`.
- **A tool says the feature is not available:** some tools follow the user's CookieYes plan limits (for example,
  banner colour changes need a paid plan). This is expected.

Documentation: https://www.cookieyes.com/documentation/mcp-server/
