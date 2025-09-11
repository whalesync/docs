---
description: Common use case templates and implementation guides
---

# Use Case Templates

These templates show you exactly how to implement popular Whalesync use cases. Each template includes field mappings, sync settings, and best practices.

## Content & Marketing

### 📝 Programmatic SEO Pages
**Apps**: Webflow + Airtable  
**Use Case**: Generate hundreds of pages automatically from a data source

**Setup**:
1. Create an Airtable base with columns: `Page Title`, `Slug`, `Meta Description`, `Content`, `Published Status`
2. In Webflow, create a CMS collection with matching fields
3. Map fields with sync direction: `Airtable → Webflow`
4. Use filters to only sync records where `Published Status = "Live"`

**Pro Tips**:
- Use Airtable formulas to generate slugs automatically
- Set up view filters in Airtable to preview pages before publishing
- Enable delete protection to prevent accidental page removal

### 🎯 Content Calendar Management
**Apps**: Notion + Airtable  
**Use Case**: Manage content pipeline with team collaboration

**Field Mappings**:
- `Content Title` ↔ `Title`
- `Due Date` ↔ `Publish Date`
- `Status` ↔ `Status` (Draft, In Review, Published)
- `Assigned Writer` ↔ `Author`
- `Tags` ↔ `Categories`

**Sync Settings**: Two-way sync with filters on status

## Sales & CRM

### 💼 Deal Tracking in Spreadsheets  
**Apps**: HubSpot + Notion  
**Use Case**: Let team view and update deals in a familiar spreadsheet format

**Key Fields**:
- `Deal Name` ↔ `Deal Title`
- `Amount` ↔ `Deal Value`
- `Close Date` ↔ `Expected Close`
- `Deal Stage` ↔ `Status`
- `Contact` ↔ `Primary Contact`

**Settings**: 
- Sync Direction: Two-way
- Filter: Only sync deals in active stages
- Enable delete protection

### 📊 Investment Deal Management
**Apps**: Affinity + Google Sheets  
**Use Case**: Let investors update deal information directly in sheets

**Setup Strategy**:
1. Use one-way sync from Affinity to Sheets for deal discovery
2. Set up two-way sync for specific editable fields like notes and status
3. Keep sensitive fields (valuations, terms) as read-only

## E-commerce & Operations

### 🛍️ Product Catalog Management
**Apps**: Shopify + Airtable  
**Use Case**: Manage product information and inventory in Airtable

**Field Mappings**:
- `Product Title` ↔ `Name`
- `Description` ↔ `Description` 
- `Price` ↔ `Price`
- `Inventory` ↔ `Stock Level`
- `Product Type` ↔ `Category`
- `Images` ↔ `Product Images` (attachment field)

**Best Practices**:
- Use Airtable's rich formatting for product descriptions
- Set up inventory alerts with Airtable formulas
- Use linked records for variants and categories

### 📦 Order Management Dashboard
**Apps**: Postgres + Airtable  
**Use Case**: Create visual dashboards for order data

**Implementation**:
1. Sync order data from Postgres to Airtable 
2. Use Airtable views for different order statuses
3. Create dashboard views for team members
4. Set up automation for order status updates

## Internal Tools

### 👥 User Management System
**Apps**: Supabase + Airtable  
**Use Case**: Manage app users with admin interface

**Core Tables**:
- **Users**: Basic user information and status
- **Subscriptions**: User plan and billing status  
- **Support Tickets**: Customer service integration

**Field Strategy**:
- One-way sync for user data (database → Airtable)
- Two-way sync for admin actions (status changes, notes)
- Read-only sync for sensitive data (passwords, payment info)

### 🏢 Company Directory
**Apps**: Notion + Google Sheets  
**Use Case**: Maintain company directory accessible to all staff

**Features**:
- Two-way sync for basic contact information
- Department filtering and views
- Integration with Google Workspace for easy access
- Photo syncing via attachment fields

## Getting Started with Templates

### 1. Choose Your Template
Pick the use case that most closely matches your needs. You can always modify the setup later.

### 2. Prepare Your Data
- **Clean your data**: Remove duplicates and ensure consistent formatting
- **Plan your fields**: Identify which fields need two-way sync vs. one-way
- **Set up filters**: Decide which records should be included in the sync

### 3. Test with Sample Data
- Start with 10-20 records to test your setup
- Verify field mappings work correctly
- Test both directions if using two-way sync

### 4. Scale Up Gradually
- Add more records in batches
- Monitor the Operations page for any issues
- Adjust field mappings as needed

## Advanced Tips

### Performance Optimization
- **Use filters**: Only sync the data you need
- **Batch updates**: Make multiple changes at once when possible
- **Monitor API limits**: Check your source app's API quotas

### Data Safety
- **Enable delete protection**: Prevent accidental data loss
- **Regular backups**: Keep backups of critical data
- **Test destructive operations**: Always test with sample data first

### Team Management
- **Access controls**: Set appropriate permissions in both apps
- **Training**: Ensure team knows which app to edit for different fields
- **Documentation**: Keep notes on your sync configuration

## Need Help?

- Check our [Field Compatibility Guide](../resources/support/field-compatibility.md) for detailed field mappings
- Review [Common Errors](../resources/support/) for troubleshooting
- Visit our [Quick Start Guide](../start-here/quick-start.md) for setup basics

{% hint style="info" %}
These templates are starting points. Every business is unique, so feel free to adapt them to your specific needs!
{% endhint %}