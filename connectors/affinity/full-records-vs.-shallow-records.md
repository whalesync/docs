---
description: Understanding what a "shallow record" is in Affinity
---

# Full records vs. shallow records

Unless you are on Affinity's Enterprise plan, Affinity has significant API limitations which limits our ability to sync all records. To work around this, Whalesync groups your records into two categories:

* Records you care about (full records)
* Records you don't care about (shallow records)

#### Affinity API limits

Affinity has the following API quota limits on its plans:

* Starter = none
* Premium = 100,000 calls/mo
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
