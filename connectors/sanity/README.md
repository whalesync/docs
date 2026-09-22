---
description: Two-way sync Sanity documents with Airtable, Notion, Google Sheets, and more.
cover: ../../.gitbook/assets/gitbook-cover_sanity.jpg
coverY: 0
---

# Sanity

## Sanity Connector Guide

This guide covers how to connect Whalesync to a [Sanity](https://www.sanity.io) project, what you need to do in Sanity first, and which fields sync.

In Whalesync terms, a Sanity **dataset** is the base you pick, each **document type** in your Studio schema is a table, and each **document** is a record.

### Before you connect: deploy your Studio schema

{% hint style="warning" %}
Whalesync reads your document types and fields from the Studio schema that is **deployed to your dataset**. Sanity's Content Lake has no built-in schema, so until you deploy one Whalesync cannot list any tables. A dataset without a deployed schema shows as **No schema deployed** in the dataset picker.
{% endhint %}

Deploying takes one command in your Sanity Studio project (Studio 3.88 or newer):

```bash
npx sanity schema deploy
```

Run it as a logged-in Studio developer, or with an Editor-role token in `SANITY_AUTH_TOKEN`. See Sanity's guide: [Schema deployment](https://www.sanity.io/docs/apis-and-sdks/schema-deployment).

Whenever you change your Studio schema, deploy it again and then refresh the schema in Whalesync so the new fields appear.

### Connecting to Sanity

Whalesync connects with a Sanity API token. See [Authorize Sanity](authorize-sanity.md) for the steps to create one.

1. In Whalesync, choose Sanity and paste the token.
2. If the token can access more than one project, enter the **Project ID** as well. Robot tokens are usually scoped to one project, so most people can leave it blank.
3. Pick the dataset to sync. Datasets without a deployed schema are listed but cannot be selected until you deploy one.

### Syncing Data

Every document type in the deployed schema is available as a table, including types that have no documents yet. Nested objects (for example an `seo` object with `metaTitle` and `metaDescription`) appear as separate fields named `seo / Meta title`, so each part can be mapped on its own.

## Supported Fields

Whalesync does not support every Sanity field type yet. If you need one that is missing, [reach out and let us know](../../resources/support/).

<table><thead><tr><th width="260">Sanity type</th><th width="220">Status</th><th>Notes</th></tr></thead><tbody>
<tr><td>String</td><td>✅ Supported</td><td>A string with an <code>options.list</code> is offered as a select, but Whalesync does not enforce the list.</td></tr>
<tr><td>Text</td><td>✅ Supported</td><td></td></tr>
<tr><td>Number</td><td>✅ Supported</td><td></td></tr>
<tr><td>Boolean</td><td>✅ Supported</td><td></td></tr>
<tr><td>Date</td><td>✅ Supported</td><td>Date only, no time.</td></tr>
<tr><td>Datetime</td><td>✅ Supported</td><td></td></tr>
<tr><td>URL</td><td>✅ Supported</td><td></td></tr>
<tr><td>Email</td><td>✅ Supported</td><td></td></tr>
<tr><td>Slug</td><td>✅ Supported</td><td>Synced as the slug text.</td></tr>
<tr><td>Reference (one target type)</td><td>✅ Supported</td><td>Synced as a link to the target document type. Weak references stay weak.</td></tr>
<tr><td>Array of references</td><td>✅ Supported</td><td>Synced as a multi-link field.</td></tr>
<tr><td>Array of strings</td><td>✅ Supported</td><td></td></tr>
<tr><td>Object</td><td>✅ Supported</td><td>Flattened into one field per sub-field, up to three levels deep. Deeper objects are synced as JSON, read only.</td></tr>
<tr><td>Reference (several target types)</td><td>➡️ Supported (1-Way)</td><td>Read only. Whalesync links point at one table, so the target document id is synced as text.</td></tr>
<tr><td>Portable Text (block content)</td><td>✅ Supported</td><td>Synced as HTML: headings, paragraphs, quotes, bold, italic, underline, strikethrough, inline code, links, nested lists, and line breaks. Images and code blocks sync when your schema allows them in the field; images pasted in from another app are uploaded to Sanity. Other custom blocks are not carried across an edit from the other app.</td></tr>
<tr><td>Image</td><td>✅ Supported</td><td>Read as the image's CDN URL. An image from another app is uploaded to your dataset; the same file is only stored once.</td></tr>
<tr><td>File</td><td>✅ Supported</td><td>Read as the file's CDN URL. A file from another app is uploaded to your dataset.</td></tr>
<tr><td>Geopoint</td><td>✅ Supported (as JSON)</td><td>Read only.</td></tr>
<tr><td>Array of objects or images</td><td>✅ Supported (as JSON)</td><td>Read only.</td></tr>
<tr><td>Fields marked <code>readOnly</code> in the Studio</td><td>➡️ Supported (1-Way)</td><td>Read only in Whalesync too.</td></tr>
<tr><td>Cross-dataset and global references</td><td>✅ Supported (as JSON)</td><td>Read only.</td></tr>
</tbody></table>

### Additional Fields

Whalesync adds fields that are not part of your Studio schema.

<table><thead><tr><th width="220">Field</th><th>Explanation</th><th width="120">Writable</th></tr></thead><tbody>
<tr><td>Record ID</td><td>The document's <code>_id</code>. When creating a document from another app, map this field to choose the id; it cannot be changed afterwards.</td><td>Once, on create</td></tr>
<tr><td>Draft</td><td>True when the document has an unpublished draft (or is only a draft). See <a href="#drafts-and-publishing">Drafts and publishing</a>.</td><td>Yes</td></tr>
<tr><td>Published</td><td>True when a published version of the document exists.</td><td>No</td></tr>
<tr><td>Created at</td><td>The document's <code>_createdAt</code>.</td><td>No</td></tr>
<tr><td>Updated at</td><td>The document's <code>_updatedAt</code>. When a draft exists, this is the draft's timestamp.</td><td>No</td></tr>
</tbody></table>

## Real-time updates

Whalesync registers a webhook in your Sanity project (named "Whalesync", visible under API → Webhooks in sanity.io/manage) so a change to a document in the Studio reaches your other apps within seconds instead of waiting for the next poll. It covers published documents and drafts. Deleting that webhook in Sanity turns real-time updates off until Whalesync re-registers it; turning the sync off removes it.

Deploying a new Studio schema does not trigger the webhook, so after `npx sanity schema deploy` refresh the schema in Whalesync.

## Drafts and publishing

In Sanity, a document with unpublished edits exists twice: the published version and a draft. Whalesync treats the pair as one record.

* **Reading:** Whalesync syncs the latest content. If a draft exists, you see the draft's values, and the **Draft** field is true.
* **Writing:** by default, a change Whalesync makes is applied to the published document **and** to the draft if there is one, so it goes live right away and is not undone the next time someone clicks Publish in the Studio.
* **Keeping a change unpublished:** map the **Draft** field and set it to true. Whalesync then writes only to the draft, creating one from the published document if needed. Nothing goes live until you publish.
* **Publishing from Whalesync:** set **Draft** to false on a record that has a draft. Whalesync publishes the draft (with your changes) and removes it, just like Publish in the Studio.
* **New records** are created as published documents, or as drafts when **Draft** is set to true.
* **Deleting** a record removes both the published document and its draft.

## Things to Keep in Mind

* **The deployed schema is the schema.** A field you add in Studio code does not exist for Whalesync until you run `npx sanity schema deploy` again and refresh the schema in Whalesync.
* **The token needs the Editor role.** A Viewer token can read your dataset but every create, update, and delete fails with a permissions error.
* **Sanity refuses to delete a referenced document.** If another document holds a strong reference to it, Sanity blocks the delete until the reference is removed or made weak.
* **Content Releases are not synced.** Documents that only exist inside a release are ignored.
* **Studio autosaves as you type,** so a document you are editing in the Studio updates its draft many times. Whalesync syncs the latest state.
* **Uploads are capped at 20 MB per file.** Larger files fail with a sync issue that names the file.
