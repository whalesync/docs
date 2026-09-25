# Authorize Mailchimp

Whalesync connects to Mailchimp in one of two ways. Signing in is the default; an API key is an alternative if you prefer not to sign in, or are setting up a sync through the [API](../../api/reference.md) or [MCP server](../../api/mcp/README.md) and need a credential to hand over.

Either way, a connection reaches every audience in one Mailchimp account.

## Sign in

1. In Whalesync, choose Mailchimp and click **Authorize**.
2. Sign in to Mailchimp and approve access for Whalesync.
3. Pick the audience to sync.

The sign-in does not expire.

## Use an API key

1. In Mailchimp, click your profile icon and choose **Profile**.
2. Open the **Extras** menu and choose **API keys**.
3. Under **Your API Keys**, click **Create A Key**, name it, for example "Whalesync", and click **Generate Key**.
4. Click **Copy Key to Clipboard**. Mailchimp shows the key only once. It ends in a dash and a data center, like `-us6`.
5. In Whalesync, choose Mailchimp, click **Use a api key instead**, paste the key, and click **Authorize**.
6. Pick the audience to sync.

Mailchimp API keys created after June 22, 2026 expire a year after they are created. When a key expires, create a new one and reconnect Mailchimp with it. Keys created before that date do not expire. See Mailchimp's [About API keys](https://mailchimp.com/help/about-api-keys/).

Reauthorizing with a key or sign-in from a different Mailchimp account than the one the connection already syncs is refused.

## Errors

| Message | What to do |
| --- | --- |
| This does not look like a Mailchimp API key. | The key was cut short. Copy the whole key, including the dash and data center at the end. |
| Mailchimp did not accept this API key. | The key was copied wrong, deleted, or has expired. Copy it again, or create a new one. |
| Mailchimp no longer accepts the credentials Whalesync is using. | The API key was deleted or has expired, or Whalesync was disconnected from the account. Create a new key or sign in again, and reconnect Mailchimp. |
| This API key belongs to a Mailchimp account that does not have the audience this connection already syncs. | Use a key from the same Mailchimp account. |
| You signed in to a Mailchimp account that does not have the audience this connection already syncs. | Sign in to the same Mailchimp account. |
| Mailchimp is limiting how many requests Whalesync can make at once. | Nothing. Whalesync will retry automatically. |
