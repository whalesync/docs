---
description: Sync your Supabase data faster with Database Webhooks!
hidden: true
---

# How to enable webhooks

## What do webhooks do?

Webhooks are an optional feature of Supabase that Whalesync can use to speed up syncing of your data out of Supabase. When webhooks are enabled, Supabase will ping Whalesync whenever data is created, updated, or deleted in your database. This can speed up syncing because we don't have to check periodically for changes.

## How do I enable them?

1. Click on the Integrations tab when your project is selected in Supabase:

<figure><img src="../../.gitbook/assets/Screenshot 2025-03-17 at 1.50.40 PM.png" alt="" width="199"><figcaption><p>Click the Integrations tab</p></figcaption></figure>

2. Search for "webhooks" and click on Database Webhooks

<figure><img src="../../.gitbook/assets/Screenshot 2025-03-17 at 2.00.27 PM.png" alt=""><figcaption><p>Find the Data Webhooks integration</p></figcaption></figure>

3. Click "Enable webhooks"

<figure><img src="../../.gitbook/assets/Screenshot 2025-03-17 at 2.03.09 PM.png" alt=""><figcaption><p>Enable webhooks</p></figcaption></figure>

4. Whalesync will automatically detect that webhooks have been enabled within 10 minutes, and will create them automatically.
