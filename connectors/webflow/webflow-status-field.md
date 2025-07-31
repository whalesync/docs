---
description: Control the status of a Webflow item via a field in other apps
---

# Webflow status field

### About Webflow Status field

Webflow lets you control the status of an item by marking it as either Published, Draft, or Archived. With our Webflow Status field sync, you can now control that state from apps like Airtable or Notion.

For example, if you manage your blog content in Notion, you can now control whether those blog posts are live or in draft from within Notion.

{% hint style="info" %}
Using the Webflow Status field may reduce sync speed by a few seconds per record.
{% endhint %}

### How to set up the Webflow Status field

1. Add a single-select field to your Airtable or Notion table and title it "Webflow Status"
2. Make sure it has _exactly_ these three options:
   1. "Archived"
   2. "Draft"
   3. "Active"
3. In Whalesync, map that field to Webflow's "Webflow Status" field
   1. If adding this field to an existing base, make sure to initialize the data from Webflow (see screenshot below)

<figure><img src="../../.gitbook/assets/CleanShot 2023-03-17 at 14.09.24.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/Screenshot 2023-02-08 at 11.49.31 AM.png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Airtable lets you set a default value for single select fields so you can, for example, set a default value of 'Draft'.\
\
\*Note - if no default value is set and the value is empty in this field, the behavior will default to 'Published'.
{% endhint %}

### "Active" vs. "Published"

In Webflow, you can make an item "Published" as well as "Staged for Publish". When an item is "Staged for Publish" it means it will become published next time you publish your Webflow site.

With our Webflow Status field, both "Published" and "Staged for Publish" are captured by the option "Active".

### Mini-demo

<figure><img src="../../.gitbook/assets/Status (1).gif" alt=""><figcaption><p>Demo using the Webflow status field</p></figcaption></figure>

### Limitations

#### Status field in conjunction with reference fields

One limitation of Webflow CMS collection items is that a **published** Webflow item cannot reference a **draft** Webflow item in a reference field. Unfortunately this is a Webflow restriction.

For example, the following will result in an error from the Webflow API:

1. Create two collections in Webflow. For this example, let's call them _People_ and _Teams_
2. Create a reference field on the _People_ collection that points to _Teams_
3. Create an item "Marketing" in the _Teams_ collection and set it to "published"
4. Create an item "Sally Smith" in the _People_ collection, add a reference to the "Marketing" item in the reference field, and set "Sally Smith" to "published"
5. Create a sync in Whalesync using the two Webflow collections and sync it to another app (such as Airtable)
6. In Airtable, set the Webflow Status field on the "Marketing" item to "Draft"

This will result in an error that will show up on the Whalesync Issues page. Webflow will reject the attempt to set the "Marketing" item to "Draft" because the **published** person "Sally Smith" is referencing the item. Unfortunately Whalesync does not have a workaround for this.
