---
description: >-
  Two-way sync Attio people, companies, deals, custom objects, lists, tasks, and
  notes with Airtable, Google Sheets, Notion, and more.
cover: ../../.gitbook/assets/Attio Gitbook Cover.jpg
coverY: 0
---

# Attio

## Attio Connector Guide

This guide covers how Attio data appears in Whalesync, which tables and field types sync, what Whalesync asks Attio for, and a few things to know before you start.

In Whalesync terms, your Attio workspace is the base, each Attio object or list is a table, and each record, list entry, task, or note is a row. People, Companies, Deals, and your custom objects sync in both directions. Lists, tasks, and notes each have their own page below.

## Supported Tables

<table><thead><tr><th width="260">Table</th><th width="220">Status</th><th>Notes</th></tr></thead><tbody>
<tr><td>👥 People</td><td>✅ Supported</td><td></td></tr>
<tr><td>🏢 Companies</td><td>✅ Supported</td><td></td></tr>
<tr><td>💰 Deals</td><td>✅ Supported</td><td></td></tr>
<tr><td>🧩 Custom objects</td><td>✅ Supported</td><td>Found automatically. See <a href="attio-custom-objects.md">Attio custom objects</a>.</td></tr>
<tr><td>📋 Lists</td><td>✅ Supported</td><td>Each list is its own table. See <a href="attio-lists.md">Attio lists</a>.</td></tr>
<tr><td>☑️ Tasks</td><td>✅ Supported</td><td>One table for the whole workspace. See <a href="attio-tasks.md">Attio tasks</a>.</td></tr>
<tr><td>📝 Notes</td><td>✅ Supported</td><td>One table for the whole workspace. See <a href="attio-notes.md">Attio notes</a>.</td></tr>
<tr><td>🧑‍💻 Users</td><td>✅ Supported</td><td>Your product's users. Only listed when the object is turned on in Attio. See <a href="#users-and-workspaces">Users and Workspaces</a>.</td></tr>
<tr><td>🏬 Workspaces</td><td>✅ Supported</td><td>Your product's accounts. Only listed when the object is turned on in Attio.</td></tr>
<tr><td>👤 Workspace Members</td><td>➡️ Supported (1-Way)</td><td>Read only. Your Attio teammates.</td></tr>
</tbody></table>

### Users and Workspaces

Attio has two standard objects, **Users** and **Workspaces**, for the people and accounts that use your own product. They are how a company gets product data into Attio, for example to see which of your customers are active or which account a contact belongs to.

Attio ships both objects switched off. They only appear in the Whalesync table picker after you turn them on in Attio under object settings. Once on, they sync in both directions like any other object. The Users table has no name field, so its primary field is the primary email address.

{% hint style="info" %}
**Users and Workspace Members are different tables.** Workspace Members are your Attio teammates, the people who log in to Attio. That table is read only. Users are the people who use your product, and that table syncs in both directions.
{% endhint %}

## Supported Fields

The field types below cover both the fields Attio gives every object and the custom attributes you add yourself.

