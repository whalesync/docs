# Authorize Klaviyo

Whalesync connects to Klaviyo in one of two ways. Signing in is the default; a private API key is an alternative if you prefer not to sign in, or are setting up a sync through the [API](../../api/reference.md) or [MCP server](../../api/mcp/README.md) and need a credential to hand over.

Either way, a connection reaches one Klaviyo account.

## Sign in

1. In Whalesync, choose Klaviyo and click **Sign in with Klaviyo**.
2. Approve the access Whalesync asks for: read access to the account, read and write access to profiles and lists, and read access to segments.
3. Pick the account to sync.

The sign-in lasts until the Whalesync app is removed from the Klaviyo account. Klaviyo also ends a sign-in that goes unused for 90 days.

## Use a private API key

1. In Klaviyo, open **Settings**, then [**API keys**](https://www.klaviyo.com/settings/account/api-keys), and click **Create Private API Key**.
2. Name it, for example "Whalesync", and choose one of:
   * A full access key.
   * A custom key with read access to **Accounts** and **Segments** and full access to **Profiles** and **Lists**.
3. Create the key and copy it. It starts with `pk_`. Klaviyo shows it only once.
4. In the connect step in Whalesync, choose to use a private API key instead, paste the key, and click **Authorize**.
5. Pick the account to sync.

A read-only key is not enough: Klaviyo refuses every write with a permission error. Reauthorizing with a key from a different Klaviyo account than the one the connection already syncs is refused.

A connection keeps its method. To switch between a key and sign-in, create a new connection.

## Errors

| Message | What to do |
| --- | --- |
| Klaviyo did not accept this private API key. Check it and try again. | The key was copied wrong or deleted. Copy it again, or create a new one. |
| This Klaviyo private API key is missing a permission Whalesync needs. | Create a full access key, or a custom key with the permissions listed above. |
| This private API key belongs to a different Klaviyo account than the one this connection already syncs. | Use a key from the same Klaviyo account. |
| Klaviyo no longer accepts the credentials Whalesync is using. Please reconnect Klaviyo. | The Whalesync app was removed from the account, or the key was deleted. Reconnect Klaviyo. |
| Klaviyo refused this request. The API key or app grant is missing a permission Whalesync needs. | The key or sign-in cannot write, for example a read-only key. Reconnect with the permissions listed above. |
| Klaviyo profiles can only be deleted from Klaviyo itself. | Whalesync does not delete profiles. Delete the profile in Klaviyo, or remove it from its lists. |
| Klaviyo needs phone numbers in international format, like +12025550123. | Fix the phone number in your other app. |
| Klaviyo needs an email, a phone number or an external ID to create a profile. | Map at least one of those columns and give the record a value. |
| Klaviyo lists need a name. | Give the list a name in your other app. |
| This record is larger than Klaviyo allows for one profile (100KB including custom properties). | Shorten or unmap the large fields. |
| Klaviyo refused this change because it conflicts with another profile. | Usually an email or phone number that already belongs to another profile. Change it, or edit the other profile in Klaviyo. |
| Klaviyo is rate limiting Whalesync. Whalesync will retry automatically. | Nothing. The sync continues on its own. |

Other problems Klaviyo reports, such as an email address in the wrong format, show Klaviyo's own message and the field it applies to.
