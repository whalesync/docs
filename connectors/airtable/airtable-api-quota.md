# Airtable API quota

Airtable has strict API quota limits on its two lowest plans:

* Airtable's **Free plan**: 1,000 calls per workspace per month
* Airtable's **Team plan**: 100,000 calls per workspace per month
* Airtable's **Business and Enterprise plans** have unlimited API quota

In order to accomplish fast two-way sync, Whalesync can use a significant number of API calls each month. The number of API calls can depend on several factors: the number of syncs you have for a workspace, the number of records you have in your bases, and the number of edits that Whalesync needs to sync.

For this reason, we highly recommend subscribing to **Airtable Business or Enterprise** when using Whalesync. The Airtable Free plan will almost certainly run out of quota and the Airtable Team plan may or may not have enough quota depending on your syncing needs.

You can learn more about Airtable's API limits in their [API docs](https://support.airtable.com/docs/getting-started-with-airtables-web-api) and on their [pricing page](https://airtable.com/pricing).
