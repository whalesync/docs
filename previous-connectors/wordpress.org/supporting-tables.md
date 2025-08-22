---
description: How to set up all the right tables when syncing WordPress
---

# Supporting tables

## Overview

There are six tables every WordPress instance has:

<table><thead><tr><th>Name</th><th>Type<select><option value="2cf6fc5309b64ecd8815745df5fcdaaa" label="Main" color="blue"></option><option value="9b401e0fa5c04bda85fd3486ce2cb75c" label="Supporting" color="blue"></option></select></th></tr></thead><tbody><tr><td>Pages</td><td><span data-option="2cf6fc5309b64ecd8815745df5fcdaaa">Main</span></td></tr><tr><td>Posts</td><td><span data-option="2cf6fc5309b64ecd8815745df5fcdaaa">Main</span></td></tr><tr><td>Users</td><td><span data-option="9b401e0fa5c04bda85fd3486ce2cb75c">Supporting</span></td></tr><tr><td>Categories</td><td><span data-option="9b401e0fa5c04bda85fd3486ce2cb75c">Supporting</span></td></tr><tr><td>Tags</td><td><span data-option="9b401e0fa5c04bda85fd3486ce2cb75c">Supporting</span></td></tr><tr><td>Media</td><td><span data-option="9b401e0fa5c04bda85fd3486ce2cb75c">Supporting</span></td></tr></tbody></table>



_(If you have Custom Posts enabled, you will see more tables for each Custom Post type)_

The star of your site are the Pages and Posts - everything else is there to support them.

{% hint style="info" %}
**Tip:** We highly recommend that you map Categories and Tags in Whalesync!\
\
You can use our [Airtable template](https://www.whalesync.com/template-packs/wordpress-blog-3) which has these tables pre-configured.
{% endhint %}

## Supporting Tables

###

### Categories and Tags

Like the Users table, if you want to sync WordPress Categories and Tags, you'll need to set up supporting tables.

{% hint style="info" %}
**Tip:** Make sure "allow linking to multiple records" is toggled so you can link multiple categories and tags.
{% endhint %}

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-26 at 11.43.53 AM.png" alt=""><figcaption></figcaption></figure>

### Users

The Users table lists all the users of your site. Tables like Media, Pages, Posts all have a field called Author that can point to a user in this list.&#x20;

{% hint style="info" %}
**Note:** Whalesync does not support mapping the Users table at this time. You will have to manage users in the WordPress UI.
{% endhint %}

### Media

The Media table contains media like images, audio, and videos that you've uploaded to your Wordpress site. Posts, Pages, and custom post types have a field called Featured Image that can point to a media item in this list.

{% hint style="info" %}
**Note:** Whalesync does not support mapping the Media table at this time. Media must be uploaded and attached to posts in the WordPress UI.
{% endhint %}

