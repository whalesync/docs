---
description: >-
  Two-way sync Close leads, contacts, opportunities, tasks, and notes with
  Airtable, Notion, Google Sheets, and more.
cover: ../../.gitbook/assets/gitbook-cover_close.jpg
coverY: 0
---

# Close

## Close Connector Guide

This guide covers how to connect Whalesync to [Close](https://www.close.com), which tables and fields sync, and a few things to know before you start.

In Whalesync terms, a Close **organization** is the base you pick. Each Close object Whalesync supports is a table, and each lead, contact, opportunity, task, or note is a row. Leads, Contacts, Opportunities, Tasks, and Notes sync in both directions. Pipelines sync both ways too, but only the pipeline name is writable. Users, Lead Statuses, and Opportunity Statuses are your organization's configuration and are read only.

### Connecting to Close

Whalesync connects with a Close API key you paste in. An API key reaches one Close organization, and that organization is the base. See [Authorize Close](authorize-close.md).

1. In Whalesync, choose Close and paste a Close API key.
2. Pick the organization to sync.
3. Pick the tables to sync.

## Supported Tables

<table><thead><tr><th width="260">Table</th><th width="220">Status</th><th>Notes</th></tr></thead><tbody>
<tr><td>👥 Leads</td><td>✅ Supported</td><td>The companies and accounts in Close. Contacts, opportunities, tasks, and notes all hang off a lead.</td></tr>
<tr><td>👤 Contacts</td><td>✅ Supported</td><td>Each contact belongs to one lead.</td></tr>
<tr><td>🤝 Opportunities</td><td>✅ Supported</td><td></td></tr>
<tr><td>☑️ Tasks</td><td>✅ Supported</td><td>Whalesync creates lead tasks, and Close's own task types can appear in the table. See <a href="#things-to-keep-in-mind">Things to Keep in Mind</a>.</td></tr>
<tr><td>🗒️ Notes</td><td>✅ Supported</td><td></td></tr>
<tr><td>🎛️ Pipelines</td><td>✅ Supported</td><td>Name is the only field that writes back to Close; the rest, including the list of statuses, are read only. Creating a row creates a pipeline in Close, and deleting one deletes the pipeline along with its statuses.</td></tr>
<tr><td>📊 Lead Statuses</td><td>➡️ Supported (1-Way)</td><td>Read only. Organization configuration.</td></tr>
<tr><td>🎲 Opportunity Statuses</td><td>➡️ Supported (1-Way)</td><td>Read only. Organization configuration.</td></tr>
<tr><td>🧑‍💻 Users</td><td>➡️ Supported (1-Way)</td><td>Read only. Your Close teammates.</td></tr>
<tr><td>✉️ Emails, 📞 Calls, 📅 Meetings, 🏃 other activities</td><td>✖️ Not supported</td><td>Notes are the only Close activity type that syncs. Tasks have their own table above.</td></tr>
</tbody></table>

## Supported Fields

### Leads

<table><thead><tr><th width="260">Close field</th><th width="220">Status</th><th>Notes</th></tr></thead><tbody>
<tr><td>Name</td><td>✅ Supported</td><td>Required to create a lead.</td></tr>
<tr><td>Description</td><td>✅ Supported</td><td></td></tr>
<tr><td>Url</td><td>✅ Supported</td><td>The lead's website.</td></tr>
<tr><td>Status id</td><td>✅ Supported</td><td>Links to the Lead Statuses table.</td></tr>
<tr><td>Addresses</td><td>✅ Supported</td><td>Multi-value. Each entry is a JSON object with <code>label</code>, <code>address_1</code>, <code>address_2</code>, <code>city</code>, <code>state</code>, <code>zipcode</code>, and <code>country</code>.</td></tr>
<tr><td>Html url</td><td>➡️ Supported (1-Way)</td><td>Read only. The lead's page in Close.</td></tr>
<tr><td>Created by, Updated by</td><td>➡️ Supported (1-Way)</td><td>Read only. Links to the Users table.</td></tr>
<tr><td>Date created, Date updated</td><td>➡️ Supported (1-Way)</td><td>Read only.</td></tr>
</tbody></table>

### Contacts

<table><thead><tr><th width="260">Close field</th><th width="220">Status</th><th>Notes</th></tr></thead><tbody>
<tr><td>Name, Title</td><td>✅ Supported</td><td></td></tr>
<tr><td>Emails</td><td>✅ Supported</td><td>Multi-value. The addresses sync; their office or home labels do not.</td></tr>
<tr><td>Phones</td><td>✅ Supported</td><td>Multi-value. The numbers sync; their labels do not.</td></tr>
<tr><td>Urls</td><td>✅ Supported</td><td>Multi-value. Each entry is a JSON object with <code>url</code> and <code>type</code>, unlike Emails and Phones, which sync the bare value.</td></tr>
<tr><td>Lead</td><td>✅ Supported</td><td>Required. Set when the contact is created. Close does not allow moving a contact to another lead afterwards.</td></tr>
<tr><td>Email</td><td>➡️ Supported (1-Way)</td><td>Read only. The contact's first email address. Write through Emails.</td></tr>
<tr><td>Organization id</td><td>➡️ Supported (1-Way)</td><td>Read only.</td></tr>
<tr><td>Created by, Updated by, Date created, Date updated</td><td>➡️ Supported (1-Way)</td><td>Read only.</td></tr>
</tbody></table>

### Opportunities

<table><thead><tr><th width="260">Close field</th><th width="220">Status</th><th>Notes</th></tr></thead><tbody>
<tr><td>Lead</td><td>✅ Supported</td><td>Required. Set when the opportunity is created, and fixed after that.</td></tr>
<tr><td>Contact</td><td>✅ Supported</td><td>The contact has to belong to the same lead.</td></tr>
<tr><td>Status id</td><td>✅ Supported</td><td>Links to the Opportunity Statuses table.</td></tr>
<tr><td>Value</td><td>✅ Supported</td><td>In cents. $1,500 is <code>150000</code>.</td></tr>
<tr><td>Value period</td><td>✅ Supported</td><td>How often the value recurs, for example <code>one_time</code> or <code>monthly</code>.</td></tr>
<tr><td>Confidence</td><td>✅ Supported</td><td>Close's percentage, 0 to 100.</td></tr>
<tr><td>Note</td><td>✅ Supported</td><td></td></tr>
<tr><td>Lead name, Status label, Status type, Value formatted, Value currency</td><td>➡️ Supported (1-Way)</td><td>Read only. Close works these out from the fields above.</td></tr>
<tr><td>Expected value, Annualized value, Annualized expected value, Date won</td><td>➡️ Supported (1-Way)</td><td>Read only. Calculated by Close.</td></tr>
<tr><td>User, User name</td><td>➡️ Supported (1-Way)</td><td>Read only. The opportunity's owner in Close.</td></tr>
<tr><td>Organization id, Created by, Updated by, Date created, Date updated</td><td>➡️ Supported (1-Way)</td><td>Read only.</td></tr>
</tbody></table>

### Tasks

<table><thead><tr><th width="260">Close field</th><th width="220">Status</th><th>Notes</th></tr></thead><tbody>
<tr><td>Text</td><td>✅ Supported</td><td>The task itself.</td></tr>
<tr><td>Date</td><td>✅ Supported</td><td>The date the task is due.</td></tr>
<tr><td>Is complete</td><td>✅ Supported</td><td></td></tr>
<tr><td>Assigned to</td><td>✅ Supported</td><td>Links to the Users table.</td></tr>
<tr><td>Lead</td><td>✅ Supported</td><td>Required. Set when the task is created, and fixed after that.</td></tr>
<tr><td>Type</td><td>✅ Supported</td><td>Set when the task is created. Whalesync creates lead tasks.</td></tr>
<tr><td>Contact, Object Type, Object ID, View, Is dateless, Due date</td><td>➡️ Supported (1-Way)</td><td>Read only. Close fills these in itself.</td></tr>
<tr><td>Organization</td><td>➡️ Supported (1-Way)</td><td>Read only. Named Organization id on the other tables.</td></tr>
<tr><td>Created by, Updated by, Date created, Date updated</td><td>➡️ Supported (1-Way)</td><td>Read only.</td></tr>
</tbody></table>

### Notes

<table><thead><tr><th width="260">Close field</th><th width="220">Status</th><th>Notes</th></tr></thead><tbody>
<tr><td>Note</td><td>✅ Supported</td><td>The text of the note. Required to create a note.</td></tr>
<tr><td>Contact</td><td>✅ Supported</td><td>Links to the Contacts table.</td></tr>
<tr><td>Lead</td><td>✅ Supported</td><td>Required. Set when the note is created, and fixed after that.</td></tr>
<tr><td>User</td><td>✅ Supported</td><td>Who the note is from. Set when the note is created, and fixed after that.</td></tr>
<tr><td>Activity at, Type</td><td>➡️ Supported (1-Way)</td><td>Read only.</td></tr>
<tr><td>Organization id, Created by, Updated by, Date created, Date updated</td><td>➡️ Supported (1-Way)</td><td>Read only.</td></tr>
</tbody></table>

### Custom fields

Close custom fields sync on Leads, Contacts, and Opportunities. Each one is a column named after the field.

<table><thead><tr><th width="260">Close custom field type</th><th width="220">Status</th><th>Notes</th></tr></thead><tbody>
<tr><td>Text, Hidden</td><td>✅ Supported</td><td>A text column.</td></tr>
<tr><td>Number</td><td>✅ Supported</td><td></td></tr>
<tr><td>Date, Date and time</td><td>✅ Supported</td><td></td></tr>
<tr><td>Choices</td><td>✅ Supported</td><td>Synced by the choice's label, not an ID. Add new choices in Close first.</td></tr>
<tr><td>User</td><td>✅ Supported</td><td>Links to the Users table.</td></tr>
<tr><td>Contact</td><td>✅ Supported</td><td>Links to the Contacts table. The contact has to belong to the same lead.</td></tr>
<tr><td>Custom object</td><td>✖️ Not supported</td><td>The field still appears, as a text column holding Close's raw object ID. Whalesync does not resolve it to the object it points at.</td></tr>
</tbody></table>

A custom field that accepts multiple values in Close becomes a multi-value column in Whalesync, whatever its type: a multiple-choice dropdown, but equally a User or Contact field set to accept several.

Adding a custom field in Close brings it in the next time you refresh the schema in Whalesync.

### Reference tables

Users, Lead Statuses, and Opportunity Statuses are read only. They are here so the fields that point at them, like a lead's status or a task's assignee, have something to link to. Pipelines is listed for a different reason: nothing links to it, and its name is the only organization configuration Whalesync can write. Pipeline id on Opportunity Statuses is plain text rather than a link to it.

<table><thead><tr><th width="260">Table</th><th>Fields</th></tr></thead><tbody>
<tr><td>Users</td><td>First name, Last name, Email, Image, Organizations, Last used timezone, Email verified at, Email verification token generated at, Date created, Date updated. All read only.</td></tr>
<tr><td>Lead Statuses</td><td>Label, Organization id. Read only.</td></tr>
<tr><td>Opportunity Statuses</td><td>Label, Type, Pipeline id, Organization id. Read only.</td></tr>
<tr><td>Pipelines</td><td>Name syncs both ways. Statuses, Organization id, Created by, Updated by, Date created, and Date updated are read only.</td></tr>
</tbody></table>

To add a lead status, an opportunity status, or a pipeline stage, add it in Close. It arrives as a new row in the matching table on the next scheduled poll.

## Things to Keep in Mind

* **The Close connector is in beta.** If something does not work as described here, [let us know](../../resources/support/).
* **Most changes in Close arrive within a minute.** Whalesync uses Close webhooks for leads, contacts, opportunities, notes, and lead tasks. Everything else is picked up on the next scheduled poll.
* **Delete leads in Close, not from your other app.** Close deletes a lead's contacts, opportunities, tasks, and notes along with it, and your other app has no way to know that happened, so those rows turn into sync issues. Deleting the lead in Close deletes the matching rows cleanly.
* **A record cannot be moved to another lead.** Close fixes the lead on a contact, opportunity, task, or note when it is created. Changing it in your other app is ignored rather than synced. Create a new record under the right lead instead.
* **A contact on an opportunity has to belong to the same lead.** Close refuses a contact from another lead, and the change is reported as a sync issue.
* **Opportunity values are in cents.** Close stores $1,500 as `150000`. Use a formula in your other app if you want to show dollars.
* **Email and phone labels are not synced.** The addresses and numbers on a contact sync, but Close's office, home, and mobile labels do not, and writing to those columns resets the label to Close's default.
* **Whalesync creates lead tasks.** Close also generates its own tasks for calls, emails, and opportunities. Close only notifies Whalesync about lead tasks, so any of the others that show up in the table are only refreshed on the next scheduled poll.
* **A task created in Close takes a few seconds to appear.** Close does not return a new task immediately, so it arrives in the following sync.
* **Statuses and pipelines are organization configuration.** Whalesync never creates a lead status, an opportunity status, or a pipeline stage for you. Pipelines are the exception: a new row in the Pipelines table creates a pipeline in Close, renaming a row renames it, and deleting a row deletes that pipeline in Close along with the statuses on it. Delete a pipeline in Close, where you can see what is attached to it, rather than from your other app.
* **Close refuses to delete the last pipeline** in an organization, and some Close plans limit how many pipelines you can have. Both come back as sync issues carrying Close's own message.
