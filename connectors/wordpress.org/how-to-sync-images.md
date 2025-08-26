---
description: A quick demo for syncing images into WordPress posts/pages
hidden: true
---

# How to sync images

{% embed url="https://www.loom.com/share/2cbc66c7701144c79866f6195e10fd30?sid=4f45a60f-52fd-49ce-875d-11220165dc9a" %}

**TL;DR**

1. Create a "Media" table in Airtable
2. In the Airtable table you want to have an image field (e.g. Posts), create a linked record field to the Media table
3. In your ACF custom image field name the field "image\_fk\_media"
4. Now you can map the linked record field in Airtable to the ACF custom field in WordPress

<figure><img src="../../.gitbook/assets/CleanShot 2023-06-21 at 18.41.49@2x.png" alt=""><figcaption></figcaption></figure>
