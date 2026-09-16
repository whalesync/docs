---
description: >-
  How to permanently delete your Whalesync account from Settings and what happens
  when you do
---

# How to delete your account

You can delete your own Whalesync account from your settings. It doesn't happen all at once: your account closes immediately, and everything we hold is permanently deleted **30 days later**. You can cancel any time before that date.

{% hint style="warning" %}
If you only want to stop syncing or stop paying, you don't need to delete your account. You can turn off a sync from its settings, or cancel your subscription on the [Billing tab](https://app.whalesync.com/settings/billing). Deleting your account can't be undone once the 30 days are up.
{% endhint %}

## Before you start

If you have a subscription that will charge again, cancel it first. The _Delete account_ button stays disabled until you do. We won't cancel a paid plan for you as a side effect of deleting your account.

Cancel your subscription on the [Billing tab](https://app.whalesync.com/settings/billing), then come back.

## Delete your account

1. Go to [Settings > Account](https://app.whalesync.com/settings/profile)
2. Scroll to the _Delete account_ card
3. Click _Delete account_
4. Read what the dialog tells you, then type your account email to confirm
5. Click _Delete account_

You'll be signed out right away, and we'll email you a confirmation naming the exact date your data will be deleted.

## What happens, and when

| When                           | What happens                                                                                                                                                                                                                 |
| ------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Right away**                 | Your account closes. Your API token and every public API key are revoked, and you're signed out everywhere. Signing back in shows a page telling you the account is being deleted, and the rest of the app is closed to you. |
| **Within an hour**             | Every sync is turned off, and we destroy our copy of the credentials for every app you connected.                                                                                                                            |
| **30 days after your request** | Your account and everything in it is permanently deleted, including your bases, syncs, records, personal information, and your Whalesync login.                                                                              |

The dialog and the confirmation email both name your exact deletion date, and so does the page you see if you sign back in.

## What we don't delete

- **Data in your connected apps.** Records Whalesync wrote into Airtable, Notion, Webflow, or anywhere else stay exactly where they are. We never delete anything from the apps you connected. If you want those records gone, delete them in that app.
- **Whalesync's access from the app's side.** We destroy our copy of your credentials, but revoking the connection at the source is done in each app's own settings. Look there for connected apps, integrations, or authorized applications.
- **Your invoices.** Billing records live in Stripe and we keep them, because we're required to retain financial records.
- **Security logs.** We keep a record of actions taken on the account as a security record.

## Need help?

If the _Delete account_ button isn't doing what you expect, feel free to [email us](mailto:support@whalesync.com) and we'll be happy to help!
