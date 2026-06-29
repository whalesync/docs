---
description: Sync localized Webflow CMS content across every locale on your site
---

# Webflow localization

If your Webflow site uses [Webflow Localization](https://webflow.com/localization) to publish CMS content in more than one language, Whalesync can sync each locale.

### How localized collections appear in Whalesync

When your Webflow site has secondary locales, each localized CMS collection shows up in Whalesync more than once:

* The **primary locale** keeps the collection's normal name (e.g. `Blog Posts`).
* Each **secondary locale** appears as a separate table with the locale tag in brackets (e.g. `Blog Posts (FR-FR)`, `Blog Posts (DE-DE)`).

Each of these is a regular Whalesync table. You map fields, turn on two-way sync, filter, and otherwise work with a locale table exactly like any other Webflow table — point it at a table in Airtable, Notion, Google Sheets, etc., and it syncs normally.

{% hint style="info" %}
The locale shown in brackets is Webflow's [BCP-47 locale tag](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Language), uppercased — `FR-FR` for French (France), `EN-GB` for English (United Kingdom), and so on. This keeps regional variants of the same language unambiguous.
{% endhint %}

### How records are created across locales

Webflow doesn't let you add a single locale to an existing CMS item through its API — every locale variant of an item has to exist from the moment the item is created. Because of that:

* **Creating a record in the primary-locale table also creates it in every other locale.** When a new record syncs into your primary collection (e.g. `Blog Posts`), Whalesync automatically materializes the matching item in all of your secondary-locale collections at the same time. You don't need to create the record separately in each locale.

This means a brand-new item starts life in every locale, ready for you to fill in translated content per locale.

### Field edits are never synced between locales

After an item exists, **Whalesync never copies field edits from one locale to another.** Each locale table syncs independently:

* Editing a field in `Blog Posts` updates only the primary-locale content in Webflow.
* Editing a field in `Blog Posts (FR-FR)` updates only the French content.

This is intentional — localized content is supposed to differ per locale, so Whalesync keeps each locale's values isolated rather than overwriting one language's translation with another's. If you want the same value in every locale, set it in each locale's table (or in the source records that map to each locale table).

{% hint style="warning" %}
Because edits don't propagate across locales, the **primary-locale value is _not_ a default** for the other locales. A newly created item's secondary-locale fields start out as Webflow's own copy of the primary content, but from then on each locale is edited independently.
{% endhint %}

### Things to keep in mind

* **Republish to go live.** As with any Webflow change made through Whalesync, localized edits won't appear on your site until you publish it in Webflow. See [Webflow](README.md) for more on publishing.
* **New locales.** If you add a secondary locale in Webflow after setting up your sync, re-fetch the schema (edit your base) in Whalesync so the new locale table shows up.
* **Don't see the locale tables?** Make sure your Webflow site actually has secondary locales configured and that your connection is reauthorized after enabling Localization. If they still don't appear, reach out to support.
