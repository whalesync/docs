---
description: How to choose an ID column when using a Supabase or Postgres view as a Live Export source
---

# Using Supabase or Postgres views as a source

When you use Supabase or Postgres as a Live Export source, you can pick database **views** as a read-only source alongside your regular tables. (Supabase runs on Postgres, so this applies to you too.) Views are a great way to reshape, filter, or join your data before it's copied to the destination.

There's one catch: views need a little help before Whalesync can copy them.

## Why Whalesync needs an ID column

To copy a source into your destination, Whalesync needs a way to uniquely identify each row so it can tell records apart and match every record back to the same row on each run.

Regular tables usually have a primary key, so Whalesync uses that automatically. Views are different. A Supabase or Postgres view is a saved query, not a stored table, so it doesn't carry a primary key and the database can't guarantee that any of its columns are unique. Even if a column looks like an ID, the view has no constraint enforcing it.

Because of this, when you add a view Whalesync asks you to **choose an ID column** yourself. Pick the column whose value identifies a row. Every record is matched back to the view through it on each run.

## Requirements for the ID column

The column you choose must meet two rules:

- **Unique across every row.** No two rows can ever share the same value. If two rows do end up with the same value, this table stops syncing until the view is fixed.
- **Never empty.** The value must always be populated. A blank or `null` ID can't be used to identify a row and will cause errors on a later run.

Whalesync can't verify these rules for you ahead of time, since the view has no constraints to check against. It's up to you to pick a column whose values are guaranteed to stay unique and populated for every row, now and as your data grows.

{% hint style="warning" %}
**You can't change the ID column later.** To use a different column, remove the table from the Live Export and add it again.
{% endhint %}

## How to choose an ID column

Good options are columns that are already unique and always present, such as:

- A primary key that the view passes straight through from an underlying table.
- A unique identifier like an email, slug, or external ID that your data guarantees is always filled in.

If no single column is unique on its own, update the view's query to produce one. A common approach is to build a stable identifier in SQL, for example combining two columns that are unique together, or exposing the underlying table's primary key in the view's `SELECT`. Whatever you choose, make sure it will stay unique and never be empty for every row the view returns.
