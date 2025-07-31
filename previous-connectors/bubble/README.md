---
cover: ../../.gitbook/assets/gitbook-cover_bubble.jpg
coverY: 0
---

# Bubble

## Bubble API Changes <a href="#h_bccce14d8a" id="h_bccce14d8a"></a>

{% hint style="warning" %}
On April 6, 2023, Bubble [announced](https://bubble.io/blog/2023-pricing-updates/) pricing changes that affected their API, and on October 1, 2024, they migrated all users to new API pricing.

Due to Bubble's API limitations, **Whalesync will be slower to sync changes out of Bubble** and you will likely need to upgrade your Bubble plan to continue using Whalesync.

Whalesync uses polling to observe changes to records, which uses Bubble's "workload units". Bubble does not support webhooks which would reduce the need for polling. We are working with the Bubble team to find a good solution, but in the meantime, please be aware that Whalesync may use a significant amount of your workload units depending on your Bubble subscription.
{% endhint %}

## Supported Fields

<table><thead><tr><th>Field</th><th>Status<select><option value="6c90dea3d4b34f409e73be79b7076c4a" label="✖️ Not Yet" color="blue"></option><option value="9e01356060cc4ea4988d69f72fe19d39" label="✅ Supported" color="blue"></option><option value="bd4357bee12749d0b80f7bc4a94ec3b5" label="➡️ Supported (1-Way)" color="blue"></option></select></th><th data-hidden></th></tr></thead><tbody><tr><td>🖇️ Composite types</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>🧑 Created by</td><td><span data-option="bd4357bee12749d0b80f7bc4a94ec3b5">➡️ Supported (1-Way)</span></td><td></td></tr><tr><td>🕠 Created date</td><td><span data-option="bd4357bee12749d0b80f7bc4a94ec3b5">➡️ Supported (1-Way)</span></td><td></td></tr><tr><td>📅 Date</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>📅 Date interval</td><td><span data-option="6c90dea3d4b34f409e73be79b7076c4a">✖️ Not Yet</span></td><td></td></tr><tr><td>📅 Date range</td><td><span data-option="6c90dea3d4b34f409e73be79b7076c4a">✖️ Not Yet</span></td><td></td></tr><tr><td>📍Geographic address</td><td><span data-option="6c90dea3d4b34f409e73be79b7076c4a">✖️ Not Yet</span></td><td></td></tr><tr><td>📂 Image/file</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>🕠 Modified date</td><td><span data-option="bd4357bee12749d0b80f7bc4a94ec3b5">➡️ Supported (1-Way)</span></td><td></td></tr><tr><td>#️⃣ Number</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>#️⃣ Number interval</td><td><span data-option="6c90dea3d4b34f409e73be79b7076c4a">✖️ Not Yet</span></td><td></td></tr><tr><td>📝 Slug</td><td><span data-option="bd4357bee12749d0b80f7bc4a94ec3b5">➡️ Supported (1-Way)</span></td><td></td></tr><tr><td>📝 Text</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>🫂 User</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>☑️ Yes/no</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr></tbody></table>

## Things to Keep in Mind <a href="#h_bccce14d8a" id="h_bccce14d8a"></a>

{% hint style="warning" %}
**Must enable data API**\
Bubble requires the Data API to be enabled for syncing to work. Follow the instructions below to enable it.
{% endhint %}

<figure><img src="../../.gitbook/assets/Data API.png" alt=""><figcaption></figcaption></figure>

1. Go to Settings > API
2. Check the box for "Enable Data API"
3. Check the box for all tables you plan to sync

{% hint style="danger" %}
**Renaming schema, tables, or columns will break Whalesync mappings**\
If you rename a table or column, you'll need to remap the impacted table/column in Whalesync. Note - remapping an impacted table will lead to duplicates unless you reset your data as well.&#x20;

If you need to rename a table in Bubble, we suggest making sure that every record has a unique identifier that can be matched on, then turn off the old sync and set up a new sync with [record-matching.md](../../features/record-matching.md "mention").
{% endhint %}

{% hint style="info" %}
**The email field for User "things" has a record sync delay if syncing with Airtable**\
Bubble has a special data table called User that they treat differently than other tables.  Specifically, you need to send it a valid email address. When syncing Bubble with Airtable, this can cause problems since Airtable saves every keystroke.\
\
To avoid this issue, Whalesync defaults to a 30-second record sync delay. See [record sync delay](broken-reference) for more details.
{% endhint %}

