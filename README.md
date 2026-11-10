# CookieYes MCP Server

Manage cookie banners, run cookie scans and check GDPR/CCPA compliance from your AI assistant.

The CookieYes MCP Server is a **hosted** remote MCP server. There is nothing to install: point any MCP client at the endpoint below and sign in with your CookieYes account.

| | |
|---|---|
| **Endpoint** | `https://app.cookieyes.com/mcp` |
| **Transport** | Streamable HTTP |
| **Authentication** | OAuth 2.1 — sign in with your CookieYes account, no API keys |
| **Plans** | Works on every CookieYes plan, including Free |
| **Official MCP Registry** | `com.cookieyes/mcp` |
| **Documentation** | https://www.cookieyes.com/documentation/mcp-server/ |

## Before you connect

1. A [CookieYes account](https://www.cookieyes.com) — Free plan works.
2. The account owner turns on **Enable OAuth-based access** in CookieYes. No client can connect until this is on.

## What you can do

| Tool | What it does |
|---|---|
| `list_domains` | List the websites in your account with their banner and compliance status |
| `get_website_details` | Get details for one website, including its scan limit |
| `get_banner_status` | Check whether the banner is live on a site and when it was last detected |
| `get_compliance_status` | See which privacy laws are enabled (GDPR, CCPA and others), geo-targeting and IAB status |
| `get_embed_code` | Get the script tag that installs the banner |
| `list_banners` | List a site's banners with law, status, layout, position and theme |
| `trigger_cookie_scan` | Start a full or custom cookie scan |
| `get_scan_results` | Read the latest scan's cookies, grouped by category |
| `update_banner_colours` | Change the banner theme or individual element colours |
| `update_banner_layout` | Change the banner layout, position and preference-centre style |

Tools that change a banner ask you to confirm the website and banner first, and changes go live only after you confirm them.

## Example prompts

- "Is my cookie banner live on example.com?"
- "Which privacy laws does my banner cover?"
- "Run a cookie scan on my site and show the cookies by category."
- "Switch my GDPR banner to the dark theme."

## Connect

Add a remote MCP server in your client with the URL `https://app.cookieyes.com/mcp`, then complete the CookieYes sign-in when prompted. Client-by-client steps are in the [documentation](https://www.cookieyes.com/documentation/mcp-server/).

## Support

- Help: support@cookieyes.com
- Privacy policy: https://www.cookieyes.com/privacy-policy/
- DPA: https://www.cookieyes.com/dpa/

This repository holds listing information for MCP directories. The server itself is operated by CookieYes Limited.
