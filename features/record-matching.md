---
description: Match records that already exist prior to turning on sync.
---

# Record matching

<figure><img src="../.gitbook/assets/record matching (1).gif" alt=""><figcaption><p>Using record matching to match contacts on the account name field across Salesforce and Airtable</p></figcaption></figure>



### About record matching

Before turning on sync, you may already have data in both of your apps. For example, if syncing Salesforce and Postgres, you may might have contact records in each:

<figure><img src="../.gitbook/assets/contacts data.png" alt=""><figcaption><p>Example where record matching will be helpful since data already exists in both apps</p></figcaption></figure>

With record matching, you can tell Whalesync how to match and merge these records when you turn on sync for the first time.

In this example, we might match on the `email` field since that field is unique for each record.

{% hint style="info" %}
Note - record matching only runs during the initial sync to match records that existed prior to activating your sync.
{% endhint %}

### Overwrite conflicting fields

Sometimes matched records do not have the exact same data in every field. In these cases, you can choose which app's data should take precedence.

<figure><img src="../.gitbook/assets/recrod matching - overwrite.png" alt=""><figcaption><p>Here the user has chosen to treat Salesforce as the source of truth for conflicting values in matched records</p></figcaption></figure>

### Advanced settings

We strongly suggest matching with unique fields (like IDs) wherever possible. If you match on a non-unique, Whalesync will alert you to any records that cannot be matched because they are not unique.

<figure><img src="../.gitbook/assets/record matching advanced record matching.png" alt=""><figcaption><p>Example where two records in Airtable have the same value in the "Email" field so they cannot be matched</p></figcaption></figure>

In these cases you can optionally add a second matching column. This tells Whalesync to first try to match records on the first column, then try to match records on the second column.

Alternatively, you can move past this screen even if you have non-unique values but be aware that those records will not be able to be matched which can result in unwanted duplicates.
