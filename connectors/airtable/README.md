---
cover: ../../.gitbook/assets/gitbook-cover_airtable.jpg
coverY: 0
---

# Airtable

## Airtable Connector Guide

This guide provides an overview of how to connect Whalesync to Airtable and answers common questions.

### Connecting to Airtable

To connect your Airtable account to Whalesync, you'll need to authenticate using OAuth. This is a secure way to grant Whalesync access to your Airtable data without sharing your password.

When you connect, Airtable will ask you to authorize Whalesync to perform specific actions. Here’s what we ask for and why:

* `data.records:read` and `data.records:write`: Allows Whalesync to read and write records (rows) in your tables to keep them in sync.
* `schema.bases:read` and `schema.bases:write`: Allows Whalesync to understand the structure of your bases, tables, and fields. We also use this to automatically create tables and fields in Airtable if you want us to.
* `data.recordComments:read` and `data.recordComments:write` : Allows Whalesync to read and write comments in records
* `webhook:manage`: Allows Whalesync to set up webhooks, which notify us instantly when data changes in Airtable, enabling real-time syncing.

You will need to grant access to the specific Bases you want to sync with Whalesync.

### Syncing Data

#### Bases and Tables

In Airtable, your data is organized into **Bases**, which are like databases or spreadsheets. Each base contains **Tables**, and tables contain your data in records (rows) and fields (columns). Whalesync uses the same terminology.

#### Syncing Specific Views

One powerful feature of our Airtable connector is the ability to sync a specific **View**. A View in Airtable lets you filter and sort your records. By choosing a view to sync in Whalesync, you can control exactly which records are included in your sync.

For example, you could create a view in Airtable called "Ready to Publish" that only shows records where a "Status" field is set to "Published". By syncing this view, you ensure only those specific records are synced by Whalesync.

If you don't select a view, Whalesync will sync **all records** in the table.

Note - you can't use Airtable view sync and two-way sync at the same time. See below for details:

{% content-ref url="airtable-view-sync.md" %}
[airtable-view-sync.md](airtable-view-sync.md)
{% endcontent-ref %}

#### Automatic Table and Field Creation

Whalesync can automatically create tables and fields in Airtable to match the structure of the other app you're syncing with.

### Important Considerations

#### API Quotas

Airtable has API request limits, especially on their Free and Team plans. If you have a large number of records or your data changes very frequently, you might hit these limits. We recommend considering Airtable's Business or Enterprise plans for heavy usage to avoid sync interruptions.

#### Attachments

Please be aware that when syncing attachment fields, the file names of your attachments may change.



## Supported Fields

<table><thead><tr><th>Field</th><th>Status<select><option value="6c90dea3d4b34f409e73be79b7076c4a" label="✖️ Not Yet" color="blue"></option><option value="9e01356060cc4ea4988d69f72fe19d39" label="✅ Supported" color="blue"></option><option value="bd4357bee12749d0b80f7bc4a94ec3b5" label="➡️ Supported (1-Way)" color="blue"></option></select></th><th data-hidden></th></tr></thead><tbody><tr><td>🤖 AI field</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>📂 Attachment (Image)</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>#️⃣ Autonumber</td><td><span data-option="bd4357bee12749d0b80f7bc4a94ec3b5">➡️ Supported (1-Way)</span></td><td></td></tr><tr><td>📇 Barcode</td><td><span data-option="bd4357bee12749d0b80f7bc4a94ec3b5">➡️ Supported (1-Way)</span></td><td></td></tr><tr><td>🔘 Button</td><td><span data-option="6c90dea3d4b34f409e73be79b7076c4a">✖️ Not Yet</span></td><td></td></tr><tr><td>☑️ Checkbox</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>🫂 Collaborator</td><td><span data-option="bd4357bee12749d0b80f7bc4a94ec3b5">➡️ Supported (1-Way)</span></td><td></td></tr><tr><td>🔢 Count</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>🧑 Created by</td><td><span data-option="bd4357bee12749d0b80f7bc4a94ec3b5">➡️ Supported (1-Way)</span></td><td></td></tr><tr><td>💱 Currency</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>📅 Date</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>⏱️ Duration</td><td><span data-option="bd4357bee12749d0b80f7bc4a94ec3b5">➡️ Supported (1-Way)</span></td><td></td></tr><tr><td>✉️ Email</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>📊 Formula</td><td><span data-option="bd4357bee12749d0b80f7bc4a94ec3b5">➡️ Supported (1-Way)</span></td><td></td></tr><tr><td>🖇️ Linked records</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>🖇️ Linked records - multiple</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>📝 Long text</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>📰 Long text - rich text</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>👀 Lookup</td><td><span data-option="bd4357bee12749d0b80f7bc4a94ec3b5">➡️ Supported (1-Way)</span></td><td></td></tr><tr><td>🏷️ Multi-select</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>#️⃣ Number</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>➗ Percent</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>📞 Phone number</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>⭐ Rating</td><td><span data-option="bd4357bee12749d0b80f7bc4a94ec3b5">➡️ Supported (1-Way)</span></td><td></td></tr><tr><td>🆔 Record ID</td><td><span data-option="bd4357bee12749d0b80f7bc4a94ec3b5">➡️ Supported (1-Way)</span></td><td></td></tr><tr><td>🌀 Rollup</td><td><span data-option="bd4357bee12749d0b80f7bc4a94ec3b5">➡️ Supported (1-Way)</span></td><td></td></tr><tr><td>🔽 Single select</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>📝 Single line text</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>🔗 URL</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr></tbody></table>

### Synthetic Fields

Whalesync adds some special fields to your Airtable tables. These fields are not visible in Airtable but are available to map in your sync.

| Field Name            | Explanation                                             | Writable |
| --------------------- | ------------------------------------------------------- | -------- |
| Airtable Record ID    | The unique identifier for a record in Airtable.         | No       |
| Airtable Created Time | The timestamp of when a record was created in Airtable. | No       |

###
