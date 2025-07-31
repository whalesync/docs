---
description: Tips to help you get started syncing Webflow E-Comm
---

# Quick Start Guide: WF E-Comm

### 1) Start with our template

If syncing Webflow E-Comm with Airtable, we highly recommend starting with our Airtable template:

{% embed url="https://airtable.com/shr6kzSL2IJ0tg1w3" %}
Click "Copy base" on the bottom right
{% endembed %}

### 2) (If not using the template) Make sure to add important tables&#x20;

You should have at least these five tables:

<figure><img src="../../.gitbook/assets/CleanShot 2023-05-24 at 18.33.21.png" alt=""><figcaption></figcaption></figure>

{% hint style="danger" %}
**The Variants table is necessary even if your products don't have variants**

Every product in Webflow has a "variant" even though Webflow doesn't show it.\
\
The Variant record of a Product stores important product information like price.
{% endhint %}

<figure><img src="../../.gitbook/assets/Productvariant.png" alt=""><figcaption><p>Example where a Webflow product doesn't "have variants" but really does under the hood</p></figcaption></figure>



### 3) (If not using the template) Make sure to add an "Initial Variant - Price"

You will need to have an "Initial Variant - Price" field in your Products table.

See the below doc to understand why this field is necessary:

{% content-ref url="how-to-create-products-and-variants.md" %}
[how-to-create-products-and-variants.md](how-to-create-products-and-variants.md)
{% endcontent-ref %}

### 4) Read the 'Things to Keep in Mind'

The 'Things to Keep in Mind' section of the doc below walks through concepts that are important to Webflow E-Commerce.

{% content-ref url="./" %}
[.](./)
{% endcontent-ref %}

### 5) Join our Slack channel

If you have any questions, don't hesitate to ask! We love to help :relaxed:.

{% embed url="https://join.slack.com/t/whalesyncpioneers/shared_invite/zt-r231pg5t-L7GRWvn52GZGm11GbiXX3Q" %}
