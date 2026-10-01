---
description: >-
  Why Whalesync syncs Affinity records as shallow records with only a name and
  email by default, and how to fully sync a list to get every field.
---

# Full records vs. shallow records

Unless you are on Affinity's Enterprise plan, Affinity has significant API limitations which limits our ability to sync all records. To work around this, Whalesync groups your records into two categories:

* Records you care about (full records)
* Records you don't care about (shallow records)

#### Affinity API limits

Affinity has the following [monthly API limits](https://developer.affinity.co/pages/external-api-v2/rate-limits) on its plans:

* Essentials = none (no API access)
* Scale = 100,000 calls/mo
* Advanced = 100,000 calls/mo
* Enterprise = unlimited

**Difference between full records and shallow records**

Full records include every field you want to sync:

<figure><img src="../../.gitbook/assets/Full Records.png" alt=""><figcaption></figcaption></figure>

Shallow records only include the display name and email address (if applicable):

![](<../../.gitbook/assets/Shallow Records.png>)

#### How to sync full records

By default, Whalesync will sync records as shallow records. If you want to fully sync a group of records you must:

1. Add them to at least one list
2. Select to fully sync that list on the table mapping screen

<figure><img src="../../.gitbook/assets/Screenshot 2024-11-28 at 4.01.41 AM.png" alt=""><figcaption><p>Open table settings on the table mapping screen</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/Screenshot 2024-11-28 at 4.01.55 AM.png" alt=""><figcaption><p>Add the lists you want to fully sync</p></figcaption></figure>
