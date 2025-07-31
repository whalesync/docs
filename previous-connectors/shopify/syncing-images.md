---
description: How to sync Shopify product images
---

# Syncing images

{% hint style="info" %}
We suggest using our [Shopify Template Pack](https://www.whalesync.com/template-packs/shopify) which has the correct tables/fields pre-created
{% endhint %}

**TL;DR**

* In order to sync product images, you'll need to create a Media table that is separate from your Products table
* You can then link a Product to Media using a linked record (aka foreign key) field

**Detailed Explanation**

<figure><img src="../../.gitbook/assets/Shopify Media.png" alt=""><figcaption></figcaption></figure>

1. In Airtable (or your other connected app), create a table called "Media"
2.  In the Media table, include at least two fields: 1) Shopify Product ID 2) Image



    <figure><img src="../../.gitbook/assets/CleanShot 2023-07-01 at 18.35.07.png" alt=""><figcaption></figcaption></figure>
3.  In the Products table, include a linked record from Product to Media



    <figure><img src="../../.gitbook/assets/CleanShot 2023-07-01 at 18.36.43.png" alt=""><figcaption></figcaption></figure>

