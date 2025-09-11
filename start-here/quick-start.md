---
description: Set up your first sync in less than 5 minutes
---

# Quick start

Seeing data sync instantly across your tools is exhilarating. With Whalesync, you can connect apps and start two-way syncing in under five minutes. Here's how:

{% hint style="success" %}
**Pro Tip**: Start with a small test dataset (10-20 records) to validate your sync before scaling up!
{% endhint %}

## Step 1: Create a new sync

From the dashboard, click "New sync" to kick off the setup flow.

<figure><img src="../.gitbook/assets/create_sync.gif" alt=""><figcaption></figcaption></figure>

## Step 2: Connect your apps

Choose the apps you want to sync and click "Authorize". For certain apps, you'll need to copy and paste an API key, but for most you can sign-in with OAuth.

<figure><img src="../.gitbook/assets/connect_apps.gif" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
If you're unsure where to find your API Keys, please visit the specific connector documentation.
{% endhint %}

**Common Authorization Types**:
- **OAuth** (recommended): Sign in directly - Airtable, Notion, HubSpot, Webflow
- **API Key**: Copy/paste from app settings - Google Sheets, some databases  
- **Connection String**: For databases like Postgres, Supabase

## Step 3: Map tables

Choose the tables you want to map together for syncing.

<figure><img src="../.gitbook/assets/table mapping.gif" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
If your table names match exactly, they will show up as suggested.
{% endhint %}

**Table Mapping Tips**:
- Map similar data types (e.g., "Contacts" to "People", "Products" to "Items")
- You can map multiple tables in one sync
- Don't see a table? Check if it exists and has the right permissions

## Step 4: Map fields

After mapping a table, you can map the specific fields you want to sync and choose the sync direction for each one.

<figure><img src="../.gitbook/assets/field mapping.gif" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Field names do not have to match, but field _types_ do need to be compatible.
{% endhint %}

**Field Mapping Guide**:
- **Two-way sync** (`↔`): Changes in either app update the other
- **One-way sync** (`→`): Changes flow in one direction only
- **Compatible fields**: Text ↔ Text, Number ↔ Currency, Date ↔ Date
- **Skip fields**: You don't need to map every field

**Common Field Mappings**:
| Type | Examples |
| --- | --- |
| **Identity** | Name, Title, Email, ID |
| **Content** | Description, Notes, Body |
| **Status** | Status, Stage, Published |
| **Dates** | Created Date, Due Date, Modified |
| **Numbers** | Price, Quantity, Score |

## Step 5: Activate sync

<figure><img src="../.gitbook/assets/activate sync.gif" alt=""><figcaption></figcaption></figure>

:tada: **Woo hoo! That's it.** Activate sync and within seconds you should see data begin syncing.

## What Happens Next?

After activation, Whalesync will:

1. **Initial Sync**: Import existing records from both apps
2. **Field Validation**: Check that all field mappings work correctly  
3. **Real-time Sync**: Keep data in sync automatically going forward

{% hint style="info" %}
After turning sync on, you can check the [operations page](../features/operations.md) to see sync updates Whalesync makes and the [issues page](../features/issues.md) to see any sync errors from your connected apps.
{% endhint %}

## Troubleshooting Your First Sync

**Sync not starting?**
- Check that both apps are properly authorized
- Verify you have the right permissions in both apps
- Look at the Issues page for specific error messages

**Missing data?**  
- Check your field mappings - unmapped fields won't sync
- Verify field types are compatible
- Some fields may be read-only (like calculated fields)

**Unexpected changes?**
- Review sync direction settings for each field
- Check if you have filters enabled that limit which records sync
- Remember: two-way sync means changes go both directions!

## Next Steps

**Explore Advanced Features**:
- [Filters](../features/filters.md) - Sync only specific records
- [Delete Protection](../features/additional-features/delete-protection.md) - Prevent accidental deletions
- [View Sync](../connectors/airtable/airtable-view-sync.md) - Sync filtered views instead of entire tables

**Get Inspired**:
- Check out [Use Case Templates](../use-cases/README.md) for implementation ideas
- Browse [Popular Syncs](../popular-syncs/webflow-+-airtable.md) to see what others are building

**Need Help?**:
- Review the [FAQ](../resources/support/faq.md) for common questions
- Check the [Troubleshooting Guide](../troubleshooting-guide.md) for solutions
- Contact support through your dashboard
