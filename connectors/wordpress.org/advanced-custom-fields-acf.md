---
description: >-
  Sync WordPress custom post types and ACF custom fields with Whalesync. Turn on
  show in REST API, add a Post Type location rule, and check field support.
---

# Advanced Custom Fields (ACF)

Whalesync supports syncing **Custom Post Types** and **Custom Fields** with ACF.

## Using ACF Custom Fields

To use ACF Custom Fields, you'll need to toggle the setting "show in REST API" on for each Field Group you want to use:

<figure><img src="../../.gitbook/assets/Setting up ACF fields.png" alt=""><figcaption></figcaption></figure>

Because of how Wordpress returns metadata for ACF fields through the API, you also need to have at least one rule in the "Location Rules" that checks for the Post Types you want the field to be a part of. For example, if you want to sync your ACF fields with the Posts table, you'll need a check for "Post Type is equal to Post".

<figure><img src="../../.gitbook/assets/Screenshot 2025-09-08 at 11.02.46 AM.png" alt=""><figcaption></figcaption></figure>

If you use more complex logic than this already, and don't want to always show the ACF fields in a group on a specific table, you can add a condition that will never match along with the check in a new rule group. This will still allow Whalesync to pick up the field, but won't affect how your fields are shown in the Wordpress UI.

<figure><img src="../../.gitbook/assets/Screenshot 2025-09-08 at 11.13.43 AM.png" alt=""><figcaption></figcaption></figure>

## Supported Field Types

<table><thead><tr><th width="358.5">Field</th><th>Status<select><option value="6c90dea3d4b34f409e73be79b7076c4a" label="✖️ Not Yet" color="blue"></option><option value="9e01356060cc4ea4988d69f72fe19d39" label="✅ Supported" color="blue"></option><option value="bd4357bee12749d0b80f7bc4a94ec3b5" label="➡️ Supported (1-Way)" color="blue"></option><option value="9b0955a85d044258a10aa0d1d3695a79" label="✅ Supported (as JSON)" color="blue"></option><option value="3ed1eb655ce94da49e887be21197ec27" label="🔜 Coming Soon" color="blue"></option></select></th><th data-hidden></th></tr></thead><tbody><tr><td>👤 Text</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>🔽 Text Area</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>☑️ Number</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>🗃️ Range</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>✉️ Email</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>📂 URL</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td><a href="https://emojipedia.org/framed-picture">🖼️</a> Password</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td><a href="https://emojipedia.org/framed-picture">🖼️</a> Image</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>👤 Author</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr></tbody></table>
