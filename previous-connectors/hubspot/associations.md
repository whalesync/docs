---
description: How to sync HubSpot associations with Whalesync
---

{% hint style="warning" %}
**Archived:** This connector is no longer offered by Whalesync. Existing syncs will continue to run, but future improvements and support will be limited. See [Previous Connectors](../) for more details.
{% endhint %}

# Associations

#### TL;DR

* Whalesync supports two-way syncing HubSpot associations :tada:
* In order to two-way sync associations, you'll need to map the field correctly
* You can map associations with foreign keys (i.e. linked records)

#### **Compatible Fields**

Each app calls it something slightly different, but here are the fields that are compatible with HubSpot associations.

| App      | Name          |
| -------- | ------------- |
| HubSpot  | Association   |
| Postgres | Foreign Key   |
| Airtable | Linked Record |
| Notion   | Relation      |
| Webflow  | Reference     |

For a more detailed explanation of how these types of fields work, see :point\_down:

{% content-ref url="../../features/additional-features/reference-fields.md" %}
[reference-fields.md](../../features/additional-features/reference-fields.md)
{% endcontent-ref %}

#### **Caveats**

{% hint style="warning" %}
For now, Whalesync is not able to sync associations for custom objects.
{% endhint %}

