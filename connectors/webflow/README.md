---
cover: ../../.gitbook/assets/gitbook-cover_webflow.jpg
coverY: 0
---

# Webflow

## Webflow Connector Guide

This guide provides an overview of how to connect Whalesync to Webflow and answers common questions.

### Connecting to Webflow

To connect Whalesync to your Webflow account, we use OAuth. This is a secure, standard way for you to grant Whalesync access without sharing your password.

When you set up Webflow in Whalesync, you'll be redirected to Webflow's website. You'll be asked to log in to your Webflow account and then approve the connection to Whalesync. You'll then choose which workspaces or individual sites you'd like to give access to. Once you approve, you'll be sent back to Whalesync to continue your setup.

### Syncing Data

Whalesync treats your Webflow **Sites** as "bases" and your **Collections** as "tables". This allows you to sync data between your Webflow CMS and other apps.

Whalesync can sync several types of data from Webflow:

* **CMS Data**: Sync items from your Webflow CMS Collections.
* **Users**: If you use Webflow Memberships, you can sync your user accounts.
* **Form Submissions**: Data from your Webflow forms can be synced to other tools for analysis or processing.

A special feature of the Webflow connector is the **"Webflow Status"** field. When you map a Webflow table, Whalesync creates this field. It lets you control whether a CMS item is "Published", "Draft", or "Archived".

{% content-ref url="webflow-status-field.md" %}
[webflow-status-field.md](webflow-status-field.md)
{% endcontent-ref %}

#### Automatic Table and Field Creation

Whalesync can automatically create tables and fields in Webflow to match the structure of the other app you're syncing with.

### Things to Keep in Mind

#### **Publishing Your Site**

Any changes you make to your Webflow data through Whalesync (like creating a new CMS item or updating an existing one) will not be live on your website until you **publish** your site in Webflow. While you can change an item's status to "Published" using the "Webflow Status" field, the final step is always to go to your Webflow dashboard and publish the site to make the changes public.

Whalesync requires you to republish your Webflow site any time you make a change to the CMS structure (eg. add a new field to a collection) in order for syncing to work.

Webflow sites need to be published to all domains otherwise Webflow rejects API calls (aka sync updates).

![](<../../.gitbook/assets/publish (3) (2).png>)

#### **Primary Field**

In Webflow, the primary field for a Collection is usually the `Name` field. Webflow requires this field to always have a non-empty value, so it's important to have this mapped correctly for reliable syncing. This is also the value that's used to display records in the Whalesync UI.

#### Multi-reference fields

Whalesync supports multi-reference fields out of the box! See the guide below to ensure this is configured correctly:&#x20;

{% content-ref url="../../features/additional-features/reference-fields.md" %}
[reference-fields.md](../../features/additional-features/reference-fields.md)
{% endcontent-ref %}

## Supported Fields

<table><thead><tr><th>Field</th><th>Status<select><option value="6c90dea3d4b34f409e73be79b7076c4a" label="✖️ Not Yet" color="blue"></option><option value="9e01356060cc4ea4988d69f72fe19d39" label="✅ Supported" color="blue"></option><option value="bd4357bee12749d0b80f7bc4a94ec3b5" label="➡️ Supported (1-Way)" color="blue"></option></select></th><th data-hidden></th></tr></thead><tbody><tr><td>🎨 Color</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>📅  Date/Time</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>✉️ Email</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>📂 File</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>🖼️ Image</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>🆔 Item ID</td><td><span data-option="bd4357bee12749d0b80f7bc4a94ec3b5">➡️ Supported (1-Way)</span></td><td></td></tr><tr><td>🔗 Link</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>🖼️ Multi-image</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>🖇️ Multi-Reference</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>#️⃣ Number</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>🔽 Option</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>📞 Phone</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>📝 Plain text - single line</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>📝 Plain text - multiple line</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>🖇️ Reference</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>📰 Rich text</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>☑️ Switch</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr><tr><td>📹 Video link</td><td><span data-option="9e01356060cc4ea4988d69f72fe19d39">✅ Supported</span></td><td></td></tr></tbody></table>

### Synthetic Fields

Whalesync adds some special fields to your Webflow tables. These fields are not present in your Webflow database but are available to map in your sync.

| Field Name        | Explanation                                                    | Writable  |
| ----------------- | -------------------------------------------------------------- | --------- |
| Webflow Status    | Controls the state of a CMS item (Active, Draft, or Archived). | Writable  |
| Webflow Record ID | The unique identifier for a record from Webflow's system.      | Read-only |
| Created On        | The timestamp for when a record was created in Webflow.        | Read-only |
| Updated On        | The timestamp for when a record was last updated in Webflow.   | Read-only |

###



