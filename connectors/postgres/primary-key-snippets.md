---
description: Handy snippets to help you set up Postgres to work with Whalesync
---

# Primary key snippets

{% tabs %}
{% tab title="Primary Key - Create" %}
The best way to create the primary key is to define it as part of creating a table. In the example below, there are two options: one using UUIDs and another using integers as primary keys (the latter is commented out). In both cases the primary key is set to auto-generate a key when a record is inserted into the table.

{% code overflow="wrap" %}
```sql
CREATE TABLE public."Table" (
"id" uuid PRIMARY KEY DEFAULT gen_random_uuid(),
--id serial PRIMARY KEY,
"description" text,
"is_published" boolean );
```
{% endcode %}
{% endtab %}

{% tab title="Primary Keys – Alter" %}
If the table already exists and you want to change the primary key, you'll need to remove the old one and add a new one.

```sql
-- Delete the old primary key.
ALTER TABLE public."Table" 
DROP COLUMN "id";
-- Add a new generated primary key.
ALTER TABLE public."Table" 
ADD COLUMN "uuid" uuid PRIMARY KEY DEFAULT gen_random_uuid();
```

If the table already exists and you already have a generated key and want to designate it as a primary key.

```sql
ALTER TABLE public."Table"
ADD CONSTRAINT table_pk PRIMARY KEY ("uuid");
```

_\*Supabase blocks access to altering a table outside of its UI, thus please use Supabase's UI._
{% endtab %}

{% tab title="Primary Key – Generate" %}
Whalesync requires that the primary key is generated (i.e. has an automatic default value). These are a few examples of functions that would generate data for you:

```
uuid_genetate_v4()
```

```
gen_random_uuid()
```

```
nextval('column_name')
```

We also support serial integers as the primary column (these are self-incrementing integers and equivalent to using the `nextval` function).
{% endtab %}
{% endtabs %}
