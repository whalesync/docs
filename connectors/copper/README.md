---
description: >-
  Two-way sync Copper people, companies, opportunities, leads, tasks, and
  projects with Airtable, Notion, Google Sheets, and more.
cover: ../../.gitbook/assets/gitbook-cover_copper.jpg
coverY: 0
---

# Copper

## Copper Connector Guide

This guide covers how to connect Whalesync to [Copper](https://www.copper.com), which tables and fields sync, and a few things to know before you start.

In Whalesync terms, a Copper **account** is the base you pick. Each Copper object Whalesync supports is a table, and each person, company, opportunity, lead, task, or project is a row. People, Companies, Opportunities, Leads, Tasks, and Projects sync in both directions. Activities and your account's configuration, such as users, pipelines, and tags, are read only.

### Connecting to Copper

Whalesync connects with a Copper API key and the email of the Copper user who created it. A connection reaches one Copper account, and that account is the base. See [Authorize Copper](authorize-copper.md).

1. In Whalesync, choose Copper, paste a Copper API key, and enter the Copper account email.
2. Pick the account to sync.
3. Pick the tables to sync.

## Supported Tables

<table><thead><tr><th width="260">Table</th><th width="220">Status</th><th>Notes</th></tr></thead><tbody>
<tr><td>👤 People</td><td>✅ Supported</td><td></td></tr>
<tr><td>🏢 Companies</td><td>✅ Supported</td><td></td></tr>
<tr><td>🤝 Opportunities</td><td>✅ Supported</td><td></td></tr>
<tr><td>🎯 Leads</td><td>✅ Supported</td><td>Copper turns Leads off by default. Turn on Leads in Copper's Settings first, or the Leads table reports an error. See <a href="#things-to-keep-in-mind">Things to Keep in Mind</a>.</td></tr>
<tr><td>☑️ Tasks</td><td>✅ Supported</td><td></td></tr>
<tr><td>📁 Projects</td><td>✅ Supported</td><td></td></tr>
<tr><td>🗒️ Activities</td><td>➡️ Supported (1-Way)</td><td>Read only.</td></tr>
<tr><td>Users, Pipelines, Pipeline Stages, Contact Types, Customer Sources, Loss Reasons, Lead Statuses, Tags, Activity Types</td><td>➡️ Supported (1-Way)</td><td>Read only. Account configuration. See <a href="#reference-tables">Reference tables</a>.</td></tr>
<tr><td>📎 Files and attachments</td><td>✖️ Not supported</td><td></td></tr>
</tbody></table>

## Supported Fields

Emails, Phone Numbers, Socials, and Websites are JSON lists in Copper's own format:

* Emails: `[{"email": "ada@example.com", "category": "work"}]`
* Phone Numbers: `[{"number": "+1 415 555 0100", "category": "mobile"}]`
* Socials and Websites: `[{"url": "https://example.com", "category": "work"}]`

Copper splits an address into the Street, City, State, Postal Code, and Country columns. Tags is a multi-value text column.

### People

<table><thead><tr><th width="260">Copper field</th><th width="220">Status</th><th>Notes</th></tr></thead><tbody>
<tr><td>Name</td><td>✅ Supported</td><td>The person's full name. Copper splits it into First Name, Middle Name, and Last Name.</td></tr>
<tr><td>Prefix, Suffix, Title</td><td>✅ Supported</td><td></td></tr>
<tr><td>Details</td><td>✅ Supported</td><td>Multi-line text.</td></tr>
<tr><td>Assignee</td><td>✅ Supported</td><td>Links to the Users table.</td></tr>
<tr><td>Contact Type</td><td>✅ Supported</td><td>Links to the Contact Types table.</td></tr>
<tr><td>Emails, Phone Numbers, Socials, Websites</td><td>✅ Supported</td><td>JSON lists. See the formats above.</td></tr>
<tr><td>Street, City, State, Postal Code, Country</td><td>✅ Supported</td><td></td></tr>
<tr><td>Tags</td><td>✅ Supported</td><td>Multi-value text.</td></tr>
<tr><td>First Name, Middle Name, Last Name</td><td>➡️ Supported (1-Way)</td><td>Read only. Write the full Name instead.</td></tr>
<tr><td>Company</td><td>➡️ Supported (1-Way)</td><td>Read only. Links to the Companies table.</td></tr>
<tr><td>Company Name</td><td>➡️ Supported (1-Way)</td><td>Read only.</td></tr>
<tr><td>Date Last Contacted, Date Created, Date Modified, Interaction Count</td><td>➡️ Supported (1-Way)</td><td>Read only.</td></tr>
</tbody></table>

### Companies

<table><thead><tr><th width="260">Copper field</th><th width="220">Status</th><th>Notes</th></tr></thead><tbody>
<tr><td>Name</td><td>✅ Supported</td><td></td></tr>
<tr><td>Email Domain</td><td>✅ Supported</td><td></td></tr>
<tr><td>Details</td><td>✅ Supported</td><td>Multi-line text.</td></tr>
<tr><td>Assignee</td><td>✅ Supported</td><td>Links to the Users table.</td></tr>
<tr><td>Primary Contact</td><td>✅ Supported</td><td>Links to the People table.</td></tr>
<tr><td>Contact Type</td><td>✅ Supported</td><td>Links to the Contact Types table.</td></tr>
<tr><td>Phone Numbers, Socials, Websites</td><td>✅ Supported</td><td>JSON lists. See the formats above.</td></tr>
<tr><td>Street, City, State, Postal Code, Country</td><td>✅ Supported</td><td></td></tr>
<tr><td>Tags</td><td>✅ Supported</td><td>Multi-value text.</td></tr>
<tr><td>Date Created, Date Modified, Interaction Count</td><td>➡️ Supported (1-Way)</td><td>Read only.</td></tr>
</tbody></table>

### Opportunities

<table><thead><tr><th width="260">Copper field</th><th width="220">Status</th><th>Notes</th></tr></thead><tbody>
<tr><td>Name</td><td>✅ Supported</td><td></td></tr>
<tr><td>Details</td><td>✅ Supported</td><td>Multi-line text.</td></tr>
<tr><td>Assignee</td><td>✅ Supported</td><td>Links to the Users table.</td></tr>
<tr><td>Company</td><td>✅ Supported</td><td>Links to the Companies table.</td></tr>
<tr><td>Primary Contact</td><td>✅ Supported</td><td>Links to the People table.</td></tr>
<tr><td>Customer Source, Loss Reason</td><td>✅ Supported</td><td>Link to the Customer Sources and Loss Reasons tables.</td></tr>
<tr><td>Pipeline, Pipeline Stage</td><td>✅ Supported</td><td>Link to the Pipelines and Pipeline Stages tables. A new opportunity without them goes into Copper's default pipeline and its first stage.</td></tr>
<tr><td>Monetary Value</td><td>✅ Supported</td><td></td></tr>
<tr><td>Monetary Unit</td><td>✅ Supported</td><td>One of USD, EUR, GBP, JPY, CNY, INR, AUD, CAD, or CHF. Only kept when the opportunity has a Monetary Value.</td></tr>
<tr><td>Win Probability</td><td>✅ Supported</td><td></td></tr>
<tr><td>Status</td><td>✅ Supported</td><td>Open, Won, Lost, or Abandoned.</td></tr>
<tr><td>Priority</td><td>✅ Supported</td><td>None, Low, Medium, or High.</td></tr>
<tr><td>Close Date</td><td>✅ Supported</td><td>A date with no time.</td></tr>
<tr><td>Tags</td><td>✅ Supported</td><td>Multi-value text.</td></tr>
<tr><td>Company Name</td><td>➡️ Supported (1-Way)</td><td>Read only.</td></tr>
<tr><td>Date Created, Date Modified, Interaction Count</td><td>➡️ Supported (1-Way)</td><td>Read only.</td></tr>
</tbody></table>

### Leads

<table><thead><tr><th width="260">Copper field</th><th width="220">Status</th><th>Notes</th></tr></thead><tbody>
<tr><td>Name</td><td>✅ Supported</td><td>The lead's full name. Copper splits it into First Name and Last Name.</td></tr>
<tr><td>Prefix, Suffix, Title, Company Name</td><td>✅ Supported</td><td></td></tr>
<tr><td>Details</td><td>✅ Supported</td><td>Multi-line text.</td></tr>
<tr><td>Email</td><td>✅ Supported</td><td>A single JSON object rather than a list, for example <code>{"email": "ada@example.com", "category": "work"}</code>.</td></tr>
<tr><td>Phone Numbers, Socials, Websites</td><td>✅ Supported</td><td>JSON lists. See the formats above.</td></tr>
<tr><td>Street, City, State, Postal Code, Country</td><td>✅ Supported</td><td></td></tr>
<tr><td>Assignee</td><td>✅ Supported</td><td>Links to the Users table.</td></tr>
<tr><td>Customer Source</td><td>✅ Supported</td><td>Links to the Customer Sources table.</td></tr>
<tr><td>Status</td><td>✅ Supported</td><td>Links to the Lead Statuses table.</td></tr>
<tr><td>Monetary Value</td><td>✅ Supported</td><td></td></tr>
<tr><td>Monetary Unit</td><td>✅ Supported</td><td>Only kept when the lead has a Monetary Value.</td></tr>
<tr><td>Tags</td><td>✅ Supported</td><td>Multi-value text.</td></tr>
<tr><td>First Name, Last Name</td><td>➡️ Supported (1-Way)</td><td>Read only. Write the full Name instead.</td></tr>
<tr><td>Status Name</td><td>➡️ Supported (1-Way)</td><td>Read only.</td></tr>
<tr><td>Date Last Contacted, Date Created, Date Modified, Interaction Count</td><td>➡️ Supported (1-Way)</td><td>Read only.</td></tr>
</tbody></table>

### Tasks

<table><thead><tr><th width="260">Copper field</th><th width="220">Status</th><th>Notes</th></tr></thead><tbody>
<tr><td>Name</td><td>✅ Supported</td><td></td></tr>
<tr><td>Details</td><td>✅ Supported</td><td>Multi-line text.</td></tr>
<tr><td>Assignee</td><td>✅ Supported</td><td>Links to the Users table.</td></tr>
<tr><td>Related Resource</td><td>✅ Supported</td><td>The record the task belongs to. Set when the task is created, and fixed after that. See the format below.</td></tr>
<tr><td>Due Date, Reminder Date</td><td>✅ Supported</td><td></td></tr>
<tr><td>Priority</td><td>✅ Supported</td><td>None or High.</td></tr>
<tr><td>Status</td><td>✅ Supported</td><td>Open or Completed.</td></tr>
<tr><td>Tags</td><td>✅ Supported</td><td>Multi-value text.</td></tr>
<tr><td>Completed Date</td><td>➡️ Supported (1-Way)</td><td>Read only.</td></tr>
<tr><td>Date Created, Date Modified, Interaction Count</td><td>➡️ Supported (1-Way)</td><td>Read only.</td></tr>
</tbody></table>

Related Resource is a JSON object with the record's Copper ID and type, for example `{"id": 123, "type": "person"}`. The type is `person`, `company`, `opportunity`, or `lead`.

### Projects

<table><thead><tr><th width="260">Copper field</th><th width="220">Status</th><th>Notes</th></tr></thead><tbody>
<tr><td>Name</td><td>✅ Supported</td><td></td></tr>
<tr><td>Details</td><td>✅ Supported</td><td>Multi-line text.</td></tr>
<tr><td>Assignee</td><td>✅ Supported</td><td>Links to the Users table.</td></tr>
<tr><td>Related Resource</td><td>✅ Supported</td><td>Same format as on Tasks. Set when the project is created, and fixed after that.</td></tr>
<tr><td>Status</td><td>✅ Supported</td><td>Open or Completed.</td></tr>
<tr><td>Tags</td><td>✅ Supported</td><td>Multi-value text.</td></tr>
<tr><td>Date Created, Date Modified, Interaction Count</td><td>➡️ Supported (1-Way)</td><td>Read only.</td></tr>
</tbody></table>

### Activities

<table><thead><tr><th width="260">Copper field</th><th width="220">Status</th><th>Notes</th></tr></thead><tbody>
<tr><td>Type, Details, Parent, Activity Date, Old Value, New Value</td><td>➡️ Supported (1-Way)</td><td>Read only.</td></tr>
<tr><td>User</td><td>➡️ Supported (1-Way)</td><td>Read only. Links to the Users table.</td></tr>
</tbody></table>

### Custom fields

Copper custom fields sync on People, Companies, Opportunities, Leads, Tasks, and Projects. Each table gets the custom fields Copper makes available on that record type, and each one is a column named after the field.

<table><thead><tr><th width="260">Copper custom field type</th><th width="220">Status</th><th>Notes</th></tr></thead><tbody>
<tr><td>Text Field, Text Area</td><td>✅ Supported</td><td>Text Area is multi-line.</td></tr>
<tr><td>Number, Currency, Percentage</td><td>✅ Supported</td><td>A number column.</td></tr>
<tr><td>Checkbox</td><td>✅ Supported</td><td></td></tr>
<tr><td>Date</td><td>✅ Supported</td><td></td></tr>
<tr><td>URL</td><td>✅ Supported</td><td></td></tr>
<tr><td>Dropdown</td><td>✅ Supported</td><td>Synced by the option's name. Matching ignores capitalization and extra spaces. Add new options in Copper first, then refresh the schema in Whalesync.</td></tr>
<tr><td>Multi-Select</td><td>✅ Supported</td><td>Same as Dropdown, with multiple values.</td></tr>
<tr><td>Connect</td><td>➡️ Supported (1-Way)</td><td>Read only. Synced as JSON.</td></tr>
<tr><td>Computed fields</td><td>➡️ Supported (1-Way)</td><td>Read only.</td></tr>
</tbody></table>

Adding a custom field in Copper brings it in the next time you refresh the schema in Whalesync.

A Dropdown or Multi-Select option added in Copper after the last schema refresh shows up as a number, which is Copper's ID for the option. Writing its name from your other app is refused as an unknown option until you refresh the schema.

### Reference tables

Users, Pipelines, Pipeline Stages, Contact Types, Customer Sources, Loss Reasons, Lead Statuses, Tags, and Activity Types are your account's configuration. They are read only. They are here so the fields that point at them, like an opportunity's stage or a person's assignee, have something to link to.

To add a pipeline, stage, contact type, or any other configuration value, add it in Copper. It arrives as a new row in the matching table on the next scheduled poll.

## Things to Keep in Mind

* **The Copper connector is in beta.** If something does not work as described here, [let us know](../../resources/support/).
* **Changes in Copper arrive shortly after they happen.** Whalesync uses Copper webhooks for People, Companies, Opportunities, Leads, Tasks, Projects, and Activities. Copper sends each notification once and does not retry, so anything missed is picked up on the next scheduled poll. The reference tables are only refreshed on the scheduled poll, and a new custom field needs a schema refresh.
* **Turn on Leads in Copper to sync Leads.** Copper turns Leads off by default. Until Leads is on, the Leads table reports "Copper Leads aren't enabled on your account." Turn it on in Copper's Settings, then press **Retry Sync**. The other tables are not affected.
* **A person's Company is read only.** Copper ignores changes to it through its API. Copper links a person to a company through Related Items in Copper, or when the person is set as the company's Primary Contact.
* **First, Middle, and Last Name are read only.** Write the full Name, and Copper splits it.
* **Related Resource on a task or project is set when it is created, and fixed after that.** Copper refuses to change it later. Changing it in your other app is not synced.
* **Some fields cannot be emptied in Copper.** Clearing one of these cells in your other app has the following effect:
  * Task and project Assignee: Copper refuses the change, and it is reported as a sync issue.
  * Opportunity, task, and project Status, opportunity Pipeline Stage, and Monetary Unit on opportunities and leads: Copper has no empty value, so the existing value is kept.
  * Opportunity and task Priority: set to None.
  * Contact Type on people and companies: set to Copper's Uncategorized type.
  * Lead Status: set to the account's default lead status.
* **Monetary Unit is only kept when the record has a Monetary Value.** Copper ignores the currency on a record with no value.
* **New opportunities go into Copper's default pipeline** and its first stage, unless you set Pipeline and Pipeline Stage.
* **The Pipelines table can be empty.** Copper does not list its built-in default pipeline, so an opportunity in that pipeline has a Pipeline value with no matching row in the Pipelines table.
* **Copper refuses links to records that do not exist.** For example, an Assignee who was removed from Copper. The change is reported as a sync issue: "Copper rejected the update: a linked record (such as the assignee or primary contact) does not exist."
* **Whalesync reads up to 100,000 records per Copper table.** This is a limit of Copper's search API.
* **A record created in Copper can take a few seconds to appear in Copper's search,** so it may arrive in the following sync rather than the current one.
