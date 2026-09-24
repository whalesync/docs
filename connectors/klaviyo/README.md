---
description: Two-way sync Klaviyo profiles and lists with Airtable, Notion, Google Sheets, and more.
cover: ../../.gitbook/assets/gitbook-cover_klaviyo.jpg
coverY: 0
---

# Klaviyo

## Klaviyo Connector Guide

This guide covers how to connect Whalesync to [Klaviyo](https://www.klaviyo.com), how your profiles and lists appear in Whalesync, and which fields sync.

In Whalesync terms, a Klaviyo **account** is the base you pick. It has three tables:

* **Profiles**, the people in the account. This is the main table and syncs both ways.
* **Lists**, your Klaviyo lists. You can create, rename, and delete lists from Whalesync.
* **Segments**, your Klaviyo segments. This table is read only.

Lists and Segments exist mainly as the targets of the Lists and Segments columns on Profiles, which link each profile to the lists and segments it belongs to.

### Connecting to Klaviyo

Whalesync connects by signing in to Klaviyo, or with a private API key you paste in. See [Authorize Klaviyo](authorize-klaviyo.md) for both.

1. In Whalesync, choose Klaviyo and sign in, or paste a private API key.
2. Pick the account to sync. The base is named after the Klaviyo account.
3. Pick the tables to sync: Profiles, Lists, Segments, or any of them.

### Syncing Data

Every profile in the account is a record in the Profiles table. Its columns are the fields Klaviyo gives every profile plus one column per custom property. See [Custom properties](#custom-properties).

A profile's lists are a link column to the Lists table. Adding a link in your other app adds the profile to that list in Klaviyo, and removing it takes the profile off the list. Adding a profile to a list does not subscribe it. Segment membership is also a link column, to the Segments table, and is read only because Klaviyo works out who is in a segment from the segment's definition.

## Supported Fields

### Profiles

<table><thead><tr><th width="260">Klaviyo field</th><th width="220">Status</th><th>Notes</th></tr></thead><tbody>
<tr><td>Email</td><td>✅ Supported</td><td>A profile needs an email, a phone number, or an external ID to be created.</td></tr>
<tr><td>Phone number</td><td>✅ Supported</td><td>International format, like <code>+12025550123</code>. Whalesync checks the format before writing and reports any other format as a sync issue for that profile.</td></tr>
<tr><td>External ID</td><td>✅ Supported</td><td>An ID from your own system.</td></tr>
<tr><td>First name, Last name, Organization, Title, Locale</td><td>✅ Supported</td><td>Text.</td></tr>
<tr><td>Image</td><td>✅ Supported</td><td>A URL. Whalesync does not upload the image.</td></tr>
<tr><td>Address line 1, Address line 2, City, State or region, Country, Postal code, Time zone</td><td>✅ Supported</td><td>The parts of the profile's location, one column each. Changing one leaves the others as they are.</td></tr>
<tr><td>Latitude, Longitude</td><td>✅ Supported</td><td>Numbers.</td></tr>
<tr><td>IP address</td><td>➡️ Supported (1-Way)</td><td>Read only.</td></tr>
<tr><td>Lists</td><td>✅ Supported</td><td>Links to the Lists table.</td></tr>
<tr><td>Segments</td><td>➡️ Supported (1-Way)</td><td>Read only. Links to the Segments table.</td></tr>
<tr><td>Email marketing consent, SMS marketing consent</td><td>➡️ Supported (1-Way)</td><td>Read only. One of <code>SUBSCRIBED</code>, <code>UNSUBSCRIBED</code>, or <code>NEVER_SUBSCRIBED</code>.</td></tr>
<tr><td>Email marketing consent at, SMS marketing consent at</td><td>➡️ Supported (1-Way)</td><td>Read only. When the consent was given or changed.</td></tr>
<tr><td>Email suppression reason</td><td>➡️ Supported (1-Way)</td><td>Read only. Why Klaviyo suppresses email to this profile, when it does.</td></tr>
<tr><td>Created, Updated, Last active</td><td>➡️ Supported (1-Way)</td><td>Read only. Last active is the time of the profile's most recent event in Klaviyo.</td></tr>
<tr><td>Historic customer lifetime value, Predicted customer lifetime value, Total customer lifetime value, Churn probability, Expected date of next order, Average order value, Number of orders, Predicted number of orders, Average days between orders</td><td>➡️ Supported (1-Way)</td><td>Read only. Klaviyo's predictive analytics, which it only fills in on paid accounts with order history. Whalesync only asks Klaviyo for them when at least one is mapped, because Klaviyo allows fewer requests a minute when they are included.</td></tr>
</tbody></table>

### Custom properties

Klaviyo has no schema for custom properties: a property exists on whichever profiles carry it. To find them, Whalesync reads the 1,000 most recently updated profiles and makes one column for each property key it sees. The column is named after the key and typed from the values seen.

<table><thead><tr><th width="260">Values seen</th><th width="220">Status</th><th>Notes</th></tr></thead><tbody>
<tr><td>Text</td><td>✅ Supported</td><td>A text column.</td></tr>
<tr><td>Numbers</td><td>✅ Supported</td><td>A number column.</td></tr>
<tr><td>True or false</td><td>✅ Supported</td><td>A checkbox.</td></tr>
<tr><td>Dates, or dates with a time</td><td>✅ Supported</td><td>A date column, for values like <code>2026-01-15</code> or <code>2026-01-15T09:30:00Z</code>. A mix of dates and other text is a text column.</td></tr>
<tr><td>Lists of text</td><td>✅ Supported</td><td>A multi-value text column.</td></tr>
<tr><td>Objects, or a mix of kinds</td><td>✅ Supported</td><td>A text column holding JSON. Whalesync reads the text as JSON when writing, so <code>{"plan": "pro"}</code> is sent to Klaviyo as an object and <code>7</code> as a number.</td></tr>
<tr><td>Keys starting with <code>$</code></td><td>➡️ Supported (1-Way)</td><td>Read only. Klaviyo adds and manages these itself, for example <code>$source</code> and <code>$consent</code>.</td></tr>
</tbody></table>

Clearing a cell removes the key from the profile in Klaviyo.

A property that only exists on older profiles does not get a column until one of those profiles changes and is among the 1,000 most recently updated. Setting the property on one profile in Klaviyo and refreshing the schema in Whalesync brings it in.

The type comes from the sample, so a value on an older profile that does not fit it reads as empty, for example text in a column typed as a number. Once profiles holding such values have been updated, refreshing the schema turns the column into text.

### Lists

<table><thead><tr><th width="260">Klaviyo field</th><th width="220">Status</th><th>Notes</th></tr></thead><tbody>
<tr><td>Name</td><td>✅ Supported</td><td>Required when creating a list from another app.</td></tr>
<tr><td>Opt-in process</td><td>➡️ Supported (1-Way)</td><td>Read only.</td></tr>
<tr><td>Created, Updated</td><td>➡️ Supported (1-Way)</td><td>Read only.</td></tr>
</tbody></table>

Deleting a list record deletes the list in Klaviyo. Klaviyo allows at most 150 new lists a day.

### Segments

<table><thead><tr><th width="260">Klaviyo field</th><th width="220">Status</th><th>Notes</th></tr></thead><tbody>
<tr><td>Name, Active, Processing, Starred, Created, Updated</td><td>➡️ Supported (1-Way)</td><td>Read only. Segments are created and edited in Klaviyo.</td></tr>
</tbody></table>

## Things to Keep in Mind

* **The Klaviyo connector is in beta.** If something does not work as described here, [let us know](../../resources/support/).
* **Profiles cannot be deleted from Whalesync.** Klaviyo only deletes a profile through a privacy erasure request, which Whalesync never sends. A delete from your other app is reported as a sync issue. Delete the profile in Klaviyo instead, or remove it from its lists.
* **Whalesync never subscribes or unsubscribes anyone, and never sends events or messages.** The consent columns are read only. Nothing Whalesync writes to Klaviyo sends a message to a profile.
* **A profile needs an email, a phone number, or an external ID to be created.** A record with none of them is reported as a sync issue.
* **Creating a profile whose email or phone number already exists in Klaviyo updates that profile.** No second profile is created, and the existing profile keeps the lists it was already on.
* **Klaviyo allows two profiles with the same email.** A change to an existing profile that gives it another profile's email is accepted, and both profiles stay. Whalesync does not merge them.
* **A profile deleted or merged in Klaviyo** drops out of the Profiles table on the next poll.
* **Klaviyo refuses a profile larger than 100KB**, custom properties included. Shorten or unmap the large fields to sync it.
* **Changes in Klaviyo arrive on the next poll.** Klaviyo only offers webhooks on its Advanced KDP plan, so Whalesync polls for changes instead.
* **Mapping the Lists or Segments column makes polls slower** in accounts with many lists or segments, because Whalesync asks Klaviyo about each one. Unmapped, they cost nothing.
* **Whalesync makes at most 10 requests a second to Klaviyo.** A large first sync takes a while.
* **Events, custom objects, catalogs, campaigns, and flows are not synced.** Segments sync as a read-only table.
