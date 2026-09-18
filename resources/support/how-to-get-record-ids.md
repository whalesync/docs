---
description: How to find the Record ID for each connector
---

# How to get record IDs

{% hint style="info" %}
Inside Whalesync you do not need any of these steps. Every table already has a built-in "\<App> Record ID" field in the field mapper. The steps below are for viewing the ID inside the app itself.
{% endhint %}

### Airtable

1. Add a Formula field using the formula: `RECORD_ID()`
2. View the IDs in the newly created field

<figure><img src="../../.gitbook/assets/Formula Field.png" alt=""><figcaption></figcaption></figure>

### Webflow

1. Open up an item in the CMS
2. Scroll to the bottom of the item
3. Copy the ID

<figure><img src="../../.gitbook/assets/Webflow Item ID.png" alt=""><figcaption></figcaption></figure>

### Postgres

1. Whalesync requires a generated ID to sync with Postgres
2. This generated ID is your record ID

<figure><img src="../../.gitbook/assets/Supabase ID.png" alt=""><figcaption></figcaption></figure>

### Notion

1. Add a Formula field using the formula: `ID()`
2. View the IDs in the newly created field

<figure><img src="../../.gitbook/assets/Notion Record ID.png" alt=""><figcaption></figcaption></figure>

### Bubble

* Bubble does not expose record ID in their data viewer

### What to do with these IDs

Map each app's built-in Record ID field into a text field on the other side of your sync. This gives every record a durable pointer to its counterpart for re-matching and debugging. See [store-record-ids-on-both-sides.md](../../features/store-record-ids-on-both-sides.md "mention").
