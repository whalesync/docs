---
description: Things to be aware of when syncing Affinity notes
---

{% hint style="warning" %}
**Archived:** This connector is no longer offered by Whalesync. Existing syncs will continue to run, but future improvements and support will be limited. See [Previous Connectors](../) for more details.
{% endhint %}

# Notes in Affinity

### Creating vs. editing

If you map the "Notes" table and intend to author notes in another tool such as Airtable or Notion, there's a limitation you should be aware of. When creating a brand new note in Affinity, Whalesync is able to set all the note's properties: its contents and which people/organizations/opportunities it's associated with.

However, when editing a note, Whalesync can **only** modify the contents of the note. It cannot change the people/organizations/opportunities it's associated with.

Therefore we recommend setting a long sync delay on the "Notes" table mapping such that Whalesync only creates notes in Affinity once you've had the chance to set the appropriate references.

<figure><img src="../../.gitbook/assets/Screenshot 2024-11-28 at 4.13.11 AM.png" alt=""><figcaption><p>Edit mapping options for the "Notes" table</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/Screenshot 2024-11-28 at 4.07.15 AM.png" alt=""><figcaption><p>Set a long delay on the source of the notes</p></figcaption></figure>

### Notes and rich text

Notes in Affinity are usually stored as rich text. Under the hood, Affinity's internal representation of notes is [Markdown](https://en.wikipedia.org/wiki/Markdown), a simple formatting language. When you create notes within Affinity's UI, Whalesync sees those notes as being formatted in Markdown. You can map the contents of notes to a rich text field in tool such as Airtable and the formatting will correctly be synced.

However, due to a bug in the Affinity API, Whalesync is only able to edit notes in Affinity as plain text. When you create rich text notes in another tool and they're synced to Affinity, they will show up with the raw Markdown formatting like this:

```
Hello World!
This is **bold**, _italic_, ~~strikethrough~~, and `code`.
Here is a [link](https://en.wikipedia.org/wiki/Whale).
```
