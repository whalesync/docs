---
cover: ../../.gitbook/assets/Supabase Gitbook Cover.jpg
coverY: 0
---

# Supabase

## Supabase Connector Guide

This guide provides an overview of how to connect Whalesync to Supabase and answers common questions.

### Connecting to Supabase

To connect your Supabase database to Whalesync, you'll need to authenticate using OAuth. This is a secure way to grant Whalesync access to your Supabase data without sharing your password. Whalesync will request access to your Supabase organization. After you select an organization, Whalesync will show you a list of your Supabase projects.

Once you select a project, Whalesync creates [a dedicated read-write service account](why-does-whalesync-create-a-database-user.md) in that Supabase project. This allows Whalesync to access your data to perform syncs. The service account is granted permissions on the `public` schema by default, which is where it can create and update records.

### Syncing Data

#### Automatic Table and Field Creation

Whalesync can automatically create tables and fields in Supabase to match the structure of the other app you're syncing with.

### Things to Keep in Mind <a href="#h_bccce14d8a" id="h_bccce14d8a"></a>

#### Primary Keys

For a table to be syncable, it must have a primary key that can uniquely identify each row. Whalesync will automatically detect the primary key on your table. If your table does not have a suitable primary key (e.g., an auto-incrementing number), Whalesync can add a synthetic primary key column to enable syncing.

**Primary keys must be auto-generated** (i.e. have a default value). To ensure data consistency, we require primary keys have default values. See [Adding default values to primary keys](adding-default-values-to-primary-keys.md).

#### Schema changes

{% hint style="danger" %}
**Renaming schema, tables, or columns will break Whalesync mappings**\
If you rename a table/column, you'll need to remap the impacted table/column in Whalesync.
{% endhint %}

#### Foreign Keys

**We support foreign keys (including two-way sync)!** In order to sync a foreign key _column_, you'll need to also sync the _table_ the column references.

#### **Permissions**

The service account created by Whalesync has read and write permissions on the `public` schema. If you want to sync tables in other schemas, you may need to grant permissions to the `whalesync_service_account` role in your Supabase project manually.

#### **Schema Changes**

After making schema changes in Supabase, like adding or removing a column, you should refresh the schema in Whalesync to see those changes reflected.

#### HTML and Markdown

{% hint style="info" %}
**Adding "\_html" to the end of a column name will preserve HTML**\
For example, "text\_html", will preserve that column's values as HTML while syncing.
{% endhint %}

See [HTML and Markdown Field Extensions](../../features/additional-features/html-and-markdown-field-extensions.md) for a way to sync HTML or Markdown into a rich text field.

#### Unsupported

Note that Whalesync does not yet support:

* Whitelisted IP addresses
* Custom SSL/TLS certificates

## Supported Schemas

In general, Whalesync supports syncing custom Supabase tables. We want to prevent interfering with internal Supabase data, so we don't support syncing Postgres schemas that Supabase uses for its own internal purposes.

<table><thead><tr><th>Schema</th><th>Status<select><option value="RQOyUDZdcogv" label="✅ Supported" color="blue"></option><option value="Rfk2xdxRw6D8" label="✖️ Not Supported" color="blue"></option></select></th></tr></thead><tbody><tr><td>public</td><td><span data-option="RQOyUDZdcogv">✅ Supported</span></td></tr><tr><td>Any other non-Supabase provided schema</td><td><span data-option="RQOyUDZdcogv">✅ Supported</span></td></tr><tr><td>auth</td><td><span data-option="Rfk2xdxRw6D8">✖️ Not Supported</span></td></tr><tr><td>extensions</td><td><span data-option="Rfk2xdxRw6D8">✖️ Not Supported</span></td></tr><tr><td>graphql</td><td><span data-option="Rfk2xdxRw6D8">✖️ Not Supported</span></td></tr><tr><td>graphql_public</td><td><span data-option="Rfk2xdxRw6D8">✖️ Not Supported</span></td></tr><tr><td>pgbouncer</td><td><span data-option="Rfk2xdxRw6D8">✖️ Not Supported</span></td></tr><tr><td>pgsodium</td><td><span data-option="Rfk2xdxRw6D8">✖️ Not Supported</span></td></tr><tr><td>pgsodium_masks</td><td><span data-option="Rfk2xdxRw6D8">✖️ Not Supported</span></td></tr><tr><td>realtime</td><td><span data-option="Rfk2xdxRw6D8">✖️ Not Supported</span></td></tr><tr><td>storage</td><td><span data-option="Rfk2xdxRw6D8">✖️ Not Supported</span></td></tr><tr><td>vault</td><td><span data-option="Rfk2xdxRw6D8">✖️ Not Supported</span></td></tr></tbody></table>



## Supported Fields

<table><thead><tr><th>Field</th><th>Status<select><option value="6c90dea3d4b34f409e73be79b7076c4a" label="✖️ Not Yet" color="blue"></option><option value="9e01356060cc4ea4988d69f72fe19d39" label="✅ Supported" color="blue"></option><option value="bd4357bee12749d0b80f7bc4a94ec3b5" label="➡️ Supported (1-Way)" color="blue"></option></select></th><th data-hidden></th></tr></thead><tbody><tr><td>🏷️ Array</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>#️⃣ Bigint</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>📝 Bit</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>☑️ Boolean</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>📝 Composite</td><td><span data-option="bd4357bee12749d0b80f7bc4a94ec3b5">➡️ Supported (1-Way)</span></td><td></td></tr><tr><td>📅 Date</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>📅 Daterange</td><td><span data-option="bd4357bee12749d0b80f7bc4a94ec3b5">➡️ Supported (1-Way)</span></td><td></td></tr><tr><td>🔗 Domain</td><td><span data-option="bd4357bee12749d0b80f7bc4a94ec3b5">➡️ Supported (1-Way)</span></td><td></td></tr><tr><td>🔘 Enum</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>🖇️ Foreign Key</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>#️⃣ Geometric</td><td><span data-option="bd4357bee12749d0b80f7bc4a94ec3b5">➡️ Supported (1-Way)</span></td><td></td></tr><tr><td>#️⃣ Integer</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>#️⃣ Interval</td><td><span data-option="bd4357bee12749d0b80f7bc4a94ec3b5">➡️ Supported (1-Way)</span></td><td></td></tr><tr><td>🗃️Json</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>💱 Money</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>📝 Network</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>#️⃣ Numeric</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>⏱️ Range</td><td><span data-option="bd4357bee12749d0b80f7bc4a94ec3b5">➡️ Supported (1-Way)</span></td><td></td></tr><tr><td>📝 Text</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>📝 Textsearch</td><td><span data-option="bd4357bee12749d0b80f7bc4a94ec3b5">➡️ Supported (1-Way)</span></td><td></td></tr><tr><td>⏱️ Time</td><td><span data-option="bd4357bee12749d0b80f7bc4a94ec3b5">➡️ Supported (1-Way)</span></td><td></td></tr><tr><td>⏱️ Timestamp</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>🆔 Uuid</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>🗃️ XML</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>🔦 Binary</td><td><span data-option="6c90dea3d4b34f409e73be79b7076c4a">✖️ Not Yet</span></td><td></td></tr></tbody></table>

## &#x20;<a href="#h_bccce14d8a" id="h_bccce14d8a"></a>
