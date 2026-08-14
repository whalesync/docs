---
description: Handling failures from the Whalesync API
---

# Error reference

Every error response has the same shape:

```json
{"error": {"type": "invalid_request_error", "code": "base_not_found",
           "message": "…", "doc_url": "https://docs.whalesync.com/api/errors#base_not_found"}}
```

Branch on `code`. Messages are written for people and may change.

`type` says how to handle the failure, independent of the status:

| `type` | Meaning |
| --- | --- |
| `authentication_error` | No usable API key. Don't retry with the same one. |
| `permission_error` | Authenticated, but not allowed to do this. |
| `invalid_request_error` | Something about the request is wrong, or the resource isn't in a state that allows it. |
| `requires_action` | A person has to do something first. Always carries `required_action`. |
| `rate_limit_error` | Over the per-key budget. Wait for `Retry-After`. |
| `api_error` | A problem on our side. Retry. |

Two fields appear on some errors. `required_action` is the step a person must take, with an `instruction` written to be relayed word for word; it appears on every `requires_action` error and on the two authentication codes. `details` carries machine-readable specifics for the codes that have them.

## Authentication and access

### `missing_api_key`

`401` · No `Authorization: Bearer ws_tok_…` header. The `required_action` links a person to key creation and names the smallest scope this endpoint needs. There is no endpoint that creates a key; API keys are created manually by a human in Whalesync → Settings → API keys.

### `invalid_api_key`

`401` · The key is unrecognized, malformed, or revoked. Deliberately the same response for all three: the API never confirms whether a key ever existed. Carries the same `required_action` as above.

### `insufficient_scope`

`403` · A `read` key was used for something that changes state. `read` keys may call every `GET` and `POST …/validate`, which writes nothing. Ask a person for a `readwrite` key; scope can't be changed after creation.

### `public_api_not_enabled`

`403` · The key is valid but the account isn't in the API's launch yet. This is not something the account owner can turn on. They should ask for API access at support@whalesync.com. Existing keys keep working once it's enabled; a new key won't help. Deliberately not a `requires_action`, because no browser step resolves it.

### `rate_limit_exceeded`

`429` · Over the per-key budget. Wait `Retry-After` seconds. `RateLimit-*` headers on every response show the budget before you hit it.

### `subscription_required`

`403` · The account has no subscription that permits creating or changing syncs. A person resolves it in billing.

## Request shape

### `invalid_request`

`400` · The request body or parameters didn't validate. The message names the problem.

### `invalid_limit`

`400` · `limit` is outside the allowed range.

### `invalid_cursor`

`400` · `cursor` isn't one this endpoint issued. Pass back the previous page's `next_cursor` unchanged. Cursors are opaque and not portable between endpoints.

### `missing_sync`

`400` · `/v1/operations` and `/v1/issues` require `?sync=`. Both are always read one sync at a time. Every sync carries pre-filtered `operations_url` and `issues_url`.

### `invalid_sync`

`400` · The `sync` filter value isn't a sync id.

### `invalid_table`

`400` · The `table` filter value isn't a table id.

### `invalid_side`

`400` · A `side` value wasn't `left` or `right`.

### `invalid_since`

`400` · A `since` value wasn't an ISO 8601 timestamp.

### `invalid_type`

`400` · A `type` filter value was outside the issue types.

### `not_found`

`404` · No such resource, or it belongs to someone else. The two are indistinguishable on purpose, so the API never reveals that an id exists.

### `invalid_idempotency_key`

`400` · The `Idempotency-Key` header was malformed or too long.

### `idempotency_key_reused`

`400` · The same key arrived with a different body, which means your retry logic is sending new work under an old key. Keys last 24 hours.

### `idempotency_key_in_use`

`409` · A duplicate landed while the first request was still running. Retry after it finishes.

## Building a sync

### `unknown_connector`

`400` · No such connector, or it isn't available to this account. List them with `GET /v1/connectors`. Connectors above the account's plan appear there with `available: false` and the plan that unlocks them.

### `connector_pair_not_allowed`

`400` · This connector can't sync to itself.

### `missing_auth`

`400` · A connector that takes credentials inline needs `auth` at creation. Field ids for `auth` come from `GET /v1/connectors`; send them exactly as given (they're the connector's own, for example `connectionString`).

### `missing_base`

`400` · A connector that takes credentials inline also needs `base` at creation.

### `auth_not_supported`

`400` · This side's app signs in through a browser, so it takes no `auth`. Send only `{"connector": "…"}` for it. The sync comes back with that side `null` and a pending action linking a person to the step that connects it, where they also choose its base.

### `base_not_supported`

