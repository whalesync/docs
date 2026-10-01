---
description: >-
  Remote MCP server that lets AI agents create, configure, and monitor
  Whalesync syncs and Live Exports. Browser sign-in, no API keys.
---

# MCP server

Whalesync has a remote MCP (Model Context Protocol) server. AI agents in Claude, Claude Code, Cursor, VS Code, ChatGPT, and other MCP clients connect to it and create, configure, and monitor syncs and Live Exports on your behalf.

```
https://api.whalesync.com/mcp
```

The server uses the same resources, ids, and error codes as the [REST API](https://docs.whalesync.com/api/reference).

## Getting started

[Client setup](https://docs.whalesync.com/api/mcp/setup) has the detailed steps for specific clients.

The first time your agent calls the server, the browser opens Whalesync's consent page. Sign in, review the requested access, and click **Connect**. Then ask the agent to build a sync or a Live Export.

## Capabilities

A connection with `read` scope can monitor your syncs. This includes the tables and fields in the mappings, the operations log, open issues, the sync state of any single record, and the deletes waiting for review. It also covers Live Exports: their mappings, schedule, status, runs, and save progress. `operate` adds pausing and activating syncs, retrying issues, and triggering and canceling Live Export runs. `readwrite` adds creating, editing, and deleting syncs and Live Exports, and editing mappings.

Sync tool names start with `sync_` (`sync_list`, `sync_create`, `sync_get_status`, and so on), and Live Export tool names start with `live_export_`. The `sync_whats_next` tool reports where a sync is in the setup flow and the next steps to get it up and running.

## Steps that happen in the browser

By design, there are a few steps that are always done by a person in the app. Your agent will send you a link to complete them:

* **Connecting an app that signs in with OAuth.** Apps like Salesforce, HubSpot, and Webflow are connected by a person in the browser. The agent sends you a connect link; you sign in and pick the base. Credentials never pass through the agent. Airtable can also be connected with a personal access token passed as `auth`, when the person has already handed one to the agent.
* **Starting a new sync.** A person needs to review and approve a sync in the app before it can be run: the first time, and after a sync has been edited. The agent builds the draft and sends you its review link.
* **Approving a delete.** On a sync that holds deletes for review, a record that goes missing on one side waits for you instead of being deleted on the other. The agent can list what's waiting and send you the review link, but approving or ignoring a delete is irreversible, so you make that call in the app.

For a Live Export, the only browser step is connecting each side, where you also pick where the destination tables go. There is no review step before an export runs. Runs overwrite the tables the export manages, so the agent should confirm with you that the destination can be overwritten.

## Scopes

Connections use the same three scopes as API keys. From weakest to strongest:

* `read`: view syncs, mappings, status, operations, issues, and records, and view Live Exports, their mappings, schedules, runs, and saves. Note that operations include the values of synced records.
* `operate`: everything in `read`, plus running things. It can't change how anything is set up, and activating a sync never starts a draft; that still needs a person in the app.
* `readwrite`: everything, including creating, editing, and deleting syncs, mappings, and Live Exports, and saving and scheduling Live Exports.

A connection granted `operate` sees the read tools plus these five:

* `sync_pause`
* `sync_activate`
* `sync_retry_issue`
* `live_export_trigger`
* `live_export_cancel_run`

The OAuth server metadata lists `read`, `operate`, `readwrite`, `openid`, and `email` in `scopes_supported`. When a client requests more than one of `read`, `operate`, and `readwrite`, the strongest one counts. On the consent page, the person can grant the requested scope or a weaker one, never a stronger one. The token response's `scope` lists everything the grant includes, so an `operate` grant comes back as `read operate openid email`.

## Live Export tools

The Live Export tools wrap the [Live Export API](https://docs.whalesync.com/api/live-export).

| Tool | Scope | What it does |
| --- | --- | --- |
| `live_export_list_connectors` | `read` | Connectors usable for Live Export, with roles and auth |
| `live_export_list` | `read` | Live exports, newest first |
| `live_export_get` | `read` | One export, including `pending_actions` to relay |
| `live_export_create` | `readwrite` | Create a draft export (connector names only by default) |
| `live_export_update` | `readwrite` | Rename, finish an API-key side, set the destination location |
| `live_export_delete` | `readwrite` | Delete the export; destination tables stay |
| `live_export_list_source_tables` | `read` | Source tables |
| `live_export_list_source_fields` | `read` | A table's fields, with planned destination name and type |
| `live_export_list_locations` | `read` | Where created tables can live |
| `live_export_get_mappings` | `read` | Mappings document and `revision` |
| `live_export_update_mappings` | `readwrite` | Replace the mappings; pass `revision` |
| `live_export_validate_mappings` | `read` | Check a mappings document |
| `live_export_save` | `readwrite` | Create destination tables and apply the mappings; waits for the result |
| `live_export_get_save` | `read` | Wait for or read the save outcome |
| `live_export_get_schedule` | `read` | Schedule and `allowed_cadences` |
| `live_export_update_schedule` | `readwrite` | On/off, cadence, timezone |
| `live_export_get_status` | `read` | Whether a run is in progress, and when the next one is |
| `live_export_trigger` | `operate` | Run now |
| `live_export_list_runs` | `read` | Run history |
| `live_export_get_run` | `read` | One run with its steps |
| `live_export_cancel_run` | `operate` | Cancel a run in progress |
| `live_export_whats_next` | `read` | Next steps for an export, or with no argument, where to start |

`live_export_save` and `live_export_get_save` wait for the save to finish: up to 40 seconds, or up to 150 seconds when the client sends a progress token. With a progress token they also send progress notifications with a message such as "Creating tables and fields in the destination — 3 of 7 done." If the wait runs out, the result says the save is still running; call `live_export_get_save` again.

`live_export_update_mappings` takes the `revision` as an argument, because MCP has no headers.

`live_export_create` is not idempotent over MCP. After an ambiguous failure, check `live_export_list` before retrying.

Save, schedule update, trigger, and delete are marked destructive (`destructiveHint`), because they write to the destination or remove the export. Clients may ask you to confirm them.

`live_export_whats_next` returns `next_steps: [{order, kind, tool?, args_hint?, relay?, why}]`, where `kind` is `call_tool`, `relay_to_person`, or `wait_and_poll`. `sync_whats_next` returns the same shape.

## Managing connections

[Settings → MCP](https://app.whalesync.com/settings/mcp) lists the agents that have been given access to your account. They can be disconnected there to immediately revoke access.

## Errors and rate limits

Tool errors carry the same stable `code` values as the REST API, documented in the [Error reference](https://docs.whalesync.com/api/errors). Requests are limited to 120 per minute per user.
