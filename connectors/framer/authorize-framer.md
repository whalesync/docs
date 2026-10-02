---
description: >-
  Connect a Framer project to Whalesync with its project URL and a Server API
  key, and what to do about each Framer connection error.
---

# Authorize Framer

Whalesync connects to Framer with the project URL and a Server API key from that project. A connection reaches one Framer project, and that project is the base the connection syncs.

## Connect a Framer project

1. Open the project in Framer and copy its URL from your browser's address bar. It looks like `https://framer.com/projects/My-Site--aBcD1234`.
2. In the project, open **Site Settings** and go to the **General** section to generate an API key. Keys are bound to one project, so create the key in the same project as the URL. Framer's own guide is [here](https://www.framer.com/developers/server-api-quick-start).
3. In Whalesync, choose Framer, paste the URL into **Framer project URL** and the key into **Framer Server API key**, and click **Authorize**. Whalesync checks the URL and key with Framer before it saves the connection.
4. Pick the project. A connection reaches one project, so there is one to pick.

To sync a different Framer site, add another connection with that site's URL and API key.

## Errors

| Message | What to do |
| --- | --- |
| Framer didn't accept this API key for this project. Create the key in the same project's settings and try again. | The key is wrong, was deleted, or belongs to a different project. Generate a key in this project's Site Settings and reconnect. |
| Framer couldn't find a project at this URL. Copy the project URL from your browser's address bar while the project is open in Framer. | The URL is mistyped or is not a project URL. Copy it again from the address bar. |
| Enter both your Framer project URL and a Server API key. | One of the two boxes was empty. Fill in both. |
| This connection already syncs a different Framer project. Use the URL and API key of that project. | When reconnecting, use the same project. To sync another site, add a new connection. |
| Couldn't reach Framer to check this project. Try again in a moment. | Framer did not respond. Try again. |
| This Framer collection has N items, more than the 5,000 Whalesync can sync from one Framer collection. Contact support to raise the limit. | [Contact support](../../resources/support/). |
| Framer needs a slug for every item. Fill in (field), which this collection builds its slugs from, or map a field to Slug in this sync. | Fill in that field in your other app, or map a field to Slug. See [Slugs](README.md#slugs). |
| Framer rejected a duplicate slug "(slug)". Each item's slug must be unique within a collection. | Change the slug in your other app. |
| This Framer collection no longer exists. It may have been deleted in Framer. Re-check the sync's table mapping. | The collection was deleted or replaced in Framer. Update the sync's table mapping. |
| Framer rejected this record: followed by Framer's own message | Framer refused the record and gave a reason, which usually names the field. Check the record in your other app. |
