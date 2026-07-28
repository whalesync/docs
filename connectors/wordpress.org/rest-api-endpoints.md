---
description: The WordPress REST API endpoints Whalesync uses under the hood
---

# REST API endpoints

## Overview

Whalesync talks to your site through the standard [WordPress REST API](https://developer.wordpress.org/rest-api/) (the `wp-json` endpoints). This page lists the specific endpoints we call and what each one is for. It's mostly here for the curious and for anyone debugging a connection at the network level — you don't need to know any of this to set up a sync.

Throughout, `{type}` is a post type slug (for example `posts`, `pages`, or a custom post type) and `{id}` is a record's ID.

## Endpoints by function

<table><thead><tr><th>Function</th><th width="140">Method</th><th>Path</th><th>Key query params</th></tr></thead><tbody><tr><td>Auth / connection probe</td><td>GET</td><td><code>wp/v2/posts</code></td><td><code>per_page=5&#x26;context=edit</code></td></tr><tr><td>Discover REST root</td><td>HEAD / GET</td><td>site root (reads <code>Link</code> header) → <code>wp-json/</code></td><td>—</td></tr><tr><td>List available post types (tables)</td><td>GET</td><td><code>wp/v2/types</code></td><td>—</td></tr><tr><td>Fetch a table's field schema</td><td>OPTIONS</td><td><code>wp/v2/{type}</code></td><td>—</td></tr><tr><td>Poll / list records</td><td>GET</td><td><code>wp/v2/{type}</code></td><td><code>per_page=100</code> + <code>page=n&#x26;orderby=id&#x26;order=asc</code> (or <code>offset=n</code>); <code>status=any</code></td></tr><tr><td>Get one record</td><td>GET</td><td><code>wp/v2/{type}/{id}</code></td><td><code>status=any</code></td></tr><tr><td>Create record (new row)</td><td>POST</td><td><code>wp/v2/{type}</code></td><td>—</td></tr><tr><td>Update record</td><td>PATCH</td><td><code>wp/v2/{type}/{id}</code></td><td>—</td></tr><tr><td>Delete record</td><td>DELETE</td><td><code>wp/v2/{type}/{id}</code></td><td><code>force=true</code></td></tr><tr><td>Upload media</td><td>POST</td><td><code>wp/v2/media</code></td><td>raw file body + <code>Content-Disposition</code></td></tr><tr><td>Get media</td><td>GET</td><td><code>wp/v2/media/{id}</code></td><td>—</td></tr></tbody></table>
