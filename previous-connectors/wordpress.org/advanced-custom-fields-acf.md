---
description: How to use Whalesync's WordPress connector with ACF
---

# Advanced Custom Fields (ACF)

Whalesync supports syncing **Custom Post Types** and **Custom Fields** with ACF :rocket:.

## Using ACF Custom Fields

To use ACF Custom Fields, you'll need to toggle the setting "show in REST API" on for each Field Group you want to use:

<figure><img src="../../.gitbook/assets/Setting up ACF fields.png" alt=""><figcaption></figcaption></figure>

## Supported Field Types

<table><thead><tr><th width="358.5">Field</th><th>Status<select><option value="6c90dea3d4b34f409e73be79b7076c4a" label="✖️ Not Yet" color="blue"></option><option value="9e01356060cc4ea4988d69f72fe19d39" label="✅ Supported" color="blue"></option><option value="bd4357bee12749d0b80f7bc4a94ec3b5" label="➡️ Supported (1-Way)" color="blue"></option><option value="9b0955a85d044258a10aa0d1d3695a79" label="✅ Supported (as JSON)" color="blue"></option><option value="3ed1eb655ce94da49e887be21197ec27" label="🔜 Coming Soon" color="blue"></option></select></th><th data-hidden></th></tr></thead><tbody><tr><td>👤 Text</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>🔽 Text Area</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>☑️ Number</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>🗃️ Range</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>✉️ Email</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>📂 URL</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td><a href="https://emojipedia.org/framed-picture/">🖼️</a> Password</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td><a href="https://emojipedia.org/framed-picture/">🖼️</a> Image</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>👤 Author</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr></tbody></table>

## How to Sync Image Fields

See :point\_down:

{% content-ref url="how-to-sync-images.md" %}
[how-to-sync-images.md](how-to-sync-images.md)
{% endcontent-ref %}

## How to Sync Author Fields

Similar to Images, WordPress treats "Users" as a separate entity, so special steps need to be taken:

1. In WordPress, go to your ACF custom field for Authors
2. In the field name add "\_fk\_users" at the end
3. In Airtable, make the field a linked record to the Users table
4. Map the fields in Whalesync

<figure><img src="../../.gitbook/assets/CleanShot 2023-06-21 at 18.40.32@2x.png" alt=""><figcaption><p>Example of adding "fk_users" in WordPress</p></figcaption></figure>
