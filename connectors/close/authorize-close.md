# Authorize Close

Whalesync connects to Close with an API key you paste in. A key reaches exactly one Close organization, and that organization is the base the connection syncs.

## Create an API key

1. In Close, open **Settings**, then **Developer**, then [**API Keys**](https://app.close.com/settings/developer/api-keys/), and create a key. Close's own guide is [here](https://help.close.com/integrations/api-keys-oauth).
2. Copy the key. It starts with `api_`, and Close shows it only once.
3. In Whalesync, choose Close, paste the key into **Close API key**, and click **Authorize**.
4. Pick the organization to sync. A key reaches one organization, so there is one to pick.

A Close API key reaches one Close organization and carries the access of the Close user who created it: in Close's words, "as determined by your Close role in case you're not a Close Admin". A key from a user whose role cannot do everything the sync needs fails on those operations, or reads less than the whole organization, so create the key from an Admin. It does not expire. It stops working the moment it is deleted in Close.

If you belong to more than one Close organization, create the key from the organization you want to sync. To sync a second organization, create a second connection with a key from that one.

Reauthorizing with a key for a different Close organization than the one the connection already syncs is refused.

## Errors

| Message | What to do |
| --- | --- |
| The Close API key Whalesync is using is no longer valid. Please reconnect Close with a new API key. | The key was copied wrong or deleted in Close. Check that you copied the whole key rather than the shorter ID Close lists it under, or create a new key and reconnect. |
| This Close organization is no longer available on the connected API key. Please reconnect Close with a key for the same organization. | The Close user the key belongs to is no longer in that organization. Add them back in Close, or reconnect with a key from a user who is in it. |
| Connection update failed. The Close connection did not share access with organization … | You reauthorized with a key for a different Close organization than the one the connection syncs. Use a key from the same organization. |
| Whalesync could not tell which Close organization this API key belongs to. Please create the key from the organization you want to sync and reconnect. | Create the key from inside the organization you want to sync, then reconnect. |
| No Close organization is available on this connection. | The Close user the key belongs to is not in an organization. Add them to one in Close. |
| Whalesync doesn't have permission to access this Close account. | The Close user who created the key does not have access to everything the sync needs. Create the key from a user who does, usually an Admin. |
| Usage limit reached. — or, when Close sends no message of its own, Your Close plan does not allow this change. Check your Close plan limits, or remove something to free up room. | A Close plan limit, for example the number of pipelines. Change the plan in Close, or free up room. |
| Close is rate limiting Whalesync. Whalesync will retry automatically. | Nothing. The sync continues on its own. |
| Close's own message about the record, for example `name: Value must not be empty.` — or, when Close sends no message of its own, Close rejected the record (HTTP 400). This usually means a required field is missing or a value is in the wrong format. | Check the record in your other app. Close usually names the field it refused. |
| Opportunity matching query does not exist | The lead behind this record was deleted in Close, which deletes its contacts and opportunities too. Delete leads in Close rather than from your other app. |

Other problems Close reports show Close's own message and the field it applies to.
