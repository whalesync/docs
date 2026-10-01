---
description: >-
  Every error code the Whalesync API returns, with its HTTP status, error type,
  and how to handle it, plus the issue codes returned when validating mappings.
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

`403` · The key's scope is below what the endpoint needs. The message names both scopes, for example `This API key has the "read" scope. The endpoint requires the "operate" scope.` From weakest to strongest the scopes are `read`, `operate`, and `readwrite`. `read` keys may call every `GET` and `POST …/validate`, which writes nothing. `operate` adds pausing and activating syncs, retrying issues, refetching records, and triggering and canceling Live Export runs. Everything else that changes state needs `readwrite`, including creating, editing, and deleting Live Exports and their mappings, saving them, and changing their schedules. Ask a person for a key with the scope the message names; scope can't be changed after creation.

### `sync_restricted_key`

`403` · The key is limited to one sync, and this endpoint isn't about one existing sync. The message is `This API key is limited to one sync and cannot be used on this endpoint.` Creating a sync and every Live Export endpoint refuse limited keys. Ask a person for a key with access to all syncs. A limited key that asks for a different sync, or for another sync's issues, operations, or records, gets `not_found` instead.

### `rate_limit_exceeded`

`429` · Over the per-key budget. Wait `Retry-After` seconds. `RateLimit-*` headers on every response show the budget before you hit it.

### `subscription_required`

`403` · The account has no subscription that permits creating or changing syncs. A person resolves it in billing.

## Request shape

### `invalid_request`

`400` · The request body or parameters didn't validate. The message names the problem.

### `invalid_limit`

`400` · `limit` is outside the allowed range. Live Export lists accept 1 to 25.

### `invalid_cursor`

`400` · `cursor` isn't one this endpoint issued. Pass back the previous page's `next_cursor` unchanged. Cursors are opaque and not portable between endpoints.

### `missing_sync`

`400` · `/sync/operations`, `/sync/issues`, `/sync/records`, and `/sync/pending-deletes` require `?sync=`. All are read one sync at a time. Every sync carries pre-filtered `operations_url`, `issues_url`, and `pending_deletes_url`. `/sync/records/{record_id}` needs `?sync=` too when the id is a connected-app id rather than a `rec_` id.

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

### `missing_query`

`400` · `GET /sync/records` requires `query`.

### `invalid_state`

`400` · The `state` filter on `/sync/pending-deletes` must be `awaiting_review` or `ignored`.

### `not_found`

`404` · No such resource, or it belongs to someone else. The two are indistinguishable on purpose, so the API never reveals that an id exists. A key limited to one sync also gets this for any other sync and for the issues, operations, and records of other syncs. A `lex_…` or `run_…` id also returns `404` when Live Export isn't available to the account. `GET /live-export/live-exports/{id}/save` returns `404` for an export that was never saved, and `GET …/schedule` returns `404` after the first save until a schedule is created.

### `invalid_idempotency_key`

`400` · The `Idempotency-Key` header was malformed or too long.

### `idempotency_key_reused`

`400` · The same key arrived with a different body, which means your retry logic is sending new work under an old key. Keys last 24 hours.

### `idempotency_key_in_use`

`409` · A duplicate landed while the first request was still running. Retry after it finishes.

The `Idempotency-Key` header is accepted on `POST /sync/syncs`, the sync mappings `PUT`, and `POST /live-export/live-exports`.

### `forbidden`

`403` · A fallback for a refusal that has no more specific code. Rare.

### `conflict`

`409` · A fallback for a state conflict that has no more specific code. Rare.

### `unprocessable`

`422` · A fallback for a request that was understood but can't be processed, when no more specific code applies. Rare.

## Building a sync

### `unknown_connector`

`400` · No such connector, or it isn't available to this account. List them with `GET /sync/connectors`. Connectors above the account's plan appear there with `available: false` and the plan that unlocks them.

### `connector_pair_not_allowed`

`400` · This connector can't sync to itself.

### `missing_auth`

