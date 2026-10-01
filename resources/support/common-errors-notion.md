---
description: >-
  Fix Notion errors in Whalesync: no databases shared via the integration token,
  no page authorized for auto-created tables, and Notion's field option limit.
---

# Common errors - Notion

#### `There are no databases shared via this integration token. Please share at least one database and try again.`

When authorizing Notion, you must search for and select the specific _database_ you want to sync and not just the _page_ the database lives in.

<figure><img src="../../.gitbook/assets/CleanShot 2025-02-22 at 08.01.53.png" alt=""><figcaption><p>Use the search in Notion auth to find the specific database you want to sync</p></figcaption></figure>

A [Notion database](https://www.notion.com/help/what-is-a-database) looks like this in Notion:

<figure><img src="../../.gitbook/assets/database.avif" alt=""><figcaption></figcaption></figure>

### “You have not authorized access to a page that can be used as a base for a sync. Please reauthorize the workspace and a page.”

Whalesync can auto-create tables and fields in Notion. To support this, Notion requires you to authorize a Notion page in addition to the databases used for syncing. The Notion page you authorized will be the destination for all auto-created tables and fields, should you choose to use this feature.

<figure><img src="../../.gitbook/assets/CleanShot 2025-09-20 at 02.02.53@2x.png" alt=""><figcaption></figcaption></figure>

### Notion limit on number of Options in a field

Whalesync can sync option fields from other apps into Notion, but Notion limits how many options one select or multi-select field can have. If your field has more options than Notion allows, map it to a Notion text field instead, and the values will sync as a comma-separated list.
