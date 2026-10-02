---
description: >-
  Create a Copper API key to connect your Copper account to Whalesync, and what
  to do about each Copper connection error.
---

# Authorize Copper

Whalesync connects to Copper with an API key and the email of the Copper user the key belongs to. A connection reaches one Copper account, and that account is the base the connection syncs.

## Create an API key

1. In Copper, open **Settings**, then **Integrations**, then **API Keys**, and click **Generate API Key**. Only Copper Admins can generate API keys. Copper's own guide is [here](https://support.copper.com/en/articles/8823347-generating-an-api-key).
2. Copy the key.
3. In Whalesync, choose Copper, paste the key into **Copper API key**, enter the email of the Copper user who generated the key into **Copper account email**, and click **Authorize**.
4. Pick the account to sync. A connection reaches one account, so there is one to pick.

A Copper API key carries the access of the Copper user who generated it. It stops working the moment it is deleted in Copper.

To sync a different Copper account, create a second connection with a key from that account.

## Errors

| Message | What to do |
| --- | --- |
| Copper rejected the credentials. Check the API key and account email. | The key was copied wrong or deleted in Copper, or the email is not the email of the user who generated the key. Enter both again, or generate a new key and reconnect. |
| Copper Leads aren't enabled on your account. | Turn on Leads in Copper's Settings, then press **Retry Sync**. Only the Leads table is affected. |
| Copper rejected the update: a linked record (such as the assignee or primary contact) does not exist. | The linked user or person was deleted or does not exist in Copper. Point the field at an existing record. |
| A value that is not one of a Dropdown or Multi-Select field's options. The message lists the valid options. | Use one of the listed option names, or add the option in Copper and refresh the schema in Whalesync. |
| Copper: followed by Copper's own message | Copper refused the record and gave a reason, usually naming the field. Check the record in your other app. |

Whalesync retries automatically when Copper is rate limiting it or has a temporary error. There is nothing to do.
