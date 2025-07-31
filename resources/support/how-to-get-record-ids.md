---
description: How to find the Record ID for each connector
---

# How to get record IDs

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

