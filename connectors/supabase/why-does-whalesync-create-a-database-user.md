---
description: >-
  tl;dr -> so that we can connect to your Supabase database in the simplest/most
  reliable way
noIndex: true
---

# Why does Whalesync create a database user?

### Why does Whalesync need to create a user in my Supabase project?

The password you set when creating a new project can't be retrieved via the Supabase API. We could ask you to provide that password when setting up a sync, but then the only way for you to revoke our access would be to rotate that password, potentially breaking your app.

Instead, we create a new login role with the same privileges as the `postgres`role, and set our own password. This role is fully controllable by you using standard Postgres commands, and can be deleted if you want to remove Whalesync's access to your project.

### What is the user called?

The user is named `whalesync_service_account_[ID]`, where ID is a string of hex digits unique to the sync. If you set up multiple syncs to the same Supabase project, you may see multiple users being created by Whalesync.

