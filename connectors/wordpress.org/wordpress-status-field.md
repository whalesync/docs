---
description: Control the status of a WordPress post via a field in other apps
---

# WordPress status field

### About WordPress Status field

* WordPress lets you control the status of a post by marking it as either Published, Draft, or Pending.
* With our WordPress Status field sync, you can now control that state from apps like Airtable or Notion.
* For example, if you manage your blog content in Notion, you can now control whether those blog posts are live or in draft from within Notion.

{% hint style="info" %}
If you want to choose when a row in Airtable or Notion is synced to Wordpress, you can also use the [selective-sync.md](../../features/additional-features/selective-sync.md "mention") feature.
{% endhint %}

### How to set up the WordPress Status field

1. Add a single-select field to your Airtable or Notion table and title it "Status"
2. Make sure it has _exactly_ these three options:
   1. "publish"
   2. "draft"
   3. "pending"
3. In Whalesync, map that field to WordPress' "Status" field

![](<../../.gitbook/assets/CleanShot 2023-05-24 at 18.23.23.png>)

{% hint style="info" %}
Airtable lets you set a default value for single select fields so you can, for example, set a default value of 'Draft'
{% endhint %}



