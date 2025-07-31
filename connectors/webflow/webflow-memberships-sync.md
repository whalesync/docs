---
description: Sync users from Webflow into other apps
---

# Webflow Memberships sync

<figure><img src="../../.gitbook/assets/Sept 20 Screenshot from TinyPNG.png" alt=""><figcaption><p>Whalesync supports syncing members through the "User accounts" table.</p></figcaption></figure>

### Supported Fields

<table><thead><tr><th>Field</th><th>Status<select><option value="a5cd90d6db5a416a882aa7a988f0c81a" label="✅ Supported" color="blue"></option><option value="342517587230452ca3e3f62868fcdc45" label="➡️ Supported (1-way)" color="blue"></option><option value="568ec9d3184541c0a36f9ef0c2c66ce1" label="✅ Supported (Write-Once)" color="blue"></option><option value="ae9d6cd5a7bc48a2ac8067e50a4b4641" label="✖️ Not Yet" color="blue"></option></select></th></tr></thead><tbody><tr><td>Access groups</td><td><span data-option="ae9d6cd5a7bc48a2ac8067e50a4b4641">✖️ Not Yet</span></td></tr><tr><td>☑️ Accept privacy</td><td><span data-option="a5cd90d6db5a416a882aa7a988f0c81a">✅ Supported</span></td></tr><tr><td>☑️ Accept communications</td><td><span data-option="a5cd90d6db5a416a882aa7a988f0c81a">✅ Supported</span></td></tr><tr><td>✉️ Email</td><td><span data-option="568ec9d3184541c0a36f9ef0c2c66ce1">✅ Supported (Write-Once)</span></td></tr><tr><td>☑️ Email Verified</td><td><span data-option="342517587230452ca3e3f62868fcdc45">➡️ Supported (1-way)</span></td></tr><tr><td>📅 Last Login</td><td><span data-option="342517587230452ca3e3f62868fcdc45">➡️ Supported (1-way)</span></td></tr><tr><td>📝 Name</td><td><span data-option="a5cd90d6db5a416a882aa7a988f0c81a">✅ Supported</span></td></tr><tr><td>🔽 Status</td><td><span data-option="342517587230452ca3e3f62868fcdc45">➡️ Supported (1-way)</span></td></tr><tr><td>🆔 Webflow Record ID</td><td><span data-option="342517587230452ca3e3f62868fcdc45">➡️ Supported (1-way)</span></td></tr></tbody></table>



Webflow's [Memberships feature](https://webflow.com/memberships) lets you manage users in your Webflow site.

### Not Yet Supported

Webflow Memberships is a relatively new feature with a relatively new API. Due to this, there are certain features we cannot support yet.

1. We do not yet support custom fields.
2. We do not yet support mapping the Access Groups table.

### Creating Users

Whalesync allows you to create new users in Webflow Memberships from other apps (e.g. Airtable). Note - the email field is a "write-once" field. See our docs on creating users for more details:

{% content-ref url="../../features/additional-features/creating-users-via-whalesync.md" %}
[creating-users-via-whalesync.md](../../features/additional-features/creating-users-via-whalesync.md)
{% endcontent-ref %}

### Template

If you're syncing Webflow users with Airtable, you can copy our free Airtable template which includes all available fields:

{% embed url="https://airtable.com/shrVADkHQUCcIWSRv" %}
