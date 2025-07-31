---
cover: ../../.gitbook/assets/gitbook-cover_memberstack.jpg
coverY: 0
---

# Memberstack

## Supported Fields

<table><thead><tr><th>Field</th><th>Status<select><option value="6c90dea3d4b34f409e73be79b7076c4a" label="✖️ Not Yet" color="blue"></option><option value="9e01356060cc4ea4988d69f72fe19d39" label="✅ Supported" color="blue"></option><option value="bd4357bee12749d0b80f7bc4a94ec3b5" label="➡️ Supported (1-Way)" color="blue"></option><option value="9b0955a85d044258a10aa0d1d3695a79" label="✅ Supported (as JSON)" color="blue"></option></select></th><th data-hidden></th></tr></thead><tbody><tr><td>✉️ Email</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>📝 Login redirect</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>☑️ Permissions</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>🆔 Plan IDs</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>🗃️ Custom fields</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>🗃️ Metadata</td><td><span data-option="9b0955a85d044258a10aa0d1d3695a79">✅ Supported (as JSON)</span></td><td></td></tr><tr><td>🆔 Memberstack record ID</td><td><span data-option="bd4357bee12749d0b80f7bc4a94ec3b5">➡️ Supported (1-Way)</span></td><td></td></tr><tr><td>🕠 Created at</td><td><span data-option="bd4357bee12749d0b80f7bc4a94ec3b5">➡️ Supported (1-Way)</span></td><td></td></tr><tr><td>🕠 Last login</td><td><span data-option="bd4357bee12749d0b80f7bc4a94ec3b5">➡️ Supported (1-Way)</span></td><td></td></tr><tr><td>🗃️ Plans Data</td><td><span data-option="bd4357bee12749d0b80f7bc4a94ec3b5">➡️ Supported (1-Way)</span></td><td></td></tr><tr><td>☑️ Verified</td><td><span data-option="bd4357bee12749d0b80f7bc4a94ec3b5">➡️ Supported (1-Way)</span></td><td></td></tr><tr><td>󠁻󠁻🗃️ JSON</td><td><span data-option="9b0955a85d044258a10aa0d1d3695a79">✅ Supported (as JSON)</span></td><td></td></tr></tbody></table>

## Things to Keep in Mind <a href="#h_bccce14d8a" id="h_bccce14d8a"></a>

### Auto-generated passwords

{% hint style="info" %}
**Creating a new user via sync, will auto-generate a password in Memberstack**
{% endhint %}

Whalesync allows you to create new Memberstack members from a synced app. For example, you can create a new member from Airtable :tada:.

When creating a new member in Airtable, Whalesync auto-generates a password for that Member. That new member will need to reset their password to log in.



### Syncing custom fields

{% hint style="info" %}
**To sync custom fields, you will need to create a member in Memberstack with the email "schema@whalesync.com" with values in custom fields.**
{% endhint %}

See :point\_down:for more details

{% content-ref url="memberstack-custom-fields.md" %}
[memberstack-custom-fields.md](memberstack-custom-fields.md)
{% endcontent-ref %}



### Default sync delay

{% hint style="info" %}
**If syncing Memberstack and Airtable, we default to a 10-second sync delay from Airtable to Memberstack**
{% endhint %}

See :point\_down:for more details

{% content-ref url="../../features/additional-features/creating-users-via-whalesync.md" %}
[creating-users-via-whalesync.md](../../features/additional-features/creating-users-via-whalesync.md)
{% endcontent-ref %}



### Metadata fields

{% hint style="info" %}
**Metadata fields sync as JSON**
{% endhint %}

We support 2-way syncing of Memberstack Metadata fields as JSON blobs. You can edit the data in those fields as long as they retain the correct JSON format.

<figure><img src="../../.gitbook/assets/metadata_json.png" alt=""><figcaption></figcaption></figure>

## Templates <a href="#h_bccce14d8a" id="h_bccce14d8a"></a>

Copy our Airtable or Notion templates to instantly have a table set up to sync with Memberstack.

{% embed url="https://whalesync.com/template-packs" %}
