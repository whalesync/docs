---
description: >-
  Two-way sync HubSpot associations by mapping them to Airtable linked records,
  Notion relations, Postgres foreign keys, or Webflow reference fields.
---

# Associations

#### TL;DR

* Whalesync supports two-way syncing HubSpot associations :tada:
* In order to two-way sync associations, you'll need to map the field correctly
* You can map associations with foreign keys (i.e. linked records)
* Associations to custom objects sync too. Map them from the standard object's table, such as Contacts or Deals

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
