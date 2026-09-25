---
description: Two-way sync Mailchimp contacts, tags, and groups with Airtable, Notion, Google Sheets, and more.
cover: ../../.gitbook/assets/gitbook-cover_mailchimp.jpg
coverY: 0
---

# Mailchimp

## Mailchimp Connector Guide

This guide covers how to connect Whalesync to [Mailchimp](https://mailchimp.com), how your audiences appear in Whalesync, and which fields sync.

In Whalesync terms, a Mailchimp **audience** is the base you pick. It has four tables, plus one for each survey:

* **Contacts**, the people in the audience. This is the main table and syncs both ways.
* **Tags**, the audience's tags. You can create, rename, and delete tags from Whalesync.
* **Segments**, the audience's saved segments. This table is read only.
* **Campaigns**, the audience's campaigns, with their report numbers. This table is read only.
* **Survey: _name_**, one table for each survey on the audience, with one record per response. These tables are read only.

The Mailchimp connector is available on Whalesync's Starter plan and up.

### Connecting to Mailchimp

1. In Whalesync, choose Mailchimp and click **Authorize**, then sign in to Mailchimp.
2. Pick the audience to sync. The base is named after the audience.
3. Pick the tables to sync.

#### Using an API key

{% hint style="info" %}
You do not need an API key. Clicking **Authorize** and signing in to Mailchimp is enough. An API key is only an alternative for people who prefer not to sign in.
{% endhint %}

To find an API key in Mailchimp:

1. Click your profile icon and choose **Profile**.
2. Open the **Extras** menu and choose **API keys**.
3. Under **Your API Keys**, click **Create A Key**, name it, for example "Whalesync", and click **Generate Key**.
4. Click **Copy Key to Clipboard**. Mailchimp shows the key only once.

Then in Whalesync, choose Mailchimp, click **Use a api key instead**, paste the key, and click **Authorize**.

Mailchimp API keys created after June 22, 2026 expire a year after they are created. When a key expires, create a new one and reconnect Mailchimp with it.

### Syncing Data

Every contact in the audience is a record in the Contacts table. Its columns are the fields Mailchimp gives every contact, plus one column for each of the audience's merge fields, groups, and marketing permissions. See [Supported Fields](#supported-fields).

A contact's tags are a link column to the Tags table. Adding a link in your other app adds the tag to the contact in Mailchimp, and removing it takes the tag off.

Segment membership is on the Segments table: each segment has a Contacts column that links to the contacts in it. See [Segments](#segments).

### Subscription status

A contact added from Whalesync without a Status column is added as `transactional`. Mailchimp stores the contact but does not subscribe it to marketing email. To subscribe people, map the Status column and set it to `subscribed` for the people who agreed to receive email.

Status can be set to `subscribed`, `unsubscribed`, or `transactional`. Whalesync never sets a contact to `pending`, because Mailchimp sends a confirmation email to pending contacts. Nothing Whalesync writes to Mailchimp sends anyone an email.

Mailchimp does not let anyone resubscribe a contact who unsubscribed themselves. That person has to sign up again through a Mailchimp signup form.

### Deleting contacts

Deleting a record archives the contact in Mailchimp. Whalesync never deletes a contact permanently, and an archived contact keeps its history in Mailchimp.

### Real-time updates

Whalesync registers a webhook on each audience whose Contacts table you map, so a change to a contact in Mailchimp reaches your other apps quickly instead of waiting for the next poll.

Mailchimp sends no webhook for tags, segments, surveys, campaigns, or archived contacts. Changes to those arrive on the regular sync.

## Supported Fields

### Contacts

<table><thead><tr><th width="260">Mailchimp field</th><th width="220">Status</th><th>Notes</th></tr></thead><tbody>
<tr><td>Email</td><td>✅ Supported</td><td>Required when creating a contact from another app. Mailchimp keeps one contact per email.</td></tr>
<tr><td>Status</td><td>✅ Supported</td><td>Can be set to <code>subscribed</code>, <code>unsubscribed</code>, or <code>transactional</code>. See <a href="#subscription-status">Subscription status</a>.</td></tr>
<tr><td>Tags</td><td>✅ Supported</td><td>Links to the Tags table.</td></tr>
<tr><td>Merge fields</td><td>✅ Supported</td><td>One column per merge field. See <a href="#merge-fields">Merge fields</a>.</td></tr>
<tr><td>Groups</td><td>✅ Supported</td><td>One column per group category. See <a href="#groups">Groups</a>.</td></tr>
<tr><td>Marketing permissions</td><td>✅ Supported</td><td>A checkbox for each permission. See <a href="#marketing-permissions">Marketing permissions</a>.</td></tr>
<tr><td>Language</td><td>✅ Supported</td><td>Mailchimp cannot clear a contact's language.</td></tr>
<tr><td>VIP</td><td>✅ Supported</td><td>A checkbox.</td></tr>
<tr><td>Contact rating, Average open rate, Average click rate</td><td>➡️ Supported (1-Way)</td><td>Read only.</td></tr>
<tr><td>Signed up, Opted in, Last changed</td><td>➡️ Supported (1-Way)</td><td>Read only.</td></tr>
<tr><td>Source, Unsubscribe reason, Email client</td><td>➡️ Supported (1-Way)</td><td>Read only.</td></tr>
<tr><td>Country code, Time zone, Latitude, Longitude</td><td>➡️ Supported (1-Way)</td><td>Read only. The contact's location as Mailchimp records it.</td></tr>
</tbody></table>

### Merge fields

Each merge field on the audience is a column on Contacts, named after the field.

<table><thead><tr><th width="260">Merge field type</th><th width="220">Status</th><th>Notes</th></tr></thead><tbody>
<tr><td>Text</td><td>✅ Supported</td><td>Emoji are stored by Mailchimp as <code>?</code>.</td></tr>
<tr><td>Number</td><td>✅ Supported</td><td></td></tr>
<tr><td>Date</td><td>✅ Supported</td><td></td></tr>
<tr><td>Birthday</td><td>✅ Supported</td><td>A month and day, like <code>07/04</code>.</td></tr>
<tr><td>Address</td><td>✅ Supported</td><td>Six columns: street, line 2, city, state, postal code, and country. Mailchimp needs a street, a city, and a postal code.</td></tr>
<tr><td>Phone</td><td>✅ Supported</td><td></td></tr>
<tr><td>Website, Image URL</td><td>✅ Supported</td><td>A URL.</td></tr>
<tr><td>Radio buttons, Drop-down</td><td>✅ Supported</td><td>A single select whose options are the field's choices.</td></tr>
<tr><td>Zip code</td><td>✅ Supported</td><td>Five-digit US zip codes.</td></tr>
</tbody></table>

A new column created from Whalesync on the Contacts table becomes a new merge field in Mailchimp. Mailchimp limits how many merge fields an audience can have, and the limit depends on your Mailchimp plan.

### Groups

Each group category on the audience is a column on Contacts, named after the category.

<table><thead><tr><th width="260">Group category type</th><th width="220">Status</th><th>Notes</th></tr></thead><tbody>
<tr><td>Checkboxes, Hidden</td><td>✅ Supported</td><td>A multi-select of the category's groups.</td></tr>
<tr><td>Radio buttons, Drop-down</td><td>✅ Supported</td><td>A single select of the category's groups.</td></tr>
</tbody></table>

### Marketing permissions

On audiences with GDPR fields turned on, each marketing permission is a checkbox column on Contacts, named **Marketing permission:** followed by the permission's text. Mailchimp only lists permissions on contacts, so these columns appear once the audience has at least one contact.

* **Creating a record only records consent given.** When a new record matches a contact already in the audience, an unchecked box does not withdraw consent that contact gave.
* **A contact brought back from archived takes its consent from the record**, for the permission columns that are mapped. An unchecked box there withdraws consent.
* **Updating a record** gives or withdraws consent to match the box.

### Tags

<table><thead><tr><th width="260">Mailchimp field</th><th width="220">Status</th><th>Notes</th></tr></thead><tbody>
<tr><td>Name</td><td>✅ Supported</td><td>Required when creating a tag from another app.</td></tr>
<tr><td>Contacts, Created, Updated</td><td>➡️ Supported (1-Way)</td><td>Read only. Contacts is the number of contacts with the tag.</td></tr>
</tbody></table>

Deleting a tag record deletes the tag in Mailchimp.

### Segments

<table><thead><tr><th width="260">Mailchimp field</th><th width="220">Status</th><th>Notes</th></tr></thead><tbody>
<tr><td>Contacts</td><td>➡️ Supported (1-Way)</td><td>Read only. Links to the contacts in the segment. Only listed for audiences of up to 25,000 contacts.</td></tr>
<tr><td>Name, Contact count, Type, Created, Updated</td><td>➡️ Supported (1-Way)</td><td>Read only. Segments are created and edited in Mailchimp.</td></tr>
</tbody></table>

For an audience with more than 25,000 contacts, unmap the Contacts column to sync the segments without their members.

### Campaigns

<table><thead><tr><th width="260">Mailchimp field</th><th width="220">Status</th><th>Notes</th></tr></thead><tbody>
<tr><td>Name, Subject, Preview text, From name, Reply-to email, Status, Type, Created, Sent, Sent to, Emails sent, Recipients, Archive URL</td><td>➡️ Supported (1-Way)</td><td>Read only.</td></tr>
<tr><td>Opens, Unique opens, Open rate, Clicks, Unique clicks, Click rate</td><td>➡️ Supported (1-Way)</td><td>Read only. The campaign's report numbers. Empty until the campaign is sent.</td></tr>
</tbody></table>

### Surveys

Each survey on the audience is a table named **Survey:** followed by the survey's name. Each response is a record.

<table><thead><tr><th width="260">Mailchimp field</th><th width="220">Status</th><th>Notes</th></tr></thead><tbody>
<tr><td>Submitted</td><td>➡️ Supported (1-Way)</td><td>Read only.</td></tr>
<tr><td>Contact</td><td>➡️ Supported (1-Way)</td><td>Read only. Links to the contact who answered. Empty for anonymous responses.</td></tr>
<tr><td>Contact email, Contact name, New contact</td><td>➡️ Supported (1-Way)</td><td>Read only.</td></tr>
<tr><td>One column per question</td><td>➡️ Supported (1-Way)</td><td>Read only. Named after the question. Choice questions are selects, and rating questions are numbers.</td></tr>
</tbody></table>

A survey created after the sync is set up appears as a new table once you refresh the schema in Whalesync. When a survey is deleted in Mailchimp, remove its table from the sync.

## Things to Keep in Mind

* **The Mailchimp connector is in beta.** If something does not work as described here, [let us know](../../resources/support/).
* **A contact added without a Status column is not subscribed.** It is stored as `transactional`. Map Status to subscribe people.
* **Whalesync never sends anyone an email.** It never sets a contact to `pending`, and campaigns are read only.
* **Deleting a record archives the contact.** Whalesync never deletes a Mailchimp contact permanently.
* **Two records with the same email are refused.** Mailchimp keeps one contact per email, so the second record is reported as a sync issue.
* **Mailchimp cannot clear a contact's language.** Clearing it in your other app leaves the old value in Mailchimp, and that value syncs back.
* **Emoji in text fields are stored as `?`.** Mailchimp replaces them, and the `?` syncs back to your other app.
* **Tags, segments, surveys, campaigns, and archived contacts change on the regular sync only.** Mailchimp sends no webhook for them.
* **Mailchimp limits merge fields per audience.** The limit depends on your Mailchimp plan.
* **API keys created after June 22, 2026 expire after a year.** See [Using an API key](#using-an-api-key).

## Troubleshooting

### New contacts are not subscribed

A contact added without a Status column is added as `transactional`, which Mailchimp stores without subscribing. Map the Status column and set it to `subscribed` for the people who agreed to receive email. Contacts already added this way can be updated the same way.

### A contact cannot be resubscribed

Mailchimp does not let anyone resubscribe a contact who unsubscribed themselves. The person has to sign up again through a Mailchimp signup form.

### A record with a duplicate email is refused

Mailchimp keeps one contact per email, so Whalesync refuses a second record with an email another record in the sync already has. Remove the duplicate record, or change its email. If you deleted a contact's record and added it back as a new record, restore the original record instead.

### A deleted contact is still in Mailchimp

Deleting a record archives the contact. Archived contacts are not listed in the audience, but Mailchimp keeps them. Whalesync never deletes a contact permanently.

### Language or emoji change back after syncing

Mailchimp cannot clear a contact's language, and it stores emoji in text fields as `?`. In both cases the value Mailchimp keeps syncs back to your other app.

### Changes in Mailchimp take a while to show up

Contact changes arrive quickly through webhooks. Tags, segments, surveys, campaigns, and archived contacts change on the regular sync only, because Mailchimp sends no webhook for them.

### The Segments table reports the audience is too large

Segment members are only listed for audiences of up to 25,000 contacts. For a larger audience, unmap the Segments table's Contacts column. The segments still sync without their members.

### A survey response has no contact

Anonymous survey responses are not linked to a contact, so their Contact column is empty.

### A new survey is missing

Refresh the schema in Whalesync. The new survey then appears as a table you can add to the sync.

### A survey's table reports that the survey no longer exists

The survey was deleted in Mailchimp. Remove its table from the sync.

### Marketing permission columns are missing

Marketing permission columns only appear on audiences with GDPR fields turned on, and only once the audience has at least one contact. Turn on GDPR fields in Mailchimp, add a contact if the audience is empty, and refresh the schema in Whalesync.

### A new record did not withdraw a contact's consent

A new record only records consent given. When it matches a contact already in the audience, an unchecked box does not withdraw consent that contact gave. Update the record to withdraw consent. A contact brought back from archived is the exception: it takes its consent from the record, for the permission columns that are mapped.

### New columns cannot be created

Mailchimp limits how many merge fields an audience can have, and the limit depends on your Mailchimp plan. Map the column to an existing merge field instead, or remove merge fields you no longer use in Mailchimp.
