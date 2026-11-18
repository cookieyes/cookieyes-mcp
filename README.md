<div align="center">

<img src="https://www.cookieyes.com/cookieyes-logo.png" alt="CookieYes" width="96" />

# CookieYes MCP Server

**Manage cookie consent banners, run cookie scans and check GDPR / CCPA compliance — straight from your AI assistant.**

[Documentation](https://www.cookieyes.com/documentation/mcp-server/) ·
[Get a free account](https://www.cookieyes.com) ·
[Support](https://www.cookieyes.com/contact/)

</div>

---

## Overview

The CookieYes MCP Server connects AI assistants and IDEs — Claude, ChatGPT, Cursor, VS Code, LobeHub and any other
[Model Context Protocol](https://modelcontextprotocol.io) client — to your [CookieYes](https://www.cookieyes.com) account.
Ask in plain language and your assistant checks whether your banner is live, scans your site for cookies, reviews which
privacy laws you cover, or restyles your banner for you.

It is a **hosted, remote MCP server**. There is nothing to install, build or run: add the endpoint to your client and
sign in with your CookieYes account.

| | |
|---|---|
| **Endpoint** | `https://app.cookieyes.com/mcp` |
| **Transport** | Streamable HTTP |
| **Authentication** | OAuth 2.1 with PKCE — sign in with your CookieYes account, no API keys |
| **Plans** | Every CookieYes plan, including Free |
| **Capabilities** | 10 tools · 6 prompts |
| **Language** | English |
| **Official MCP Registry** | `com.cookieyes/mcp` |

## Contents

- [Before you connect](#before-you-connect)
- [Tools](#tools)
- [Prompts](#prompts)
- [Example requests](#example-requests)
- [Connect your client](#connect-your-client)
- [Security and privacy](#security-and-privacy)
- [Plan limits](#plan-limits)
- [Managing and revoking access](#managing-and-revoking-access)
- [FAQ](#faq)
- [Support](#support)
- [License](#license)

## Before you connect

1. **A CookieYes account.** [Sign up](https://www.cookieyes.com) if you don't have one — the Free plan works.
2. **MCP access turned on.** The account owner opens the profile menu → **MCP access**
   ([direct link](https://app.cookieyes.com/settings/mcp-access)) and switches on **Enable OAuth-based access**.
   No client can connect until this is on. Anyone on the account can see the status — an **MCP enabled** badge on
   **Organisations & Sites** — but only the owner can change it.
3. **An MCP client** that supports remote servers with OAuth.

## Tools

Read-only tools never change your account. Write tools change your live configuration, so the assistant first confirms
the website and banner with you, and most clients also ask you to approve the call.

### Websites and setup

| Tool | Type | What it does |
|---|---|---|
| `list_domains` | Read-only | Lists the websites in your account with their plan, banner status and compliance status. Supports search and pagination. |
| `get_website_details` | Read-only | Shows details for one website, including its plan's cookie-scan page limit. |
| `get_embed_code` | Read-only | Returns the script tag that installs the CookieYes banner on your site. |

### Banners

| Tool | Type | What it does |
|---|---|---|
| `list_banners` | Read-only | Lists a website's banners with their law (GDPR / CCPA), status, layout, position and theme. |
| `get_banner_status` | Read-only | Checks whether the banner is live on the site, when it was last detected, and whether it has been disabled. |
| `update_banner_colours` | Write | Switches the theme (Light, Dark, Auto-generated) or sets individual colours for the banner, buttons, links, toggles, the preference centre and blocked-content placeholders. Colours are hex values; the assistant converts names and RGB for you. |
| `update_banner_layout` | Write | Changes the layout (box, banner or popup), its position on the page, and the preference-centre style (centre, push-down, left or right sidebar). |

### Compliance and scanning

| Tool | Type | What it does |
|---|---|---|
| `get_compliance_status` | Read-only | Shows which privacy laws are enabled (GDPR, CCPA and others), plus geo-targeting and IAB TCF status. |
| `trigger_cookie_scan` | Write | Starts a cookie scan — a full crawl up to your plan's page limit, or a custom scan of URLs you choose to include or exclude. |
| `get_scan_results` | Read-only | Returns the latest completed scan, with cookies grouped by category. |

## Prompts

Ready-made, guided workflows. In clients that support MCP prompts they appear as slash commands or in a prompt picker.

| Prompt | What it does |
|---|---|
| `check_banner_setup` | Checks whether the cookie consent banner is active on a website. |
| `discover_cookies` | Scans a website and walks you through the cookies and trackers it finds. |
| `check_compliance` | Reviews a website's compliance configuration. |
| `monitor_domains` | Checks banner status across all of your websites at once. |
| `update_banner_theme` | Guides you through changing the banner theme or colours. |
| `customise_banner_layout` | Guides you through changing the banner layout, position or preference-centre style. |

## Example requests

**Check your setup**
- "Show all my sites."
- "Is my cookie banner live on example.com?"
- "Which of my sites have an inactive banner?"
- "Give me the installation code for my site."

**Compliance**
- "Is my site set up for GDPR?"
- "Which privacy laws does my banner cover?"

**Cookie scanning**
- "Scan my website for cookies."
- "What cookies are on my site? Group them by category."

**Banner design**
- "Switch my GDPR banner on example.com to the dark theme."
- "Set the accept button to navy blue."
- "Move my banner to the bottom right as a box."

## Connect your client

Every client uses the same endpoint, `https://app.cookieyes.com/mcp`. When you connect, you are sent to CookieYes to
log in, review the permissions and click **Allow**. When you see **Your CookieYes account is now connected**, return to
your client.

<details>
<summary><b>LobeHub</b></summary>

Install **CookieYes** from the LobeHub MCP marketplace, or add a custom MCP server with the URL
`https://app.cookieyes.com/mcp` (Streamable HTTP), then complete the CookieYes sign-in.

</details>

<details>
<summary><b>Claude (web and desktop)</b></summary>

1. Open **Settings** → **Connectors**.
2. Search for **CookieYes**, select it and click **Connect**.

</details>

<details>
<summary><b>Claude Code</b></summary>

```bash
claude mcp add --transport http cookieyes https://app.cookieyes.com/mcp
```

Then authenticate from inside Claude Code with `/mcp`, or run `claude mcp login cookieyes`.

</details>

<details>
<summary><b>ChatGPT</b></summary>

1. Open **Settings** → **Plugins** → **Browse plugins**.
2. Search for **CookieYes** and click **Install plugin**.

You can also click **+** in any chat, search for **CookieYes** and install it from there.

</details>

<details>
<summary><b>Cursor</b></summary>

Open **Settings** → **Tools & Integrations** → **MCP Tools** → **Add Custom MCP**, and add:

```json
{
  "mcpServers": {
    "cookieyes-mcp": {
      "url": "https://app.cookieyes.com/mcp"
    }
  }
}
```

Cursor calls MCP tools in **Agent** mode.

</details>

<details>
<summary><b>Visual Studio Code</b></summary>

Run **MCP: Add Server** from the Command Palette, choose **HTTP**, and paste the endpoint. Or edit `mcp.json` directly:

```json
{
  "servers": {
    "cookieyes": {
      "type": "http",
      "url": "https://app.cookieyes.com/mcp"
    }
  }
}
```

</details>

<details>
<summary><b>Windsurf</b></summary>

Open **Cascade MCP Registry** from the command palette, click **Edit** config, and add to `mcp_config.json`:

```json
{
  "mcpServers": {
    "cookieyes-mcp": {
      "url": "https://app.cookieyes.com/mcp"
    }
  }
}
```

Save, then click **Connect** next to `cookieyes-mcp`.

</details>

<details>
<summary><b>opencode</b></summary>

Add to `opencode.json` in your project root:

```json
{
  "mcp": {
    "cookieyes": {
      "type": "remote",
      "url": "https://app.cookieyes.com/mcp"
    }
  }
}
```

Then run `opencode mcp auth cookieyes`.

</details>

<details>
<summary><b>Codex, Zed, GitHub Copilot CLI, Lovable and others</b></summary>

Add a remote (Streamable HTTP) MCP server with the URL `https://app.cookieyes.com/mcp`, keep OAuth as the
authentication method, then click **Authenticate**. Step-by-step instructions for each client — including Vercel Connect
and the Cloudflare AI Playground — are in the [documentation](https://www.cookieyes.com/documentation/mcp-server/).

</details>

## Security and privacy

- **OAuth 2.1 with PKCE.** Your client receives a scoped access token. Your CookieYes password is never shared with it.
- **Owner opt-in.** Nothing can connect until the account owner turns on MCP access, and they can turn it off at any time.
- **Confirmation before changes.** The assistant confirms the website and banner before any write, and never changes
  several banners in one step without your approval. Keep your client's per-tool approval turned on and review write calls.

**What the server can access:** your websites and their banner configuration (status, layout, position, colours,
compliance settings), and cookie scan results.

**What it never accesses:** personal data, consent logs or visitor data; cookie values, session data or user identifiers;
your cookie policy and other legal text; billing details, passwords or team-member information.

See the [CookieYes privacy policy](https://www.cookieyes.com/privacy-policy/) and [DPA](https://www.cookieyes.com/dpa/).

## Plan limits

The server works on every plan, but tools follow your plan's limits:

- **Cookie scans** — the number of pages and scans per month depends on your plan.
- **Banner colours** — Free plans can switch between the Light and Dark themes. Auto-generated themes and custom colours
  need a paid plan.

## Managing and revoking access

- **Disconnect one client:** profile menu → **MCP access** → find the client under **Connectors** → **Disconnect**.
- **Pause every client:** the account owner switches off **Enable OAuth-based access**. Switching it back on restores
  access straight away.
- **From your client:** remove the CookieYes server in the client's own settings.

## FAQ

**Do I need to install or host anything?**
No. CookieYes runs the server. You only add the URL to your client.

**Is this the same as the CookieYes connector in Claude or the plugin in ChatGPT?**
Yes. They are all the same hosted server; "connector" and "plugin" are what those apps call an MCP server.

**Is it free?**
Yes, the server is available on every plan, including Free. Some tools have plan-based limits (see [Plan limits](#plan-limits)).

**My client says access is restricted.**
MCP access is turned off for that account. The account owner can turn it on under **MCP access**.

**Which languages are supported?**
English.

## Support

- Documentation: https://www.cookieyes.com/documentation/mcp-server/
- Email: support@cookieyes.com
- Contact: https://www.cookieyes.com/contact/

## About this repository

This repository holds the public listing information for MCP directories such as LobeHub (`lhm.plugin.json`). It does
not contain the server's source code; the server is operated by CookieYes Limited.

## License

The contents of this repository are released under the [MIT License](LICENSE). Use of the hosted CookieYes service is
governed by the [CookieYes Terms of Service](https://www.cookieyes.com/terms-and-conditions/).
