---
description: When to use Live Export and when to use a standard Whalesync sync
---

# Live Export vs. sync

Whalesync offers two ways to move your data, built for different jobs:

- A **Sync** **keeps two apps in sync**. Both stay live and up to date, and you can edit data in either one. More powerful and configurable.
- **Live Export** makes a **read-only copy** of your data in another tool. You view, query, or share it, but don't edit it. Simpler and quicker to set up.

## Sample uses

{% hint style="success" %}
**Sync**: two apps stay in step, and you edit data in both.

- Control your Webflow site from Airtable.
- Update your HubSpot deals status from Notion.
- Let an operator edit your Supabase database from a friendly Airtable interface.
{% endhint %}

{% hint style="info" %}
**Live Export**: a read-only copy for viewing, sharing, or analysis.

- Analyze your Shopify orders in Notion.
- Share a subset of your Hubspot fields with a teammate in Airtable.
- Keep a queryable backup of your production data in Supabase.
{% endhint %}

## At a glance

|                        | Sync                                          | Live Export                                        |
| ---------------------- | --------------------------------------------- | -------------------------------------------------- |
| **Main purpose**       | Keep two apps in sync                         | Read-only copy of your data in another tool        |
| **Complexity**         | More powerful and configurable                | Simpler and quicker to set up                      |
| **Direction**          | One-way or [two-way](../features/two-way-sync.md) | One-way only                                   |
| **Destination**        | Editable — two-way sends your edits back      | Read-only mirror, overwritten on each run          |
| **Updates**            | Real time, as data changes                    | On demand or on a schedule                         |
| **Destination tables** | Existing tables or newly created tables       | Newly created for you                              |
| **Apps**               | Any connected app, on either side             | From any app, into Airtable, Notion, or Supabase   |

A few of these deserve a note:

- **Edits in a Live Export destination don't stick.** They aren't sent back to your source, and each run overwrites them. If you need edits to flow back, use a two-way sync.
- **Live Export builds the destination for you.** It creates the tables and fields in the base, schema, or page you choose. To write into tables you already maintain, use a sync.
- **Live Export destinations are Airtable, Notion, and Supabase.** You can export *from* any connected app; see what's available [here](https://app.whalesync.com/exports/setup/new/connect).

Still unsure? [Reach out](../resources/support/README.md) and we'll help you pick.
