---
cover: ../../.gitbook/assets/gitbook-cover_salesforce.jpg
coverY: 0
---

# Salesforce

## Salesforce Connector Guide

This guide provides an overview of how to connect Whalesync to Salesforce and answers common questions.

### Connecting to Salesforce

To connect Salesforce to Whalesync, you will need to authenticate using your Salesforce account. This process uses OAuth 2.0, a standard and secure method for authorization.

When you set up a new Salesforce connection, you will be prompted to log in to your Salesforce account. After logging in, Salesforce will ask you to grant Whalesync permission to access your data. The data that Whalesync can access is determined by the permissions of the Salesforce user who authorizes the connection. We recommend using a Salesforce account with administrative privileges to ensure Whalesync has access to all the objects and fields you intend to sync.

To connect to a Salesforce sandbox instead of your production org, check the "Use sandbox" box when authenticating.

### Syncing Data

#### Salesforce Views

Salesforce allows you to create "Views" to segment your data within an object. For example, you can create a view of "New Leads" in your Leads object. Whalesync can sync with a specific Salesforce View. When setting up your sync, you can choose a view for each Salesforce object you want to sync. This will restrict the synced records to only those that appear in the selected view.

If you do not select a specific view, Whalesync will sync all records in the object.

Please note that some Salesforce objects, such as `Profile` and `RecordType`, do not support views. For these objects, Whalesync will sync all records.

### Things to Keep in Mind

* **Beta Connector**: The Salesforce connector is currently in beta. We are continuously working to improve it.
* **Permissions**: Whalesync's access to your Salesforce data is based on the permissions of the Salesforce user who sets up the connection. If you are unable to see certain objects or fields in Whalesync, ensure the connected user account has the necessary permissions in Salesforce.
* **Backups**: We strongly encourage you to have a backup and restore strategy for your Salesforce data. Two-way data sync is powerful, and having backups provides an extra layer of safety. Salesforce offers backup solutions which you can explore.
* **Restricted Picklists**: If you try to sync a new value to a Salesforce picklist field that has a restricted set of options, you will encounter an error. To resolve this, you can either add the new value as an option to the picklist in your Salesforce settings or remove the restriction from the field.
* **Deleting Records**: Salesforce prevents the deletion of records that are linked to other records through a relationship. For example, you cannot delete an Account if it is still linked to Opportunities. If you encounter an error when trying to delete a record, you will first need to remove its associations with other records in Salesforce.
* **API Usage**: Syncing data uses Salesforce API calls. Salesforce accounts have API call limits based on their edition and number of user licenses. While Whalesync is optimized to use the API efficiently, very large syncs or frequent updates may contribute significantly to your API usage. You can monitor your API usage in the "Company Information" section of your Salesforce setup.
* **Formula Fields**: Formula fields in Salesforce are read-only. Whalesync can read data from these fields, but cannot write data to them.
* **Encrypted Text Fields**: Whalesync supports Encrypted Text fields. Please note that these fields are "write-once", meaning that after a value has been set, it cannot be updated via the API.

### Synthetic Fields

Whalesync adds a few read-only fields to your data to help manage the sync. These fields are "synthetic," meaning they are not part of your original Salesforce data but are added by Whalesync.

| Field Name             | Explanation                                                                            | Writable |
| ---------------------- | -------------------------------------------------------------------------------------- | -------- |
| `Salesforce Record ID` | The unique identifier for a record from Salesforce. This is the Salesforce `Id` field. | No       |

### Supported Objects and Fields

Whalesync supports a wide variety of Salesforce objects and fields.

#### Supported Objects

| Tables                       | Status                         |
| ---------------------------- | ------------------------------ |
| 👤 Account                   | ✅ Supported                    |
| 📊 Campaign                  | ✅ Supported                    |
| :bar\_chart: Campaign Member | ✅ Supported                    |
| :briefcase: Case             | :white\_check\_mark: Supported |
| 👤 Contact                   | ✅ Supported                    |
| 🧳 Custom Object             | ✅ Supported                    |
| 👤 Lead                      | ✅ Supported                    |
| 📈 Opportunity               | ✅ Supported                    |
| 👤 Profile                   | :white\_check\_mark: Supported |
| :e-mail: RecordType          | :white\_check\_mark: Supported |
| ✅ Task                       | ✅ Supported                    |
| 👤 User                      | ✅ Supported                    |

#### Supported Fields

| Fields                          | Status      |
| ------------------------------- | ----------- |
| 💵 Auto Number                  | ✅ Supported |
| 📝 Formula                      | ✅ Supported |
| 🔎 Lookup Relationship          | ✅ Supported |
| 🤝 Master-Detail Relationship   | ✅ Supported |
| 🔎 External Lookup Relationship | ✅ Supported |
| ✅ Checkbox                      | ✅ Supported |
| 💵 Currency                     | ✅ Supported |
| 📅 Date                         | ✅ Supported |
| 🕕 Date/Time                    | ✅ Supported |
| 📧 Email                        | ✅ Supported |
| 🗺️ Geolocation                 | ✅ Supported |
| #️⃣ Number                      | ✅ Supported |
| % Percent                       | ✅ Supported |
| ☎️ Phone                        | ✅ Supported |
| 🗒️ Picklist                    | ✅ Supported |
| 🗒️ Picklist (Multi-Select)     | ✅ Supported |
| 📘 Text                         | ✅ Supported |
| 📘 Text Area                    | ✅ Supported |
| 📘 Text Area (Long)             | ✅ Supported |
| 📘 Text Area (Rich)             | ✅ Supported |
| 📘 Text (Encrypted)             | ✅ Supported |
| 🕧 Time                         | ✅ Supported |
| 🔗 URL                          | ✅ Supported |
