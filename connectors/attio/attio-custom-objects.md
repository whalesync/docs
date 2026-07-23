---
description: Sync your Attio custom objects just like People and Companies
---

# Attio custom objects

### About custom objects

[Custom objects](https://attio.com/help/reference/managing-your-data/objects/create-and-manage-custom-objects) let you track things in Attio beyond the built-in objects — think Projects, Invoices, Properties, or anything else specific to your business.

Whalesync syncs custom objects exactly like the standard Attio objects (People, Companies, Deals). Anything you can do with a built-in object, you can do with a custom one.

### How to sync a custom object

When mapping tables, your custom objects appear in the dropdown list of tables alongside the standard Attio tables. Choose the custom object you'd like to sync and map its fields like any other table.

### Foreign keys

Custom objects fully support reference fields (foreign keys), in both directions:

* Other tables can reference your custom object — for example, a Deals table with a link to your custom "Properties" object.
* Your custom object can reference other tables — for example, a custom "Invoices" object with a link to Companies.

For more on how reference fields work across apps, see :point\_down:

{% content-ref url="../../features/additional-features/reference-fields.md" %}
[reference-fields.md](../../features/additional-features/reference-fields.md)
{% endcontent-ref %}

### Syncing via a list

Custom objects also work with [Attio lists](attio-lists.md). If you have a list whose parent object is a custom object — say, a "Renewals pipeline" list of your custom "Contracts" records — you can sync that list just like a list of Companies or People, including creating new entries from your other app.

### Things to keep in mind

{% hint style="warning" %}
**Record labels come from the "name" attribute.** Whalesync uses an attribute called "name", if present, to label records in the UI. If your custom object doesn't have a "name" attribute, records will be labeled with their unique identifier instead. This only affects how records are displayed in Whalesync — your data syncs the same either way.
{% endhint %}
