---
description: How to use Whalesync's WordPress connector with ACF
---

# Advanced Custom Fields (ACF)

Whalesync supports syncing **Custom Post Types** and **Custom Fields** with ACF.

## Using ACF Custom Fields

To use ACF Custom Fields, you'll need to toggle the setting "show in REST API" on for each Field Group you want to use:

<figure><img src="../../.gitbook/assets/Setting up ACF fields.png" alt=""><figcaption></figcaption></figure>

## Image Fields

{% hint style="warning" %}
Whalesync does not currently support Image fields.
{% endhint %}

In order to sync an image into an ACF field, the ACF field needs to be of Text or URL. Whalesync will sync an image URL into the field when you upload an image on the other side of the sync (e.g. in an Airtable Attachment field). To display this correctly, your Wordpress template will need to retrieve the image as a URL, and not an image reference or array:

```php
<img src="<?php the_field('my_acf_image_field_name'); ?>">
```

## Supported Field Types

<table><thead><tr><th width="358.5">Field</th><th>Status<select><option value="6c90dea3d4b34f409e73be79b7076c4a" label="✖️ Not Yet" color="blue"></option><option value="9e01356060cc4ea4988d69f72fe19d39" label="✅ Supported" color="blue"></option><option value="bd4357bee12749d0b80f7bc4a94ec3b5" label="➡️ Supported (1-Way)" color="blue"></option><option value="9b0955a85d044258a10aa0d1d3695a79" label="✅ Supported (as JSON)" color="blue"></option><option value="3ed1eb655ce94da49e887be21197ec27" label="🔜 Coming Soon" color="blue"></option></select></th><th data-hidden></th></tr></thead><tbody><tr><td>👤 Text</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>🔽 Text Area</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>☑️ Number</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>🗃️ Range</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>✉️ Email</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>📂 URL</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td><a href="https://emojipedia.org/framed-picture/">🖼️</a> Password</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td><a href="https://emojipedia.org/framed-picture/">🖼️</a> Image</td><td><span data-option="3ed1eb655ce94da49e887be21197ec27">🔜 Coming Soon</span></td><td></td></tr><tr><td>👤 Author</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr></tbody></table>
