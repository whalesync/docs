---
description: >-
  Add the Whalesync MCP server to Claude, Claude Code, ChatGPT, Codex,
  Cursor, VS Code, or any other MCP client.
---

# Client setup

The server URL is all that a client needs to get started:

```
https://api.whalesync.com/mcp
```

There is no key or secret to put in the config. Authorization is [handled in the browser](#approving-the-connection) when you first connect.

## Claude (web, desktop, and mobile)

Whalesync is in the Claude connectors directory: open [claude.ai/directory/whalesync](https://claude.ai/directory/whalesync) and click **Connect**, or find Whalesync under Settings → Connectors → Browse connectors. Claude opens a browser sign-in to Whalesync on first use.

If your organization restricts directory connectors, you can still add a custom connector with the server URL `https://api.whalesync.com/mcp`. Anthropic's guide: [Get started with custom connectors using remote MCP](https://support.claude.com/en/articles/11175166-get-started-with-custom-connectors-using-remote-mcp).

## Claude Code

```bash
claude mcp add --transport http whalesync https://api.whalesync.com/mcp
```

Reference: [Connect Claude Code to tools via MCP](https://code.claude.com/docs/en/mcp).

## ChatGPT

Create a connector and paste the server URL. Custom MCP connectors in ChatGPT require developer mode, which is not available on every plan. OpenAI's guide: [Developer mode and MCP apps in ChatGPT](https://help.openai.com/en/articles/12584461-developer-mode-and-mcp-apps-in-chatgpt).

## Codex

```bash
codex mcp add whalesync --url https://api.whalesync.com/mcp
```

Or add the server to `~/.codex/config.toml`:

```toml
[mcp_servers.whalesync]
url = "https://api.whalesync.com/mcp"
```

`codex mcp login whalesync` starts the browser sign-in without waiting for first use. Reference: [Model Context Protocol](https://developers.openai.com/codex/mcp) in the Codex docs.

## Grok

In [grok.com/connectors](https://grok.com/connectors), choose **New Connector → Custom** and paste the server URL. Grok opens the browser sign-in when it first connects. xAI's guide: [Connectors](https://grok.com/connectors).

## Cursor

Add the server to `~/.cursor/mcp.json`, or to `.cursor/mcp.json` inside a project:

```json
{
  "mcpServers": {
    "whalesync": {
      "url": "https://api.whalesync.com/mcp"
    }
  }
}
```

Reference: [Whalesync](https://cursor.directory/plugins/whalesync) in the Cursor directory.

## VS Code

```bash
code --add-mcp '{"name":"whalesync","type":"http","url":"https://api.whalesync.com/mcp"}'
```

Reference: [Add and manage MCP servers in VS Code](https://code.visualstudio.com/docs/agent-customization/mcp-servers).

## Other clients

Any client that supports remote MCP servers over streamable HTTP works. Add `https://api.whalesync.com/mcp` as a remote server or custom connector. Where a config file is expected, the `mcpServers` JSON shown for Cursor is the common shape.

## Approving the connection

1. The first time the agent uses the server, the client opens your browser to Whalesync's consent page. 
2. The page shows the client's name and the access it requested. A request for read and write can be downgraded to read only.
3. Click **Connect**. The browser returns to the client and the agent is connected.

The new connection appears under [Settings → MCP](https://app.whalesync.com/settings/mcp).

## Troubleshooting

* **The agent reports a 401 or an expired authorization**: reconnect from the client. If the connection no longer appears under Settings → MCP, it was revoked, and reconnecting runs consent again.
* **"Connection request has expired"** on the consent page: more than ten minutes passed since the client started the connection. Retry from the client.

