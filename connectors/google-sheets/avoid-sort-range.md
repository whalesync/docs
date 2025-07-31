---
description: Sheet's "sort range" feature will cause sync problems
---

# Avoid sort range

<figure><img src="../../.gitbook/assets/Sort range.png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
Avoid using "sort range" on Sheets that are syncing.
{% endhint %}

#### Why to avoid sort range?

* To sync your data, Whalesync needs an "ID" for each of your records.
* Google Sheets doesn't have a concept of "record IDs", so Whalesync adds one with a `Whalesync ID` column
* Using "Sort range" can lead to scrambling all the Whalesync IDs in your rows if the Whalesync ID column is not included in the sort.
* This which will lead to unintended changes to your data.

**How to use sort range safely**

* If you must use sort range, be sure to include the Whalesync ID column in your sort range to avoid unintended changes.
