---
description: >-
  Two-way sync Framer CMS collections with Airtable, Notion, Google Sheets, and
  more. Covers the project URL, Server API keys, supported fields, and slugs.
---

# Framer

## Framer Connector Guide

This guide covers how to connect Whalesync to a [Framer](https://www.framer.com) project, which fields sync, and a few things to know before you start.

{% hint style="info" %}
The Framer connector is in beta.
{% endhint %}

In Whalesync terms, a Framer **project** (your site) is the base, and each connection reaches one project. Each **CMS collection** is a table, and each **CMS item** is a record. Whalesync creates, updates, and deletes items in both directions.

### Connecting to Framer

Whalesync connects with two things: the **Framer project URL** and a **Framer Server API key** from the same project. Sign in with Framer is not available. See [Authorize Framer](authorize-framer.md) for the steps.

#### How to get your project URL

Open the project in Framer and copy the URL from your browser's address bar. It looks like `https://framer.com/projects/My-Site--aBcD1234`.

#### How to get your API key

In the project, open **Site Settings** and go to the **General** section to generate an API key. Keys are bound to one project, so the key must come from the same project as the URL. Framer's Server API is in beta. See Framer's guide: [Server API quick start](https://www.framer.com/developers/server-api-quick-start).

#### Connect

1. In Whalesync, choose Framer.
2. Paste the URL into **Framer project URL** and the key into **Framer Server API key**, then click **Authorize**. Whalesync checks the URL and key with Framer before it saves the connection.
3. Pick the project. A connection reaches one project, so there is one to pick.
4. Pick the collections to sync.

To sync another site, add another connection with that site's URL and API key.

## Supported Fields

Whalesync does not support every Framer field type yet. If you need one that is missing, [reach out and let us know](../../resources/support/).

<table><thead><tr><th width="260">Framer field</th><th width="220">Status</th><th>Notes</th></tr></thead><tbody>
<tr><td>Plain Text</td><td>✅ Supported</td><td></td></tr>
<tr><td>Formatted Text</td><td>✅ Supported</td><td>Synced as HTML. Apps with rich text, such as Airtable, show it as rich text.</td></tr>
<tr><td>Number</td><td>✅ Supported</td><td>Decimals are kept.</td></tr>
<tr><td>Toggle</td><td>✅ Supported</td><td></td></tr>
<tr><td>Date</td><td>✅ Supported</td><td>Date and time.</td></tr>
<tr><td>Link</td><td>✅ Supported</td><td></td></tr>
<tr><td>Color</td><td>✅ Supported</td><td>Synced as text, for example <code>#09F</code> or <code>rgba(12, 34, 56, 0.5)</code>.</td></tr>
<tr><td>Option</td><td>✅ Supported</td><td>Synced as the option's name. Values from your other app must match one of the field's options.</td></tr>
<tr><td>Image</td><td>✅ Supported</td><td>Synced as the image URL. Maps to an Airtable attachment field. See <a href="#images-and-files">Images and files</a>.</td></tr>
<tr><td>File</td><td>✅ Supported</td><td>Synced as the file URL.</td></tr>
<tr><td>Gallery</td><td>✅ Supported</td><td>Synced as a list of image URLs. Maps to an Airtable attachment field that holds several images.</td></tr>
<tr><td>Reference</td><td>✅ Supported</td><td>Synced as a link to a record in the referenced collection. Sync that collection too.</td></tr>
<tr><td>Multi Reference</td><td>✅ Supported</td><td>Synced as a multi-link field.</td></tr>
<tr><td>Slug</td><td>✅ Supported</td><td>See <a href="#slugs">Slugs</a>.</td></tr>
<tr><td>Draft</td><td>✅ Supported</td><td>Framer's draft setting. Draft items are not published to the live site.</td></tr>
<tr><td>Divider</td><td>✖️ Not supported</td><td>Layout only. It holds no data.</td></tr>
</tbody></table>

### Additional Fields

Whalesync adds a field that is not part of your collection.

<table><thead><tr><th width="220">Field</th><th>Explanation</th><th width="120">Writable</th></tr></thead><tbody>
<tr><td>Framer Record ID</td><td>The item's id in Framer.</td><td>No</td></tr>
</tbody></table>

## Images and files

Framer copies every image and file Whalesync sends it to Framer's own storage (`framerusercontent.com`). After the first sync, the URL in Framer is different from the original URL. This is expected and does not cause repeated updates.

Images from Airtable attachment fields arrive in Framer, and Framer images and galleries arrive in Airtable as attachments.

## Slugs

Every Framer item needs a unique slug. Map a field to **Slug** to control it.

If a new item arrives without a slug, Whalesync builds one from the field your collection bases its slugs on, usually Title, the same way Framer's editor does. For example, `Hello World` becomes `hello-world`. If that slug is already taken, Whalesync adds `-2`, `-3`, and so on.

If there is nothing to build a slug from, the record shows a sync issue asking you to fill in that field or map a field to Slug. Framer refuses a slug that is already used in the collection.

## Things to Keep in Mind

* **The Framer connector is in beta.** If something does not work as described, [let us know](../../resources/support/).
* **Publish in Framer to see changes on your live site.** Whalesync saves changes to your Framer CMS right away, but your published site only updates when you publish it in Framer. Whalesync does not publish for you, because publishing would also ship any other unpublished edits.
* **Changes in Framer are picked up on a schedule.** Framer does not notify Whalesync about changes, so Whalesync checks your collections regularly.
* **Create collections and fields in Framer.** Whalesync cannot create Framer collections or fields. Add them in Framer, then refresh the schema in Whalesync.
* **Collections can have up to 5,000 items.** Framer only returns a collection all at once, so Whalesync syncs collections of up to 5,000 items. A larger collection shows a sync issue with the number of items it has. [Contact support](../../resources/support/) to raise the limit.
* **Option values must match.** Framer refuses a value that is not one of the field's options, and the record shows a sync issue.
* **Sync referenced collections too.** A Reference field links to records in another collection, so that collection has to be part of the sync. Whalesync asks for it when you map the field.
