---
description: Why Whalesync adds a "Whalesync ID" column to your sheets
---

# Whalesync ID column

To enable syncing, Whalesync adds a “Whalesync ID” column to each sheet in your Google Sheets.

<figure><img src="../../.gitbook/assets/whalesync ID.png" alt="" width="563"><figcaption><p>Example Whalesync ID column</p></figcaption></figure>

#### Why does Whalesync need to add a Whalesync ID column?

Unlike most apps and databases, Google Sheets doesn’t assign a unique ID to each row. To enable syncing, Whalesync adds its own ID column to uniquely identify each row.

#### Can I edit this column?

In general, you want to avoid editing this column since it is how Whalesync identifies each row. For example, this is why we suggest [avoiding sort range](avoid-sort-range.md).
