---
description: >-
  Remote MCP server that lets AI agents create, configure, and monitor
  Whalesync syncs. Browser sign-in, no API keys.
---

# MCP server

Whalesync has a remote MCP (Model Context Protocol) server. AI agents in Claude, Claude Code, Cursor, VS Code, ChatGPT, and other MCP clients connect to it and create, configure, and monitor syncs on your behalf.

```
https://api.whalesync.com/mcp
```

The server uses the same resources, ids, and error codes as the [REST API](https://docs.whalesync.com/api/reference).

## Getting started

[Client setup](https://docs.whalesync.com/api/mcp/setup) has the detailed steps for specific clients.

The first time your agent calls the server, the browser opens Whalesync's consent page. Sign in, review the requested access, and click **Connect**. Then ask the agent to build a sync.

## Capabilities

A connection with `read` scope can monitor your syncs. This includes the tables and fields in the mappings, the operations log, and open issues. `readwrite` adds creating, editing, pausing, activating, and deleting syncs, editing mappings, and retrying issues.

The `whats_next` tool reports where a sync is in the setup flow and the next steps to get it up and running.

## Steps that happen in the browser

By design, there are a few steps that are always done by a person in the app. Your agent will send you a link to complete them:

* **Connecting an app that signs in with OAuth.** Apps like Airtable, HubSpot, and Webflow are connected by a person in the browser. The agent sends you a connect link; you sign in and pick the base. Credentials never pass through the agent.
* **Starting a new sync.** A person needs to review and approve a sync in the app before it can be run: the first time, and after a sync has been edited. The agent builds the draft and sends you its review link.

## Scopes

Connections use the same two scopes as API keys:

* `read`: view syncs, operations, and issues. Note that operations include the values of synced records.
* `readwrite`: everything in `read`, plus creating and changing syncs.

## Managing connections

[Settings → MCP](https://app.whalesync.com/settings/mcp) lists the agents that have been given access to your account. They can be disconnected there to immediately revoke access.

## Errors and rate limits

Tool errors carry the same stable `code` values as the REST API, documented in the [Error reference](https://docs.whalesync.com/api/errors). Requests are limited to 120 per minute per user.