`400` · An API-key side sent `base` without `auth`. Airtable behaves as an API-key side here. On an API-key side the two travel together: send both, or omit both and a person connects it in the browser, picking the base there. Send both and the side is built and its credentials validated live; omit both and the side comes back `null` with a `user_authorization` pending action, exactly like an OAuth side. (This also fires when a PATCH changes a side's `connector` without supplying the full `auth` and `base` the new connector needs.) Field ids for `auth` come from `GET /sync/connectors`; send them exactly as given (they're the connector's own, for example `connectionString`).

### `missing_base`

`400` · The mirror of `missing_auth`: an API-key side sent `auth` without `base`. Send both, or omit both and a person connects it in the browser, picking the base there.

### `auth_not_supported`

`400` · This side's app signs in through a browser, so it takes no `auth`. Send only `{"connector": "…"}` for it. The sync comes back with that side `null` and a pending action linking a person to the step that connects it, where they also choose its base. Deferring a side to a person this way now works for every connector, not only browser sign-in apps: an API-key side declared by connector alone is deferred the same way (a choice there, rather than the only option — see `missing_auth`). Airtable is not one of these; it takes `auth` inline like an API-key connector.

### `base_not_supported`

`400` · Same as `auth_not_supported`: a browser sign-in side takes no `base` either. The person who connects the app picks its base. Airtable is not one of these; it takes `auth` inline like an API-key connector.

### `oauth_connector_not_supported`

`400` · Credentials for a browser sign-in app can't be sent over the API, so they can't be set or rotated here. This does **not** mean such syncs must be built in the app: creating one works, per `auth_not_supported` above. Reconnecting an existing one is done by a person in Whalesync. Airtable is not one of these; it takes `auth` inline like an API-key connector.

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

### `initial_sync_running`

`409` · `activate` was called while the sync's first sync is still running. The sync turns itself on when that finishes. Poll the sync until `status` is `active`.

## Mappings and schema

### `sync_active`

`409` · Mappings can't be edited, and schema can't be force-refreshed, while a sync is running. An active sync's schema is kept fresh in the background and a manual fetch would race it. Pause first. Plain reads always work.

### `invalid_mappings`

`400` · The document is malformed or the write path rejected it. `details.issues` carries the specifics with a JSON pointer into your document. Run `POST …/validate` first to get the same list without attempting a write.

### `revision_mismatch`

`412` · The `If-Match` revision is stale. The mappings changed since you read them, probably edited in the app. Fetch the document again and reapply your edit. This applies to the Live Export mappings `PUT` too. Over MCP, the stale value is the `revision` argument rather than `If-Match`.

### `create_failed`

`400` · A `{"create": …}` placeholder couldn't be created in the destination app. The message carries the app's reason and the document path. Re-sending a `create` that matches an object of the same name adopts it, so retrying after a partial failure is safe.

### `table_setup_failed`

`400` · A mapped table couldn't be prepared for syncing. Some connectors add a Whalesync ID column to a table before it can sync, and that step failed. The message carries the app's reason.

### `table_ambiguous`

`400` · A bare `remote_id` matched tables on both sides. Use the prefixed `table_…` id.

### `auth_required`

`409` · `requires_action` · A side still has no connection, so there's nothing to map or list schema for. The `required_action` links a person to the step that connects it. Poll the sync or live export until the side stops being `null`. On Live Export, `side` is `source` or `destination`. Live Export mappings validation also reports `auth_required` as an issue code when a side isn't connected.

### `confirmation_required`

`409` · `requires_action` · The sync is a `draft`: no one has reviewed and started it under its current mappings. The API can't start a sync a person hasn't approved. Hand over the `required_action` (the same page as the sync's `review_url`), then poll until `status` is `active`. Any mappings edit returns a sync to `draft`, so this recurs after every change.

## Validation issues

These are not errors. `POST …/validate` returns `200` with an `issues` array, and the mappings `PUT` repeats the same objects in `details.issues` when it refuses. Each carries a `path` pointing into your document. `severity: "error"` means a person can't start the sync until it's fixed; `warning` never blocks.

Live Export validation (`POST /live-export/live-exports/{id}/mappings/validate`) returns a different shape: `{"valid": bool, "issues": [{"code", "message", "path"}]}`, with `path` like `tables[0]` or `null` and no `severity`. Its issue codes are the [Live Export](#live-export) codes a mappings `PUT` would return, plus `auth_required` and `internal`.

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

### `internal`

Live Export only. Validation itself failed unexpectedly. Retry.

## Records and deletes

### `ambiguous_record`

`400` · A record id from a connected app matched records in more than one table. Add `?table=` to pick one. A `rec_` id is never ambiguous.

### `no_copy_to_refetch`

`400` · `POST /sync/records/{record_id}/refetch` asked for a side that has no copy of the record, or, with no `side`, neither side has one. The message names the side, for example "This record has no copy on the left side to fetch." Refetch the other side, or omit `side`.

### `delete_approval_disabled`

`409` · `/sync/pending-deletes` was called on a sync that auto-approves deletes, so it has no queue. A sync's `delete_approval` field says which mode it is in before you call.

## Live Export

These codes come from the `/live-export/` endpoints. The [Live Export API reference](https://docs.whalesync.com/api/live-export) describes the flow they belong to.

### `live_export_unavailable`

`403` · Live Export isn't available to this account, either because the plan doesn't include it (the message names the plan) or because it isn't enabled. Returned on writes; reads return empty lists or `404` instead. A person resolves it in billing.

### `connector_not_supported`

`400` · The connector isn't available for that role (source or destination) on Live Export. Check `GET /live-export/connectors` and its `roles`.

### `oauth_auth_not_allowed`

`400` · `auth` was sent for a connector that connects with OAuth in the browser. Omit `auth` and relay the pending action.

### `connection_failed`

`400` · The app rejected the inline credentials. The message carries the app's reason. On create, nothing was kept, so retry with corrected credentials.

### `side_already_connected`

`409` · A `PATCH` sent `auth` for a side that is already connected. Reconnecting is done in the app (`app_url`).

### `invalid_location`

`400` · The `location` isn't one this destination offers, or `location` was sent on the source. Use an id from `GET …/destination/locations`.

### `live_export_invalid_structure`

`409` · The export was changed outside Whalesync and can't be operated on over the API. Open it in the app.

### `missing_live_export`

`400` · `/live-export/runs` requires `?live_export=`.

### `invalid_live_export`

`400` · The `live_export` filter value isn't a `lex_…` id.

### `unknown_source_table`

`400` · A `source_table` isn't a table of the source. Use ids from `GET …/source/tables`.

### `unknown_source_field`

`400` · A `source_field` isn't an exportable field of that table. Use ids from `GET …/fields`. Link fields are never offered.

### `duplicate_source_table`

`400` · The same source table appears twice in the mappings document.

### `duplicate_field_name`

`400` · Two fields in one table would create the same destination column name.

### `multiple_primary_fields`

`400` · More than one field in a table has `"primary": true`.

### `empty_table_mapping`

`400` · A table maps no fields.

### `existing_field_not_supported`

`400` · A new table maps onto an existing destination column instead of using `{"create": …}`. This isn't supported over the API yet; use the app.

### `applied_table_not_editable`

`400` · The document changes the fields of a table already created in the destination. Remove the whole table from the document, or edit it in the app.

### `empty_mappings`

`400` · `POST …/save` was called with no tables mapped. `PUT` a mappings document first.

### `not_provisioned`

`409` · The schedule or `trigger` was called before the export's first save. Map and save first (`mappings_url`).

### `unsaved_changes`

`409` · `trigger` was called while the mappings have unsaved edits, so the run would use the last-saved mappings. Save first, or send `{"force": true}` to run the last-saved version deliberately.

### `run_in_progress`

`409` · A run is already in progress, and the message names it. Wait for it to finish or cancel it.

### `run_not_active`

`409` · `cancel` was called on a run that already finished.

### `plan_required`

`403` · The schedule `cadence` is above what the plan allows. Pick one from `allowed_cadences`.

## Server

### `internal_error`

`500` · An unexpected error on Whalesync's side. Retry; if it persists, contact support@whalesync.com. The response deliberately carries no internal detail.
