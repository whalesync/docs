---
description: Sync Attio notes as a table in Whalesync
---

# Attio notes

### About Attio notes

[Attio notes](https://attio.com/help/reference/attio-101/productivity/introduction-to-notes) are the written notes attached to a person, company, deal, or other record. Whalesync shows all the notes in your workspace as one **Notes** table, and it syncs in both directions. You can write and edit notes from your other app, and notes written in Attio show up on the other side.

### How to sync notes

When mapping tables, choose **Notes** alongside People, Companies, and your other Attio tables. Each row is one note, with these columns:

<table><thead><tr><th width="220">Column</th><th width="200">Status</th><th>Notes</th></tr></thead><tbody>
<tr><td>Title</td><td>✅ Supported</td><td></td></tr>
<tr><td>Content (Markdown)</td><td>✅ Supported</td><td>The body of the note, with formatting. See <a href="#formatting">Formatting</a>.</td></tr>
<tr><td>Content (plain text)</td><td>➡️ Supported (1-Way)</td><td>Read only. The same body without formatting, produced by Attio.</td></tr>
<tr><td>Parent object</td><td>✅ Supported</td><td>Which kind of record the note belongs to, such as <code>people</code> or <code>companies</code>. Set when the note is created. See below.</td></tr>
<tr><td>Parent record</td><td>✅ Supported</td><td>The ID of the record the note belongs to. Set when the note is created. See below.</td></tr>
<tr><td>Created at</td><td>➡️ Supported (1-Way)</td><td>Read only.</td></tr>
</tbody></table>

### The parent record

Every note belongs to exactly one record. Two columns say which one:

* **Parent object** is the object the record belongs to, written the way Attio names it in a URL: `people`, `companies`, `deals`, or the name of a custom object.
* **Parent record** is the Attio record ID of the record itself.

Both are required to create a note from your other app. If either is empty, the note cannot be created and Whalesync shows a sync issue for that row.

{% hint style="warning" %}
**A note cannot be moved to another record.** Attio does not allow the parent of a note to change after it is created. If you change Parent object or Parent record in your other app, Whalesync does not write the change back, and the columns return to the true parent on the next sync. To move a note, delete it and create a new one on the other record.
{% endhint %}

### Formatting

The note body is Markdown. Attio supports headings 1 through 3, bulleted and numbered lists, bold, italic, strikethrough, highlight, and links.

When Whalesync creates the Notes table in your other app, the Content columns are created as long text so line breaks survive. If you map to a table you created yourself, make the body column a long-text or rich-text field.

{% hint style="info" %}
**Images do not sync.** Attio does not let images in notes be added or read from outside Attio. A note that contains images syncs without them; the rest of the note is unaffected.
{% endhint %}

### Things to keep in mind

* **A new note in Attio may sync twice.** Attio creates the note the moment you click "new", before you type. The empty note syncs immediately, and the text you type follows a few minutes later. See [Things to keep in mind](README.md#things-to-keep-in-mind) on the Attio page.
* **Content (plain text) comes from Attio.** It is produced from the Markdown body and cannot be edited directly. Edit Content (Markdown) instead.

### Limitations

* **One table for the whole workspace.** Notes are not split by object. Filter on Parent object in your other app if you only want notes on, say, companies.
* **Images are not synced** in either direction.