<table><thead><tr><th width="260">Field type</th><th width="220">Status</th><th>Notes</th></tr></thead><tbody>
<tr><td>🆔 Record ID</td><td>➡️ Supported (1-Way)</td><td>Read only.</td></tr>
<tr><td>🔤 Name</td><td>✅ Supported</td><td>Person names are split into first and last name.</td></tr>
<tr><td>📄 Text</td><td>✅ Supported</td><td></td></tr>
<tr><td>🔢 Number and rating</td><td>✅ Supported</td><td></td></tr>
<tr><td>☑️ Checkbox</td><td>✅ Supported</td><td></td></tr>
<tr><td>📅 Date</td><td>✅ Supported</td><td>Created at is read only.</td></tr>
<tr><td>🔽 Single-select and multi-select</td><td>✅ Supported</td><td>Synced by option name. Options have to exist in Attio first.</td></tr>
<tr><td>🚦 Status</td><td>✅ Supported</td><td>Synced by status name.</td></tr>
<tr><td>💲 Currency</td><td>✅ Supported</td><td></td></tr>
<tr><td>📧 Email addresses</td><td>✅ Supported</td><td></td></tr>
<tr><td>📞 Phone numbers</td><td>✅ Supported</td><td></td></tr>
<tr><td>🔗 Domains and social media</td><td>✅ Supported</td><td>Includes LinkedIn, X, and other profile links.</td></tr>
<tr><td>📍 Location</td><td>✅ Supported</td><td>City, state, and country sync in both directions. Street address, postal code, and coordinates are not synced.</td></tr>
<tr><td>⬅️ Record links (Company, Team, Associated deals, custom links)</td><td>✅ Supported</td><td>A link to another table in your sync. A link that can point at several different objects is not supported.</td></tr>
<tr><td>🙋 Owner</td><td>✅ Supported</td><td>A link to the Workspace Members table.</td></tr>
<tr><td>💪 Connection strength, Created by, Strongest connection</td><td>➡️ Supported (1-Way)</td><td>Read only.</td></tr>
<tr><td>💬 Last interaction, Next interaction</td><td>➡️ Supported (1-Way)</td><td>Read only.</td></tr>
<tr><td>📋 List attributes</td><td>✅ Supported</td><td>Synced on the list's own table. See <a href="attio-lists.md">Attio lists</a>.</td></tr>
<tr><td>📑 Tabs</td><td>✖️ Not supported yet</td><td></td></tr>
</tbody></table>

## Permissions

When you connect Attio, Whalesync asks for the following access. Each item is there for one reason.

**Read only**

* **Workspace members**, so the Workspace Members table and the Owner and Assignee fields can show your teammates.
* **Object configuration**, so Whalesync can discover your objects and their attributes, including custom objects and select options.
* **List configuration**, so Whalesync can discover your lists and the attributes on them.

**Read and write**

* **Records**, so People, Companies, Deals, Users, Workspaces, and custom objects sync in both directions.
* **List entries**, so list rows sync in both directions.
* **Notes** and **tasks**, because those tables sync in both directions too.
* **Webhooks**, so Attio can tell Whalesync the moment something changes.

Whalesync only reads your configuration. It never creates or changes objects, attributes, lists, or select options in Attio. Comments, meetings, call recordings, files, and sequences are not requested and are not synced.

## How to Use

{% embed url="https://youtu.be/jUTvu0d7OUw" %}

## Things to Keep in Mind

* **Most changes arrive within a minute.** Whalesync uses Attio webhooks, so edits in Attio reach your other apps almost immediately. Some custom attribute types, including single-select and multi-select, do not send webhooks. Changes to those fields are picked up on the next scheduled poll.
* **A record edited right after it is created can take five to ten minutes to settle.** Attio creates a record or note the moment you click "new", before you type anything. The first, empty version syncs immediately, and what you type follows after a short cooling-off period. Nothing is lost.
* **Deleting a list entry does not delete the record.** Removing a row from a list table takes the entry out of the list in Attio. The company or person itself is untouched.
* **Parent record fields on a list row are read only.** To edit the company or person behind a list entry, add that table to your sync.
* **When a list entry and its parent record have a field with the same name, the list column wins.** "Created at" on a list table is when the entry was added to the list, not when the record was created.
* **Whalesync does not create select options or statuses.** Add the option in Attio first, then set it from your other app.

## More about Attio

{% content-ref url="attio-lists.md" %}
[attio-lists.md](attio-lists.md)
{% endcontent-ref %}

{% content-ref url="attio-custom-objects.md" %}
[attio-custom-objects.md](attio-custom-objects.md)
{% endcontent-ref %}

{% content-ref url="attio-tasks.md" %}
[attio-tasks.md](attio-tasks.md)
{% endcontent-ref %}

{% content-ref url="attio-notes.md" %}
[attio-notes.md](attio-notes.md)
{% endcontent-ref %}

### Using record links when syncing Attio with Google Sheets

For more on how record links (foreign keys) work with Google Sheets:

{% content-ref url="../google-sheets/foreign-keys.md" %}
[foreign-keys.md](../google-sheets/foreign-keys.md)
{% endcontent-ref %}
