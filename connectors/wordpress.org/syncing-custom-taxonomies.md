---
description: How to sync WordPress custom taxonomies with Whalesync
---

# Syncing custom taxonomies

Whalesync automatically discovers the two built-in WordPress taxonomies — **Categories** and **Tags** — and surfaces them as their own tables you can map (see [Supporting tables](supporting-tables.md)).

{% hint style="warning" %}
**Custom taxonomies are not discovered as their own tables.** A custom taxonomy you've registered (for example `site-category`) won't appear as a separate mappable table, and refreshing the schema or reconnecting the connector won't change that. You can still sync to it using the steps below.
{% endhint %}

## How to sync to a custom taxonomy

WordPress represents a taxonomy assignment on a post as the taxonomy term's numeric **ID**, not its name. So to sync a custom taxonomy, you map a field containing the term ID(s) to one of these columns on your Posts, Pages, or custom post type table:

* The **native taxonomy field** WordPress adds to the post type when the taxonomy is registered with **Show in REST API** enabled and associated with that post type.
* An **[ACF](advanced-custom-fields-acf.md) field of type "Taxonomy"**, if you've set one up.

Both accept the numeric term ID and check off the matching term on the post.

### 1. Find the term IDs

You can find a term's ID either way:

* List the taxonomy's terms at `https://your-site.com/wp-json/wp/v2/<taxonomy>` and read each term's `id`.
* Or open the term's edit page in WordPress admin — the ID is the `tag_ID` value in the URL (e.g. `.../term.php?taxonomy=site-category&tag_ID=22`).

### 2. Get the IDs into your source

Because WordPress wants the ID and not the label, the cleanest setup in Airtable is a small lookup table:

1. Create a table that maps each term's **name** to its **WordPress ID**.
2. On the table you're syncing, add a "Link to another record" field pointing at that lookup table, plus a Lookup field that pulls in the ID.
3. Sync the Lookup field. This way you pick terms by name in Airtable instead of memorizing IDs.

### 3. Map it in Whalesync

Map that ID field to the taxonomy column on the matching post type table, and run your sync. The term will be assigned to the post the same way the built-in Categories field works.

{% hint style="info" %}
**Tip:** To assign more than one term to a record, use a field that outputs multiple IDs and toggle "allow linking to multiple records" so multiple values sync through.
{% endhint %}

{% hint style="warning" %}
**Seeing two columns for the same taxonomy?** If a taxonomy is both associated with a post type **and** exposed as an ACF field, Whalesync shows two similarly-named columns — the native one (named after the taxonomy, e.g. "Site Category") and the ACF one (named after its field name, e.g. "Acf Site Category"). Map only one of them, and make sure it's the one you intend — mapping the wrong column won't error, it just won't update the post.
{% endhint %}

## Notes

* **Terms must already exist in WordPress.** This assigns posts to existing terms by their ID — it does not create new terms in the taxonomy. Create the terms in WordPress first, and keep your lookup table up to date if you add more.
* **Permissions:** make sure the WordPress user Whalesync connects with is an **Editor** or **Admin** so it is allowed to assign terms.
