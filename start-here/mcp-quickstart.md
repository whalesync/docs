---
description: >-
  Build a Whalesync sync by chatting with your AI agent. Connect the Whalesync
  MCP server, sign in to your apps, map tables, then review and activate.
---

# MCP quickstart

You can set up a Whalesync sync without touching the dashboard. Connect your AI agent to Whalesync's MCP server, then ask it to build the sync in plain language. The agent will walk you through the process.

## Step 1: Connect your agent

Add the Whalesync MCP server to your agent. [Client setup](../api/mcp/setup.md) has the steps for most agents, or just directly use the server URL: `https://api.whalesync.com/mcp`.

## Step 2: Ask your agent to build a sync

Tell the agent what you want to sync, for example:

> Create a new Whalesync sync between Airtable and Webflow.

The agent will walk you through the remaining steps.

You can also ask for a Live Export, for example:

> Set up a Live Export from HubSpot into Airtable, refreshed daily.

The agent sends you a connect link for each app, asks which tables to copy, saves the export, and turns on the schedule. A Live Export has no review step, and its runs overwrite the tables it manages, so the agent confirms with you that the destination can be overwritten. The rest of this page follows a sync.

## Step 3: Sign in to your apps

To connect an app, the agent sends you a link that opens Whalesync in your browser. Your credentials go straight to Whalesync and never pass through the agent.

## Step 4: Map your tables

The agent reads the tables and fields on both sides. Use plain language to pick which to map and the direction for each. Whalesync can even create new tables in your apps if they don't exist yet.

## Step 5: Review and activate

A sync only runs after you review and approve its mappings in the app. The agent sends you a review link. Open it, confirm the mappings look right, and start the sync. Within seconds you should see data begin syncing.

{% hint style="info" %}
Your agent can also monitor a running sync — the operations it makes and any open issues. See the [MCP server](../api/mcp/README.md) overview for the full list of what an agent can do.
{% endhint %}
