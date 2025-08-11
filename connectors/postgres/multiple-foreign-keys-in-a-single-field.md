---
description: >-
  This describes how to sync a multi-foreign key field in another app (e.g. Airtable) to Postgres or Supabase
---

# Multiple foreign keys in a single field

### **About foreign key arrays**

Unfortunately, Postgres (including Supabase) does not support arrays of foreign keys. Some of the other apps we connect with (e.g. Airtable) do, so we've tried to build a workaround for this. With this workaround you'll be able to sync Airtable linked records with a fake Postgres foreign key array.

### **How it works**

At a high-level, you can configure a Postgres/Supabase column to be an array BUT signal to Whalesync that you'd like us to treat it as a foreign key array.

Since Postgres just sees this as an array, the field no longer has the same validation, but it will sync.

{% hint style="info" %}
**Note:** a bad value here will not break Whalesync, that value will simply not sync until you correct it.&#x20;
{% endhint %}

### **How do I implement this?**

Imagine you have two tables:

- Contacts
- Company

To create a foreign key array you can:

1. Ensure both tables have a primary key (e.g. uuid)
2. In Company, create an array column "People_fk_Contacts" with type uuid\[] to match the type of the table id.

   1. The "\_fk" designates to Whalesync that you want this to be a foreign key.
   2. The "\_Contacts" designates that it should point to the Contacts table.

   (\*note - must match capitlization)

3. Set up your sync in Whalesync as normal, mapping your fields.

### **Example snippet**

```sql
CREATE TABLE public."Contacts" (
"id" uuid PRIMARY KEY DEFAULT gen_random_uuid(),
"Email" text );

CREATE TABLE public."Company" (
"id" uuid PRIMARY KEY DEFAULT gen_random_uuid(),
"Name" text,
"People_fk_Contacts" uuid[] );
```
