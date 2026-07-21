---
description: Sync Attio lists as their own tables in Whalesync
---

# Attio lists

### About Attio lists

[Attio lists](https://attio.com/help/reference/attio-101/attios-data-model/understanding-lists) let you organize a curated set of records — like the companies in your current fundraising pipeline or the people attending an event. Each entry in a list points at a record from the list's parent object (for example, a Company or a Person), and lists can have their own attributes such as a status or a rating that only exist on the list.

With Whalesync, each of your Attio lists shows up as its own table that you can map and sync, just like People or Companies.

### How to sync a list

When mapping tables, your lists appear alongside the standard Attio tables (People, Companies, Deals, etc.). Choose the list you'd like to sync and map its fields like any other table.

Each row in a list table is one **list entry**, and its fields come from three places:

1. **List attributes** — the fields that belong to the list itself (like a pipeline stage or rating). These sync normally, in both directions.
2. **The Parent Record field** — which record this entry points at (see below).
3. **The parent record's fields** — the fields of the Company, Person, or other record the entry points at, included on the row as **read-only** columns.

### The Parent Record field

Every list entry belongs to exactly one record in the list's parent object. Whalesync exposes this as a **Parent Record** field containing that record's Attio record ID.

A few things to know about this field:

* **It's required when creating an entry.** To add a new entry to a list through Whalesync, the Parent Record field must contain the Attio record ID of the record you want to add. If it's empty, the entry can't be created and Whalesync will show a sync error for that row.
* **It can't be changed after creation.** Attio doesn't allow an entry to be re-pointed at a different record. If you change the value in your other app, Whalesync won't push the change, and the field will revert to the true parent on the next sync.
* **It's a plain text field, not a linked record.** This is intentional — see the next section.

### Syncing a list without its parent table

Because the Parent Record field is a plain ID field rather than a linked record (foreign key), **you can sync a list all by itself** — you don't need to also add the People or Companies table to your sync just to make the list work.

You still get the parent record's data, though: Whalesync merges the parent object's fields into each list entry as read-only columns. So a "Fundraising pipeline" list of companies will show each company's name, domains, and other fields right on the list row, even if the Companies table isn't part of your sync.

{% hint style="info" %}
**Want to edit the parent record's fields too?** The parent fields on a list row are read-only. To make changes to the companies or people themselves, add the parent table (e.g. Companies) to your sync and edit the fields there.
{% endhint %}

### Things to keep in mind

{% hint style="info" %}
**Deleting a list entry doesn't delete the record.** If a row is deleted from a synced list table, Whalesync removes the entry from the list in Attio — the underlying company or person record is not touched.
{% endhint %}

{% hint style="warning" %}
**Parent record fields may lag slightly if the parent table isn't synced.** When you sync a list by itself, changes to the entries themselves sync in real time, but edits made directly to a parent record (like renaming a company) are picked up on the next scheduled polling round rather than instantly. Syncing the parent table alongside the list keeps those fields up to date in real time.
{% endhint %}

{% hint style="warning" %}
**Field name overlaps favor the list.** Both the list entry and its parent record have fields like "Created at" and "Created by". When names overlap, the column on the list table refers to the **entry** (e.g. when the record was added to the list), not the parent record.
{% endhint %}

### Limitations

* **Lists with multiple parent objects are read-only.** Almost all lists have a single parent object, but if a list accepts entries from more than one object type, Whalesync can sync it one-way (out of Attio) only.
* **Deleting a list breaks its table.** Lists are matched by their internal ID, so renaming a list in Attio is fine — the sync keeps working. But if a list is deleted in Attio, its table will show an error in Whalesync and you'll need to remove it from your mapping.
