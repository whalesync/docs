---
cover: ../../.gitbook/assets/gitbook-cover_notion.jpg
coverY: 0
---

# Notion

## Notion Connector Guide

This guide provides an overview of how to connect Whalesync to Notion and answers common questions.

### Connecting to Notion

To connect Whalesync to Notion, you will need to authenticate using your Notion account. This process uses OAuth, which is a secure way to grant Whalesync access to your data without sharing your password.

When you authorize the connection, you will be taken to Notion's website. There, you can select which workspace and which specific pages or databases you want Whalesync to be able to access. Whalesync will only have permission to read and write to the pages and databases you explicitly select.

### Syncing Data

Whalesync enables two-way synchronization for most Notion fields. This means that if you update a record in Notion, the change will be reflected in the connected application, and if you update a record in the other application, the change will be reflected in Notion.

Some fields in Notion, such as `Created time` or `Last edited by`, are inherently read-only. Whalesync can read data from these fields and sync it to other apps, but cannot write new data into them. For a detailed list of what is supported, please see the "Supported Fields" section below.

#### Automatic Table and Field Creation

Whalesync can automatically create tables and fields in Notion to match the structure of the other app you're syncing with.

### Things to Keep in Mind

#### Relation fields

Whalesync supports relation fields out of the box! Note - Notion requires the "Two-way relation" option to be toggled in order for them to work.

![](<../../.gitbook/assets/Screenshot 2025-01-10 at 2.00.27 AM.png>)

#### Page Content Syncing

Whalesync can [sync the full content of your Notion pages](notion-page-sync.md). However, there are limitations for pages with very high complexity (i.e. a large number of nested blocks). If you have issues syncing complex pages, please contact support.

#### Rollup Fields

Syncing data from Notion's rollup fields is not yet supported.

#### Auto-Creating Databases

If you use Whalesync's "Auto-create tables" feature to create a new database in Notion, you will need to have specified a parent page when authenticating with Notion. This tells Whalesync where to place the new database.

### Synthetic Fields

Whalesync adds a few read-only fields to your Notion data to help manage the sync. These fields are not present in Notion itself but are available in Whalesync.

| Field Name       | Description                                                                                       | Writable |
| ---------------- | ------------------------------------------------------------------------------------------------- | -------- |
| Notion Record ID | The unique identifier for a page in Notion. This is used by Whalesync to track records.           | No       |
| Page Content     | The full content of a Notion page, including text, images, and other blocks, represented as HTML. | No       |
| Created At       | The timestamp of when a record was first created by the sync.                                     | No       |
| Updated At       | The timestamp of when a record was last updated by the sync.                                      | No       |

## Supported Fields

<table><thead><tr><th>Field</th><th>Status<select><option value="6c90dea3d4b34f409e73be79b7076c4a" label="✖️ Not Yet" color="blue"></option><option value="9e01356060cc4ea4988d69f72fe19d39" label="✅ Supported" color="blue"></option><option value="bd4357bee12749d0b80f7bc4a94ec3b5" label="➡️ Supported (1-Way)" color="blue"></option></select></th><th data-hidden></th></tr></thead><tbody><tr><td>🤖 AI field</td><td><span data-option="bd4357bee12749d0b80f7bc4a94ec3b5">➡️ Supported (1-Way)</span></td><td></td></tr><tr><td>☑️ Checkbox</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>🧑 Created by</td><td><span data-option="bd4357bee12749d0b80f7bc4a94ec3b5">➡️ Supported (1-Way)</span></td><td></td></tr><tr><td>🕠 Created time</td><td><span data-option="bd4357bee12749d0b80f7bc4a94ec3b5">➡️ Supported (1-Way)</span></td><td></td></tr><tr><td>📅 Date</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>✉️ Email</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>📂 Files &#x26; Media</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>📊 Formula</td><td><span data-option="bd4357bee12749d0b80f7bc4a94ec3b5">➡️ Supported (1-Way)</span></td><td></td></tr><tr><td>🧑 Last edited by</td><td><span data-option="bd4357bee12749d0b80f7bc4a94ec3b5">➡️ Supported (1-Way)</span></td><td></td></tr><tr><td>🕠 Last edited time</td><td><span data-option="bd4357bee12749d0b80f7bc4a94ec3b5">➡️ Supported (1-Way)</span></td><td></td></tr><tr><td>🏷️ Multi-Select</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>#️⃣ Number</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>📝 Page content</td><td><span data-option="bd4357bee12749d0b80f7bc4a94ec3b5">➡️ Supported (1-Way)</span></td><td></td></tr><tr><td>🫂 Person</td><td><span data-option="bd4357bee12749d0b80f7bc4a94ec3b5">➡️ Supported (1-Way)</span></td><td></td></tr><tr><td>📞 Phone</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>🖇️ Relation</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>🌀 Rollup</td><td><span data-option="6c90dea3d4b34f409e73be79b7076c4a">✖️ Not Yet</span></td><td></td></tr><tr><td>🔽 Select</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>🟢 Status</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>📝 Text</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>🔗 URL</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr></tbody></table>

## &#x20;<a href="#h_bccce14d8a" id="h_bccce14d8a"></a>



