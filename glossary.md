---
description: Key terms and concepts used in Whalesync documentation
---

# Glossary

Understanding these key terms will help you get the most out of Whalesync and this documentation.

## Core Concepts

**Two-Way Sync**  
Data changes in either app automatically update the other app. This is Whalesync's primary feature.

**One-Way Sync**  
Data flows in only one direction. Changes in the source app update the destination, but not vice versa.

**Field Mapping**  
The process of connecting fields between two apps so they sync together. For example, mapping "Name" in Airtable to "Title" in Webflow.

**Connector**  
The integration that allows Whalesync to connect to a specific app or platform (e.g., Airtable connector, Webflow connector).

**Sync Direction**  
Specifies which way data flows between apps:
- `A → B`: Only changes from A update B
- `A ↔ B`: Changes in either A or B update the other

## Technical Terms

**API (Application Programming Interface)**  
How Whalesync communicates with your apps to read and write data.

**API Key**  
A secret code that gives Whalesync permission to access your data in certain apps.

**OAuth**  
A secure authorization method where you log into your account directly (no need to share passwords).

**Webhook**  
A way for apps to instantly notify Whalesync when data changes, enabling real-time sync.

**Record**  
A single row of data, like one contact, one product, or one blog post.

**Table**  
A collection of records with the same structure. Also called a "database" or "collection" in some apps.

**Field**  
A single piece of information, like a name, email, or date. Also called a "column" or "property."

## Field Types

**Text Field**  
Stores plain text information like names, descriptions, or notes.

**Number Field**  
Stores numeric values like prices, quantities, or scores.

**Date/DateTime Field**  
Stores dates and times with proper formatting.

**Attachment/File Field**  
Stores uploaded files, images, or documents.

**Single Select**  
Allows choosing one option from a predefined list (like a dropdown menu).

**Multi-Select**  
Allows choosing multiple options from a predefined list.

**Checkbox/Boolean**  
Stores true/false or yes/no values.

**Linked Records/Foreign Key**  
References records in other tables, creating relationships between data.

**Formula/Calculated Field**  
Automatically calculates values based on other fields. Usually read-only.

**Synthetic Field**  
Special fields that Whalesync creates to provide additional data like record IDs or creation timestamps.

## Sync Features

**Record Matching**  
How Whalesync identifies which records in different apps should sync together.

**Delete Protection**  
A safety feature that prevents records from being accidentally deleted during sync.

**View Sync**  
Syncing only records that match specific filters or views instead of entire tables.

**Auto-Create Tables**  
Automatically creating new tables/collections when they don't exist in the destination app.

**Operations**  
A log of all sync activities showing what data was created, updated, or deleted.

**Issues**  
Error messages and warnings that occur during syncing, helping you troubleshoot problems.

**Filters**  
Rules that determine which records should be included in the sync.

## App-Specific Terms

### Airtable
- **Base**: A database containing multiple tables
- **View**: A filtered/sorted display of table data
- **Linked Records**: References to records in other tables

### Notion
- **Database**: A collection of pages with properties
- **Page**: An individual record/item
- **Property**: A field/column in a database

### Webflow
- **CMS Collection**: A dynamic content database
- **CMS Item**: A single piece of content
- **Site**: A Webflow website project

### HubSpot
- **Contact**: A person in your CRM
- **Deal**: A sales opportunity
- **Company**: An organization record
- **Association**: A relationship between different record types

### Databases (Postgres/Supabase)
- **Schema**: The structure defining tables and relationships
- **Primary Key**: A unique identifier for each record
- **Foreign Key**: A reference to a record in another table
- **View**: A saved query that looks like a table

## Common Abbreviations

**CRM**: Customer Relationship Management  
**CMS**: Content Management System  
**API**: Application Programming Interface  
**OAuth**: Open Authorization  
**CRUD**: Create, Read, Update, Delete  
**JSON**: JavaScript Object Notation (a data format)  
**CSV**: Comma-Separated Values (a file format)  
**URL**: Uniform Resource Locator (web address)

## Getting Help

If you encounter unfamiliar terms not listed here:

- Check the specific connector documentation for app-specific terminology
- Review the [FAQ](resources/support/faq.md) for common questions
- Use the search function to find relevant documentation
- Contact support through your Whalesync dashboard

{% hint style="info" %}
This glossary focuses on terms used in Whalesync documentation. Each connected app may have additional specific terminology in their own documentation.
{% endhint %}