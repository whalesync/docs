---
description: Common error messages from Notion and how to resolve them
---

# Common errors - Notion

#### `There are no databases shared via this integration token. Please share at least one database and try again.`

When authorizing Notion, you must search for and select the specific _database_ you want to sync and not just the _page_ the database lives in.

<figure><img src="../../.gitbook/assets/CleanShot 2025-02-22 at 08.01.53.png" alt=""><figcaption><p>Use the search in Notion auth to find the specific database you want to sync</p></figcaption></figure>

A [Notion database](https://www.notion.com/help/what-is-a-database) looks like this in Notion:

<figure><img src="../../.gitbook/assets/database.avif" alt=""><figcaption></figcaption></figure>

### “You have not authorized access to a page that can be used as a base for a sync. Please reauthorize the workspace and a page.”

We recently added support for auto-create tables and fields for Notion. With this new feature, Notion now requires users to authorize a Notion page in addition to the usual databases used for syncing. The Notion page you authorized will be the destination for all auto-created tables and fields, should you choose to use this feature.

### Notion limit on number of Options in a field:

While we support syncing option field from other app to Notion, Notion has a limitation on the number of options that are allowed in a single field. This is currently a limitation as we don't support syncing Option fields into a text field as a comma-separated list.
