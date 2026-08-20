---
description: A quick tutorial on how to sync a Postgres (or Supabase) view with Whalesync
---

# How to sync Postgres views

Whalesync can't modify Postgres views safely, so it won't create its usual primary key column on a view the way it does for regular tables. Views still need a unique column for tracking each record — you add it yourself, and this page shows how.

## What Whalesync looks for

A column on the **view itself** named exactly `whalesync_postgres_id` (all lowercase). That's the only thing Whalesync checks for — it doesn't matter whether the column comes from the underlying table, an alias, or an expression.

Once the column exists, click **Refresh tables** in Whalesync and the view is ready to sync.

## What the column's values must satisfy

Whalesync uses this column as the ID of each record, so its values must be:

1. **Unique** — no two rows of the view ever share a value.
2. **Non-null** — every row has a value.
3. **Stable** — a row keeps the same value for its whole life. The value must never change when the row is updated.

Any column type works (`uuid`, `integer`, `bigint`, `text`, …) as long as the values meet those three rules. Whalesync does not validate them up front: duplicates, nulls, or changing values will cause records to be skipped, merged together, or treated as deleted and re-created during sync.

## Option 1: expose an existing column (no changes to the underlying table)

If the underlying table already has a compatible column — typically its primary key — you don't have to modify the table at all. Append it to the view's select list under the required name:

```sql
CREATE OR REPLACE VIEW public.my_view AS
SELECT
  t.name,
  t.created_at,
  t.id AS whalesync_postgres_id  -- existing unique, non-null, stable column
FROM public.my_table t;
```

Note: `CREATE OR REPLACE VIEW` can only **append new columns at the end** of the view's column list — it can't rename or reorder existing output columns. Adding `t.id AS whalesync_postgres_id` as a new last column works even if the view already exposes `t.id` under another name. If you need to restructure the view instead, `DROP VIEW` and recreate it (watch out for dependent objects).

### Views over joins or aggregates

If the view joins tables or groups rows so that no single base-table column is unique per view row, build a stable composite value from the keys that define each row:

```sql
CREATE OR REPLACE VIEW public.my_view AS
SELECT
  o.placed_at,
  c.name,
  (o.id::text || ':' || c.id::text) AS whalesync_postgres_id
FROM public.orders o
JOIN public.customers c ON c.id = o.customer_id;
```

This is unique and stable as long as the combined keys are.

## Option 2: add a new column to the underlying table

If no existing column qualifies, add the same column Whalesync would create on a regular table, then include it in the view:

```sql
ALTER TABLE public.my_table
  ADD COLUMN whalesync_postgres_id uuid NOT NULL DEFAULT gen_random_uuid() UNIQUE;

CREATE OR REPLACE VIEW public.my_view AS
SELECT
  t.name,
  t.created_at,
  t.whalesync_postgres_id
FROM public.my_table t;
```

## Let an AI assistant write the query for you

Copy the prompt below into Claude Code (or another AI assistant) along with your view definition, then run the SQL it returns in the Supabase SQL editor or your Postgres client.

> Read https://docs.whalesync.com/connectors/postgres/how-to-sync-postgres-views.md for context.
> My Postgres view needs a column named exactly `whalesync_postgres_id`. Its values must be unique across all rows of the view, never null, and never change for the life of a row — Whalesync reads it as each record's ID.
>
> Prefer exposing an existing compatible column (such as the underlying table's primary key) by appending it to the view's select list as `AS whalesync_postgres_id`. Remember that `CREATE OR REPLACE VIEW` can only append new columns at the end of the column list. If the view joins or aggregates tables so that no single column is unique per row, build a stable composite value from the keys that define each row. Only if nothing compatible exists, add a column `whalesync_postgres_id uuid NOT NULL DEFAULT gen_random_uuid() UNIQUE` to the underlying table and include it in the view.
>
> Here is my view definition:
>
> ```sql
> -- paste the SQL definition of your view here
> ```
>
> Give me the SQL to run, and tell me which existing column you chose and why it satisfies the uniqueness, non-null, and stability requirements.

To get your view's definition, run:

```sql
SELECT pg_get_viewdef('public.my_view'::regclass, true);
```

(or copy it from the Supabase dashboard under Database → Views).

## After adding the column

Go back to Whalesync and click **Refresh tables**. The view will drop out of the "needs setup" state and can be mapped and synced like any other table.


## Video Tutorial

{% hint style="warning" %}
This video tutorial is a little out of date and may not match the current UI. It also only covers the approach of adding a column to the underlying table.
{% endhint %}

{% embed url="https://www.loom.com/share/7e33536a9c224120999cfb5b0d274174?sid=1c152ef0-0f51-4243-b093-b38e5f327bc2" %}
