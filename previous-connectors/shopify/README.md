---
cover: ../../.gitbook/assets/gitbook-cover_shopify.jpg
coverY: 0
---

# Shopify

## Supported Tables

<table><thead><tr><th>Tables</th><th>Status<select><option value="6c90dea3d4b34f409e73be79b7076c4a" label="✖️ Not Yet" color="blue"></option><option value="9e01356060cc4ea4988d69f72fe19d39" label="✅ Supported" color="blue"></option><option value="bd4357bee12749d0b80f7bc4a94ec3b5" label="➡️ Supported (1-Way)" color="blue"></option><option value="9b0955a85d044258a10aa0d1d3695a79" label="✅ Supported (as JSON)" color="blue"></option></select></th><th data-hidden></th></tr></thead><tbody><tr><td>Products</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>Images</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>Options</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>Variants</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>Collects</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>Custom Collections</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>Customers</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>Inventory</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>Blogs</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>Pages</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>Orders</td><td><span data-option="bd4357bee12749d0b80f7bc4a94ec3b5">➡️ Supported (1-Way)</span></td><td></td></tr><tr><td>Locations</td><td><span data-option="bd4357bee12749d0b80f7bc4a94ec3b5">➡️ Supported (1-Way)</span></td><td></td></tr><tr><td>Discount Code</td><td><span data-option="6c90dea3d4b34f409e73be79b7076c4a">✖️ Not Yet</span></td><td></td></tr><tr><td>Gift Card</td><td><span data-option="6c90dea3d4b34f409e73be79b7076c4a">✖️ Not Yet</span></td><td></td></tr><tr><td>Transactions</td><td><span data-option="6c90dea3d4b34f409e73be79b7076c4a">✖️ Not Yet</span></td><td></td></tr><tr><td>Refunds</td><td><span data-option="6c90dea3d4b34f409e73be79b7076c4a">✖️ Not Yet</span></td><td></td></tr><tr><td>Articles</td><td><span data-option="6c90dea3d4b34f409e73be79b7076c4a">✖️ Not Yet</span></td><td></td></tr></tbody></table>

## Things to Keep in Mind <a href="#h_bccce14d8a" id="h_bccce14d8a"></a>

### Backing up data

{% hint style="danger" %}
**We strongly recommend using a Shopify Backup service**
{% endhint %}

Two-way sync is very powerful. To protect against manual error and for extra peace of mind, we recommend using a backup service like the one below when using two-way sync :point\_down:

{% embed url="https://apps.shopify.com/backup" %}

### Syncing images

{% hint style="info" %}
**You must create a separate Media table in order to sync product images**
{% endhint %}

See the article below for more details :point\_down:

{% content-ref url="syncing-images.md" %}
[syncing-images.md](syncing-images.md)
{% endcontent-ref %}



### Syncing variants

{% hint style="info" %}
**You must create a separate Variants table in order to sync product variants**
{% endhint %}

See the article below for more details :point\_down:

{% content-ref url="syncing-variants.md" %}
[syncing-variants.md](syncing-variants.md)
{% endcontent-ref %}

