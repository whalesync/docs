---
description: Quick fixes for common sync issues and error troubleshooting
---

# Troubleshooting Guide

This guide helps you resolve common sync issues quickly. For connector-specific errors, check the detailed guides linked below.

## Quick Diagnostics

### 🔍 Check Sync Status
1. Go to your [Whalesync dashboard](https://www.whalesync.com/dashboard)
2. Check the **Operations** page to see recent sync activity
3. Check the **Issues** page for specific error messages

### ⚡ Common Quick Fixes

| Problem | Quick Fix |
| --- | --- |
| **Sync not starting** | Check if sync is activated in your dashboard |
| **Changes not syncing** | Verify field mappings and ensure fields are mapped correctly |
| **Partial data missing** | Check if you're using view sync with filters |
| **Webhook delays** | Some connectors don't support real-time webhooks - changes may take a few minutes |

## Field-Related Issues

### Field Type Compatibility
Not all field types can sync between different apps. Check our [Field Compatibility Guide](resources/support/field-compatibility.md) for detailed mappings.

### Common Field Issues
- **Attachment fields**: May change file names during sync
- **Formula/Calculated fields**: Usually read-only (one-way sync only)  
- **Multi-select fields**: Need compatible field types on both sides
- **Date/Time fields**: Check timezone settings if dates appear incorrect

## Authentication Issues

### API Key Problems
1. **Expired keys**: Refresh or regenerate API keys in your source app
2. **Permission issues**: Ensure the API key has read/write access to the tables you want to sync
3. **OAuth expiration**: Re-authorize the connection in your Whalesync dashboard

### Connection Troubleshooting
- **Database connections**: Check if your database is accessible from external IPs
- **Firewall issues**: Ensure Whalesync IP addresses are whitelisted if required
- **SSL/TLS issues**: Most connectors require secure HTTPS connections

## Performance & Limits

### API Rate Limits
Different platforms have different API limits:
- **Airtable**: Has strict rate limits, especially on free plans
- **Notion**: API calls are limited per workspace
- **Google Sheets**: Has daily quota limits

**Solution**: Consider upgrading your plan or reducing sync frequency for large datasets.

### Large Data Sets
For syncing large amounts of data (>10,000 records):
1. Start with a small subset to test your sync
2. Use filters to limit initial sync scope
3. Monitor the Operations page during initial sync

## Connector-Specific Troubleshooting

For detailed error messages and solutions specific to each connector:

### Popular Connectors
- [Airtable Common Errors](resources/support/common-errors-airtable.md)
- [Notion Common Errors](resources/support/common-errors-notion.md) 
- [Webflow Common Errors](resources/support/common-errors-webflow.md)
- [Postgres Common Errors](resources/support/common-errors-postgres.md)

### Other Resources
- [Known Issues](resources/support/known-issues.md) - Platform-wide known issues
- [Sync Behavior Questions](resources/support/sync-behavior-questions.md) - How sync behavior works
- [Troubleshooting Attachment Fields](resources/support/troubleshooting-attachment-fields.md) - File and image sync issues

## Data Safety

### Before Making Changes
- **Test with sample data** first when possible
- **Use filters** to limit sync scope initially  
- **Backup important data** before enabling two-way sync

### Delete Protection
Whalesync includes delete protection features. Learn more in [Delete Protection](features/additional-features/delete-protection.md).

## Still Need Help?

If you can't resolve your issue:

1. Check the [Operations](features/operations.md) and [Issues](features/issues.md) pages for specific error details
2. Review the [FAQ](resources/support/faq.md) for common questions
3. Contact support through your Whalesync dashboard

{% hint style="info" %}
When contacting support, include:
- Specific error messages from the Issues page
- Screenshots of your field mappings
- Details about when the issue started occurring
{% endhint %}