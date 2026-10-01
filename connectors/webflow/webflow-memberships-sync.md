---
description: >-
  Webflow discontinued Memberships, later called User Accounts, on January 29,
  2026, so Whalesync can no longer sync Webflow users. What it means for you.
---

# Webflow Memberships sync

{% hint style="warning" %}
**Discontinued:** Webflow shut down User Accounts, previously called Memberships, on January 29, 2026. Whalesync can no longer sync Webflow users.
{% endhint %}

Webflow Memberships, later renamed User Accounts, let a Webflow site manage logged-in users. Whalesync synced those users through a **User accounts** table, so you could manage members from Airtable or another app.

Webflow [retired User Accounts](https://webflow.com/updates/deprecating-logic-and-user-accounts) on January 29, 2026, along with its API. Whalesync has no way to read or write Webflow users anymore.

## What this means for your syncs

* Syncs of your Webflow CMS collections are not affected.
* If a sync still has the Webflow **User accounts** table mapped, unmap it. Webflow no longer serves that data, so the table can't sync.

## Moving your members to another tool

Webflow recommends [Memberstack](https://www.memberstack.com) and [Outseta](https://www.outseta.com) as replacements. Whalesync has a [Memberstack connector](../memberstack/README.md), so if you move to Memberstack you can sync your members with Airtable, Notion, Google Sheets, and other apps.

To create new members from a sync, see [Creating users via Whalesync](../../features/additional-features/creating-users-via-whalesync.md).
