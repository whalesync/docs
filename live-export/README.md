---
description: Keep a live, updated copy of your data in another tool
---

# Live Export

**Live Export** creates a continuously updated, **read-only copy** of your data in a place that's easier to query, view, and share, like Airtable, Supabase, or Notion.

Unlike a standard Whalesync sync, **Live Export** is one-way and read-only: your source stays the system of record, while **Live Export** mirrors that data to a destination of your choice, and keeps it up-to-date as your source changes.

{% hint style="info" %}
**Live Export** is separate from Whalesync's standard two-way sync. It's built for making a clean, read-only copy of your data rather than keeping two apps in sync.
{% endhint %}

{% embed url="https://www.loom.com/share/07cf25f5b2ee40ebb187d475d7007d89" %}

## Features

- **Pick what to copy.** Choose exactly which tables and fields from your source get copied over.
- **Automatic table creation.** **Live Export** creates all the destination tables and fields for you in the base, schema, or page you choose.
- **Manual or scheduled updates.** Refresh your copy on demand by clicking **Run now**, or set it to update automatically on a schedule.
- **Resolves reference fields.** Linked and reference fields are resolved for you, so relationships between records carry over to the copy.
- **Always a mirror.** Because it's one-way, the copy tracks your source: records that are removed from the source are removed from the copy, and edits you make in the copy are overwritten.

## Supported apps

**Live Export** supports a different set of services than two-way sync. You can see what's available [here](https://app.whalesync.com/exports/setup/new/connect). We are always adding more services, so [reach out](resources/support/README.md) if there's something you are missing.

## Setting up a Live Export

Setup runs through a short wizard:

1. **Connect.** Pick and connect your source and your destination, then choose where the tables should be created: an Airtable base, a Notion page, or a Supabase schema. Whalesync will create the tables there for you.
2. **Choose data.** Select the tables and fields you want to copy. Some destinations (like Airtable and Notion) require a primary/title field, which you'll pick here.
3. **Activate.** Optionally set a schedule, then run your first sync.

## Update frequency

A **Live Export** can update two ways:

- **Manually**: click **Run now** any time to refresh the copy.
- **On a schedule**: turn on scheduled runs to keep the copy current automatically.

Scheduling is off by default (manual only). When you turn it on, you can choose to run every 10 minutes, every 30 minutes, hourly, or daily.

## FAQs

<details>

<summary>How is Live Export different from a normal Whalesync sync?</summary>

A normal Whalesync sync keeps two apps in sync, and can be two-way. **Live Export** is always one-way and the destination is read-only; it's a copy of your source, not a second system you edit. Your source stays the system of record.

</details>

<details>

<summary>Which destinations are supported?</summary>

You can copy to Airtable, Notion, and Supabase. You can copy from any app Whalesync connects to.

</details>

<details>

<summary>Do I need to create the tables first?</summary>

No. **Live Export** creates the destination tables and fields for you. You just choose where they go.

</details>

<details>

<summary>Is the copy read-only?</summary>

Yes. **Live Export** writes to the destination one way. Edits made in the destination aren't sent back to your source, and will be overwritten on the next run.

</details>

<details>

<summary>How often does the copy update?</summary>

Whenever you click **Run now**, or on a schedule if you turn one on: every 10 minutes, every 30 minutes, hourly, or daily.

</details>

<details>

<summary>What happens to records that are deleted in the source?</summary>

They're removed from the copy too, so the destination stays a true mirror. Rows that **Live Export** didn't create are left untouched.

</details>

<details>

<summary>Does Live Export count against my plan's record limit?</summary>

Yes, **Live Export** records count toward the same plan quota.

</details>

<details>

<summary>What happens if I delete a Live Export?</summary>

The **Live Export** stops running, but the data already copied to the destination is left untouched.

</details>
