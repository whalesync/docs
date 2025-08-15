---
description: Setting to disable deletes in one of your tables for extra piece of mind
---

# Delete protection

Sometimes you're syncing data that you really want to ensure teammates don't accidentally delete (e.g. CRM data).

For these cases, you can set the table in Whalesync to not delete records.

<figure><img src="../../.gitbook/assets/Edit 4 (1).png" alt=""><figcaption><p>Delete protection means Whalesync will not delete records in HubSpot even with 2-way sync turned on</p></figcaption></figure>

### How it works

If you turn off deletes for a table, Whalesync will continue to 2-way sync all changes to that table _except_ deletes.

### How to turn off deletes in table settings

1. Edit your Whalesync base
2. Select the desired table
3. Click the **Advanced settings** tab
4. Set the **Delete Protection** field to enabled
5. Save changes

{% hint style="warning" %}
Do not forget step 5 or your table setting will not be saved!
{% endhint %}