`400` · Same as `auth_not_supported`: a browser sign-in side takes no `base` either. The person who connects the app picks its base.

### `oauth_connector_not_supported`

`400` · Credentials for a browser sign-in app can't be sent over the API, so they can't be set or rotated here. This does **not** mean such syncs must be built in the app: creating one works, per `auth_not_supported` above. Reconnecting an existing one is done by a person in Whalesync.

### `invalid_auth`

`400` · The credentials were rejected by the app they're for. The message carries what that app said.

### `connection_error`

`400` · The app couldn't be reached with those credentials: wrong host, network failure, or a database that isn't accepting connections.

### `base_not_found`

`400` · The `base` couldn't be resolved. `details.bases` lists what the credentials can reach; pick one and retry. Nothing is created by a failed create. Prefer the base's `remote_id`: names aren't unique.

### `base_ambiguous`

`400` · The `base` matched more than one by name. `details.bases` lists the candidates; pick one by `remote_id` and retry. Base names are not unique.

### `base_conflict`

`400` · Both sides point at the same base with the same credentials. A base can't sync to itself.

### `sync_not_draft`

`409` · A side's `connector` or `base` can only be changed while the sync is a `draft`. Credentials (`auth`) can be rotated at any time.

## Mappings and schema

### `sync_active`

`409` · Mappings can't be edited, and schema can't be force-refreshed, while a sync is running. An active sync's schema is kept fresh in the background and a manual fetch would race it. Pause first. Plain reads always work.

### `invalid_mappings`

`400` · The document is malformed or the write path rejected it. `details.issues` carries the specifics with a JSON pointer into your document. Run `POST …/validate` first to get the same list without attempting a write.

### `revision_mismatch`

`412` · The `If-Match` revision is stale. The mappings changed since you read them, probably edited in the app. Fetch the document again and reapply your edit.

### `create_failed`

`400` · A `{"create": …}` placeholder couldn't be created in the destination app. The message carries the app's reason and the document path. Re-sending a `create` that matches an object of the same name adopts it, so retrying after a partial failure is safe.

### `table_ambiguous`

`400` · A bare `remote_id` matched tables on both sides. Use the prefixed `table_…` id.

### `auth_required`

`409` · `requires_action` · A side still has no connection, so there's nothing to map or list schema for. The `required_action` links a person to the step that connects it. Poll the sync until the side stops being `null`.

### `confirmation_required`

`409` · `requires_action` · The sync is a `draft`: no one has reviewed and started it under its current mappings. The API can't start a sync a person hasn't approved. Hand over the `required_action` (the same page as the sync's `review_url`), then poll until `status` is `active`. Any mappings edit returns a sync to `draft`, so this recurs after every change.

## Validation issues

These are not errors. `POST …/validate` returns `200` with an `issues` array, and the mappings `PUT` repeats the same objects in `details.issues` when it refuses. Each carries a `path` pointing into your document. `severity: "error"` means a person can't start the sync until it's fixed; `warning` never blocks.

### `incompatible_field_types`

The two fields can't carry each other's values in the direction they're mapped. Evaluated per direction; a pair can be fine one way and not the other.

### `required_field_unmapped`

The destination requires this field, so a record can't be written without it.

### `foreign_key_target_unmapped`

A linked-record field points at a table that isn't in the mappings. Map the target table too.

### `foreign_key_target_mismatch`

The two sides' link fields point at tables that aren't mapped to each other.

### `unknown_table`

A table reference doesn't resolve on that side. References may be a `remote_id`, a Whalesync id, or an exact unique name; resolution is per side.

### `unknown_field`

A field reference doesn't resolve on that side. Same resolution rules as `unknown_table`.

### `orphaned_table`

The reference resolves to a table the app no longer has. It was deleted or renamed since the schema was last fetched. Refresh the schema with `?refresh=true`.

### `orphaned_field`

The reference resolves to a field the app no longer has. Refresh the schema with `?refresh=true`.

### `view_required`

A table synced through views needs a `view` on its side. Read the legal values from the table's `views.options`.

### `view_not_found`

The `view` value isn't one that table offers. Note that `view` is part of the full-replace document, so omitting it in a later `PUT` clears the previous choice and fails with `view_required`.

### `view_not_supported`

A `view` was given for a table that doesn't sync through views (`views` is null).

### `create_unsupported`

The connector can't create tables or fields, so a `{"create": …}` placeholder can't be honored on that side. Severity `error`.

### `create_name_collision`

Something with that name already exists, and the create will adopt it rather than make a new one. Severity `warning`; it never blocks.

## Server

### `internal_error`

`500` · An unexpected error on Whalesync's side. Retry; if it persists, contact support@whalesync.com. The response deliberately carries no internal detail.
