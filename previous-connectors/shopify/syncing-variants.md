---
description: How to sync Shopify product variants
---

# Syncing variants

{% hint style="info" %}
We suggest using our [Shopify Template Pack](https://www.whalesync.com/template-packs/shopify) which has the correct tables/fields pre-created
{% endhint %}

## **Summary**

* In order to sync product variants, you'll need to create a Variants table and an Options table that are separate from your Products table
* You can then link a Product to those Options and Variants using a linked record (aka foreign key) field
* If you want to create new Variants from Airtable, you must create them by adding _Options_ (just like you would in Shopify).

### **Detailed Explanation**

<figure><img src="../../.gitbook/assets/Variants Mapping.png" alt=""><figcaption></figcaption></figure>

1. In Airtable (or your other connected app), create a table called "Variants" and a table called "Options"
2. In your Products table, created linked records (aka foreign keys) from Product to Options and Variants

{% hint style="info" %}
If you want to create new Variants from Airtable, you must create them by adding _Options_ (just like you would in Shopify). Editing the Variants table directly will not work.
{% endhint %}

## Limitations

{% hint style="warning" %}
Due to the Shopify API, Whalesync only supports up to 100 Variants. Syncing more than 100 Variants could have unexpected behavior.
{% endhint %}
