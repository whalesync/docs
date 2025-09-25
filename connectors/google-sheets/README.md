---
cover: ../../.gitbook/assets/gitbook-cover_google-sheets.jpg
coverY: 0
---

# Google Sheets

## Google Sheets Connector Guide

This guide provides an overview of how to connect Whalesync to Google Sheets and answers common questions.

### Connecting to Google Sheets

To connect Whalesync to Google Sheets, you will need to authenticate your Google account. Whalesync uses OAuth, a secure standard that allows you to grant access to your Google Sheets without sharing your password.

When you set up Google Sheets in Whalesync, you will be prompted to:

1. Provide the URL of your sheet
2. Sign in to your Google account.
3. Grant Whalesync permission to access your spreadsheets. This permission allows Whalesync to read and write data according to your sync configuration.

Once authenticated, you can select the specific spreadsheet you want to sync.

### Syncing Data

**Sheets (tabs)**

Whalesync uses the name of a sheet (i.e. a tab in a workbook) for syncing. Avoid changing the name of a sheet after setting up your sync, as this will break the sync configuration.

**Rows**

Whalesync uses the first row to define the fields for syncing. By default, Whalesync freezes the first row to preserve this mapping.

Don't delete or move the first row. Altering it will cause sync problems because Whalesync uses it to map your data. After the initial sync, you're free to reorder rows or columns—just keep the first row unchanged.

**Columns**

Whalesync adds a "Whalesync ID" column to your sheet to enable syncing. This column is automatically created in column A and is used to track records.

You are free to rename other columns after setting up a sync. Avoid editing the "Whalesync ID" column to prevent sync errors.

### Formatting Special Fields in Google Sheets

To use special field types like relations (linked records), multi-select dropdowns, or checkboxes, you format the column headers in your Google Sheet in a specific way. Whalesync detects these formats and configures the fields accordingly.

* **Relation (Linked Record) Fields**: To link records to another table (sheet), name your column header using the format `Related_TableName`. For example, in a "Tasks" sheet, to create a field that links to a sheet named "Users", the column header should be `Related_Users`. The table name in the header must exactly match the name of the sheet you are linking to, including capitalization, as described in the [foreign keys documentation](https://docs.whalesync.com/connectors/google-sheets/foreign-keys).
* **Multi-Select Fields**: To create a multi-select field, prefix the column name with `multi_`. For example, a column named `multi_Tags` will be treated as a multi-select field. [Read more about multi-select fields here](multi-select-fields.md).
* **Checkbox (Boolean) Fields**: To create a checkbox field, prefix the column name with `boolean_`. For example, a column named `boolean_Is Active` will be treated as a checkbox that stores TRUE/FALSE values.
* **Other Field Types:** See [the page on formatting columns and field types](formatting-columns.md) for more information on how to ensure your columns are set up correctly.

### Things to Keep in Mind

⚠️ Before syncing Google Sheets some things to note before turning on syncing.

**Do not use the "Sort range" feature on sheets that are syncing!** This action will cause sync problems as it can change the internal row IDs that Whalesync relies on.

Whalesync uses the first row of Google Sheets for sync mapping. Do not delete or move it to avoid issues.

{% hint style="warning" %}
When syncing with Google Sheets, ensure that the Sheet you’re connecting isn’t already used in another sync. Setting up multiple syncs using the same Sheet can lead to conflicts and issues in syncing.
{% endhint %}

### Synthetic Fields

Whalesync adds special read-only fields to your tables that contain metadata about the sync. These fields provide useful information but are managed by Whalesync and cannot be edited.

| Field Name              | Explanation                                                                                                                        | Writable |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------- | -------- |
| Google Sheets Record ID | A unique identifier Whalesync uses to track each row. This column is located in column A of your sheet and labeled "Whalesync ID". | No       |

### Supported Fields

| Field         | Status               |
| ------------- | -------------------- |
| 📝Text        | ✅ Supported          |
| 🔢 Number     | ✅ Supported          |
| 📅 Date       | ✅ Supported          |
| #️⃣Percentage | ✅ Supported          |
| 💰 Currency   | ✅ Supported          |
| 📧 Email      | ✅ Supported          |
| 📜 Drop-Down  | ✅ Supported          |
| 🗳️ Checkbox  | ➡️ Supported (1-Way) |
| Relation      | ✅ Supported          |

## Video Guide <a href="#h_bccce14d8a" id="h_bccce14d8a"></a>

{% embed url="https://youtu.be/ledVk0ck-Vc" %}
A quick video demo for how to sync Google Sheets and Airtable
{% endembed %}



