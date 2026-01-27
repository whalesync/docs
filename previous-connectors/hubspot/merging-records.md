---
description: >-
  Merging records in HubSpot will cause records to be deleted in your synced
  spreadsheet
---

{% hint style="warning" %}
**Archived:** This connector is no longer offered by Whalesync. Existing syncs will continue to run, but future improvements and support will be limited. See [Previous Connectors](../) for more details.
{% endhint %}

# Merging records

In HubSpot, you have the ability to merge duplicate records.

<figure><img src="../../.gitbook/assets/hubspot-merge.png" alt=""><figcaption><p>Screenshot of merging records in HubSpot</p></figcaption></figure>

From Whalesync's perspective, here's what happens when merging records:

* HubSpot deletes both of the original records
* HubSpot creates a new record with the properties of the two original records merged in

If you're syncing records to a spreadsheet like Airtable, Google Sheets, or Notion, the following will happen:

* Whalesync will delete both of the original records
* Whalesync will create a new record

If you're using the merge record feature of HubSpot, **please take care if you have non-synced fields** in your spreadsheet, since the **original spreadsheet records will be deleted**.
