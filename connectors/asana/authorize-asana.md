# Authorize Asana

Whalesync connects to Asana in one of two ways. Signing in is the default; a personal access token is an alternative if you prefer not to sign in, or are setting up a sync through the [API](../../api/reference.md) or [MCP server](../../api/mcp/README.md) and need a credential to hand over.

Either way, Whalesync acts as the Asana user who connected: it sees that user's projects, and tasks it creates or edits show that user as the actor in Asana. Many teams create a dedicated Asana user for this.

## Sign in

1. In Whalesync, choose Asana and click **Sign in with Asana**.
2. Pick the Asana account to use and click **Allow**. Whalesync asks for full access to that account, which is what Asana requires to list a project's sections.
3. Pick the workspace to sync.

The sign-in lasts until you revoke it in Asana, under **My settings**, then **Apps**.

## Use a personal access token

1. Open [app.asana.com/0/my-apps](https://app.asana.com/0/my-apps) and, under **Personal access tokens**, click **Create new token**.
2. Name it, for example "Whalesync", and click **Create token**.
3. Copy the token. Asana shows it only once.
4. In the connect step in Whalesync, choose **Use a personal access token instead**, paste the token, and click **Authorize**.
5. Pick the workspace to sync.

A token does not expire. It reaches every workspace the user belongs to. Reauthorizing with a token for a different user, one that cannot see a workspace the connection already syncs, is refused.

A connection keeps its method. To switch between token and sign-in, create a new connection.

## Errors

| Message | What to do |
| --- | --- |
| Asana did not accept this personal access token | The token was copied wrong or revoked. Copy it again, or create a new one. |
| Asana no longer accepts the credentials Whalesync is using | The sign-in was revoked or the token deleted. Reconnect Asana. |
| Whalesync doesn't have permission to access this in Asana | The connected user lost access to the project. Add them back, or reconnect as someone who has access. |
