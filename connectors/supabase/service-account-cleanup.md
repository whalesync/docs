---
description: How to remove the Whalesync database user from your Supabase or Postgres project
---

# Removing the Whalesync database user

When you connect Supabase to Whalesync, we create [a dedicated database user](why-does-whalesync-create-a-database-user.md) in your project so we can read and write only the data you sync. If you stop using Whalesync and want your project fully cleaned up, this guide walks you through disconnecting and removing that user.

### Which kind of connection do you have?

* **Supabase (signed in with Supabase).** Whalesync created a database user named `whalesync_service_account_[ID]`. Complete all three steps below to remove it.
* **Postgres or Supabase connection string.** You gave Whalesync a connection string for a user you created yourself, so there is no extra `whalesync_service_account_[ID]` user. Complete **Step 1**, then rotate or delete that database user on your side. You can stop after Step 1.

If you aren't sure which you have, open the Supabase **SQL Editor** and run:

```sql
select rolname from pg_roles where rolname like 'whalesync_service_account_%';
```

If it returns a row, you have the first kind and should complete all three steps.

### Step 1: Stop and delete your syncs

In Whalesync, stop and delete every sync that uses this Supabase project. Once no sync uses it, Whalesync no longer reads from or writes to your database.

### Step 2: Revoke Whalesync's access in Supabase

In the Supabase dashboard, remove Whalesync's authorization so its access can't be reused:

1. Go to your **Organization settings**
2. Open **OAuth Apps** (sometimes shown under **Integrations** or **Apps**)
3. Find **Whalesync** and click **Revoke**

{% hint style="info" %}
The exact labels move around in Supabase's dashboard. You're looking for the list of authorized third-party apps.
{% endhint %}

### Step 3: Remove the leftover database user

In the Supabase dashboard, open the project that was connected to Whalesync, then open the **SQL Editor** from the left sidebar.

The `whalesync_service_account_[ID]` user is managed by the Whalesync integration, so a plain `drop role` is denied with `42501: permission denied`. Supabase's supported way to remove it is to first hand the user over to your `postgres` role, then drop it.

Run these statements one at a time, replacing `<role>` with the exact user name and keeping the double quotes:

```sql
-- give your postgres role control of the user
grant "<role>" to postgres;

-- move anything it owns to postgres (usually nothing) and clear its access
reassign owned by "<role>" to postgres;
drop owned by "<role>";

-- remove the user
drop role "<role>";
```

Run the `select` from the top of this guide again to confirm the user is gone. It should return no rows.

### If a step fails

If any step fails — either a `42501: permission denied` error or the connection dropping — email us at [support@whalesync.com](mailto:support@whalesync.com) and we'll remove the user for you.

There's no rush: you already stopped all syncing and revoked access in Steps 1 and 2, so the leftover user can't do anything until it's dropped.
