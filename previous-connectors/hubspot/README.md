---
cover: ../../.gitbook/assets/gitbook-cover_hubspot.jpg
coverY: 0
---

{% hint style="warning" %}
**Archived:** This connector is no longer offered by Whalesync. Existing syncs will continue to run, but future improvements and support will be limited. See [Previous Connectors](../) for more details.
{% endhint %}

# HubSpot

## Supported Objects

<table><thead><tr><th>Objects</th><th>Status<select><option value="6c90dea3d4b34f409e73be79b7076c4a" label="✖️ Not Yet" color="blue"></option><option value="9e01356060cc4ea4988d69f72fe19d39" label="✅ Supported" color="blue"></option><option value="bd4357bee12749d0b80f7bc4a94ec3b5" label="➡️ Supported (1-Way)" color="blue"></option><option value="9b0955a85d044258a10aa0d1d3695a79" label="✅ Supported (as JSON)" color="blue"></option></select></th><th data-hidden></th></tr></thead><tbody><tr><td>📞 Calls</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>👥 Contact</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>🏢 Companies</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>📡 Communications</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>⚙️ Custom Objects</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>🤝 Deals</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>📧 Emails</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>🧾 Line Items</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>🤝 Meetings</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>📝 Notes</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>📦 Products</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td><span data-gb-custom-inline data-tag="emoji" data-code="1f4c3">📃</span> Quotes</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span> Tasks</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>🏦 Taxes</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>🎫 Tickets</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>🧑‍🔧 Services</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr></tbody></table>

## Things to Keep in Mind

### Backup Service

{% hint style="warning" %}
**If two-way syncing HubSpot, we recommend using a backup service.**&#x20;
{% endhint %}

HubSpot does not have built-in backup/restore functionality. Two-way sync is very powerful. A consequence is a mistake in a connected app could impact all of your HubSpot data at once.

As a precaution, we suggest using a HubSpot backup solution such as:

- [SysCloud Backup](https://ecosystem.hubspot.com/marketplace/apps/syscloud-backup-for-hubspot-595013)
- [Pro Backup](https://ecosystem.hubspot.com/marketplace/apps/pro-backup-380854)

### Associations

See guide below on how to sync Association fields.

{% content-ref url="associations.md" %}
[associations.md](associations.md)
{% endcontent-ref %}

### Properties with supported webhooks

See guide below on which HubSpot properties have webhooks supported.

{% content-ref url="webhooks.md" %}
[webhooks.md](webhooks.md)
{% endcontent-ref %}

## Video Guide

{% embed url="https://www.youtube.com/watch?v=y-pfnZiQkZY" %}

## Setup Guide

Whalesync integrates HubSpot with other apps like Airtable and Salesforce. This enables you to do things like:

- Manage your HubSpot Contacts from an internal Airtable app
- Sync all HubSpot Deals to Salesforce continuously

### Install

1.  Create a new base

    <figure><img src="../../.gitbook/assets/HubSpot 1.png" alt=""><figcaption></figcaption></figure>

2.  Choose HubSpot and click 'Authorize'

    <figure><img src="../../.gitbook/assets/HubSpot 2.png" alt=""><figcaption></figcaption></figure>

3.  Choose your HubSpot account

    <figure><img src="../../.gitbook/assets/CleanShot 2023-12-29 at 12.06.33.png" alt=""><figcaption></figcaption></figure>

4.  Choose your connected app (e.g. Airtable, Notion, Salesforce, etc.) and authorize

    <figure><img src="../../.gitbook/assets/HubSpot 4.png" alt=""><figcaption></figcaption></figure>

### Configure

5.  Map the tables (aka Objects) you want to sync between HubSpot and your connected app and click 'Map Fields'

    <figure><img src="../../.gitbook/assets/HubSpot 5.png" alt=""><figcaption></figcaption></figure>

6.  Map the fields you want to sync between HubSpot and your connected app and click 'Save Base'

    <figure><img src="../../.gitbook/assets/HubSpot 6.png" alt=""><figcaption></figcaption></figure>

### Use

7.  Toggle sync on to begin syncing

    <figure><img src="../../.gitbook/assets/Sync Active.png" alt=""><figcaption></figcaption></figure>

### Disconnect

8.  To turn sync off, toggle sync off

    <figure><img src="../../.gitbook/assets/Disable Sync.png" alt=""><figcaption></figcaption></figure>

9.  To delete your base, click the settings button and then 'Delete'

    <figure><img src="../../.gitbook/assets/Delete Sync.png" alt=""><figcaption></figcaption></figure>
