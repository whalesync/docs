---
description: >-
  Create Memberstack members through a sync from Airtable or another app. Covers
  write-once email fields and why these tables default to a 10-second sync
  delay.
---

# Creating users via Whalesync

<figure><img src="../../.gitbook/assets/create_user_in_Airtable.gif" alt=""><figcaption></figcaption></figure>

#### About creating users

Whalesync supports syncing with membership apps like Memberstack. When syncing with these apps we allow you to create users.

{% hint style="info" %}
Webflow Memberships (later User Accounts) was discontinued by Webflow on January 29, 2026, so Webflow users can no longer be created or synced. See [Webflow Memberships sync](../../connectors/webflow/webflow-memberships-sync.md).
{% endhint %}

For example, you can add a new user in Airtable and have that create a new member in Memberstack (:tada:).

#### "Write-once" fields

<figure><img src="../../.gitbook/assets/Screenshot 2024-09-20 at 3.02.21 AM.png" alt=""><figcaption></figcaption></figure>

* The email field for membership apps like Memberstack is what's called a "write-once" field.
* You can create new emails from both connected apps (e.g. Memberstack or Airtable)
* But once an email has been created, it cannot be updated

If you try to update a "write-once" field, you'll get an issue like this:

_"Please set the email address back from john2@gmail.com to john@gmail.com"_

#### Record sync delay

Write-once fields can normally cause issues if synced with an app like Airtable since Airtable saves every keystroke. The result can be sending a partial email to Memberstack (e.g. "john@gmai".)

To avoid this issue, we default to a record sync delay of 10 seconds for these types of tables. See the record sync delay page for more details:

{% content-ref url="delay-before-syncing.md" %}
[delay-before-syncing.md](delay-before-syncing.md)
{% endcontent-ref %}



