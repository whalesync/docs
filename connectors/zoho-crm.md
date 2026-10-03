---
description: >-
  Two-way sync Zoho CRM leads, contacts, accounts, deals, and custom modules
  with Airtable, Notion, Google Sheets, and more.
cover: ../.gitbook/assets/gitbook-cover_zoho.jpg
coverY: 0
---

# Zoho CRM

## Zoho CRM Connector Guide

This guide covers how to connect Whalesync to [Zoho CRM](https://www.zoho.com/en-us/crm/), which modules and fields sync, and how syncing uses your Zoho API credits.

In Whalesync terms, your Zoho CRM **organization** is the base. Each Zoho module is a table, and each record is a row. Whalesync reads the modules and fields from your organization when you connect, so the tables match your Zoho setup, custom modules and custom fields included. A read-only Users table lists the people in your organization, so owner fields have something to link to.

### Connecting to Zoho CRM

Whalesync connects by signing in to Zoho.

1. In Whalesync, choose Zoho CRM.
2. Pick your **Data Center**, the region your Zoho account lives in. It matches the address you use for Zoho CRM (see the table below).
3. Click **Authorize**, sign in to Zoho, and accept the access Whalesync asks for.
4. Pick the base. There is one, named Zoho CRM.
5. Pick the modules to sync.

<table><thead><tr><th width="260">Data Center</th><th>Your Zoho CRM address</th></tr></thead><tbody>
<tr><td>United States (.com)</td><td><code>crm.zoho.com</code></td></tr>
<tr><td>Europe (.eu)</td><td><code>crm.zoho.eu</code></td></tr>
<tr><td>India (.in)</td><td><code>crm.zoho.in</code></td></tr>
<tr><td>Australia (.com.au)</td><td><code>crm.zoho.com.au</code></td></tr>
<tr><td>Japan (.jp)</td><td><code>crm.zoho.jp</code></td></tr>
<tr><td>Canada (.ca)</td><td><code>crm.zohocloud.ca</code></td></tr>
<tr><td>China (.com.cn)</td><td><code>crm.zoho.com.cn</code></td></tr>
<tr><td>Saudi Arabia (.sa)</td><td><code>crm.zoho.sa</code></td></tr>
</tbody></table>

If connecting fails after you sign in, check the data center first. Picking one other than your account's makes the connection fail.

Whalesync works with the access of the Zoho user who signs in. A user whose profile cannot see a module, or some of its records, syncs less than the whole organization, so sign in as an administrator.

### Syncing Data

Every module Zoho lets apps read through its API is a table, named as it is in your Zoho account. Its columns are the module's fields, standard and custom, under their Zoho labels, plus a read-only **Zoho CRM Record ID** column.

A lookup field is a link column to the table of the module it points at, and owner and other user fields link to the Users table. Changing a link in your other app changes the lookup, or the owner, in Zoho.

Adding a module or field in Zoho brings it in the next time you refresh the schema in Whalesync. Whalesync cannot create modules or fields in Zoho.

## Supported Tables

<table><thead><tr><th width="260">Table</th><th width="220">Status</th><th>Notes</th></tr></thead><tbody>
<tr><td>👤 Leads, 👤 Contacts, 👥 Accounts, 🤝 Deals</td><td>✅ Supported</td><td></td></tr>
<tr><td>☑️ Tasks, 📅 Meetings, 📞 Calls</td><td>✅ Supported</td><td>Meetings is the module Zoho's API calls Events.</td></tr>
<tr><td>🎛️ Campaigns</td><td>✅ Supported</td><td></td></tr>
<tr><td>🗒️ Notes</td><td>✅ Supported</td><td>Existing notes sync both ways, but new ones cannot be created from your other app. Zoho requires the record a note belongs to, and that field is read only.</td></tr>
<tr><td>📦 Products, Vendors, Cases, Solutions</td><td>✅ Supported</td><td>When your Zoho edition includes them.</td></tr>
<tr><td>🧾 Quotes, Sales Orders, Purchase Orders, Invoices</td><td>✅ Supported</td><td>Existing records sync both ways, but new ones cannot be created from your other app. See <a href="#things-to-keep-in-mind">Things to Keep in Mind</a>.</td></tr>
<tr><td>🧩 Custom modules</td><td>✅ Supported</td><td>Sync like the standard modules.</td></tr>
<tr><td>Modules Zoho does not let apps write to</td><td>➡️ Supported (1-Way)</td><td>Read only. Zoho decides which modules apps can create or edit records in.</td></tr>
<tr><td>🧑‍💻 Users</td><td>➡️ Supported (1-Way)</td><td>Read only. Everyone in your organization. See <a href="#users">Users</a>.</td></tr>
<tr><td>Activities</td><td>✖️ Not supported</td><td>Zoho's combined view. Sync Tasks, Meetings, and Calls instead.</td></tr>
<tr><td>Subforms</td><td>✖️ Not supported</td><td>Neither as tables nor as fields on the parent record.</td></tr>
<tr><td>Email Analytics, Email Template Analytics, Email Sentiment</td><td>✖️ Not supported</td><td>Zoho lists these modules but does not let apps read their records.</td></tr>
</tbody></table>

## Supported Fields

Fields sync by their Zoho field type, the same way in every module.

<table><thead><tr><th width="260">Zoho field type</th><th width="220">Status</th><th>Notes</th></tr></thead><tbody>
<tr><td>Single Line, Multi Line, Email, Phone, URL</td><td>✅ Supported</td><td></td></tr>
<tr><td>Number, Long Integer, Decimal, Currency, Percent</td><td>✅ Supported</td><td></td></tr>
<tr><td>Checkbox</td><td>✅ Supported</td><td></td></tr>
<tr><td>Date, Date/Time</td><td>✅ Supported</td><td>Date/Time values come back in the time zone of the Zoho user who connected. The moment is the same.</td></tr>
<tr><td>Pick List</td><td>✅ Supported</td><td>Synced by the option's text. Add new options in Zoho first. Zoho's <code>-None-</code> syncs as an empty cell.</td></tr>
<tr><td>Multi-Select Pick List</td><td>✅ Supported</td><td>A multi-value column. Add new options in Zoho first.</td></tr>
<tr><td>Lookup</td><td>✅ Supported</td><td>Links to the table of the module it points at. Contact Name on activities links to Contacts.</td></tr>
<tr><td>Lookup to a module that is not a table in Whalesync</td><td>➡️ Supported (1-Way)</td><td>Read only. A text column holding <code>Name (id)</code>. This covers lookups that can point at more than one module, such as an attachment's Parent ID.</td></tr>
<tr><td>Owner, User</td><td>✅ Supported</td><td>Links to the Users table. Linking a different user reassigns the record in Zoho.</td></tr>
<tr><td>Related To, on Tasks, Meetings, and Calls</td><td>✅ Supported</td><td>A JSON object naming the module and the record, for example <code>{"type": "Deals", "id": "5725767000000524157", "name": "Big deal"}</code>. To set it, write <code>type</code>, the module's API name, and <code>id</code>.</td></tr>
<tr><td>Formula, Rollup Summary, Auto-Number</td><td>➡️ Supported (1-Way)</td><td>Read only. Calculated by Zoho.</td></tr>
<tr><td>Created Time, Modified Time, Created By, Modified By</td><td>➡️ Supported (1-Way)</td><td>Read only, as is any other field Zoho does not let apps edit.</td></tr>
<tr><td>Tag</td><td>➡️ Supported (1-Way)</td><td>Read only. The tag names, separated by commas. Change tags in Zoho.</td></tr>
<tr><td>File Upload, Image Upload</td><td>➡️ Supported (1-Way)</td><td>Read only. The file names, separated by commas. The files themselves do not sync.</td></tr>
<tr><td>Multi-module lookups</td><td>➡️ Supported (1-Way)</td><td>Read only. The names of the linked records, separated by commas.</td></tr>
<tr><td>Reminders, repeat settings, consent, and other structured fields</td><td>➡️ Supported (1-Way)</td><td>Read only. A text column holding Zoho's JSON.</td></tr>
<tr><td>Subform, Multi-Select Lookup, Multi-User Lookup</td><td>✖️ Not supported</td><td>The column appears, but stays empty. Zoho leaves these fields out when apps list records.</td></tr>
</tbody></table>

### Users

The Users table is read only. It is there so owner and user fields have something to link to.

<table><thead><tr><th width="260">Field</th><th>Notes</th></tr></thead><tbody>
<tr><td>Full Name, First Name, Last Name, Email</td><td></td></tr>
<tr><td>Role, Profile</td><td>Text, as <code>Name (id)</code>.</td></tr>
<tr><td>Status</td><td>Whether the user is active. Inactive users are listed too.</td></tr>
</tbody></table>

## Things to Keep in Mind

* **The Zoho CRM connector is in beta.** If something does not work as described here, [let us know](../resources/support/).
* **Changes in Zoho arrive on the next scan.** Zoho does not notify Whalesync of changes, so Whalesync scans your synced modules on a schedule. To change how often, see [Sync frequency](../features/additional-features/sync-frequency.md).
* **Scans use your Zoho API credits.** Zoho allows each organization a set number of API credits in a rolling 24 hours, from 5,000 on the Free edition to 50,000 or more on paid editions, growing with your number of user licenses. See Zoho's [API limits](https://www.zoho.com/crm/developer/docs/api/v8/api-limits.html). Each scan reads every record and every field of each synced module, not only the fields you map. One credit reads 200 records and up to 50 fields, so a module with 10,000 records and 60 fields costs 100 credits a scan. Each record Whalesync creates or updates costs at least two more, one to write it and one to read it back, and each deletion costs one. If you run short, sync fewer modules or scan less often.
* **A module with more than 100,000 records cannot sync yet.** Whalesync stops reading it and reports an error on that table.
* **Quotes, Sales Orders, Purchase Orders, and Invoices cannot be created from your other app.** Zoho requires line items to create one, and line items are a subform, which Whalesync does not sync. Create these records in Zoho. Updates to existing ones sync both ways.
* **New records need the fields Zoho requires.** Zoho refuses a new record without them, for example Last Name on a lead or contact, or Deal Name and Stage on a deal. Custom fields you have made mandatory in Zoho count too.
* **Zoho automations run on records Whalesync writes.** Workflow rules, approvals, and blueprints run on records Whalesync creates and updates, as they do for any app using Zoho's API. Deleting a record from your other app does not run Zoho's workflow rules for the deletion, and Zoho's validation rules are not applied to records Whalesync writes.
* **Some modules in the list cannot be read.** A module the signed-in user's profile cannot access, or one that depends on a Zoho feature your organization has not turned on, such as Visits without SalesIQ, still appears when you pick tables. Syncing it reports an error on that table only. Remove it from the sync, or give the user access in Zoho.
* **Emoji become `?`.** Zoho replaces emoji and some other characters in text fields with `?`, and the `?` syncs back to your other app.

## Errors

| Message | What to do |
| --- | --- |
| Zoho rejected the credentials. Reconnect the Zoho account. | Whalesync's access was revoked in Zoho, or the user who signed in no longer has access. Reconnect Zoho CRM, signing in as a user who does. |
| Failed to poll Zoho `Visits`: followed by Zoho's message | The signed-in user cannot read that module. Their Zoho profile lacks access, or the module depends on a Zoho feature your organization has not turned on. Remove the table from the sync, or give the user access in Zoho. |
| Module "`Leads`" exceeds Zoho's 100,000-record page_token limit; Bulk Read is required. | The module has more records than Whalesync can read from Zoho today. Remove the table from the sync. |
| Zoho: followed by Zoho's reason for refusing a record, for example `Zoho: required field not found` | Check the record in your other app. The usual causes are a field Zoho requires that is missing, or a value that does not fit the field, such as an invalid email address. |
| Zoho: followed by another message from Zoho | Zoho's own explanation, for example that your organization has reached its record storage limit. Messages about API limits or too many requests are retried automatically. If they keep coming back, see the API credits note in [Things to Keep in Mind](#things-to-keep-in-mind). |

Messages name modules by their Zoho API names, which can differ from what you see in Zoho. Meetings appears as `Events`, for example.
