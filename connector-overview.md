---
description: Compare features and capabilities across different connectors
---

# Connector Overview

This overview helps you understand the capabilities of different Whalesync connectors and choose the best apps for your use case.

## Connector Categories

### 📊 Spreadsheets & Databases
| App | Sync Speed | Two-Way Sync | Auto-Create | Best For |
| --- | --- | --- | --- | --- |
| **Airtable** | Real-time | ✅ Full | ✅ Yes | Rich databases with views and formulas |
| **Google Sheets** | ~1-5 min | ✅ Full | ❌ No | Simple spreadsheets, team collaboration |
| **Notion** | Real-time | ✅ Full | ✅ Yes | All-in-one workspace, documentation |
| **Postgres** | Real-time | ✅ Full | ✅ Yes | Production databases, complex queries |
| **Supabase** | Real-time | ✅ Full | ✅ Yes | Modern app backend, real-time features |

### 🌐 Website & Content Management
| App | Sync Speed | Two-Way Sync | Auto-Create | Best For |
| --- | --- | --- | --- | --- |
| **Webflow** | Real-time | ✅ Full | ✅ Yes | Designer websites, CMS collections |
| **WordPress.org** | Real-time | ✅ Full | ❌ No | Blog posts, custom post types, ACF |
| **Wix CMS** | Real-time | ✅ Full | ✅ Yes | Wix website dynamic content |

### 📈 CRM & Sales
| App | Sync Speed | Two-Way Sync | Auto-Create | Best For |
| --- | --- | --- | --- | --- |
| **HubSpot** | Real-time | ✅ Full | ❌ No | Complete CRM, marketing automation |
| **Salesforce** | Real-time | ✅ Full | ❌ No | Enterprise CRM, complex sales processes |
| **Affinity** | Real-time | ✅ Full | ❌ No | Investor relations, deal flow management |
| **Attio** | Real-time | ✅ Full | ❌ No | Modern CRM, relationship mapping |

### 💳 E-commerce & Payments  
| App | Sync Speed | Two-Way Sync | Auto-Create | Best For |
| --- | --- | --- | --- | --- |
| **Stripe** | Real-time | ➡️ One-way | ❌ No | Payment data, customer records |

### 👥 User Management
| App | Sync Speed | Two-Way Sync | Auto-Create | Best For |
| --- | --- | --- | --- | --- |
| **Memberstack** | Real-time | ✅ Full | ❌ No | Website memberships, user management |

## Feature Comparison

### Real-time Sync Support
**Real-time (via webhooks)**: Airtable, Notion, Webflow, HubSpot, Salesforce, most modern SaaS apps  
**Polling-based (1-5 min delay)**: Google Sheets, some database connections  

### Field Type Support

#### Rich Content
- **Best**: Notion (blocks), Airtable (rich text), Webflow (rich text)
- **Good**: WordPress.org (blocks), Google Sheets (basic)
- **Limited**: Most CRMs (plain text only)

#### Attachments/Images
- **Supported**: Airtable, Notion, Webflow, WordPress.org
- **Coming Soon**: Some newer connectors
- **Not Supported**: Google Sheets, most CRMs

#### Linked Records/Relationships
- **Advanced**: Airtable (linked records), Notion (relations), Postgres (foreign keys)
- **Basic**: HubSpot (associations), Salesforce (lookups)
- **Limited**: Google Sheets (text references)

## Popular Combinations

### Content Marketing
- **Airtable + Webflow**: Programmatic SEO, dynamic websites
- **Notion + WordPress**: Content planning and publishing  
- **Google Sheets + Webflow**: Simple content management

### Sales & CRM
- **HubSpot + Notion**: Deal tracking in familiar interface
- **Salesforce + Airtable**: Enhanced reporting and analysis
- **Affinity + Google Sheets**: Investor-friendly deal sharing

### App Development  
- **Supabase + Airtable**: Admin interface for app data
- **Postgres + Notion**: Database documentation and management
- **Memberstack + Airtable**: User management dashboard

### E-commerce
- **Stripe + Airtable**: Customer and payment analysis
- **Webflow + Airtable**: Product catalog management

## Choosing Your Stack

### For Simple Use Cases
**Recommendation**: Google Sheets + any business app  
**Why**: Familiar interface, easy team access, no learning curve

### For Rich Data Management  
**Recommendation**: Airtable + business app  
**Why**: Powerful views, formulas, attachment support, great UI

### For Documentation & Collaboration
**Recommendation**: Notion + business app  
**Why**: All-in-one workspace, great for team workflows

### For Production Apps
**Recommendation**: Postgres/Supabase + admin interface  
**Why**: Reliable, scalable, real-time capabilities

### For Content Websites
**Recommendation**: Airtable/Notion + Webflow  
**Why**: Content management + beautiful websites

## Getting Started

1. **Identify your primary need**: Content, CRM, e-commerce, app data, etc.
2. **Choose your "source of truth"**: Where will you primarily manage data?
3. **Pick complementary tools**: What do you need the synced data for?
4. **Start simple**: Begin with basic field mappings, add complexity later
5. **Test with sample data**: Validate your sync before going live

## Need Help Choosing?

- Check out [Use Case Templates](../use-cases/README.md) for specific implementation guides
- Review [Popular Syncs](../popular-syncs/webflow-+-airtable.md) for proven combinations  
- Read individual connector documentation for detailed capabilities
- Contact support for personalized recommendations

{% hint style="info" %}
This overview covers current capabilities. New connectors and features are added regularly - check the changelog for updates!
{% endhint %}