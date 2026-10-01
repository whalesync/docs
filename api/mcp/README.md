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

A connection with `read` scope can monitor your syncs. This includes the tables and fields in the mappings, the operations log, open issues, the sync state of any single record, and the deletes waiting for review. `operate` adds pausing and activating syncs, retrying issues, and triggering and canceling Live Export runs. `readwrite` adds creating, editing, and deleting syncs and Live Exports, and editing mappings.

Sync tool names start with `sync_` (`sync_list`, `sync_create`, `sync_get_status`, and so on), and Live Export tool names start with `live_export_`. The `sync_whats_next` tool reports where a sync is in the setup flow and the next steps to get it up and running.

## Steps that happen in the browser

By design, there are a few steps that are always done by a person in the app. Your agent will send you a link to complete them:

* **Connecting an app that signs in with OAuth.** Apps like Salesforce, HubSpot, and Webflow are connected by a person in the browser. The agent sends you a connect link; you sign in and pick the base. Credentials never pass through the agent. Airtable can also be connected with a personal access token passed as `auth`, when the person has already handed one to the agent.
* **Starting a new sync.** A person needs to review and approve a sync in the app before it can be run: the first time, and after a sync has been edited. The agent builds the draft and sends you its review link.
* **Approving a delete.** On a sync that holds deletes for review, a record that goes missing on one side waits for you instead of being deleted on the other. The agent can list what's waiting and send you the review link, but approving or ignoring a delete is irreversible, so you make that call in the app.

## Scopes

Connections use the same three scopes as API keys. From weakest to strongest:

* `read`: view syncs, mappings, status, operations, issues, and records. Note that operations include the values of synced records.
* `operate`: everything in `read`, plus running things. It can't change how anything is set up, and activating a sync never starts a draft; that still needs a person in the app.
* `readwrite`: everything, including creating, editing, and deleting syncs, mappings, and Live Exports.

A connection granted `operate` sees the read tools plus these five:

* `sync_pause`
* `sync_activate`
* `sync_retry_issue`
* `live_export_trigger`
* `live_export_cancel_run`

The OAuth server metadata lists `read`, `operate`, `readwrite`, `openid`, and `email` in `scopes_supported`. When a client requests more than one of `read`, `operate`, and `readwrite`, the strongest one counts. On the consent page, the person can grant the requested scope or a weaker one, never a stronger one. The token response's `scope` lists everything the grant includes, so an `operate` grant comes back as `read operate openid email`.

## Managing connections

[Settings → MCP](https://app.whalesync.com/settings/mcp) lists the agents that have been given access to your account. They can be disconnected there to immediately revoke access.

## Errors and rate limits

Tool errors carry the same stable `code` values as the REST API, documented in the [Error reference](https://docs.whalesync.com/api/errors). Requests are limited to 120 per minute per user.
